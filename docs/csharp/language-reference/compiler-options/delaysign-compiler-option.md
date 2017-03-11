---
title: "/delaysign (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/delaysign"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "-delaysign compiler option [C#]"
  - "delaysign compiler option [C#]"
  - "/delaysign compiler option [C#]"
ms.assetid: bcb058eb-2933-4e7f-b356-5c941db4de75
caps.latest.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# /delaysign (C# Compiler Options)
此选项将使编译器在输出文件中保留空间，以便以后添加数字签名。  
  
## 语法  
  
```  
/delaysign[ + | - ]  
```  
  
## 参数  
 `+` &#124; `-`  
 如果需要完全签名的程序集，则使用 **\/delaysign\-**。  如果只想将公钥放在程序集中，则使用 **\/delaysign\+**。  默认值为 **\/delaysign\-**。  
  
## 备注  
 如果不与 [\/keyfile](../../../csharp/language-reference/compiler-options/keyfile-compiler-option.md) 或 [\/keycontainer](../../../csharp/language-reference/compiler-options/keycontainer-compiler-option.md) 一起使用，**\/delaysign** 选项将无效。  
  
 如果要求完全签名的程序集，编译器将对包含清单（程序集元数据）的文件进行散列处理，并用私钥对该散列数据进行签名。  产生的数字签名存储在包含清单的文件中。  当果程序集的签名延迟时，编译器将不会计算和存储签名，但会在文件中保留空间以便以后添加签名。  
  
 例如，使用 **\/delaysign\+** 将允许测试人员把程序集放入全局缓存中。  测试完成后，可以通过使用[程序集链接器](../Topic/Al.exe%20\(Assembly%20Linker\).md)实用工具将私钥放入程序集中对程序集进行完全签名。  
  
 有关更多信息，请参见[创建和使用具有强名称的程序集](../Topic/Creating%20and%20Using%20Strong-Named%20Assemblies.md)和[延迟为程序集签名](../Topic/Delay%20Signing%20an%20Assembly.md)。  
  
### 在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的**“属性”**页。  
  
2.  修改**“仅延迟签名”**属性。  
  
 有关如何以编程方式设置此编译器选项的信息，请参见 <xref:VSLangProj80.ProjectProperties3.DelaySign%2A>。  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)