---
title: "打包和部署自定义 My 扩展 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "My 命名空间"
  - "My 命名空间, 自定义"
  - "My 命名空间, 扩展"
ms.assetid: fd89c54b-0290-4c50-95a3-ff17d4487a21
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# 打包和部署自定义 My 扩展 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

Visual Basic 提供了一种通过使用 Visual Studio 模板来部署自定义 `My` 命名空间扩展的简便方法。  对于您的 `My` 扩展为其必要组成部分的新项目类型，如果要为其创建项目模板，则只需要在导出模板时，将您的自定义 `My` 扩展代码包括在该项目中。  有关导出项目模板的更多信息，请参见[如何：创建项目模板](../Topic/How%20to:%20Create%20Project%20Templates.md)。  
  
 如果您的自定义 `My` 扩展在单个代码文件中，则可将该文件作为项模板导出，用户可将该项模板添加到任何类型的 Visual Basic 项目中。  然后，您就可自定义项模板，以在 Visual Basic 项目中启用您的自定义 `My` 扩展的其他功能和行为。  这些功能具体如下：  
  
-   允许用户从 Visual Basic 项目设计器的**“My 扩展”**页管理您的自定义 `My` 扩展。  
  
-   当向项目添加对指定程序集的引用时，自动添加您的自定义 `My` 扩展。  
  
-   在**“添加项”**对话框中隐藏 `My` 扩展项模板，以使项目项列表中不包含该扩展项模板。  
  
 本主题讨论如何将自定义 `My` 扩展打包为可从 Visual Basic 项目设计器的**“My 扩展”**页进行管理的隐藏项模板。  当向项目添加对指定程序集的引用时，还可自动添加自定义 `My` 扩展。  
  
## 创建 My 命名空间扩展  
 为自定义 `My` 扩展创建部署包的第一步是将扩展创建为单个代码文件。  有关如何创建自定义 `My` 扩展的详细信息和指南，请参见[扩展 Visual Basic 中的 My 命名空间](../../../visual-basic/developing-apps/customizing-extending-my/extending-the-my-namespace.md)。  
  
## 将 My 命名空间扩展导出为项模板  
 创建了包含您的 `My` 命名空间扩展的代码文件后，就可以将该代码文件导出为 Visual Studio 项模板。  有关如何将文件导出为 Visual Studio 项模板的说明，请参见[如何：创建项模板](../Topic/How%20to:%20Create%20Item%20Templates.md)。  
  
> [!NOTE]
>  如果 `My` 命名空间扩展具有对特定程序集的依赖项，则您可自定义您的项模板，从而在添加对该程序集的引用时，自动安装您的 `My` 命名空间扩展。  这样，您就可在将代码文件导出为 Visual Studio 项模板时，将该程序集引用排除在外。  
  
## 自定义项模板  
 您可通过自定义，来从 Visual Basic 项目设计器的**“My 扩展”**页管理您的项模板。  您还可通过自定义，从而在向项目添加对指定程序集的引用时，自动添加项模板。  若要启用这些自定义，则请将名称为 CustomData 文件的新文件添加到模板，然后将新元素添加到您的 .vstemplate 文件的 XML。  
  
### 添加 CustomData 文件  
 CustomData 文件是具有 .CustomData 文件扩展名（文件名可设置为对您的模板而言有意义的任何值）并包含 XML 的文本文件。  当用户使用 Visual Basic 项目设计器的**“My 扩展”**页时，CustomData 文件中的 XML 将指示 Visual Basic 包含您的 `My` 扩展。  您可选择将 \<`AssemblyFullName>` 特性添加到您的 CustomData 文件的 XML 中。  这将指示 Visual Basic 在向项目添加对特定程序集的引用时，自动安装您的自定义 `My` 扩展。  您可以使用任何文本编辑器或 XML 编辑器创建 CustomData 文件，然后将该文件添加到项模板的压缩文件夹（.zip 文件）中。  
  
 例如，下面的 XML 显示了 CustomData 文件的内容；在向 Visual Basic 项目添加对 Microsoft.VisualBasic.PowerPacks.Vs.dll 程序集的引用时，该 CustomData 文件会将模板项添加到 Visual Basic 项目的“My 扩展”文件夹中。  
  
```  
<VBMyExtensionTemplate   
    ID="Microsoft.VisualBasic.Samples.MyExtensions.MyPrinterInfo"   
    Version="1.0.0.0"  
    AssemblyFullName="Microsoft.VisualBasic.PowerPacks.vs"  
/>  
```  
  
 CustomData 文件中包含具有下表所列特性的 \<`VBMyExtensionTemplate>` 元素。  
  
|||  
|-|-|  
|特性|说明|  
|`ID`|必选。  扩展的唯一标识符。  如果具有此 ID 的扩展已被添加到项目中，则将不会提示用户再次添加。|  
|`Version`|必选。  项模板的版本号。|  
|`AssemblyFullName`|可选。  一个程序集名称。  在向项目添加对此程序集的引用时，将提示用户从此项模板添加 `My` 扩展。|  
  
### 向 .vstemplate 文件添加 \<CustomDataSignature\> 元素  
 若要将您的 Visual Studio 项模板标识为 `My` 命名空间扩展，则还必须修改项模板的 .vstemplate 文件。  您必须将一个 `<CustomDataSignature>` 元素添加到 `<TemplateData>` 元素。  `<CustomDataSignature>` 元素必须包含文本 `Microsoft.VisualBasic.MyExtension`，如下面的示例所示。  
  
```  
<CustomDataSignature>Microsoft.VisualBasic.MyExtension</CustomDataSignature>  
```  
  
 您不能直接修改压缩文件夹（.zip 文件）中的文件。  而必须先复制压缩文件夹中的 .vstemplate 文件，接着修改该文件，然后用更新后的副本替换压缩文件夹中的 .vstemplate 文件。  
  
 下面的示例演示了添加了 `<CustomDataSignature>` 元素的 .vstemplate 文件的内容。  
  
```  
<VSTemplate Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" Type="Item">  
  <TemplateData>  
    <DefaultName>MyCustomExtensionModule.vb</DefaultName>  
    <Name>MyPrinterInfo</Name>  
    <Description>Custom My Extensions Item Template</Description>  
    <ProjectType>VisualBasic</ProjectType>  
    <SortOrder>10</SortOrder>  
    <Icon>__TemplateIcon.ico</Icon>  
    <CustomDataSignature       >Microsoft.VisualBasic.MyExtension</CustomDataSignature>  
  </TemplateData>  
  <TemplateContent>  
    <References />  
    <ProjectItem SubType="Code"   
                 TargetFileName="$fileinputname$.vb"  
                 ReplaceParameters="true"  
     >MyCustomExtensionModule.vb</ProjectItem>  
  </TemplateContent>  
</VSTemplate>  
```  
  
## 安装模板  
 若要安装模板，则可将压缩文件夹（.zip 文件）复制到 Visual Basic 项模板文件夹（例如，My Documents\\Visual Studio 2008\\Templates\\Item Templates\\Visual Basic）中。  另外，还可将模板发布为 Visual Studio 安装程序 \(.vsi\) 文件。  有关将您的模板发布为 Visual Studio 安装程序文件的信息，请参见[NIB: How to: Publish Project Templates](http://msdn.microsoft.com/zh-cn/b9087f58-64e9-4767-bf54-e3bf40d63b20)。  
  
## 请参阅  
 [扩展 Visual Basic 中的 My 命名空间](../../../visual-basic/developing-apps/customizing-extending-my/extending-the-my-namespace.md)   
 [扩展 Visual Basic 应用程序模型](../../../visual-basic/developing-apps/customizing-extending-my/extending-the-visual-basic-application-model.md)   
 [自定义 My 中可用的对象](../../../visual-basic/developing-apps/customizing-extending-my/customizing-which-objects-are-available-in-my.md)   
 [“项目设计器”\-\>“My 扩展”页](/visual-studio/ide/reference/my-extensions-page-project-designer-visual-basic)