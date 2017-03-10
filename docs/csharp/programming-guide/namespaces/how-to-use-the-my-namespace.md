---
title: "如何：使用 My 命名空间（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "C# 语言, My 命名空间访问"
ms.assetid: e7152414-0ea5-4c8e-bf02-c8d5bbe45ff4
caps.latest.revision: 12
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 12
---
# 如何：使用 My 命名空间（C# 编程指南）
<xref:Microsoft.VisualBasic.MyServices> 命名空间（Visual Basic 中的 `My`）提供对许多 .NET Framework 类的简单直观的访问，使您能够编写可与计算机、应用程序、设置、资源等交互的代码。  虽然 `MyServices` 命名空间最初是为使用 Visual Basic 而设计的，但它也可以在 C\# 应用程序中使用。  
  
 有关在 Visual Basic 中使用 `MyServices` 命名空间的更多信息，请参见 [使用 My 开发](../../../visual-basic/developing-apps/development-with-my/index.md)。  
  
## 添加引用  
 在解决方案中使用 `MyServices` 类之前，必须添加一个对 Visual Basic 库的引用。  
  
#### 添加对 Visual Basic 库的引用  
  
1.  在**“解决方案资源管理器”**中右击**“引用”**节点，再选择**“添加引用”**。  
  
2.  出现**“引用”**对话框后，向下滚动列表，选择“Microsoft.VisualBasic.dll”。  
  
     您可能还需要在程序开头的 `using` 节中包括以下行。  
  
     [!code-cs[csProgGuideNamespaces#18](../../../csharp/programming-guide/namespaces/codesnippet/csharp/Namespaces/Namespaces3.cs#18)]  
  
## 示例  
 此示例调用 `MyServices` 命名空间中包含的各种静态方法。  要编译此代码，必须在项目中添加一个对 Microsoft.VisualBasic.DLL 的引用。  
  
 [!code-cs[csProgGuideNamespaces#19](../../../csharp/programming-guide/namespaces/codesnippet/csharp/Namespaces/Namespaces3.cs#19)]  
  
 并不是 `MyServices` 命名空间中的所有的类都可以从 C\# 应用程序调用：例如 <xref:Microsoft.VisualBasic.MyServices.FileSystemProxy> 类就不兼容。  在这种特定情况下，可以改用作为 <xref:Microsoft.VisualBasic.FileIO.FileSystem>（它也包含在 VisualBasic.dll 中）的一部分的静态方法。  例如，下面介绍了如何使用这样的方法来复制目录：  
  
 [!code-cs[csProgGuideNamespaces#20](../../../csharp/programming-guide/namespaces/codesnippet/csharp/Namespaces/Namespaces3.cs#20)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [命名空间](../../../csharp/programming-guide/namespaces/index.md)   
 [使用命名空间](../../../csharp/programming-guide/namespaces/using-namespaces.md)