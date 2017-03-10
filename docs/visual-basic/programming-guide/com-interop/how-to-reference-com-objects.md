---
title: "如何：从 Visual Basic 中引用 COM 对象 | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "COM 互操作, 引用 COM 对象"
  - "COM 对象, 引用"
  - "互操作程序集"
  - "对象 [Visual Basic], 引用"
  - "引用对象, Visual Basic 中的 COM 对象"
ms.assetid: 9c518fb4-27d9-4112-9e6a-5a7d0210af6f
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# 如何：从 Visual Basic 中引用 COM 对象
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

在 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 中，如果添加对带有类型库的 COM 对象的引用，将需要为 COM 库创建互操作程序集。  对 COM 对象成员的引用被路由到 Interop 程序集，然后转发到实际的 COM 对象。  来自 COM 对象的响应被路由到互操作程序集，并转发到 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 应用程序。  
  
 通过在 .NET 程序集中嵌入 COM 对象的类型信息，您可以引用 COM 对象而无需使用互操作程序集。  若要嵌入类型信息，请为对 COM 对象的引用将 `Embed Interop Types` 属性设置为 `True`。  如果使用命令行编译器进行编译，请使用 `/link` 选项来引用 COM 库。  有关更多信息，请参见 [\/link](../../../visual-basic/reference/command-line-compiler/link.md)。  
  
 当您从集成开发环境 \(IDE\) 添加对类型库的引用时，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] 会自动创建互操作程序集。  当从命令行工作时，可以使用 Tlbimp 实用工具手动创建 Interop 程序集。  
  
### 向 COM 对象添加引用  
  
1.  在**“项目”**菜单上，选择**“添加引用”**，然后单击对话框中的**“COM”**选项卡。  
  
2.  从 COM 对象列表中选择要用的组件。  
  
3.  为简化对 Interop 程序集的访问，请在要使用 COM 对象的类或模块的上面添加一条 `Imports` 语句。  例如，下面的代码示例将导入 `Microsoft InkEdit Control 1.0` 库中所引用对象的命名空间 `INKEDLib`。  
  
     [!code-vb[VbVbalrInterop#40](../../../visual-basic/programming-guide/com-interop/codesnippet/visualbasic/vbvbalrinterop/Class1.vb#40)]  
  
### 使用 Tlbimp 创建 Interop 程序集  
  
1.  如果 Tlbimp 的位置不是搜索路径的一部分，并且当前路径不在 Tlbimp 的位置所在的目录中，请将 Tlbimp 的位置添加到搜索路径中。  
  
2.  在命令提示符下调用 Tlbimp，提供下列信息：  
  
    -   包含类型库的 DLL 的名称和位置  
  
    -   要放置信息的命名空间的名称和位置  
  
    -   目标 Interop 程序集的名称和位置  
  
     以下代码提供了一个示例：  
  
    ```  
    Tlbimp test3.dll /out:NameSpace1 /out:Interop1.dll  
    ```  
  
     可以使用 Tlbimp 为类型库创建 Interop 程序集，甚至也可以为未注册的 COM 对象创建 Interop 程序集。  但是，由 Interop 程序集引用的 COM 对象必须在要使用它们的计算机上正确注册。  可以使用包含在 Windows 操作系统中的 Regsvr32 实用工具注册一个 COM 对象。  
  
## 请参阅  
 [COM 互操作](../../../visual-basic/programming-guide/com-interop/index.md)   
 [Tlbimp.exe（类型库导入程序）](../Topic/Tlbimp.exe%20\(Type%20Library%20Importer\).md)   
 [Tlbexp.exe（类型库导出程序）](../Topic/Tlbexp.exe%20\(Type%20Library%20Exporter\).md)   
 [演练：用 COM 对象实现继承](../../../visual-basic/programming-guide/com-interop/walkthrough-implementing-inheritance-with-com-objects.md)   
 [互操作性疑难解答](../../../visual-basic/programming-guide/com-interop/troubleshooting-interoperability.md)   
 [Imports 语句（.NET 命名空间和类型）](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)