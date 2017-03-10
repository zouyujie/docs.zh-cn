---
title: "如何：在 Visual Basic 中上载文件 | Microsoft Docs"
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
  - "文件, 上载"
  - "My.Computer.Network.UploadFile 方法"
  - "网络, 上载文件"
  - "UploadFile 方法"
  - "上载文件"
ms.assetid: a8b37924-c523-4fd3-b5ca-cb0074df29cd
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# 如何：在 Visual Basic 中上载文件
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

可以使用 <xref:Microsoft.VisualBasic.Devices.Network.UploadFile%2A> 方法上载文件，并将上载后的文件存储在远程位置。  如果 `ShowUI` 参数设置为 `True`，则显示一个对话框，该对话框显示上载的进度并允许用户取消该操作。  
  
### 上载文件  
  
-   使用 `UploadFile` 方法上载文件，同时将源文件的位置和目标目录的位置指定为字符串或 URI（统一资源标识符）。此示例将 `Order.txt` 文件上载到 `http://www.cohowinery.com/uploads.aspx`。  
  
     [!code-vb[VbResourceTasks#6](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/visualbasic/how-to-upload-a-file_1.vb)]  
  
### 上载文件并显示该操作的进度  
  
-   使用 `UploadFile` 方法上载文件，同时将源文件的位置和目标目录的位置指定为字符串或 URI。  此示例在不提供用户名或密码的情况下将 `Order.txt` 文件上载到 `http://www.cohowinery.com/uploads.aspx`，显示上载操作的进度，并将超时间隔设置为 500 毫秒。  
  
     [!code-vb[VbResourceTasks#7](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/visualbasic/how-to-upload-a-file_2.vb)]  
  
### 在提供用户名和密码的情况下上载文件  
  
-   使用 `UploadFile` 方法上载文件，同时将源文件的位置和目标目录的位置指定为字符串或 URI，并指定用户名和密码。  此示例将 `Order.txt` 文件上载到 `http://www.cohowinery.com/uploads.aspx`，同时提供用户名 `anonymous` 和一个空密码。  
  
     [!code-vb[VbResourceTasks#8](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/visualbasic/how-to-upload-a-file_3.vb)]  
  
## 可靠编程  
 以下情况可能会引发异常：  
  
-   本地文件路径无效 \(<xref:System.ArgumentException>\)。  
  
-   身份验证失败 \(<xref:System.Security.SecurityException>\)。  
  
-   连接超时 \(<xref:System.TimeoutException>\)。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Devices.Network?displayProperty=fullName>   
 <xref:Microsoft.VisualBasic.Devices.Network.UploadFile%2A>   
 [如何：下载文件](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-download-a-file.md)   
 [如何：分析文件路径](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-parse-file-paths.md)