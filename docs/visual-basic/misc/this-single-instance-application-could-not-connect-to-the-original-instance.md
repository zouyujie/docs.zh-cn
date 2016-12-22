---
title: "此单实例应用程序未能连接到原始实例 | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vbrAppModel_SingleInstanceCantConnect"
ms.assetid: 7c2c0cee-02a1-4157-be03-39d18e18408f
caps.latest.revision: 12
caps.handback.revision: 12
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 此单实例应用程序未能连接到原始实例
此单实例应用程序未能连接到原始实例。 一些可能导致此问题的原因包括：  
  
-   原始实例停止了响应。  
  
-   应用程序没有创建内核对象的权限。 有关内核对象的详细信息，请参阅 [Mutexes](../Topic/Mutexes.md)。  
  
     内核对象的基名称是通过串联程序集的 GUID、主版本号和次版本号得到的。 例如，基名称可能是 `3639f15d-9547-43da-8145-60da347829915.1`。  
  
### 在开发应用程序时更正此错误  
  
1.  检查应用程序未进入未响应状态。  
  
2.  检查应用程序是否具有创建内核对象的足够权限。  
  
3.  重启应用程序的原始实例。  
  
4.  重启计算机，以清除可能正在使用连接到原始实例应用程序所需资源的任何进程。  
  
5.  记录发生错误的环境，并与 Microsoft 产品支持服务联系。  
  
## 请参阅  
 [NIB：如何：指定应用程序的实例化行为 \(Visual Basic\)](http://msdn.microsoft.com/zh-cn/48539ad8-d960-4210-beab-ee65f6c6dc6e)   
 [调试器基础知识](/visual-studio/debugger/debugger-basics)   
 [PAVEOVER 产品支持和辅助功能](http://msdn.microsoft.com/zh-cn/14e1d293-7b6d-40a6-bf3e-a92f8ee6c88c)