---
title: "/reference (C# Compiler Options) | Microsoft Docs"
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
  - "/reference"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/r compiler option [C#]"
  - "reference compiler option [C#]"
  - "r compiler option [C#]"
  - "/reference compiler option [C#]"
  - "-r compiler option [C#]"
  - "metadata import [C#]"
  - "public type information [C#]"
  - "-reference compiler option [C#]"
ms.assetid: 8d13e5b0-abf6-4c46-bf71-2daf2cd0a6c4
caps.latest.revision: 28
caps.handback.revision: 28
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /reference (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

**\/reference** 选项导致编译器将指定文件中的 [公开](../../../csharp/language-reference/keywords/public.md) 类型信息导入到当前项目中，从而使您可以从指定的程序集文件引用元数据。  
  
## 语法  
  
```  
/reference:[alias=]filename  
/reference:filename  
```  
  
## 参数  
 `filename`  
 包含程序集清单的文件的名称。  若要导入多个文件，请为每个文件包括一个单独的 **\/reference** 选项。  
  
 `alias`  
 一个有效的 C\# 标识符，表示将包含程序集中所有命名空间的根命名空间。  
  
## 备注  
 若要从多个文件导入，请为每个文件包括一个 **\/reference** 选项。  
  
 导入的文件必须包含一个清单；输出文件必须已使用 [\/目标:模块](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md) 以外的 [\/目标](../../../csharp/language-reference/compiler-options/target-compiler-option.md) 选项之一编译过。  
  
 **\/r** 是 **\/reference** 的缩写形式。  
  
 使用 [\/addmodule](../../../csharp/language-reference/compiler-options/addmodule-compiler-option.md) 从不包含程序集清单的输出文件导入元数据。  
  
 如果您引用了一个程序集（程序集 A），其本身又引用了另一个程序集（程序集 B），则在下列情况下需要引用程序集 B：  
  
-   使用来自程序集 A 的类型继承自程序集 B 中的类型或实现程序集 B 中的接口。  
  
-   调用具有程序集 B 中的返回类型或参数类型的字段、属性、事件或方法。  
  
 使用 [\/lib](../../../csharp/language-reference/compiler-options/lib-compiler-option.md) 指定一个或多个程序集引用所在的目录。  **\/lib** 主题还讨论了编译器在哪些目录中搜索程序集。  
  
 为使编译器可以识别程序集（而不是模块）中的某个类型，需要强制解析此类型，这可以通过定义此类型的实例来完成。  还有其他方法可为编译器解析程序集中的类型名称：例如，如果您从程序集中的类型继承，编译器就能识别类型名称。  
  
 有时必须从一个程序集内部引用同一组件的两个不同版本。  为此，请在每个文件的 **\/reference** 开关上使用 alias 子选项，以区分两个文件。  此别名将用作组件名称的限定符，并解析为其中一个文件中的组件。  
  
 默认情况下使用 csc 响应 \(.rsp\) 文件，该文件引用常用的 .NET Framework 程序集。  如果希望编译器不要使用 csc.rsp，请使用 [\/noconfig](../../../csharp/language-reference/compiler-options/noconfig-compiler-option.md)。  
  
> [!NOTE]
>  在 Visual Studio 中，请使用**“添加引用”**对话框。  有关更多信息，请参见[如何：使用“添加引用”对话框添加或移除引用](http://msdn.microsoft.com/zh-cn/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)。  在 Visual Studio 2010 和更高版本中，若要确保通过使用 `/reference` 添加引用与通过使用**“添加引用”**对话框添加引用之间的行为等效，必须将您要添加的程序集的**“嵌入互操作类型”**属性设置为**“False”**。  **“True”**为该属性的默认值。  
  
## 示例  
 本示例演示如何使用[外部别名](../../../csharp/language-reference/keywords/extern-alias.md)功能。  
  
 编译源文件，并从先前已编译的 `grid.dll` 和 `grid20.dll` 中导入元数据。 ``  这两个 DLL 包含同一组件的不同版本，您将使用两个带有别名选项的 **\/reference** 编译源文件。  这两个选项如下所示：  
  
 \/reference:GridV1\=grid.dll 和 \/reference:GridV2\=grid20.dll  
  
 这将设置外部别名“GridV1”和“GridV2”，您将在程序中通过外部语句使用它们：  
  
```  
extern alias GridV1;  
extern alias GridV2;  
// Using statements go here.  
```  
  
 完成此操作后，您可以通过在控件名称前添加 GridV1 前缀来引用 grid.dll 中的网格控件，如下所示：  
  
```  
GridV1::Grid  
```  
  
 此外，您可以通过在控件名称前添加 GridV2 前缀来引用 grid20.dll 中的网格控件，如下所示：  
  
```  
GridV2::Grid   
```  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)