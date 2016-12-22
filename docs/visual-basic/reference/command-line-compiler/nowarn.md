---
title: "/nowarn | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "/nowarn 编译器选项 [Visual Basic]"
  - "nowarn 编译器选项 [Visual Basic]"
  - "-nowarn 编译器选项 [Visual Basic]"
ms.assetid: 7ebf2106-0652-4fdc-bf60-70fc86465d83
caps.latest.revision: 15
caps.handback.revision: 15
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /nowarn
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

取消编译器生成警告的能力。  
  
## 语法  
  
```  
/nowarn[:numberList]  
```  
  
## 参数  
  
|||  
|-|-|  
|术语|定义|  
|`numberList`|可选。  编译器应取消的警告的 ID 号列表，以逗号分隔。  如果没有指定警告 ID，则取消所有警告。|  
  
## 备注  
 `/nowarn` 选项可导致编译器不生成警告。  若要取消单个警告，请在 `/nowarn` 选项后加上冒号并在后面指定警告 ID。  用逗号分隔多个警告编号。  
  
 仅需要指定警告标识符的数值部分。  例如，如果要取消 BC42024（未使用的局部变量），请指定 `/nowarn:42024`。  
  
 有关警告 ID 号的更多信息，请参见 [在 Visual Basic 中配置警告](/visual-studio/ide/configuring-warnings-in-visual-basic)。  
  
||  
|-|  
|在 Visual Studio 集成开发环境中设置 \/nowarn|  
|1.  在**“解决方案资源管理器”**中选择一个项目。  在**“项目”**菜单上，单击**“属性”**。  有关更多信息，请参见[Introduction to the Project Designer](http://msdn.microsoft.com/zh-cn/898dd854-c98d-430c-ba1b-a913ce3c73d7)。<br />2.  单击**“编译”**选项卡。<br />3.  选中**“禁用所有警告”**复选框以禁用所有警告。<br />     \- 或 \-<br />     若要禁用特定警告，请在警告旁边的下拉列表中单击**“无”**。|  
  
## 示例  
 下面的代码编译 `T2.vb` 并且不显示任何警告。  
  
```  
vbc /nowarn t2.vb  
```  
  
## 示例  
 下面的代码编译 `T2.vb` 并且不为未使用的局部变量 \(42024\) 显示警告。  
  
```  
vbc /nowarn:42024 t2.vb  
```  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [在 Visual Basic 中配置警告](/visual-studio/ide/configuring-warnings-in-visual-basic)