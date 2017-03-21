---
title: "/debug (Visual Basic) | Microsoft Docs"
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
  - "/debug 编译器选项 [Visual Basic]"
  - "debug 编译器选项 [Visual Basic]"
  - "-debug 编译器选项 [Visual Basic]"
  - "调试编译器开关"
ms.assetid: c2b0bea5-1d5e-499f-9bd5-4f6c6b715ea2
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# /debug (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

让编译器生成调试信息并将其放入输出文件中。  
  
## 语法  
  
```  
/debug[+ | -]  
' -or-  
/debug:[full | pdbonly]  
```  
  
## 参数  
  
|||  
|-|-|  
|术语|定义|  
|`+`  &#124; `-`|可选。  指定 `+` 或 `/debug` 将使编译器生成调试信息，并将这些信息放入一个 .pdb 文件中。  指定 `-` 与不指定 `/debug` 的效果相同。|  
|`full`  &#124; `pdbonly`|可选。  指定编译器生成的调试信息类型。  如果未指定 `/debug:pdbonly`，则默认选项为 `full`，它允许您为正在运行的程序附加一个调试器。  `pdbonly` 参数允许在调试器中启动程序时进行源代码调试，但仅在正在运行的程序附加到调试器时才显示汇编语言代码。|  
  
## 备注  
 使用该选项创建调试版本。  如果未指定 `/debug`、`/debug+` 或 `/debug:full`，将无法调试程序的输出文件。  
  
 默认情况下，不发出调试信息 \(`/debug-`\)。  若要发出调试信息，请指定 `/debug` 或 `/debug+`。  
  
 有关如何配置应用程序调试性能的信息，请参见[令映像更易于调试](../Topic/Making%20an%20Image%20Easier%20to%20Debug.md)。  
  
||  
|-|  
|在 Visual Studio 集成开发环境中设置 \/debug|  
|1.  在**“解决方案资源管理器”**中选定一个项目，然后在**“项目”**菜单中单击**“属性”**。  有关更多信息，请参见[Introduction to the Project Designer](http://msdn.microsoft.com/zh-cn/898dd854-c98d-430c-ba1b-a913ce3c73d7)。<br />2.  单击**“编译”**选项卡。<br />3.  单击**“高级编译选项”**。<br />4.  修改**“生成调试信息”**框中的值。|  
  
## 示例  
 下面的示例将调试信息放入输出文件 `App.exe` 中：  
  
```  
vbc /debug /out:app.exe test.vb  
```  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/bugreport](../../../visual-basic/reference/command-line-compiler/bugreport.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)