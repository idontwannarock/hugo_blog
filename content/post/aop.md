---
title: "AOP 及 Spring AOP 簡述"
date: 2018-04-10T13:22:52+08:00
draft: false
tags:
- Spring
- Java
- AOP
categories:
- Programming
- Spring
#disqusIdentifier: fdsF34ff34
keywords:
- Spring
- Java
- AOP
clearReading: true
#thumbnailImage: image-1.png
thumbnailImagePosition: right
#autoThumbnailImage: yes
metaAlignment: center
#coverImage: image-2.png
#coverCaption: "A beautiful sunrise"
#coverMeta: out
#coverSize: full
comments: true
showTags: true
showPagination: true
showSocial: true
showDate: true
showMeta: true
---
<!-- toc -->

> 這篇文章是初學的時候撰寫的，其中一些觀念並不正確，步驟也可能因為更新或觀念問題而不適用或者多餘，此篇文章僅為留做紀錄

# 簡述

- AOP(Aspect-Oriented Programming) 是一種基於 OOP(Object-Oriented Programming) 的改進
- AOP 是基於動態代理 (Dynamic Proxy) 這種 design pattern
- AOP 主要的設計對象是切面 (Aspect)，而切面是用來模組化橫切關注點 (Cross-Cutting Concern)
- 切面需要定義公共功能，但可以明確定義功能在哪裡或以什麼方式應用，而不必修改受影響的類別。如此切面關注點就可以被模組化到特殊的類別 (切面) 裡面

# 優點

- 交易相關的邏輯位於同一位置，便於維護與升級
- 業務邏輯更簡潔，只包含核心業務代碼

# AOP術語及概念

- **Cross-Cutting Concern 橫切關注點**：橫跨應用系統多個流程、模組的功能，例如日誌 (Logging)、安全 (Security) 檢查、交易 (Transaction) 等動作，在許多流程的多個位置都需要執行，這種動作就被稱為橫切關注點
- **Aspect 切面**：橫切關注點被模組化後的一種特殊物件；還未模組化前是橫切關注點，抽取後成為一組一組的切面；另一方面來說代理會將一個一個切面重組為橫切關注點
- **Advice 通知**：切面必須要完成的工作或行為，也就是切面的實作內容。切面裡面的各個方法即是一個、一個的通知
- **Target 目標**：被通知的物件，也就是要被橫切的業務邏輯類別
- **Proxy 代理**：向目標物件通知之後創建的對象。容器會建立一個代理，依照設定去縫合 (weave) 切面到應用程式中
- **JoinPoint 連接點**：程序執行的某個特定位置或時機。例如某個類別的某個方法呼叫前、呼叫後、拋出異常後等等。
	- 連接點由兩個因素決定：**以方法表示的程式執行點、相對執行點表示的方位**。例如 A 類別的 a() 方法執行前的 JoinPoint 連接點決定要素為：執行點 A#a()，方位為執行前的位置
	- 概念類比：**JoinPoint 連接點相當於資料庫的紀錄，切面相當於查詢條件**
- **Pointcut 切面定義**：每個類別都有多個連接點，**類別的所有方法某種程度上都可以想成是 JoinPoint 連接點**。AOP通過切面定位到特定的連接點

# Spring AOP

## 簡述

- AspectJ：Java 社群最完整、最廣為人知的 AOP 實作
- Spring 2.0 以上，可以使用基於 AspectJ 的 annotation 註解或基於 XML 設定的 AOP

## Dependencies

### Spring

- commons logging
- spring beans
- spring context
- spring core
- spring expression

### Spring AOP

- aopalliance
- aspectj weaver
- spring aop
- spring aspects

**註：Spring 框架的版本可以更動，但須一致**

## 設定

- 在 XML 文件中加入 aop namespace

### 基於註解的方式

- 在 XML 文件中加入以下設定：
	- `<aop:aspectj-autoproxy/>`
- 把橫切關注點的程式碼抽象到切面的類別中
	- 切面首先是一個 IOC 中的 bean，所以要加上 `@Component` 註解
	- 切面還需要加入 `@Aspect` 註解
- 在類別中聲明各種通知：
	- 聲明一個方法
	- 在方法前加入五種註解，並配合要通知的目標：
		- `@Before`：執行點之前
		- `@After`：執行點之後，但無法取得回傳值
		- `@AfterReturning`：執行點之後，但可以取得回傳值，執行順序在 `@After` 之前
		- `@AfterThrowing`：執行出現異常後，可以取得異常資訊，執行順序在 `@After` 之前
		- `@Around`：執行點前、後、回傳值等全都包括，通常會配合 ProceedingJoinPoint 類別當參數使用
- 可以在通知方法中聲明一個類別為 JoinPoint 的參數，然後就可以藉此物件取出目標連接點的細節，例如方法名稱及其參數等

### 基於 XML 文件的方式

- 所有相關類別都不需要任何註解
- XML 文件中加入 aop 跟 beans namespace
- 在 XML 文件中先設定好有關的 bean，包括目標類別及切面類別
- 再於 XML 文件中在`<aop:config></aop:config>`元素內設定 AOP 有關設定
- 其中設定的元素跟屬性都跟註解相同