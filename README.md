onbon bx06 api
=====================

最新版本 [Version 0.5.0-UDPATE.3](https://github.com/api2doc/onbon.bx06.api/releases/tag/v0.5.0-UPDATE.3)

本函式庫主要針對 [上海仰邦](http://www.onbonbx.com/) 六代全彩顯示屏控制器進行控制與節目的下載，用戶可透過此 API 進行二次開發與系統整合。
- [Java 文檔](http://api2doc.github.io/onbon.bx06.api)

- [小技巧](TIPS.md)

- [安卓設定](https://github.com/api2doc/onbon.bx06.mobiledemo) (僅 onbon bx06 api 0.5.0 或以上支援)

## 執行環境
- Java 6 或以上

- Andorid 5.0 或以上 (僅 onbon bx06 api 0.5.0 或以上支援)

## Android 開發時需要參考的 JAR 檔 (7/10)
- bx06.message-0.5.0-SNAPSHOT.jar

- bx06-0.5.0-SNAPSHOT.jar

- log4j-1.2.14.jar

- simple-xml-2.7.1.jar

- uia.comm-__x.x.x__.jar (__x.x.x__ 由各版本決定)

- uia.message-__x.x.x__.jar (__x.x.x__ 由各版本決定)

- uia.utils-__x.x.x__.jar (__x.x.x__ 由各版本決定)

## Java 6 範例

### Client 模式

``` Java
// 初始化系統環境 (同一程序 內只需初始化一次)
Bx6GEnv.initial();

// 建立屏幕物件
Bx6GScreenClient screen = new Bx6GScreenClient("Hello Screen");

// 連線
screen.connect("192.168.1.1", 5005);

// 執行命令
Result<ReturnPingStatus> result1 = screen.ping();
Result<ReturnControllerStatus> result2 = screen.checkControllerStatus();
...

// 斷線
screen.disconnect();
```
