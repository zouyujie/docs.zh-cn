---
title: "反射 (C#) | Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: f80a2362-953b-4e8e-9759-cd5f334190d4
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: ab40ab2258703670576084eccf7fd7e1b113d08d
ms.lasthandoff: 03/13/2017

---
# <a name="reflection-c"></a>反射 (C#)
反射提供描述程序集、模块和类型的对象（<xref:System.Type> 类型）。 可以使用反射动态地创建类型的实例，将类型绑定到现有对象，或从现有对象中获取类型，然后调用其方法或访问器字段和属性。 如果代码中使用了特性，可以利用反射来访问它们。 有关更多信息，请参阅[特性](https://msdn.microsoft.com/library/5x6cd29c)。  
  
 下面一个简单的反射示例，使用静态方法 `GetType`被 `Object` 基类的所有类型继承）以获取变量类型：  
  
```csharp  
// Using GetType to obtain type information:  
int i = 42;  
System.Type type = i.GetType();  
System.Console.WriteLine(type);  
```  
  
 输出为：  
  
 `System.Int32`  
  
 下面的示例使用反射获取已加载的程序集的完整名称。  
  
```csharp  
// Using Reflection to get information from an Assembly:  
System.Reflection.Assembly info = typeof(System.Int32).Assembly;  
System.Console.WriteLine(info);  
```  
  
 输出为：  
  
 `mscorlib, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089`  
  
> [!NOTE]
>  C# 关键字 `protected` 和 `internal` 在 IL 中没有任何意义，且不会用于反射 API 中。 在 IL 中对应的术语为“系列”**和“程序集”**。 若要标识使用反射的 `internal` 方法，请使用 <xref:System.Reflection.MethodBase.IsAssembly%2A> 属性。 若要标识 `protected internal` 方法，请使用 <xref:System.Reflection.MethodBase.IsFamilyOrAssembly%2A>。  
  
## <a name="reflection-overview"></a>反射概述  
 反射在以下情况下很有用：  
  
-   需要访问程序元数据中的特性时。 有关详细信息，请参阅[检索存储在特性中的信息](http://msdn.microsoft.com/library/37dfe4e3-7da0-48b6-a3d9-398981524e1c)。  
  
-   检查和实例化程序集中的类型。  
  
-   在运行时构建新类型。 使用 <xref:System.Reflection.Emit> 中的类。  
  
-   执行后期绑定，访问在运行时创建的类型上的方法。 请参阅主题 [Dynamically Loading and Using Types](http://msdn.microsoft.com/library/db985bec-5942-40ec-b13a-771ae98623dc)（动态加载和使用类型）。  
  
## <a name="related-sections"></a>相关章节  
 更多相关信息：  
  
-   [反射](http://msdn.microsoft.com/library/d1a58e7f-fb39-4d50-bf84-e3b8f9bf9775)  
  
-   [查看类型信息](http://msdn.microsoft.com/library/7e7303a9-4064-4738-b4e7-b75974ed70d2)  
  
-   [反射类型和泛型类型](http://msdn.microsoft.com/library/f7180fc5-dd41-42d4-8a8e-1b34288e06de)  
  
-   <xref:System.Reflection.Emit>  
  
-   [检索存储在特性中的信息](http://msdn.microsoft.com/library/37dfe4e3-7da0-48b6-a3d9-398981524e1c)  
  
## <a name="see-also"></a>请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [Assemblies in the Common Language Runtime](https://msdn.microsoft.com/library/k3677y81)（公共语言运行时中的程序集）
