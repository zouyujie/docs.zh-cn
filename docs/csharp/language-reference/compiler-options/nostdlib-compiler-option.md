---
title: "/nostdlib (C# Compiler Options) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/nostdlib"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "nostdlib compiler option [C#]"
  - "-nostdlib compiler option [C#]"
  - "/nostdlib compiler option [C#]"
ms.assetid: ec197989-fa49-4725-a455-e06b551eb65f
caps.latest.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 18
---
# /nostdlib (C# Compiler Options)
**\/nostdlib** 可防止导入 mscorlib.dll，这定义了整个 System 命名空间。  
  
## 语法  
  
```  
/nostdlib[+ | -]  
```  
  
## 备注  
 如果你想要定义或创建自己的 System 命名空间和对象，请使用此选项。  
  
 如果未指定 **\/nostdlib**，则 mscorlib.dll 将被导入到程序中（与指定 **\/nostdlib\-** 相同）。 指定 **\/nostdlib** 与指定 **\/nostdlib\+** 相同。  
  
### 在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的“属性”页。  
  
2.  单击“生成”属性页。  
  
3.  单击**“高级”**按钮。  
  
4.  修改“不引用 mscorlib.dll”属性。  
  
 有关如何以编程方式设置此编译器选项的信息，请参阅 <xref:VSLangProj80.CSharpProjectConfigurationProperties3.NoStdLib%2A>。  
  
## 请参阅  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)