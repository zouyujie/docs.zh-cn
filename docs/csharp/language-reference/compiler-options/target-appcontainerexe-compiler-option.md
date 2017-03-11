---
title: "/target:appcontainerexe（C# 编译器选项） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
ms.assetid: e7e62229-23ea-4e53-bef5-380d951bf95f
caps.latest.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 13
---
# /target:appcontainerexe（C# 编译器选项）
如果使用 **\/target:appcontainerexe** 编译器选项，则编译器会创建一个必须在应用容器中运行的 Windows 可执行 \(.exe\) 文件。  此选项与 [\/target:winexe](../../../csharp/language-reference/compiler-options/target-winexe-compiler-option.md) 等效，但专门用于 [!INCLUDE[win8_appname_long](../../../csharp/includes/win8-appname-long-md.md)] 应用。  
  
## 语法  
  
```  
/target:appcontainerexe  
```  
  
## 备注  
 为了要求应用在应用容器中运行，此选项在[可移植可执行](http://go.microsoft.com/fwlink/p/?LinkId=236960) \(PE\) 文件中设置了一位。  设置该位时，如果 CreateProcess 方法尝试在应用容器外启动该可执行文件，就会发生错误。  
  
 除非使用 [\/out](../../../csharp/language-reference/compiler-options/out-compiler-option.md) 选项，否则输出文件名采用包含 [Main](../../../csharp/programming-guide/main-and-command-args/main-and-command-line-arguments.md) 方法的输入文件的名称。  
  
 如果在命令提示符处指定此选项，则在下一个 **\/out** 或 **\/target** 选项之前，会使用所有文件来创建可执行文件。  
  
### 在 IDE 中设置此编译器选项  
  
1.  在**“解决方案资源管理器”**中，打开项目的快捷菜单，然后选择**“属性”**。  
  
2.  在**“应用程序”**选项卡上，在**“输出类型”**列表中选择**“Windows 应用商店应用”**。  
  
     此选项仅可用于 [!INCLUDE[win8_appname_long](../../../csharp/includes/win8-appname-long-md.md)] 应用模板。  
  
 有关如何以编程方式设置此编译器选项的信息，请参阅 <xref:VSLangProj80.ProjectProperties3.OutputType%2A>。  
  
## 示例  
 以下命令将 `filename.cs` 编译为一个只能在应用容器中运行的 Windows 可执行文件。  
  
```  
csc /target:appcontainerexe filename.cs  
```  
  
## 请参阅  
 [\/target \(Specify Output File Format\)](../../../csharp/language-reference/compiler-options/target-compiler-option.md)   
 [\/target:winexe \(Create a Windows Program\)](../../../csharp/language-reference/compiler-options/target-winexe-compiler-option.md)   
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)