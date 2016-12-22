---
title: "演练：在 Visual Basic 中对字符串进行加密和解密 | Microsoft Docs"
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
  - "解密, 字符串"
  - "加密, 字符串"
  - "字符串 [Visual Basic], 解密"
  - "字符串 [Visual Basic], 加密"
ms.assetid: 1f51e40a-2f88-43e2-a83e-28a0b5c0d6fd
caps.latest.revision: 18
caps.handback.revision: 18
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 演练：在 Visual Basic 中对字符串进行加密和解密
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

本演练演示如何借助 3DES \(<xref:System.Security.Cryptography.TripleDES>\) 算法的加密服务提供程序 \(CSP\) 版本，使用 <xref:System.Security.Cryptography.DESCryptoServiceProvider> 类加密和解密字符串。  首先，创建封装 3DES 算法的简单包装器类，并将加密数据存储为 Base\-64 编码字符串。  之后，可使用该包装器在可公开访问的文本文件中安全地存储私有用户数据。  
  
 您可以使用加密来保护用户的机密信息（如密码），并使未经授权的用户无法读取凭据。  这样可防止授权用户的身份被盗用，从而保护用户的资产并提供不可否认性。  加密还可防止未经授权的用户访问用户数据。  
  
 有关更多信息，请参见[加密服务](../Topic/Cryptographic%20Services.md)。  
  
> [!IMPORTANT]
>  与 DES 相比，Rijndael（现在称为“高级加密标准 \(AES\)”）和“三重数据加密标准 \(3DES\)”算法提供的安全性更高，原因是破解它们所需的计算量更大。  有关更多信息，请参见<xref:System.Security.Cryptography.DES>和<xref:System.Security.Cryptography.Rijndael>。  
  
### 创建加密包装器  
  
1.  创建 `Simple3Des` 选件类封装加密和解密方法。  
  
     [!code-vb[VbVbalrStrings#38](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/walkthrough-encrypting-and-decrypting-strings_1.vb)]  
  
2.  将加密命名空间的导入包含 `Simple3Des` 选件类文件的开头。  
  
     [!code-vb[VbVbalrStrings#77](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/walkthrough-encrypting-and-decrypting-strings_2.vb)]  
  
3.  在 `Simple3Des` 选件类中，添加一个私有字段以存储 3DES 加密服务提供程序。  
  
     [!code-vb[VbVbalrStrings#39](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/walkthrough-encrypting-and-decrypting-strings_3.vb)]  
  
4.  添加私有方法，该方法将从指定密钥的哈希创建指定长度的字节数组。  
  
     [!code-vb[VbVbalrStrings#41](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/walkthrough-encrypting-and-decrypting-strings_4.vb)]  
  
5.  添加用来初始化 3DES 加密服务提供程序的构造函数。  
  
     `key` 参数控制 `EncryptData` 和 `DecryptData` 方法。  
  
     [!code-vb[VbVbalrStrings#40](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/walkthrough-encrypting-and-decrypting-strings_5.vb)]  
  
6.  添加加密字符串的公共方法。  
  
     [!code-vb[VbVbalrStrings#42](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/walkthrough-encrypting-and-decrypting-strings_6.vb)]  
  
7.  添加解密字符串的公共方法。  
  
     [!code-vb[VbVbalrStrings#43](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/walkthrough-encrypting-and-decrypting-strings_7.vb)]  
  
     包装类现在可用来保护用户资产了。  在本示例中，它用于在可公开访问的文本文件中安全地存储私有用户数据。  
  
### 测试加密包装器  
  
1.  在其他类中添加一个方法，该方法将使用包装器的 `EncryptData` 方法为字符串加密，并将它写入用户的“我的文档”文件夹。  
  
     [!code-vb[VbVbalrStrings#78](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/walkthrough-encrypting-and-decrypting-strings_8.vb)]  
  
2.  添加一个方法，该方法将从用户的“我的文档”文件夹读取加密字符串，并使用包装器的 `DecryptData` 方法为字符串解密。  
  
     [!code-vb[VbVbalrStrings#79](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/walkthrough-encrypting-and-decrypting-strings_9.vb)]  
  
3.  添加用于调用 `TestEncoding` 和 `TestDecoding` 方法的用户界面代码。  
  
4.  运行该应用程序。  
  
     测试应用程序时，您将注意到：如果提供的密码不正确，应用程序不会解密数据。  
  
## 请参阅  
 <xref:System.Security.Cryptography>   
 <xref:System.Security.Cryptography.DESCryptoServiceProvider>   
 <xref:System.Security.Cryptography.DES>   
 <xref:System.Security.Cryptography.TripleDES>   
 <xref:System.Security.Cryptography.Rijndael>   
 [加密服务](../Topic/Cryptographic%20Services.md)