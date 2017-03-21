---
title: "/nowin32manifest (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/nowin32manifest"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "nowin32manifest compiler option [C#]"
  - "-nowin32manifest compiler option [C#]"
  - "/nowin32manifest compiler option [C#]"
ms.assetid: 6f06365b-b87b-46a2-b187-b3bfeaf4862d
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 13
---
# /nowin32manifest (C# Compiler Options)
使用 **\/nowin32manifest** 选项可指示编译器不将任何应用程序清单嵌入到可执行文件中。  
  
## 语法  
  
```  
/nowin32manifest  
```  
  
## 备注  
 使用此选项时，除非在 Win32 资源文件或以后的生成步骤中提供应用程序清单，否则应用程序会受到 Windows Vista 上虚拟化的影响。  有关虚拟化的更多信息，请参见[New UAC Technologies for Windows Vista](http://msdn.microsoft.com/zh-cn/80efa4c7-3904-45c5-82e8-2d558fe67db9)。  
  
 在 Visual Studio 的**“应用程序属性”**页中，通过在**“清单”**下拉列表中选择**“创建不带清单的应用程序”**选项来设置此选项。  有关更多信息，请参见[“项目设计器”\-\>“应用程序”页 \(C\#\)](/visual-studio/ide/reference/application-page-project-designer-csharp)。  
  
 有关创建清单的更多信息，请参见 [\/win32manifest \(Import a Custom Win32 Manifest File\)](../../../csharp/language-reference/compiler-options/win32manifest-compiler-option.md)。  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)