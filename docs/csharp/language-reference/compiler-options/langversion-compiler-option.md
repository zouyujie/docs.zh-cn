---
title: "/langversion (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/langversion"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/langversion compiler option [C#]"
  - "-langversion compiler option [C#]"
  - "langversion compiler option [C#]"
ms.assetid: 3fb00b05-a0ff-4782-b313-13a4c0f62d94
caps.latest.revision: 33
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 33
---
# /langversion (C# Compiler Options)
导致编译器只接受所选 C\# 语言规范中包含的语法。  
  
## 语法  
  
```  
/langversion:option  
```  
  
## 参数  
 `option`  
 以下为有效值：  
  
|选项|含义|  
|--------|--------|  
|default|编译器接受所有有效的语言语法。|  
|ISO\-1|编译器只接受 ISO\/IEC 23270:2003 C\# 语言规范中包含的语法。|  
|ISO\-2|编译器只接受 ISO\/IEC 23270:2006 C\# 语言规范中包含的语法。  此规范上在[ISO](http://go.microsoft.com/fwlink/?LinkId=144406)网站。|  
|3|编译器只接受 3.0 版本 [C\# 语言规范](../../../csharp/language-reference/language-specification.md)中包含的语法。|  
  
## 备注  
 C\# 应用程序所引用的元数据不受 **\/langversion** 编译器选项的影响。  
  
 由于 C\# 编译器的每个版本都包含语言规范的扩展，因此 **\/langversion** 不提供该编译器早期版本的等效功能。  
  
 无论您使用的是何种 **\/langversion** 设置，都将使用当前版本的公共语言运行时来创建 .exe 或 .dll。  这种情况的一个例外是友元程序集和 [\/moduleassemblyname \(Specify Friend Assembly for Module\)](../../../csharp/language-reference/compiler-options/moduleassemblyname-compiler-option.md)，它们用于 **\/langversion:ISO\-1**。  
  
### 在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的**“属性”**页。  
  
2.  单击**“生成”**属性页。  
  
3.  单击“高级”按钮。  
  
4.  修改**“语言版本”**属性。  
  
 有关如何以编程方式设置此编译器选项的信息，请参阅 <xref:VSLangProj80.CSharpProjectConfigurationProperties3.LanguageVersion%2A>。  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)   
 [C\# 语言规范](../../../csharp/language-reference/language-specification.md)