---
title: "/define (C# Compiler Options) | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "/define"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "-define compiler option [C#]"
  - "/define compiler option [C#]"
  - "-d compiler option [C#]"
  - "define compiler option [C#]"
  - "/d compiler option [C#]"
  - "d compiler option [C#]"
ms.assetid: f17d7b4d-82d0-4133-8563-68cced1cac6e
caps.latest.revision: 21
caps.handback.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /define (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

**\/define** 选项将 `name` 定义为程序的所有源代码文件中的一个符号。  
  
## 语法  
  
```  
/define:name[;name2]  
```  
  
## 参数  
 `name`, `name2`  
 要定义的一个或多个符号的名称。  
  
## 备注  
 使用 **\/define** 选项与使用 [\#define](../../../csharp/language-reference/preprocessor-directives/preprocessor-define.md) 预处理器指令具有相同的效果，不同点在于编译器选项对项目中的所有文件都有效。  在源文件中的 [\#undef](../../../csharp/language-reference/preprocessor-directives/preprocessor-undef.md) 指令移除定义之前，符号在源文件中始终保持已定义状态。  使用 \/define 选项时，一个文件中的 `#undef` 指令不会影响到项目中的其他源代码文件。  
  
 可以将用该选项创建的符号与 [\#if](../../../csharp/language-reference/preprocessor-directives/preprocessor-if.md)、[\#else](../../../csharp/language-reference/preprocessor-directives/preprocessor-else.md)、[\#elif](../../../csharp/language-reference/preprocessor-directives/preprocessor-elif.md) 和 [\#endif](../../../csharp/language-reference/preprocessor-directives/preprocessor-endif.md) 一起使用，以按条件编译源文件。  
  
 **\/d** 是 **\/define** 的缩写形式。  
  
 通过使用分号或逗号分隔符号名称，可以使用 **\/define** 定义多个符号。  例如：  
  
```  
/define:DEBUG;TUESDAY  
```  
  
 C\# 编译器自身没有定义可以在源代码中使用的符号或宏；所有符号定义必须是用户定义的。  
  
> [!NOTE]
>  与 C\+\+ 这样的语言相同，C\# `#define` 不允许给符号赋值。  例如，不能使用 `#define` 创建宏或定义常数。  如果您需要定义常数，请使用 `enum` 变量。  如果您希望创建 C\+\+ 样式的宏，请考虑其他方式，例如泛型。  由于宏有容易出错的坏名声，因此 C\# 不允许使用宏，而是提供了其他更安全的选择。  
  
### 在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的**“属性”**页。  
  
2.  在**“生成”**选项卡上，键入要在**“条件编译符号”**框中定义的符号。  例如，如果要使用下面的代码示例，只需在文本框中键入 `xx`。  
  
 有关如何以编程方式设置此编译器选项的信息，请参见 <xref:VSLangProj80.CSharpProjectConfigurationProperties3.DefineConstants%2A>。  
  
## 示例  
  
```  
// preprocessor_define.cs  
// compile with: /define:xx  
// or uncomment the next line  
// #define xx  
using System;  
public class Test   
{  
    public static void Main()   
    {  
        #if (xx)   
            Console.WriteLine("xx defined");  
        #else  
            Console.WriteLine("xx not defined");  
        #endif  
    }  
}  
```  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)