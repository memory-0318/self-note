---
date: 2023-04-29T14:28:00+08:00
title: "在Java模擬當前時間"
tags: ["Java"]
author: "Brian Su"
description: "如何在Java中模擬特定時間?"
header_img: "pexels-clock.jpg"
draft: false
toc: "true"
categories: [
    "themes",
    "syntax",
]
---

## 需求
- 在測試與時效性有關的系統行為時，會希望「假裝」系統真的到特定的時間點，驗證系統有什麼不一樣的行為，而不是真的非得等到那個時候才能驗證。
## 思路
- 在Java中，當下時間多半是透過`ZonedDateTime.now()`或`LocalDateTime.now()`等方式取得，這些function均透過`java.time.Clock`物件取得當下瞬間的時間。
	- `LocalDateTime.now()`預設只會透過`Clock`取得當下瞬間的時間，因為`LocalDateTime`沒有時區資訊。
	- `OffsetDateTime.now()`預設除透過`Clock`取得當下瞬間的時間，還會將時差 (Offset)帶入轉換計算。
	- `ZonedDateTime.now()`除了瞬間時間資訊外，還會帶入時區，有時區資訊就還能額外處理日光節約時間，這點與`OffsetDateTime.now()`不同。
- 為了要模擬當下時間且不依賴 Spring等框架的幫助，額外設計一個Wrapper包裝`ZonedDateTime`等物件，可依需求要模擬時間，或直接取得實際當下的時間。
## 作法
- 新增一個Wrapper
```java
public static class TimeUtils {
	private static Clock clock = Clock.systemUTC();

	// 設定時區
	public static void setTimeZone(ZoneId zoneId) {
		clock = Clock.system(zoneId);
	}

	// 將Clock凍結在指定的瞬間
	public static void setFixed(Instant instant, ZonedId zonedId) {
		clock = Clock.fixed(instant, zonedId);
	}

	// 取得瞬時時間
	public static ZonedDateTime currentZonedDateTime() {
		return ZonedDateTime.now(clock);
	}
}
```