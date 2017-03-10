---
title: "如何：实现自定义事件访问器（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "访问器 [C#], 事件访问器"
  - "add 访问器 [C#]"
  - "事件 [C#], add 访问器"
  - "事件 [C#], remove 访问器"
  - "remove 访问器 [C#]"
ms.assetid: bf903abf-03a4-4f7b-ab6b-b7e59bc2ee1e
caps.latest.revision: 7
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 7
---
# 如何：实现自定义事件访问器（C# 编程指南）
事件是特殊类型的多路广播委托，只能从声明它的类中调用。  客户端代码通过提供对应在引发事件时调用的方法的引用来订阅事件。  这些方法通过事件访问器添加到委托的调用列表中，事件访问器类似于属性访问器，不同之处在于事件访问器被命名为 `add` 和 `remove`。  在大多数情况下都不需要提供自定义的事件访问器。  如果您在代码中没有提供自定义的事件访问器，编译器会自动添加事件访问器。  但在某些情况下，您可能需要提供自定义行为。  在主题[如何：实现接口事件](../../../csharp/programming-guide/events/how-to-implement-interface-events.md)中就演示了这样一种情况。  
  
## 示例  
 下面的示例演示如何实现自定义的 add 和 remove 事件访问器。  虽然可以替换这些访问器内的任何代码，但建议您在添加或移除新的事件处理程序方法之前先锁定该事件。  
  
```  
event EventHandler IDrawingObject.OnDraw  
        {  
            add  
            {  
                lock (PreDrawEvent)  
                {  
                    PreDrawEvent += value;  
                }  
            }  
            remove  
            {  
                lock (PreDrawEvent)  
                {  
                    PreDrawEvent -= value;  
                }  
            }  
        }  
  
```  
  
## 请参阅  
 [事件](../../../csharp/programming-guide/events/index.md)   
 [event](../../../csharp/language-reference/keywords/event.md)