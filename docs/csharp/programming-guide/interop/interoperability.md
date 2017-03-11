---
redirect_url: /dotnet/articles/csharp/programming-guide/interop/
caps.handback.revision: 31
---
# 互操作性（C# 编程指南）
互操作性使您能够保留和利用在现有非托管代码中的投入。  运行在公共语言运行时 \(CLR\) 的控制之下的代码称为“托管代码”，运行在 CLR 之外的代码称为“非托管代码”。  COM、COM\+、C\+\+ 组件、ActiveX 组件和 Microsoft Win32 API 都是非托管代码的示例。  
  
 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 通过平台调用服务、<xref:System.Runtime.InteropServices> 命名空间、C\+\+ 互操作性和 COM 互操作性（COM 互操作）来实现与非托管代码的互操作性。  
  
## 本节内容  
 [互操作性概述](../../../csharp/programming-guide/interop/interoperability-overview.md)  
 介绍在 C\# 托管代码和非托管代码之间进行互操作的方法。  
  
 [如何：通过使用 Visual C\# 功能访问 Office 互操作对象](../../../csharp/programming-guide/interop/how-to-access-office-onterop-objects.md)  
 描述 Visual C\# 2010 中引入的功能以便于 Office 编程。  
  
 [如何：在 COM 互操作编程中使用索引属性](../../../csharp/programming-guide/interop/how-to-use-indexed-properties-in-com-interop-rogramming.md)  
 描述如何使用索引属性以访问包含参数的 COM 属性。  
  
 [如何：使用平台调用播放波形文件](../../../csharp/programming-guide/interop/how-to-use-platform-invoke-to-play-a-wave-file.md)  
 介绍如何使用平台调用服务在 Windows 操作系统中播放 .wav 声音文件。  
  
 [演练：Office 编程](../../../csharp/programming-guide/interop/walkthrough-office-programming.md)  
 演示如何创建包含一个指向该工作簿的 Excel 工作簿和 Word 文档。  
  
 [COM 类示例](../../../csharp/programming-guide/interop/example-com-class.md)  
 演示如何将 C\# 类作为 COM 对象公开。  
  
## C\# 语言规范  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## 请参阅  
 <xref:System.Runtime.InteropServices.Marshal.ReleaseComObject%2A?displayProperty=fullName>   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [与非托管代码交互操作](../Topic/Interoperating%20with%20Unmanaged%20Code.md)   
 [演练：Office 编程](../../../csharp/programming-guide/interop/walkthrough-office-programming.md)