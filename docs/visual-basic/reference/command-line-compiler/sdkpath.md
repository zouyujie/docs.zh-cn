---
title: "/sdkpath | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "sdkpath"
  - "/sdkpath"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "/sdkpath 编译器选项 [Visual Basic]"
  - "sdkpath 编译器选项 [Visual Basic]"
  - "-sdkpath 编译器选项 [Visual Basic]"
ms.assetid: fec8a3f1-b791-4a37-8af7-344859f8212d
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# /sdkpath
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定 Mscorlib.dll 和 Microsoft.VisualBasic.dll 的位置。  
  
## 语法  
  
```  
/sdkpath:path  
```  
  
## 参数  
 `path`  
 包含用于编译的 Mscorlib.dll 版本和 Microsoft.VisualBasic.dll 版本的目录。  直到加载后，才会对该路径进行验证。  如果目录名包含空格，则将该目录名置于引号 \(" "\) 中。  
  
## 备注  
 此选项指示 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 编译器从非默认位置加载 Mscorlib.dll 文件和 Microsoft.VisualBasic.dll 文件。  `/sdkpath`  选项设计为与 [\/netcf](../../../visual-basic/reference/command-line-compiler/netcf.md) 一起使用。  [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact-md.md)] 使用这些支持库的不同版本，以避免使用未在设备上找到的类型和语言功能。  
  
> [!NOTE]
>  `/sdkpath` 选项不能在 Visual Studio 开发环境中使用；它仅在从命令行进行编译时可用。  当加载 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 设备项目时，将设置 `/sdkpath` 选项。  
  
 使用 `/vbruntime` 编译器选项，您可以指定编译器是否应在不引用 Visual Basic 运行库的情况下进行编译。  有关更多信息，请参见 [\/vbruntime](../../../visual-basic/reference/command-line-compiler/vbruntime.md)。  
  
## 示例  
 下面的代码使用 [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact-md.md)] 编译 `Myfile.vb`，并使用 C 驱动器上 [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact-md.md)] 的默认安装目录中的 Mscorlib.dll 版本和 Microsoft.VisualBasic.dll 版本。  通常，应该使用最新版 [!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact-md.md)]。  
  
```  
vbc /netcf /sdkpath:"c:\Program Files\Microsoft Visual Studio .NET 2003\CompactFrameworkSDK\v1.0.5000\Windows CE " myfile.vb  
```  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [\/netcf](../../../visual-basic/reference/command-line-compiler/netcf.md)   
 [\/vbruntime](../../../visual-basic/reference/command-line-compiler/vbruntime.md)