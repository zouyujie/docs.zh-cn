---
title: "/nowin32manifest (Visual Basic) | Microsoft Docs"
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
  - "/nowin32manifest 编译器选项 [Visual Basic]"
  - "nowin32manifest 编译器选项 [Visual Basic]"
  - "-nowin32manifest 编译器选项 [Visual Basic]"
ms.assetid: c0528aae-83b3-4425-99f0-19448e9843e3
caps.latest.revision: 7
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 7
---
# /nowin32manifest (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指示编译器不将任何应用程序清单嵌入到可执行文件中。  
  
## 语法  
  
```  
/nowin32manifest  
```  
  
## 备注  
 使用此选项时，除非在 Win32 资源文件或以后的生成步骤中提供应用程序清单，否则应用程序会受到 Windows Vista 上虚拟化的影响。  有关虚拟化的更多信息，请参见[Windows Vista 上的 ClickOnce 部署](/visual-studio/deployment/clickonce-deployment-on-windows-vista)。  
  
 有关创建清单的更多信息，请参见 [\/win32manifest](../../../visual-basic/reference/command-line-compiler/win32manifest.md)。  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [“项目设计器”, “应用程序”页 \(Visual Basic\)](/visual-studio/ide/reference/application-page-project-designer-visual-basic)