---
title: "/reference (Visual Basic) | Microsoft Docs"
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
  - "/r 编译器选项 [Visual Basic]"
  - "/reference 编译器选项 [Visual Basic]"
  - "r 编译器选项 [Visual Basic]"
  - "-r 编译器选项 [Visual Basic]"
  - "reference 编译器选项 [Visual Basic]"
  - "-reference 编译器选项 [Visual Basic]"
ms.assetid: 66bdfced-bbf6-43d1-a554-bc0990315737
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /reference (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

使编译器将指定程序集中的类型信息对当前正在编译的项目可用。  
  
## 语法  
  
```  
/reference:fileList  
' -or-  
/r:fileList  
```  
  
## 参数  
  
|||  
|-|-|  
|术语|定义|  
|`fileList`|必选。  程序集文件名的逗号分隔列表。  如果文件名包含空格，则将该文件名置于引号中。|  
  
## 备注  
 导入的文件必须包含程序集元数据。  在程序集以外，只有公共类型是可见的。  [\/addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md) 选项导入模块中的元数据。  
  
 如果引用一个程序集（程序集 A），而其本身引用了另一个程序集（程序集 B），那么在下列情况下需要引用程序集 B：  
  
-   程序集 A 中的类型继承自程序集 B 中的类型或实现程序集 B 中的接口。  
  
-   调用具有程序集 B 中的返回类型或参数类型的字段、属性、事件或方法。  
  
 使用 [\/libpath](../../../visual-basic/reference/command-line-compiler/libpath.md) 指定一个或多个程序集引用所在的目录。  
  
 要使编译器识别程序集（不是模块）中的类型，必须将它强制解析此类型。  如何达到此目的的示例为定义该类型的一个实例。  还可以使用其他方法来为编译器解析程序集中的类型名称。  例如，如果继承了某个程序集中的类型，那么该类型名称将为编译器所了解。  
  
 默认情况下，使用 Vbc.rsp 响应文件，该文件会引用常用的 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] 程序集。  如果不希望编译器使用 Vbc.rsp，请使用 `/noconfig`。  
  
 `/reference`  的缩写形式是 `/r`。  
  
## 示例  
 下面的代码编译源文件 `nput.vb` 并引用 `etad1.dll` 和 `etad2.dll` 中的程序集来生成 `ut.exe`。  
  
```  
vbc /reference:metad1.dll,metad2.dll /out:out.exe input.vb  
```  
  
## 请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [\/noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)   
 [\/target](../../../visual-basic/reference/command-line-compiler/target.md)   
 [Public](../../../visual-basic/language-reference/modifiers/public.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)