---
title: "如何：发布符合 .NET Framework 准则的事件（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "事件 [C#], 实现准则"
ms.assetid: 9310ae16-8627-44a2-b08c-05e5976202b1
caps.latest.revision: 31
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 31
---
# 如何：发布符合 .NET Framework 准则的事件（C# 编程指南）
下面的过程演示了如何将符合标准 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 模式的事件添加到您的类和结构中。  [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 类库中的所有事件均基于 <xref:System.EventHandler> 委托，定义如下：  
  
```  
public delegate void EventHandler(object sender, EventArgs e);  
```  
  
> [!NOTE]
>  [!INCLUDE[dnprdnlong](../../../csharp/programming-guide/events/includes/dnprdnlong-md.md)] 引入了此委托的一个泛型版本，即 <xref:System.EventHandler%601>。  下面的示例显示如何使用这两种版本。  
  
 虽然您定义的类中的事件可基于任何有效委托类型（甚至是可返回值的委托），但是，通常建议您使用 <xref:System.EventHandler> 让事件基于 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 模式，如下面的示例所示。  
  
### 采用 EventHandler 模式发布事件  
  
1.  （如果不需要与事件一起发送自定义数据，请跳过此步骤，进入步骤 3a。）在发行者类和订阅方类均可看见的范围中声明自定义数据的类。  然后添加保留您的自定义事件数据所需的成员。  在此示例中，会返回一个简单字符串。  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
2.  （如果您使用的是 <xref:System.EventHandler%601> 的泛型版本，请跳过此步骤。）在发布类中声明一个委托。  为它指定以 EventHandler 结尾的名称。  第二个参数指定自定义 EventArgs 类型。  
  
    ```  
    public delegate void CustomEventHandler(object sender, CustomEventArgs a);  
    ```  
  
3.  使用以下任一步骤，在发布类中声明事件。  
  
    1.  如果没有自定义 EventArgs 类，事件类型就是非泛型 EventHandler 委托。  无需声明委托，因为它已在创建 C\# 项目时包含的 <xref:System> 命名空间中进行了声明。  将以下代码添加到发行者类中。  
  
        ```  
        public event EventHandler RaiseCustomEvent;  
        ```  
  
    2.  如果使用的是 <xref:System.EventHandler> 的非泛型版本，并且您有一个由 <xref:System.EventArgs> 派生的自定义类，请在发布类中声明您的事件，并且将来自步骤 2 的委托用作类型。  
  
        ```  
        public event CustomEventHandler RaiseCustomEvent;  
  
        ```  
  
    3.  如果使用的是泛型版本，则不需要自定义委托。  相反，在发行者类中，您应将事件类型指定为 `EventHandler<CustomEventArgs>`，将尖括号中的内容替换为自己的类的名称。  
  
        ```  
        public event EventHandler<CustomEventArgs> RaiseCustomEvent;  
        ```  
  
## 示例  
 下面的示例通过将自定义 EventArgs 类和 <xref:System.EventHandler%601> 用作事件类型来演示上述步骤。  
  
 [!code-cs[csProgGuideEvents#2](../../../csharp/programming-guide/events/codesnippet/csharp/how-to-publish-events-th_1.cs)]  
  
## 请参阅  
 <xref:System.Delegate>   
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [事件](../../../csharp/programming-guide/events/index.md)   
 [委托](../../../csharp/programming-guide/delegates/index.md)