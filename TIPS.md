# onbon bx06 api 小技巧

## 1. 延長通訊逾時檢查

若網路處於較慢的環境，可調控制卡整逾檢查時間。API 預設值為 7000 毫秒。

``` Java
Bx6GEnv.initial();
Bx6GController.TIMEOUT = 60000;  // 單位為毫秒
```
或
``` Java
Bx6GEnv.initial("applog4j.properties", 6000);
```


## 2. 初始化時載入 log4j 屬性。

啟動初始化時，可同時決定是否載入正確設定的 log4j 配置檔案。檔案名稱可以是絕對路徑或相對路徑。當為相對路徑時，API 會從應用程式資料下搜尋該配置檔案。

#### API 初始化
``` Java
// 不載入 log4j 配置檔案
Bx6GEnv.initial();

// 載入的 log4j 配置檔案在應用程式資料夾內
Bx6GEnv.initial("appLog4j.properties");

// 載入的 log4j 配置檔案在應用程式資料夾外
Bx6GEnv.initial("c:/somewhere/appLog4j.properties");
```

#### log4j 配置檔案：appLog4j.properties
``` yml
log4j.rootLogger=ALL, system, error

#System log file
log4j.appender.system=org.apache.log4j.DailyRollingFileAppender
log4j.appender.system.Threshold=ALL
log4j.appender.system.File=log/all_log.txt
log4j.appender.system.layout=org.apache.log4j.PatternLayout
log4j.appender.system.layout.ConversionPattern=%-5p %d{HH:mm:ss.SSS} %-55c - %m%n

#Error log file
log4j.appender.error=org.apache.log4j.DailyRollingFileAppender
log4j.appender.error.Threshold=ERROR
log4j.appender.error.File=log/err_log.txt
log4j.appender.error.layout=org.apache.log4j.PatternLayout
log4j.appender.error.layout.ConversionPattern=%-5p %d{HH:mm:ss.SSS} %-50c %-20M %-5L - %m%n
```

## 3. 檢查區域範圍有校性

在上傳節目前，確認加入節目中的區域是否超出屏幕有效範圍，避免黑屏的現象發生。

``` Java
// 建立節目
ProgramBxFile program = new ProgramBxFile("P000", screen.getProfile());

// 將圖文區域加入節目
program.addArea(area1);
program.addArea(area2);
program.addArea(area3);

// 檢查
BxArea failed = program.validate(); // 返回第一個超出屏幕範圍的區域
if(failed != null) {
    System.out.println("This area is out of range");
}
```
