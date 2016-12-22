---
title: "编译器错误 CS2033 | Microsoft Docs"
ms.custom: ""
ms.date: "10/29/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "CS2033"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS2033"
ms.assetid: edb5784a-5195-4f72-b73d-d1ec9ed3766e
caps.latest.revision: 9
caps.handback.revision: 9
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 编译器错误 CS2033
包含短文件名“filename”的长文件名已存在，无法创建同名短文件名  
  
 编译名称超过八个字符的任何 C\# 文件。 然后，编译另一个具有前面的文件名称的较短形式的文件，例如名称的前六个字符再加上"~1"。 第二个编译将生成此错误。  
  
 若要解决此错误，请将较短文件名重命名为一个与长文件名不冲突的文件名。