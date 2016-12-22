---
title: "/win32icon | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
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
  - "/win32icon 编译器选项 [Visual Basic]"
  - "win32icon 编译器选项 [Visual Basic]"
  - "-win32icon 编译器选项 [Visual Basic]"
ms.assetid: aecaab01-9353-46c5-941c-6edabd4eff92
caps.latest.revision: 13
caps.handback.revision: 13
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /win32icon
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

将 .ico 文件插入到输出文件中。  此.ico文件表示在 **\*\*\* 文件资源管理器 \*\*\***的输出文件。  
  
## 语法  
  
```  
/win32icon:filename  
```  
  
## 参数  
  
|||  
|-|-|  
|术语|定义|  
|`filename`|要添加到输出文件中的 .ico 文件。  如果文件名包含空格，则将该文件名置于引号 \(" "\) 中。|  
  
## 备注  
 可以使用 Microsoft Windows 资源编译器 \(RC\) 创建 .ico 文件。  编译 Visual C\+\+ 程序时将调用资源编译器；.ico 文件是从 .rc 文件创建的。  `/win32icon` 和 `/win32resource` 选项是互斥的。  
  
 请参见 [\/linkresource](../../../visual-basic/reference/command-line-compiler/linkresource.md) 以引用一个 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] 资源文件，或者参见 [\/resource](../../../visual-basic/reference/command-line-compiler/resource.md) 以附加一个 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] 资源文件。  若要导入 .res 文件，请参见 [\/win32resource](../../../visual-basic/reference/command-line-compiler/win32resource.md)。  
  
||  
|-|  
|在 Visual Studio IDE 中设置 \/win32icon|  
|1.  在**“解决方案资源管理器”**中选择一个项目。  在**“项目”**菜单上，单击**“属性”**。  有关更多信息，请参见[Introduction to the Project Designer](http://msdn.microsoft.com/zh-cn/898dd854-c98d-430c-ba1b-a913ce3c73d7)。<br />2.  单击**“应用程序”**选项卡。<br />3.  在**“图标”**框中修改此值。|  
  
## 示例  
 下面的代码编译 `In.vb` 并附加一个 .ico 文件、`Rf.ico`。  
  
```  
vbc /win32icon:rf.ico in.vb  
```  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)