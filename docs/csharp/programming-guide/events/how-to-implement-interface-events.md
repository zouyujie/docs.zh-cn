---
title: "如何：实现接口事件（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "事件 [C#], 接口中"
  - "接口 [C#], 类中的事件实现"
ms.assetid: 63527447-9535-4880-8e95-35e2075827df
caps.latest.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 21
---
# 如何：实现接口事件（C# 编程指南）
[接口](../../../csharp/language-reference/keywords/interface.md)可声明[事件](../../../csharp/language-reference/keywords/event.md)。  下面的示例演示如何在类中实现接口事件。  实现接口事件的规则与实现任何接口方法或属性的规则基本相同。  
  
### 在类中实现接口事件  
  
-   在类中声明事件，然后在适当的区域调用该事件。  
  
    ```  
    namespace ImplementInterfaceEvents  
    {  
        public interface IDrawingObject  
        {  
            event EventHandler ShapeChanged;  
        }  
        public class MyEventArgs : EventArgs   
        {  
            // class members  
        }  
        public class Shape : IDrawingObject  
        {  
            public event EventHandler ShapeChanged;  
            void ChangeShape()  
            {  
                // Do something here before the event…  
  
                OnShapeChanged(new MyEventArgs(/*arguments*/));  
  
                // or do something here after the event.   
            }  
            protected virtual void OnShapeChanged(MyEventArgs e)  
            {  
                if(ShapeChanged != null)  
                {  
                   ShapeChanged(this, e);  
                }  
            }  
        }  
  
    }  
    ```  
  
## 示例  
 下面的示例演示如何处理以下的不常见情况：您的类是从两个以上的接口继承的，每个接口都含有同名事件）。  在这种情况下，您至少要为其中一个事件提供显式接口实现。  为事件编写显式接口实现时，必须编写 `add` 和 `remove` 事件访问器。  这两个事件访问器通常由编译器提供，但在这种情况下编译器不能提供。  
  
 您可以提供自己的访问器，以便指定这两个事件是由您的类中的同一事件表示，还是由不同事件表示。  例如，根据接口规范，如果事件应在不同时间引发，则可以将每个事件与类中的一个单独实现关联。  在下面的示例中，订户将形状引用强制转换为 `IShape` 或 `IDrawingObject`，从而确定自己将会接收哪个 `OnDraw` 事件。  
  
 [!code-cs[csProgGuideEvents#10](../../../csharp/programming-guide/events/codesnippet/CSharp/how-to-implement-interface-events_1.cs)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [事件](../../../csharp/programming-guide/events/index.md)   
 [委托](../../../csharp/programming-guide/delegates/index.md)   
 [显式接口实现](../../../csharp/programming-guide/interfaces/explicit-interface-implementation.md)   
 [如何：在派生类中引发基类事件](../../../csharp/programming-guide/events/how-to-raise-base-class-events-in-derived-classes.md)