---
title: "在 .NET Framework 文件 I/O 和文件系统中使用的类 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "文件 I/O 类"
ms.assetid: 4a5ca924-eea8-4a95-a5f0-6ac10de276a3
caps.latest.revision: 15
caps.handback.revision: 15
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 在 .NET Framework 文件 I/O 和文件系统中使用的类 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

下表列出了类常用于 .NET framework 文件 I\/O，分类到文件 I\/O 用于创建流的类、类和类用于读取和写入流。  
  
 若要输入 [!INCLUDE[dnprdnlong](../../../../csharp/programming-guide/events/includes/dnprdnlong_md.md)] 文档和查找更完整列表，请参见 [类库概述](../Topic/.NET%20Framework%20Class%20Library%20Overview.md)。  
  
## 文件、驱动器和目录的基本 I\/O 类  
 下表列出并描述了用于文件 I\/O 的主类。  
  
|类|说明|  
|-------|--------|  
|<xref:System.IO.Directory?displayProperty=fullName>|用于创建，移动和枚举提供静态方法通过目录和子目录。|  
|<xref:System.IO.DirectoryInfo?displayProperty=fullName>|用于创建，移动和枚举提供实例方法通过目录和子目录。|  
|<xref:System.IO.DriveInfo?displayProperty=fullName>|用于创建，移动和枚举的实例方法。|  
|<xref:System.IO.File?displayProperty=fullName>|用于创建，复制，删除，移动和打开文件并帮助提供静态方法在 `FileStream`的创建。|  
|<xref:System.IO.FileAccess?displayProperty=fullName>|定义读取的常数，编写或读写访问文件。|  
|<xref:System.IO.FileAttributes?displayProperty=fullName>|用于文件和目录的特性例如 `Archive`、 `Hidden`和 `ReadOnly`。|  
|<xref:System.IO.FileInfo?displayProperty=fullName>|用于创建，复制，删除，移动和打开文件并帮助提供静态方法在 `FileStream`的创建。|  
|<xref:System.IO.FileMode?displayProperty=fullName>|控件如何打开文件。  此参数在许多构造函数中指定为 `FileStream` 和 `IsolatedStorageFileStream`以及 <xref:System.IO.File> 和 <xref:System.IO.FileInfo>`Open` 方法。|  
|<xref:System.IO.FileShare?displayProperty=fullName>|定义控件的其他文件流可以拥有同一文件的访问类型常量。|  
|<xref:System.IO.Path?displayProperty=fullName>|提供用于处理目录字符串的方法和属性。|  
|<xref:System.Security.Permissions.FileIOPermission?displayProperty=fullName>|通过定义 <xref:System.Security.Permissions.FileIOPermissionAttribute.Read%2A>、 <xref:System.Security.Permissions.FileIOPermissionAttribute.Write%2A>、 <xref:System.Security.Permissions.FileIOPermissionAttribute.Append%2A> 和 <xref:System.Security.Permissions.FileIOPermissionAttribute.PathDiscovery%2A> 权限管理文件和文件夹的访问。|  
  
## 用于创建流的类  
 下表列出并描述了用于创建流的主要类。  
  
|类|说明|  
|-------|--------|  
|<xref:System.IO.BufferedStream?displayProperty=fullName>|在另一个流添加一个缓冲区的层读取和写入操作。|  
|<xref:System.IO.FileStream?displayProperty=fullName>|通过其 <xref:System.IO.FileStream.Seek%2A> 方法支持随机访问文件。  默认情况下<xref:System.IO.FileStream> 同步方式打开文件，但是也支持异步操作。|  
|<xref:System.IO.MemoryStream?displayProperty=fullName>|创建备份存储区是内存的流，而不是文件。|  
|<xref:System.Net.Sockets.NetworkStream?displayProperty=fullName>|提供网络访问的基础数据流。|  
|<xref:System.Security.Cryptography.CryptoStream?displayProperty=fullName>|定义将数据流链接到加密转换。|  
  
## 类用于从流读取和写入流  
 下表显示用于从流读取和写入流的特定类向流的文件。  
  
|**类**|**说明**|  
|-----------|------------|  
|<xref:System.IO.BinaryReader?displayProperty=fullName>|从\+中读取编码字符串和基元数据类型。 <xref:System.IO.FileStream>。|  
|<xref:System.IO.BinaryWriter?displayProperty=fullName>|编写编码字符串和基元数据类型。 <xref:System.IO.FileStream>。|  
|<xref:System.IO.StreamReader?displayProperty=fullName>|读取 <xref:System.IO.FileStream>的字符，使用 <xref:System.IO.StreamReader.CurrentEncoding%2A> 来回转换字节字符。  <xref:System.IO.StreamReader> 尝试确定某一给定流的正确 <xref:System.IO.StreamReader.CurrentEncoding%2A> 的构造函数，根据 <xref:System.IO.StreamReader.CurrentEncoding%2A>的显示特定于序文，如字节顺序标记。|  
|<xref:System.IO.StreamWriter?displayProperty=fullName>|为 `FileStream`字符写入，使用 <xref:System.IO.StreamWriter.Encoding%2A> 将字符转换为字节。|  
|<xref:System.IO.StringReader?displayProperty=fullName>|读取 `String`的字符。  输出可以是任何编码的流或 `String`。|  
|<xref:System.IO.StringWriter?displayProperty=fullName>|为 `String`字符写入。  输出可以是任何编码的流或 `String`。|  
  
## 请参阅  
 [编写流](../Topic/Composing%20Streams.md)   
 [文件和流 I\/O](../Topic/File%20and%20Stream%20I-O.md)   
 [异步文件 I\/O](../Topic/Asynchronous%20File%20I-O.md)   
 [.NET Framework 文件 I\/O 和文件系统基础知识 \(Visual Basic\)](../../../../visual-basic/developing-apps/programming/drives-directories-files/basics-of-net-framework-file-io-and-the-file-system.md)