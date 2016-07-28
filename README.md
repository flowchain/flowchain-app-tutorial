Flowchain 物聯網中文教材

# 1. Flowchain 簡介

如果要「簡單介紹」這是什麼技術，還真的不簡單。所以，不如根據這份中文教材，體驗 Flowchain 在物聯網開發上的創新。

## Flowchain 起源

Flowchain 發源自 [WoT.City](https://wotcity.com) 計畫，WoT 是 Web of Things 的縮寫。要把 Flowchain 說清楚，就必須把 Web of Things 講明白。你可以在[這裡](https://www.w3.org/WoT/IG/wiki/Implementations)找到一份 Web of Things Implementations 的清單，這份清單整理 W3C Web of Things 的相關計畫。

也就是說，WoT.City 是 W3C Web of Things (WoT) 的一個計畫，它也是一個開源項目，也是 WoT 的技術。這就是故事的開始。

WoT.City 主要在處理 *Connectivity*，例如：WebSocket、CoAP 與 Thing Description 等。WoT.City 是 Connecitivity Layer，目前它已經打包成  [wotcity.io](https://www.npmjs.com/package/wotcity.io) 模組，但是你不需要直接使用 wotcity.io 模組。

wotcity.io 被封裝為 [devify-server](https://github.com/DevifyPlatform/devify-server) 模組，devify-server 是一份 IoT server boilerplate，這是什麼呢？簡單說，就是一套給 IoT 用的伺服器程式模板，你可以用 devify-server 很容易寫出一個「負責收集感測器資料」的 IoT server。這套 IoT server 可以執行在 Desktop、Server 或 IoT device 上，它使用的是 Nodoe.js 技術，這表示只要有 Node.js 執行環境的硬體，都可以成為 devify-server 的執行環境。

架構上，devify-server 封裝了 wotcity.io，並且負責 Event Handling、Broker Server 與 Serverless 的角色。不過，你也不需要學習 devify-server 的程式設計。devify-server 再被封裝了，成為 *Flowchain* 技術。

Flowchain 帶來一些好消息，其中之一就是採用 Flow-Based Programming 的物聯網開發模式。

## Flowchain 設計模式

Flowchain 的名稱來自 _Flow-Based Programming_，故名思義，這是一個 Flow-Based Programming (FBP) 的技術。Flow-Based Programming 並不是新鮮事，非常知名的 [Flux](https://facebook.github.io/flux/docs/overview.html) 就是一個 Flow-Based Programming 的模式。

實際上，Flowchain 的設計能讓它與 Flux 模式非常良好地結合，在這份教材的最後，你將能學會 Flowchain 如何與 Flux 結合，應用在物聯網開發上。

Flowchain 採用 Flow-Based Programming 的觀念，這一點都不難，請見這個例子：

```
{
	"author": "jollen",
	"type": "coapToWebsocketBroker",
	"connections": [
		{
			"upproc": "io.devify.console",
		 	"upport": "out",
		 	"downproc": "io.devify.fs",
		 	"downport": "in"
		},
		{
			"upproc": "io.devify.fs",
		 	"upport": "out",
		 	"downproc": "io.devify.sms",
		 	"downport": "in"
		}
	]
}
```

Flowchain 大幅簡化了典型的 Flow-Based Programming 模式，這讓 Flowchain 更適用於 IoT 場景，而且執行 Flowchain 應用程式的 Runtime 也只有大約 300+ 行左右的程式碼實作。

Flowchain 架構設計包含幾個特色：

* 單一資料方向流（single data direction）：與 Flux 相同的是，Flowchain 的設計是單一資料方向流，它不採用雙向資料流（two-way）的設計
* Component-based 設計：組件（component）透過 inPort 與 outPort 來輸入與輸出資料，組件可以直接重用或程式碼重用（Code Reuse），而且組件之間沒有耦合性
* Decoupled Architecture：因為 Flowchain 的 component 間是完全沒有耦合的，所以 Flowchain 的應用程式，是高度 decoupled 架構，這點與 Flux 相同



