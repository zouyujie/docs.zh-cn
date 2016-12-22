---
title: "/lib (C# Compiler Options) | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "/lib"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "lib compiler option [C#]"
  - "-lib compiler option [C#]"
  - "/lib compiler option [C#]"
ms.assetid: b0efcc88-e8aa-4df4-a00b-8bdef70b7673
caps.latest.revision: 16
caps.handback.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /lib (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

**\/lib** 选项指定通过 [\/reference \(Import Metadata\)](../../../csharp/language-reference/compiler-options/reference-compiler-option.md) 选项引用的程序集的位置。  
  
## 语法  
  
```  
/lib:dir1[,dir2]  
```  
  
## 参数  
 `dir1`  
 在当前工作目录（调用编译器的目录）或公共语言运行时的系统目录中未找到引用的程序集时，编译器将在其中进行查找的目录。  
  
 `dir2`  
 要在其中搜索程序集引用的一个或多个附加目录。  用逗号分隔每个附加目录的名称，中间不要有空格。  
  
## 备注  
 编译器按以下顺序搜索未完全限定的程序集引用：  
  
1.  当前工作目录。  该目录为从其调用编译器的目录。  
  
2.  公共语言运行时系统目录。  
  
3.  由 **\/lib** 指定的目录。  
  
4.  由 LIB 环境变量指定的目录。  
  
 使用 **\/reference** 指定程序集引用。  
  
 **\/lib** 是累加的；每一次指定的值都追加到以前的值中。  
  
 另一种使用 **\/lib** 的方法是，将任何所需的程序集复制到工作目录中；这使您可以仅将程序集名称传递给 **\/reference**。  然后可以从工作目录中删除这些程序集。  由于程序集清单中未指定依赖程序集的路径，因此应用程序可以在目标计算机上启动，然后查找并使用全局程序集缓存中的程序集。  
  
 编译器可以引用程序集并不表示公共语言运行时可以在运行时找到并加载程序集。  有关运行时如何搜索引用的程序集的详细信息，请参见 [运行时如何定位程序集](../Topic/How%20the%20Runtime%20Locates%20Assemblies.md)。  
  
### 在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的**“属性页”**对话框。  
  
2.  单击**“引用路径”**属性页。  
  
3.  修改列表框的内容。  
  
 有关如何以编程方式设置此编译器选项的信息，请参见 <xref:VSLangProj80.ProjectProperties3.ReferencePath%2A>。  
  
## 示例  
 编译 t2.cs 以创建 .exe 文件。  编译器将在工作目录和驱动器 C 上根目录中查找程序集引用。  
  
```  
csc /lib:c:\ /reference:t2.dll t2.cs  
```  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)