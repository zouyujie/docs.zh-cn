---
title: "创建和使用组件 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "组件 [Visual Basic]"
ms.assetid: ee6a4156-73f7-4e9b-8e01-c74c4798b65c
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# 创建和使用组件 (Visual Basic)
[!INCLUDE[vs2017banner](../../visual-basic/includes/vs2017banner.md)]

“组件”是一种类，它实现 <xref:System.ComponentModel.IComponent?displayProperty=fullName> 接口或者直接或间接地从实现 <xref:System.ComponentModel.IComponent> 的类派生。  [!INCLUDE[dnprdnshort](../../csharp/getting-started/includes/dnprdnshort-md.md)] 组件是可重用的对象，它可以与其他对象进行交互，还可以提供对外部资源和设计时支持的控制。  
  
 组件的一个重要特性就是它们是可设计的，这意味着可以在 [!INCLUDE[vsprvs](../../csharp/includes/vsprvs-md.md)] 集成开发环境中使用作为组件的类。  您可以将组件添加到“工具箱”、拖放到窗体以及在设计图面上操作。  请注意，对组件的基本设计时支持已经内置于 [!INCLUDE[dnprdnshort](../../csharp/getting-started/includes/dnprdnshort-md.md)] 中；组件开发人员无须进行任何额外的工作就可利用基本设计时功能。  
  
 “控件”与组件类似，它们都是可设计的。  不过，控件提供用户界面，而组件则不提供。  控件必须从以下基本控件类之一派生：<xref:System.Windows.Forms.Control> 或 <xref:System.Web.UI.Control>。  
  
## 创建组件的时间  
 如果类将在设计图面（如 Windows 窗体设计器或 Web 窗体设计器）上使用，但没有用户界面，此类应该是一个组件并实现 <xref:System.ComponentModel.IComponent>，或者是从直接或间接实现 <xref:System.ComponentModel.IComponent> 的类派生的。  
  
 <xref:System.ComponentModel.Component> 和 <xref:System.ComponentModel.MarshalByValueComponent> 类是 <xref:System.ComponentModel.IComponent> 接口的基实现。  这两个类的主要区别是：<xref:System.ComponentModel.Component> 类由引用封送，而 <xref:System.ComponentModel.IComponent> 则由值封送。  以下列表为实施者提供了全面的指南。  
  
-   如果组件需要由引用封送，请从 <xref:System.ComponentModel.Component> 派生。  
  
-   如果组件需要由值封送，请从 <xref:System.ComponentModel.MarshalByValueComponent> 派生。  
  
-   如果由于单一继承导致无法从其中一个基实现派生组件，则请实现 <xref:System.ComponentModel.IComponent>。  
  
 有关设计时支持的更多信息，请参见 [组件的设计时特性\)](../Topic/Design-Time%20Attributes%20for%20Components.md) 和 [Extending Design\-Time Support](../Topic/Extending%20Design-Time%20Support.md)。  
  
## 组件类  
 <xref:System.ComponentModel> 命名空间提供用于实现组件和控件的运行时和设计时行为的类。  此命名空间包括用于特性和类型转换器的实现、数据源绑定和组件授权的基类和接口。  
  
 核心组件类包括：  
  
-   <xref:System.ComponentModel.Component>.  <xref:System.ComponentModel.IComponent> 接口的一个基实现。  此类可以实现在应用程序之间共享对象。  
  
-   <xref:System.ComponentModel.MarshalByValueComponent>.  <xref:System.ComponentModel.IComponent> 接口的一个基实现。  
  
-   <xref:System.ComponentModel.Container>.  <xref:System.ComponentModel.IContainer> 接口的基实现。  此类封装零个或多个组件。  
  
 部分用于侦听组件的类包括：  
  
-   <xref:System.ComponentModel.License>.  所有许可证的抽象基类。  而许可证将授予组件的特定实例。  
  
-   <xref:System.ComponentModel.LicenseManager>.  提供属性和方法，用以将许可证添加到组件和管理 <xref:System.ComponentModel.LicenseProvider>。  
  
-   <xref:System.ComponentModel.LicenseProvider>.  实现许可证提供程序的抽象基类。  
  
-   <xref:System.ComponentModel.LicenseProviderAttribute>.  指定要与某个类一起使用的 <xref:System.ComponentModel.LicenseProvider> 类。  
  
 常用于描述和保存组件的类。  
  
-   <xref:System.ComponentModel.TypeDescriptor>.  提供有关组件特征的信息，如组件的特性、属性和事件。  
  
-   <xref:System.ComponentModel.EventDescriptor>.  提供有关事件的信息。  
  
-   <xref:System.ComponentModel.PropertyDescriptor>.  提供有关属性的信息。  
  
## 相关章节  
 [类、组件和控件](../Topic/Class%20vs.%20Component%20vs.%20Control.md)  
 定义组件和控件，并讨论它们与类之间的区别。  
  
 [组件创作](../Topic/Component%20Authoring.md)  
 组件入门路线图。  
  
 [Component Authoring Walkthroughs](../Topic/Component%20Authoring%20Walkthroughs.md)  
 链接到提供组件编程的逐步骤说明的主题。  
  
 [组件类](../Topic/Component%20Classes.md)  
 描述什么使类成为组件，公开组件功能的方法，控制对组件的访问和控制如何创建组件实例。  
  
 [控件和组件创作疑难解答](../Topic/Troubleshooting%20Control%20and%20Component%20Authoring.md)  
 解释如何解决常见问题。  
  
## 请参阅  
 [How to: Access Design\-Time Support in Windows Forms](../Topic/How%20to:%20Access%20Design-Time%20Support%20in%20Windows%20Forms.md)   
 [How to: Extend the Appearance and Behavior of Controls in Design Mode](../Topic/How%20to:%20Extend%20the%20Appearance%20and%20Behavior%20of%20Controls%20in%20Design%20Mode.md)   
 [How to: Perform Custom Initialization for Controls in Design Mode](../Topic/How%20to:%20Perform%20Custom%20Initialization%20for%20Controls%20in%20Design%20Mode.md)