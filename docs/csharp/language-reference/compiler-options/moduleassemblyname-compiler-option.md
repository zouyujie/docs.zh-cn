---
title: "/moduleassemblyname (C# Compiler Option) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/moduleassemblyname"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "moduleassemblyname compiler option [C#]"
  - "/moduleassemblyname compiler option [C#]"
  - ".moduleassemblyname compiler option [C#]"
ms.assetid: d464d9b9-f18d-423b-95e9-66c7878fd53a
caps.latest.revision: 10
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 10
---
# /moduleassemblyname (C# Compiler Option)
指定一个程序集，其非公共类型可由 netmodule 访问。  
  
## 语法  
  
```  
/moduleassemblyname:assembly_name  
```  
  
## 参数  
 `assembly_name`  
 程序集的名称，.netmodule 可以访问该程序集的非公共类型。  
  
## 备注  
 应使用**\/moduleassemblyname**，当生成 .netmodule，且满足以下条件的位置：  
  
-   netmodule 需要具有访问现有程序集中非公共类型的权限。  
  
-   知道 .netmodule 将生成的程序集的名称。  
  
-   现存的程序集已经被授予.netmodule 将生成到的程序集友元程序集访问权限。  
  
 有关建立.netmodule 的更多信息，请参见 [\/target:module \(Create Module to Add to Assembly\)](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md)。  
  
 有关友元程序集的更多信息，请参见 [友元程序集](../Topic/Friend%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md)。  
  
 此选项在开发环境中不可用；它仅在从命令行编译时才可用。  
  
 此编译器选项在 Visual Studio 中不可用，且不能通过编程方式进行更改。  
  
## 示例  
 此示例生成具有私有类型的程序集，并且该程序集授予称为 csman\_an\_assembly 的程序集友元程序集访问权限。  
  
```  
// moduleassemblyname_1.cs  
// compile with: /target:library  
using System;  
using System.Runtime.CompilerServices;  
  
[assembly:InternalsVisibleTo ("csman_an_assembly")]  
  
class An_Internal_Class   
{  
    public void Test()   
    {   
        Console.WriteLine("An_Internal_Class.Test called");   
    }  
}  
```  
  
## 示例  
 该例建立一个可访问程序集 moduleassemblyname\_1.dll 中非公共类型的.netmodule。  通过了解此 .netmodule 将生成到调用 csman\_an\_assembly的程序集，可以指定 **\/moduleassemblyname**，允许 .netmodule 在已经别授予csman\_an\_assembly的友元程序集访问权限的程序集中访问非公共类型。  
  
```  
// moduleassemblyname_2.cs  
// compile with: /moduleassemblyname:csman_an_assembly /target:module /reference:moduleassemblyname_1.dll  
class B {  
    public void Test() {  
        An_Internal_Class x = new An_Internal_Class();  
        x.Test();  
    }  
}  
```  
  
## 示例  
 此代码示例通过引用以前生成的程序集和 .netmodule ，生成程序集 csman\_an\_assembly。  
  
```  
// csman_an_assembly.cs  
// compile with: /addmodule:moduleassemblyname_2.netmodule /reference:moduleassemblyname_1.dll  
class A {  
    public static void Main() {  
        B bb = new B();  
        bb.Test();  
    }  
}  
```  
  
  **已调用 An\_Internal\_Class.Test**   
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)