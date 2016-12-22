---
title: "/codepage (Visual Basic) | Microsoft Docs"
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
  - "/codepage 编译器选项 [Visual Basic]"
  - "codepage 编译器选项 [Visual Basic]"
  - "-codepage 编译器选项 [Visual Basic]"
ms.assetid: be36ec33-6800-4505-838c-4124564f5cc9
caps.latest.revision: 17
caps.handback.revision: 17
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /codepage (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

指定要用于编译中所有源代码文件的代码页。  
  
## 语法  
  
```  
/codepage:id  
```  
  
## 参数  
  
|||  
|-|-|  
|术语|定义|  
|`id`|必需。  编译器使用 `id` 指定的代码页解释源文件的编码。|  
  
## 备注  
 若要编译使用特定编码保存的源代码，可以使用 `/codepage` 指定应使用哪个代码页。  `/codepage` 选项适用于编译中的所有源代码文件。  有关更多信息，请参见[.NET Framework 中的字符编码](../Topic/Character%20Encoding%20in%20the%20.NET%20Framework.md)。  
  
 如果源代码文件是使用当前的 ANSI 代码页、Unicode 或 UTF\-8 结合签名来保存的，则不需要 `/codepage` 选项。  默认情况下，[!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] 使用当前 ANSI 代码页保存所有源代码文件，除非用户在**“编码”**对话框中指定了其他编码。  [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] 使用**“编码”**对话框打开用不同的代码页保存的源代码文件。  
  
> [!NOTE]
>  `/codepage` 选项不能在 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] 开发环境中使用；它仅在从命令行进行编译时可用。  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)