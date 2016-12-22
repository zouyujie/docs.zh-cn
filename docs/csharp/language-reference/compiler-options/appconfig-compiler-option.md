---
title: "/appconfig (C# Compiler Options) | Microsoft Docs"
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
  - "/appconfig"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/appconfig compiler option [C#]"
ms.assetid: 1cdbcbcc-7813-4010-b5b8-e67c107c5a98
caps.latest.revision: 26
caps.handback.revision: 26
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /appconfig (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

**\/appconfig** 编译器选项使 C\# 应用程序能够在程序集绑定时向公共语言运行时 \(CLR\) 指明程序集应用程序配置 \(app.config\) 文件的位置。  
  
## 语法  
  
```  
/appconfig:file  
```  
  
## 参数  
 `file`  
 必选。  包含程序集绑定设置的应用程序配置文件。  
  
## 备注  
 **\/appconfig** 的一种用途是升级方案，在该方案中，程序集必须同时引用特定引用程序集的 .NET Framework 版本和 .NET Framework for Silverlight 版本。  例如，以 Windows Presentation Foundation \(WPF\) 编写的 XAML 设计器可能必须同时引用设计器用户界面的 WPF 桌面和 Silverlight 附带的 WPF 子集。  相同设计器程序集必须访问这两个程序集。  默认情况下，单独引用会导致编译器错误，因为程序集绑定将这两个程序集视为等效。  
  
 **\/appconfig** 编译器选项使您能够通过使用 `<supportPortability>` 标记指定禁用默认行为的 app.config 文件的位置，如下面的示例所示。  
  
 `<supportPortability PKT="7cec85d7bea7798e" enable="false"/>`  
  
 编译器将该文件的位置传递给 CLR 的程序集绑定逻辑。  
  
> [!NOTE]
>  如果您要使用 Microsoft Build Engine \(MSBuild\) 生成应用程序，可通过向 .csproj 文件添加属性标记来设置 **\/appconfig** 编译器选项。  若要使用已经设置在项目中 app.config 文件，添加属性标记 `<UseAppConfigForCompiler>` 到 .csproj 文件并设置其值到 `true`。  若要指定一个不同的 app.config 文件，添加属性标记 `<AppConfigForCompiler>`并设置其值到文件的所在位置。  
  
## 示例  
 下面的示例演示一个 app.config 文件，它使应用程序可以具有对任何 .NET Framework 程序集的 .NET Framework 实现和 .NET Framework for Silverlight 实现的引用，该程序集存在于两个实现中。  **\/appconfig** 编译器选项指定此 app.config 文件的位置。  
  
```  
<configuration>  
      <runtime>  
      <assemblyBinding>  
            <supportPortability PKT="7cec85d7bea7798e" enable="false"/>  
            <supportPortability PKT="31bf3856ad364e35" enable="false"/>  
      </assemblyBinding>  
      </runtime>  
</configuration>  
```  
  
## 请参阅  
 [.NET Framework Assembly Unification Overview](http://msdn.microsoft.com/zh-cn/8d8cc65e-031d-463b-bde3-2c6dc2e3bc48)   
 [\<supportPortability\> 元素](../Topic/%3CsupportPortability%3E%20Element.md)   
 [C\# Compiler Options Listed Alphabetically](../../../csharp/language-reference/compiler-options/listed-alphabetically.md)