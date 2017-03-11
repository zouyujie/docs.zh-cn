---
title: "/warnaserror (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "/warnaserror 编译器选项 [Visual Basic]"
  - "warnaserror 编译器选项 [Visual Basic]"
  - "-warnaserror 编译器选项 [Visual Basic]"
ms.assetid: 49819f1d-a1bd-4201-affe-5afe6d9712e1
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# /warnaserror (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

使编译器将出现的第一个警告视为错误。  
  
## 语法  
  
```  
/warnaserror[+ | -][:numberList]  
```  
  
## 参数  
  
|||  
|-|-|  
|术语|定义|  
|\+ &#124; \-|可选。  默认情况下，`/warnaserror-` 有效；此时警告不阻止编译器生成输出文件。  `/warnaserror`  选项与 `/warnaserror+` 相同，它使警告被视为错误。|  
|`numberList`|可选。  `/warnaserror` 选项应用的逗号分隔的警告 ID 编号列表。  如果未指定警告 ID，`/warnaserror` 选项将应用于所有警告。|  
  
## 备注  
 `/warnaserror` 选项将所有警告都视为错误。  任何平常被报告为警告的消息都被报告为错误。  编译器将后面出现的相同警告报告为警告。  
  
 默认情况下，`/warnaserror-` 有效，它使警告仅起通知作用。  `/warnaserror`  选项与 `/warnaserror+` 相同，它使警告被视为错误。  
  
 如果只需将一些特定警告视为错误，可以指定一个逗号分隔的警告编号列表，将它们视为错误。  
  
> [!NOTE]
>  `/warnaserror` 选项不控制显示警告的方式。  使用 [\/nowarn](../../../visual-basic/reference/command-line-compiler/nowarn.md) 选项可禁用警告。  
  
||  
|-|  
|在 Visual Studio IDE 中设置 \/warnaserror 将所有警告视为错误|  
|1.  在**“解决方案资源管理器”**中选择一个项目。  在**“项目”**菜单上，单击**“属性”**。  有关更多信息，请参见[Introduction to the Project Designer](http://msdn.microsoft.com/zh-cn/898dd854-c98d-430c-ba1b-a913ce3c73d7)。<br />2.  单击**“编译”**选项卡。<br />3.  请确保未选中**“禁用所有警告”**复选框。<br />4.  选中**“将所有警告视为错误”**复选框。|  
  
||  
|-|  
|在 Visual Studio IDE 中设置 \/warnaserror 将特定警告视为错误|  
|1.  在**“解决方案资源管理器”**中选择一个项目。  在**“项目”**菜单上，单击**“属性”**。<br />2.  单击**“编译”**选项卡。<br />3.  请确保未选中**“禁用所有警告”**复选框。<br />4.  请确保未选中**“将所有警告视为错误”**复选框。<br />5.  从应被视为错误的警告旁边的**“通知”**列中选择**“错误”**。|  
  
## 示例  
 下面的代码编译 `In.vb` 并指示编译器在每个警告第一次出现时都显示为错误。  
  
```  
vbc /warnaserror in.vb  
```  
  
## 示例  
 下面的代码编译 `T2.vb` 并只将对无用局部变量 \(42024\) 的警告视为错误。  
  
```  
vbc /warnaserror:42024 t2.vb  
```  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [在 Visual Basic 中配置警告](/visual-studio/ide/configuring-warnings-in-visual-basic)