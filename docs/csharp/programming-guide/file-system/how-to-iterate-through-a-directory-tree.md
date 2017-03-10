---
title: "如何：循环访问目录树（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "文件迭代 [C#]"
  - "循环访问文件夹 [C#]"
ms.assetid: c4be4a75-6b1b-46a7-9d38-bab353091ed7
caps.latest.revision: 10
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 10
---
# 如何：循环访问目录树（C# 编程指南）
词组“循环访问目录树”的意思是在指定的根文件夹下，访问每个嵌套子目录中任意深度的所有文件。  您不必打开每一个文件。  可以只检索 `string` 形式的文件名或子目录名，或者可以检索 <xref:System.IO.FileInfo?displayProperty=fullName> 或 <xref:System.IO.DirectoryInfo?displayProperty=fullName> 对象形式的其他信息。  
  
> [!NOTE]
>  在 Windows 中，可交换使用术语“目录”和“文件夹”。  大多数文档和用户界面文本使用术语“文件夹”，但 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 类库使用术语“目录”。  
  
 最简单的例子，如果您确信您拥有指定根目录下所有目录的访问权限，则您可以使用 `System.IO.SearchOption.AllDirectories` 标志。  该标志返回与指定模式相匹配的所有嵌套子目录。  下面的示例演示如何使用该标志。  
  
```c#  
root.GetDirectories("*.*", System.IO.SearchOption.AllDirectories);  
```  
  
 此方法的缺点是，如果指定根目录下任何一个子目录引发了 <xref:System.IO.DirectoryNotFoundException> 或 <xref:System.UnauthorizedAccessException>，则整个方法将会失败并且不返回任何目录。  使用 <xref:System.IO.DirectoryInfo.GetFiles%2A> 方法时也是如此。  如果一定要处理特定子文件夹中的这些异常，则必须手动遍历该目录树，如下面的示例所示。  
  
 手动遍历目录树时，可以先处理子目录（前序遍历），或者可以先处理文件（后序遍历）。  如果执行前序遍历，则在循环访问直接位于当前文件夹本身中的文件之前，请先遍历当前文件夹下的整个树。  本文档后面的示例执行的是后序遍历，但您可以轻松地将它们修改为执行前序遍历。  
  
 另外还可以选择是使用递归遍历，还是使用基于堆栈的遍历。  本文档后面的示例对这两种方法进行了演示。  
  
 如果必须对文件和文件夹上执行各种操作，则可以通过下面的方法将这些示例模块化：将操作重构到单独的函数，这样您就可以通过单个委托来调用这些函数。  
  
> [!NOTE]
>  NTFS 文件系统可以包含交接点、符号链接和硬链接形式的重新分析点。  .NET Framework 方法（如 <xref:System.IO.DirectoryInfo.GetFiles%2A> 和 <xref:System.IO.DirectoryInfo.GetDirectories%2A>）将不返回重新分析点下的任何子目录。  此行为可防止两个重新分析点相互引用时陷入无限循环。  通常，为了确保您不会无意修改或删除文件，在使用重新分析点时应特别小心。  如果需要精确控制重新分析点，请使用平台调用或本机代码直接调用相应的 Win32 文件系统方法。  
  
## 示例  
 下面的示例演示如何使用递归遍历目录树。  递归方法很简洁，但如果目录树很大且嵌套很深，则有可能会引起堆栈溢出异常。  
  
 对于所处理的特定异常以及在每个文件和文件夹上执行的特定操作，都只是作为示例提供。  您应该修改此代码来满足自己特定的需要。  有关更多信息，请参见代码中的注释。  
  
 [!code-cs[csFilesandFolders#1](../../../csharp/programming-guide/file-system/codesnippet/csharp/csFilesFolders/FileIteration.cs#1)]  
  
## 示例  
 下面的示例演示在不使用递归的情况下如何循环访问目录树中的文件和文件夹。  该技术使用泛型 <xref:System.Collections.Generic.Stack%601> 集合类型，该类型是一个后进先出 \(LIFO\) 堆栈。  
  
 对于所处理的特定异常以及在每个文件和文件夹上执行的特定操作，都只是作为示例提供。  您应该修改此代码来满足自己特定的需要。  有关更多信息，请参见代码中的注释。  
  
 [!code-cs[csFilesandFolders#2](../../../csharp/programming-guide/file-system/codesnippet/csharp/csFilesFolders/FileIteration.cs#2)]  
  
 通常，测试每个文件夹以确定您的应用程序是否有权限打开它是非常耗时的。  因此，代码示例只是将该部分操作放到了一个 `try/catch` 块内。  您可以修改该 `catch` 块，以便在访问某个文件夹遭受拒绝时，您可以提升自己的权限，然后再次访问它。  通常，只捕捉那些无需使应用程序停留在一个未知状态就可以处理的异常。  
  
 如果必须将目录树的内容存储到内存或磁盘中，则最好只存储每个文件的 <xref:System.IO.FileSystemInfo.FullName%2A> 属性（`string` 类型）。  然后，可以根据需要使用该字符串创建一个新的 <xref:System.IO.FileInfo> 或 <xref:System.IO.DirectoryInfo> 对象，或者打开任何需要进行其他处理的文件。  
  
## 可靠编程  
 可靠文件迭代代码必须考虑文件系统的诸多复杂性。  有关更多信息，请参见 [NTFS Technical Reference](http://go.microsoft.com/fwlink/?LinkId=79488)（NTFS 技术参考）。  
  
## 请参阅  
 <xref:System.IO>   
 [LINQ and File Directories](../../../visual-basic/programming-guide/concepts/linq/linq-and-file-directories.md)   
 [文件系统和注册表](../../../csharp/programming-guide/file-system/file-system-and-the-registry.md)