---
title: "发生错误，因为无法获得单个实例启动所需的操作系统资源 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrAppModel_CantGetMemoryMappedFile"
dev_langs: 
  - "VB"
ms.assetid: 0d9f2a30-ff72-4355-8060-744f22339359
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# 发生错误，因为无法获得单个实例启动所需的操作系统资源
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

应用程序未能获取所需的操作系统资源。  一些可能导致此问题的原因是：  
  
-   应用程序不具备创建命名操作系统对象的权限。  
  
-   公共语言运行时不具备创建内存映射文件的权限。  
  
-   应用程序需要访问某个操作系统对象，但另一个进程正在使用该对象。  
  
### 更正此错误  
  
1.  检查该应用程序具有创建命名操作系统对象的足够权限。  
  
2.  检查公共语言运行时具有创建内存映射文件的足够权限。  
  
3.  重新启动计算机以清除可能正使用连接到原始实例应用程序所需的资源的任何进程。  
  
4.  记录发生错误的环境，并与 Microsoft 产品支持服务联系  
  
## 请参阅  
 [“项目设计器”, “应用程序”页 \(Visual Basic\)](/visual-studio/ide/reference/application-page-project-designer-visual-basic)   
 [调试器基础知识](/visual-studio/debugger/debugger-basics)   
 [与我们交流](/visual-studio/ide/talk-to-us)