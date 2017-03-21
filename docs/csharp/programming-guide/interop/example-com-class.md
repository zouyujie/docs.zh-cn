---
title: "COM 类示例（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "COM, 公开 Visual C# 对象"
  - "示例 [C#], COM 类"
ms.assetid: 6504dea9-ad1c-4993-a794-830fec5270af
caps.latest.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 17
---
# COM 类示例（C# 编程指南）
下面是一个公开为 COM 对象的类的示例。  将这些代码放置到 .cs 文件中并添加到您的项目中后，请将**“Register for COM Interop”**属性设置为**“True”**。  有关更多信息，请参见[NIB: How to: Register a Component for COM Interop](http://msdn.microsoft.com/zh-cn/4de7d474-56e8-4027-994d-d47ca4725c5e)。  
  
 向 COM 公开 Visual C\# 对象要求声明一个类接口、一个事件接口（如果需要）和类本身。  类成员必须遵循下列规则才能对 COM 可见：  
  
-   类必须是公共的。  
  
-   属性、方法和事件必须是公共的。  
  
-   属性和方法必须在类接口上声明。  
  
-   事件必须在事件接口中声明。  
  
 其他没有在这些接口中声明的类的公共成员对于 COM 是不可见的，但它们对于其他 .NET Framework 对象将是可见的。  
  
 若要向 COM 公开属性和方法，必须在类接口上声明这些属性和方法，并用 `DispId` 特性予以标记，然后在类中实现它们。  成员在接口中声明的顺序即是用于 COM vtable 的顺序。  
  
 若要从类中公开事件，必须在事件接口上声明这些事件，并用 `DispId` 特性予以标记。  该类不应实现此接口。  
  
 类实现类接口；它可以实现多个接口，但第一个实现将作为默认类接口。  在此处实现向 COM 公开的方法和属性。  它们必须标记为是公共的，并且必须与类接口中的声明匹配。  同时，在此处声明由类引发的事件。  它们必须标记为是公共的，并且必须与事件接口中的声明匹配。  
  
## 示例  
 [!code-cs[csProgGuideInterop#8](../../../csharp/programming-guide/interop/codesnippet/CSharp/example-com-class_1.cs)]  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [互操作性](../../../csharp/programming-guide/interop/interoperability.md)   
 [“项目设计器”\-\>“生成”页 \(C\#\)](/visual-studio/ide/reference/build-page-project-designer-csharp)