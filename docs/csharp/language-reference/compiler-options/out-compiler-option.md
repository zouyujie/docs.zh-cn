---
title: "/out (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/out"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/out compiler option [C#]"
  - "out compiler option [C#]"
  - "-out compiler option [C#]"
ms.assetid: 70d91d01-7bd2-4aea-ba8b-4e9807e9caa5
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# /out (C# Compiler Options)
**\/out** 选项指定输出文件的名称。  
  
## 语法  
  
```  
/out:filename  
```  
  
## 参数  
 `filename`  
 由编译器创建的输出文件的名称。  
  
## 备注  
 在命令行中，可以为编译指定多个输出文件。  编译器希望在 **\/out** 选项之后找到一个或多个源代码文件。  这样一来，所有的源代码文件都将被编译到 **\/out** 选项所指定的那个输出文件中。  
  
 指定要创建的文件的完整名称和扩展名。  
  
 如果不指定输出文件的名称：  
  
-   .exe 文件将从包含 **Main** 方法的源代码文件中获取其名称。  
  
-   一个.dll或者netmodule 将从第一个源代码文件中获取其名称。  
  
 用于编译一个输出文件的源代码文件不能在相同的编译中用作另一个输出文件的编译。  
  
 当在命令行编译中产生多个输出文件时，请记住其中只有一个输出文件可以是程序集并且只有用 **\/out** 隐式或显式指定的第一个输出文件才是程序集。  
  
 作为编译的一部分产生的任何模块都变成与编译中产生的所有程序集相关的文件。  使用 [ildasm.exe](../Topic/Ildasm.exe%20\(IL%20Disassembler\).md) 浏览程序集清单以查看相关的文件。  
  
 为使 EXE 成为友元程序集的目标，需要 \/out 编译器选项。  有关更多信息，请参见[友元程序集](../Topic/Friend%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md)。  
  
### 在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的**“属性”**页。  
  
2.  单击**“应用程序”**属性页。  
  
3.  修改**“程序集名称”**属性。  
  
     若要以编程方式设置此编译器选项：<xref:VSLangProj80.ProjectProperties3.OutputFileName%2A> 是只读属性，它由项目类型（exe、库等）和程序集名称的组合确定。  必须修改这两个属性中的一个或全部才能设置输出文件名。  
  
## 示例  
 编译 `t.cs` 并创建输出文件 `t.exe`，同时又生成 `t2.cs` 并创建模块输出文件 `mymodule.netmodule`：  
  
```  
csc t.cs /out:mymodule.netmodule /target:module t2.cs  
```  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [友元程序集](../Topic/Friend%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)