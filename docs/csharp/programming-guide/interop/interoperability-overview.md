---
title: "互操作性概述（C# 编程指南） | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "C# 语言, 互操作性"
  - "C++ 互操作"
  - "COM 互操作"
  - "互操作性, 关于互操作性"
  - "平台调用"
ms.assetid: c025b2e0-2357-4c27-8461-118f0090aeff
caps.latest.revision: 43
caps.handback.revision: 43
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# 互操作性概述（C# 编程指南）
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

本主题描述在 C\# 托管和非托管代码之间实现互操作性的方法。  
  
## 平台调用  
 平台调用是一种服务，它使托管代码可以调用在动态链接库 \(DLL\)（如 Microsoft Win32 API 中的那些 DLL）中实现的非托管函数。  此服务将查找并调用导出的函数，然后根据需要跨越互用边界封送其参数（整数、字符串、数组、结构等）。  
  
 有关更多信息，请参见[使用非托管 DLL 函数](../Topic/Consuming%20Unmanaged%20DLL%20Functions.md)和 [如何：使用平台调用播放波形文件](../../../csharp/programming-guide/interop/how-to-use-platform-invoke-to-play-a-wave-file.md)。  
  
> [!NOTE]
>  [公共语言运行时](../Topic/Common%20Language%20Runtime%20\(CLR\).md) \(CLR\) 管理对系统资源的访问。  调用 CLR 外部的非托管代码会避开此安全机制，因此会带来安全风险。  例如，非托管代码可能会直接调用非托管代码中的资源，从而避开 CLR 安全机制，。  有关更多信息，请参见 [.NET Framework Security](http://go.microsoft.com/fwlink/?LinkId=37122)（.NET Framework 安全性）。  
  
## C\+\+ Interop  
 可以使用 C\+\+ Interop（又称为 It Just Works \(IJW\)）包装本机 C\+\+ 类，使得用 C\# 或其他 .NET Framework 语言编写的代码可以使用它。  为此，可以编写 C\+\+ 代码来包装本机 DLL 或 COM 组件。  与其他 .NET Framework 语言不同，[!INCLUDE[vcprvc](../../../csharp/programming-guide/interop/includes/vcprvc_md.md)] 支持互操作性，允许托管代码和非托管代码存在于同一个应用程序中，甚至存在于同一个文件中。  然后，可以使用 **\/clr** 编译器开关生成 C\+\+ 代码，从而生成托管程序集。  最后，在 C\# 项目中添加一个对该程序集的引用，并像使用其他托管类那样使用被包装对象。  
  
## 向 C\# 公开 COM 组件  
 可以使用 C\# 项目中的 COM 组件。  一般步骤如下所示：  
  
1.  找到要使用的 COM 组件并注册它。  使用 regsvr32.exe 注册或注销 COM DLL。  
  
2.  在项目中添加对 COM 组件或类型库的引用。  
  
     添加引用时，[!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] 会用到[Tlbimp.exe（类型库导入程序）](../Topic/Tlbimp.exe%20\(Type%20Library%20Importer\).md)，后者将类型库作为输入并输出一个 .NET Framework 互操作程序集。  该程序集又称为运行时可调用包装 \(RCW\)，其中包含了包装类型库中的 COM 类和接口的托管类和接口。  [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] 将生成组件的引用添加至项目。  
  
3.  创建在 RCW 中定义的类的实例。  而这样会创建 COM 对象的实例。  
  
4.  像使用其他托管对象那样使用该对象。  当垃圾回收对该对象进行回收后，COM 对象的实例也会从内存中释放出来。  
  
 有关更多信息，请参见 [向 .NET Framework 公开 COM 组件](../Topic/Exposing%20COM%20Components%20to%20the%20.NET%20Framework.md)。  
  
## 向 COM 公开 C\#  
 COM 客户端可以使用已经正确公开的 C\# 类型。  公开 C\# 类型的基本步骤如下所示：  
  
1.  在 C\# 项目中添加互操作特性。  
  
     可以通过修改 [!INCLUDE[csprcs](../../../csharp/includes/csprcs_md.md)] 项目属性使程序集 COM 可见。  有关更多信息，请参见 [“程序集信息”对话框](/visual-studio/ide/reference/assembly-information-dialog-box)。  
  
2.  生成 COM 类型库并对它进行注册以供 COM 使用。  
  
     可以修改 [!INCLUDE[csprcs](../../../csharp/includes/csprcs_md.md)] 项目属性以自动注册 COM interop 的 C\# 组件。  [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] 使用 [Regasm.exe（程序集注册工具）](../Topic/Regasm.exe%20\(Assembly%20Registration%20Tool\).md)，方法是使用 `/tlb` 命令行切换，其将管理的组件作为输入，以生成类型库。  此类型库描述程序集中的 `public` 类型并添加注册表项，以便 COM 客户端可以创建托管类。  
  
 有关更多信息，请参见[向 COM 公开 .NET Framework 组件](../Topic/Exposing%20.NET%20Framework%20Components%20to%20COM.md)和 [COM 类示例](../../../csharp/programming-guide/interop/example-com-class.md)。  
  
## 请参阅  
 [Improving Interop Performance](http://go.microsoft.com/fwlink/?LinkId=99564)   
 [Introduction to COM Interop](http://go.microsoft.com/fwlink/?LinkId=112406)   
 [Marshaling between Managed and Unmanaged Code](http://go.microsoft.com/fwlink/?LinkId=112398)   
 [与非托管代码交互操作](../Topic/Interoperating%20with%20Unmanaged%20Code.md)   
 [Advanced COM Interoperability](http://msdn.microsoft.com/zh-cn/3ada36e5-2390-4d70-b490-6ad8de92f2fb)   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)