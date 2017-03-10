---
title: "My.Resources 对象 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "My.Resources"
  - "My.Resources.MyResources.ResourceManager"
  - "My.Resources.MyResources.Culture"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "My.Resources 对象"
ms.assetid: 34c3f2dc-7b87-432c-9d5f-17ea666bb266
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# My.Resources 对象
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

提供用于访问应用程序资源的属性和类  
  
## 备注  
 `My.Resources` 对象提供对应用程序资源的访问，并使您能够动态地检索应用程序的资源。  有关更多信息，请参见 [管理应用程序资源 \(.NET\)](/visual-studio/ide/managing-application-resources-dotnet)。  
  
 `My.Resources` 对象仅公开全局资源。  它不提供对与窗体相关联的资源文件的访问。  必须从窗体中访问窗体资源。  有关更多信息，请参见 [Walkthrough: Localizing Windows Forms](http://msdn.microsoft.com/zh-cn/9a96220d-a19b-4de0-9f48-01e5d82679e5)。  
  
 从 `My.Resources` 对象可以访问应用程序的区域性特定资源文件。  默认情况下，`My.Resources` 对象从与 <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.UICulture%2A> 属性中的区域性匹配的资源文件中查找资源。  不过，您可以重写此行为，并指定用于资源的特定区域性。  有关更多信息，请参见 [桌面应用程序中的资源](../Topic/Resources%20in%20Desktop%20Apps.md)。  
  
## 属性  
 `My.Resources` 对象的属性提供对您的应用程序资源的只读访问。  若要添加或移除资源，请使用**“项目设计器”**。  有关更多信息，请参见 [How to: Add or Remove Resources](http://msdn.microsoft.com/zh-cn/7b77bc06-3952-4799-b029-def3f8f7f88d)。  使用 `My.Resources.``resourceName` 可访问通过**“项目设计器”**添加的资源。  
  
 您还可以通过以下方式添加或移除资源文件：在**“解决方案资源管理器”**中选择项目，然后在**“项目”**菜单中单击**“添加新项”**或**“添加现有项”**。  使用 `My.Resources.``resourceFileName`.`resourceName` 可以访问以这种方式添加的资源。  
  
 每个资源都有名称、类别和值，这些资源设置确定访问资源的属性在 `My.Resources` 对象中的显示方式。  对于在**“项目设计器”**中添加的资源：  
  
-   名称确定属性名。  
  
-   资源数据是属性值。  
  
-   类别确定属性的类型：  
  
|||  
|-|-|  
|类别|属性数据类型|  
|**字符串**|[String](../../../visual-basic/language-reference/data-types/string-data-type.md)|  
|**图像**|<xref:System.Drawing.Bitmap>|  
|**图标**|<xref:System.Drawing.Icon>|  
|**音频**|<xref:System.IO.UnmanagedMemoryStream><br /><br /> <xref:System.IO.UnmanagedMemoryStream> 类从 <xref:System.IO.Stream> 类派生而来，因此可以对它使用以流为参数的方法（如 <xref:Microsoft.VisualBasic.Devices.Audio.Play%2A> 方法）。|  
|**Files**|-   [String](../../../visual-basic/language-reference/data-types/string-data-type.md)，用于文本文件。<br />-   <xref:System.Drawing.Bitmap>，用于图像文件。<br />-   <xref:System.Drawing.Icon>，用于图标文件。<br />-   <xref:System.IO.UnmanagedMemoryStream>，用于声音文件。|  
|**其他**|由设计器的**“类型”**一栏中的信息决定。|  
  
## 类  
 `My.Resources` 对象将每个资源文件公开为具有共享属性的类。  类名与资源文件的文件名相同。  如上一部分所述，资源文件中的资源公开为类中的属性。  
  
## 示例  
 此示例将窗体的标题对应用程序资源文件中名为的 `Form1Title` 字符串资源。  为了使示例工作，应用程序必须在其资源文件中名为的 `Form1Title` 字符串。  有关更多信息，请参见 [How to: Add or Remove Resources](http://msdn.microsoft.com/zh-cn/7b77bc06-3952-4799-b029-def3f8f7f88d)。  
  
 [!code-vb[VbVbalrMyResources#1](../../../visual-basic/developing-apps/programming/app-settings/codesnippet/visualbasic/VbVbalrMyResources2/Form1.vb#1)]  
  
## 示例  
 此示例将窗体的图标设置为名为 `Form1Icon` 的图标，它存储在应用程序的资源文件中。  为了使示例工作，应用程序必须在其资源文件中名为的 `Form1Icon` 图标。  
  
 [!code-vb[VbVbalrMyResources#2](../../../visual-basic/developing-apps/programming/app-settings/codesnippet/visualbasic/VbVbalrMyResources2/Form1.vb#2)]  
  
## 示例  
 此示例将窗体的背景图像设置为名为 `Form1Background`的图像资源，应用程序资源文件。  若要使此示例正常工作，应用程序必须在其资源文件中名为的 `Form1Background` 图像资源。  
  
 [!code-vb[VbVbalrMyResources#3](../../../visual-basic/developing-apps/programming/app-settings/codesnippet/visualbasic/VbVbalrMyResources2/Form1.vb#3)]  
  
## 示例  
 此示例播放存储为应用程序的资源文件中名为的 `Form1Greeting` 音频资源中的声音。  为了使示例工作，应用程序必须在其资源文件中名为的 `Form1Greeting` 音频资源。  `My.Computer.Audio.Play` 方法仅对 Windows 窗体应用程序可用。  
  
 [!code-vb[VbVbalrMyResources#4](../../../visual-basic/developing-apps/programming/app-settings/codesnippet/visualbasic/VbVbalrMyResources2/Form1.vb#4)]  
  
## 示例  
 此示例检索应用程序的字符串资源的法语区域性版本。  该资源名为 `Message`。  更改 `My.Resources` 对象使用，该示例使用 <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.ChangeUICulture%2A>的区域性。  
  
 若要使此示例正常工作，应用程序必须在其资源文件中名为的 `Message` 字符串，因此，应用程序应有该资源文件， Resources.fr\-FR.resx 的法语区域性版本。  有关更多信息，请参见 [How to: Add or Remove Resources](http://msdn.microsoft.com/zh-cn/7b77bc06-3952-4799-b029-def3f8f7f88d)。  如果应用程序没有资源文件的法语区域性版本， `My.Resource` 对象将从默认区域性资源文件中检索该资源。  
  
 [!code-vb[VbVbalrMyResources#10](../../../visual-basic/developing-apps/programming/app-settings/codesnippet/visualbasic/VbVbalrMyResources2/Form1.vb#10)]  
  
## 请参阅  
 [How to: Add or Remove Resources](http://msdn.microsoft.com/zh-cn/7b77bc06-3952-4799-b029-def3f8f7f88d)   
 [管理应用程序资源 \(.NET\)](/visual-studio/ide/managing-application-resources-dotnet)   
 [桌面应用程序中的资源](../Topic/Resources%20in%20Desktop%20Apps.md)   
 [Walkthrough: Localizing Windows Forms](http://msdn.microsoft.com/zh-cn/9a96220d-a19b-4de0-9f48-01e5d82679e5)