---
title: "了解何时使用 Override 和 New 关键字（C# 编程指南） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "new 关键字 [C#]"
  - "override 关键字 [C#]"
  - "多态性 [C#], 使用 override 和 new [C#]"
ms.assetid: 323db184-b136-46fc-8839-007886e7e8b0
caps.latest.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# 了解何时使用 Override 和 New 关键字（C# 编程指南）
在 C\# 中，派生类中方法的名称可与基类中方法的名称相同。  可通过使用 [new](../../../csharp/language-reference/keywords/new.md) 和 [override](../../../csharp/language-reference/keywords/override.md) 关键字指定方法互动的方式。  `override` 修饰符 *extends* 基类方法，且 `new` 修饰符将其“隐藏”起来。  这种区别在本主题中的示例显示出来。  
  
 在控制台应用程序中，声明下面的 `BaseClass` 和 `DerivedClass` 两个类.  `DerivedClass` 继承自 `BaseClass`。  
  
```c#  
class BaseClass  
{  
    public void Method1()  
    {  
        Console.WriteLine("Base - Method1");  
    }  
}  
  
class DerivedClass : BaseClass  
{  
    public void Method2()  
    {  
        Console.WriteLine("Derived - Method2");  
    }  
}  
  
```  
  
 在 `Main` 方法中，声明变量 `bc`、`dc` 和 `bcdc`。  
  
-   `bc` 的类型为 `BaseClass`，并且其值的类型为 `BaseClass`。  
  
-   `dc`的类型为 `DerivedClass`，并且其值的类型为 `DerivedClass`。  
  
-   `bcdc`的类型为 `BaseClass`，并且其值的类型为 `DerivedClass`。  这是要密切注意的变量。  
  
 由于 `bc` 和 `bcdc` 具有类型 `BaseClass`，因此，除非您使用强制转换，否则它们只会直接访问 `Method1`。  变量 `dc` 可以访问 `Method1` 和 `Method2`。  下面的代码演示这些关系。  
  
```c#  
class Program  
{  
    static void Main(string[] args)  
    {  
        BaseClass bc = new BaseClass();  
        DerivedClass dc = new DerivedClass();  
        BaseClass bcdc = new DerivedClass();  
  
        bc.Method1();  
        dc.Method1();  
        dc.Method2();  
        bcdc.Method1();  
    }  
    // Output:  
    // Base - Method1  
    // Base - Method1  
    // Derived - Method2  
    // Base - Method1  
}  
  
```  
  
 接下来，将以下 `Method2` 方法添加到 `BaseClass`。  此方法的签名与 `DerivedClass` 中 `Method2` 方法的签名相匹配。  
  
```c#  
public void Method2()  
{  
    Console.WriteLine("Base - Method2");  
}  
  
```  
  
 由于 `BaseClass` 现在有 `Method2` 方法，因此可以为 `BaseClass` 变量 `bc` 和 `bcdc` 添加第二个调用语句，如下面的代码所示。  
  
```c#  
bc.Method1();  
bc.Method2();  
dc.Method1();  
dc.Method2();  
bcdc.Method1();  
bcdc.Method2();  
  
```  
  
 当生成项目时，您将看到在 `BaseClass` 中添加 `Method2` 方法将引发警告。  警告提示，`DerivedClass` 中的 `Method2` 方法将 `Method2` 方法隐藏在 `BaseClass` 中。  如果要获得该结果，则建议您使用 `Method2` 定义中的 `new` 关键字。  或者，可以重命名 `Method2` 方法之一来解决警告，但这始终不实用。  
  
 在添加 `new` 之前，运行该程序以查看其他调用语句生成的输出。  显示以下结果。  
  
```c#  
// Output:  
// Base - Method1  
// Base - Method2  
// Base - Method1  
// Derived - Method2  
// Base - Method1  
// Base - Method2  
  
```  
  
 `new` 关键字可以保留生成输出的关系，但它将取消警告。  具有 `BaseClass` 类型的变量继续访问 `BaseClass` 成员，具有 `DerivedClass` 类型的变量首先继续访问 `DerivedClass` 中的成员，然后再考虑从 `BaseClass` 继承的成员.  
  
 要禁止显示警告，请向 `DerivedClass` 中的 `Method2` 定义添加 `new` 修饰符，如下面的示例所示：  可在 `public` 前后添加修饰符。  
  
```c#  
public new void Method2()  
{  
    Console.WriteLine("Derived - Method2");  
}  
  
```  
  
 再次运行该程序以确认没有更改输出。  还确认警告不再出现。  通过使用 `new`，您断言您了解它修改的成员将隐藏从基类继承的成员。  关于通过继承隐藏名称的更多信息，请参见 [new 修饰符](../../../csharp/language-reference/keywords/new-modifier.md)。  
  
 要将此行为与使用 `override` 的效果进行对比，请将以下方法添加到 `DerivedClass`。  可在 `public` 的前面或后面添加 `override` 修饰符。  
  
```c#  
public override void Method1()  
{  
    Console.WriteLine("Derived - Method1");  
}  
  
```  
  
 将 `virtual` 修饰符添加到 `BaseClass` 中的 `Method1` 的定义。  可在 `public` 的前面或后面添加 `virtual` 修饰符。  
  
```c#  
public virtual void Method1()  
{  
    Console.WriteLine("Base - Method1");  
}  
  
```  
  
 再次运行项目。  尤其请注意下面输出的最后两行。  
  
```c#  
// Output:  
// Base - Method1  
// Base - Method2  
// Derived - Method1  
// Derived - Method2  
// Derived - Method1  
// Base - Method2  
  
```  
  
 使用 `override` 修饰符使 `bcdc` 能够访问 `DerivedClass` 中定义的 `Method1` 方法。  通常，这是继承层次结构中所需的行为。  让具有从派生类创建的值的对象使用派生类中定义的方法。  通过使用 `override` 扩展基类方法可实现该行为。  
  
 下面的代码包括完整的示例。  
  
```c#  
using System;  
using System.Text;  
  
namespace OverrideAndNew  
{  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            BaseClass bc = new BaseClass();  
            DerivedClass dc = new DerivedClass();  
            BaseClass bcdc = new DerivedClass();  
  
            // The following two calls do what you would expect. They call  
            // the methods that are defined in BaseClass.  
            bc.Method1();  
            bc.Method2();  
            // Output:  
            // Base - Method1  
            // Base - Method2  
  
            // The following two calls do what you would expect. They call  
            // the methods that are defined in DerivedClass.  
            dc.Method1();  
            dc.Method2();  
            // Output:  
            // Derived - Method1  
            // Derived - Method2  
  
            // The following two calls produce different results, depending   
            // on whether override (Method1) or new (Method2) is used.  
            bcdc.Method1();  
            bcdc.Method2();  
            // Output:  
            // Derived - Method1  
            // Base - Method2  
        }  
    }  
  
    class BaseClass  
    {  
        public virtual void Method1()  
        {  
            Console.WriteLine("Base - Method1");  
        }  
  
        public virtual void Method2()  
        {  
            Console.WriteLine("Base - Method2");  
        }  
    }  
  
    class DerivedClass : BaseClass  
    {  
        public override void Method1()  
        {  
            Console.WriteLine("Derived - Method1");  
        }  
  
        public new void Method2()  
        {  
            Console.WriteLine("Derived - Method2");  
        }  
    }  
}  
  
```  
  
 以下示例显示了不同上下文中的类似行为。  该示例定义了三个类：一个名为 `Car` 的基类，和两个由其派生的 `ConvertibleCar` 和 `Minivan`。  基类中包含 `DescribeCar` 方法。  该方法给出了对一辆车的基本描述，然后调用 `ShowDetails` 来提供其他的信息。  这三个类中的每一个类都定义了 `ShowDetails` 方法。  `new` 修饰符用于定义 `ConvertibleCar` 类中的 `ShowDetails`。  `override` 修饰符用于定义 `Minivan` 类中的 `ShowDetails`。  
  
```c#  
// Define the base class, Car. The class defines two methods,  
// DescribeCar and ShowDetails. DescribeCar calls ShowDetails, and each derived  
// class also defines a ShowDetails method. The example tests which version of  
// ShowDetails is selected, the base class method or the derived class method.  
class Car  
{  
    public void DescribeCar()  
    {  
        System.Console.WriteLine("Four wheels and an engine.");  
        ShowDetails();  
    }  
  
    public virtual void ShowDetails()  
    {  
        System.Console.WriteLine("Standard transportation.");  
    }  
}  
  
// Define the derived classes.  
  
// Class ConvertibleCar uses the new modifier to acknowledge that ShowDetails  
// hides the base class method.  
class ConvertibleCar : Car  
{  
    public new void ShowDetails()  
    {  
        System.Console.WriteLine("A roof that opens up.");  
    }  
}  
  
// Class Minivan uses the override modifier to specify that ShowDetails  
// extends the base class method.  
class Minivan : Car  
{  
    public override void ShowDetails()  
    {  
        System.Console.WriteLine("Carries seven people.");  
    }  
}  
  
```  
  
 该示例测试被调用的 `ShowDetails` 版本。  以下方法，`TestCars1` 为每个类提供了一个实例，并在每个实例上调用 `DescribeCar`。  
  
```c#  
public static void TestCars1()  
{  
    System.Console.WriteLine("\nTestCars1");  
    System.Console.WriteLine("----------");  
  
    Car car1 = new Car();  
    car1.DescribeCar();  
    System.Console.WriteLine("----------");  
  
    // Notice the output from this test case. The new modifier is  
    // used in the definition of ShowDetails in the ConvertibleCar  
    // class.    
  
    ConvertibleCar car2 = new ConvertibleCar();  
    car2.DescribeCar();  
    System.Console.WriteLine("----------");  
  
    Minivan car3 = new Minivan();  
    car3.DescribeCar();  
    System.Console.WriteLine("----------");  
}  
  
```  
  
 `TestCars1` 生成以下输出：  尤其请注意 `car2` 的结果，该结果可能不是您所需的内容。  对象的类型是 `ConvertibleCar`，但 `DescribeCar` 不会访问 `ConvertibleCar` 中定义的 `ShowDetails` 版本，因为方法已声明包含  `new` 修饰符，而不是 `override` 修饰符。  因此，`ConvertibleCar` 对象显示与 `Car` 对象相同的说明。  比较 `car3` 的结果，它是一个 `Minivan` 对象。  在这种情况下，在 `Minivan` 类中声明的 `ShowDetails` 方法重写 `Car` 类中声明的 `ShowDetails` 方法，显示的说明描述微型面包车。  
  
```c#  
  
// TestCars1  
// ----------  
// Four wheels and an engine.  
// Standard transportation.  
// ----------  
// Four wheels and an engine.  
// Standard transportation.  
// ----------  
// Four wheels and an engine.  
// Carries seven people.  
// ----------  
  
```  
  
 `TestCars2` 创建 `Car` 类型的对象列表。  对象的值由 `Car`、`ConvertibleCar` 和 `Minivan` 类实例化而来。  `DescribeCar` 是调用列表中的每个元素。  以下代码显示了 `TestCars2` 的定义。  
  
```c#  
public static void TestCars2()  
{  
    System.Console.WriteLine("\nTestCars2");  
    System.Console.WriteLine("----------");  
  
    var cars = new List<Car> { new Car(), new ConvertibleCar(),   
        new Minivan() };  
  
    foreach (var car in cars)  
    {  
        car.DescribeCar();  
        System.Console.WriteLine("----------");  
    }  
}  
  
```  
  
 显示以下输出。  请注意，此输出与由 `TestCars1` 显示的输出相同。  `ConvertibleCar` 类的 `ShowDetails` 方法不被调用，无论对象的类型是 `ConvertibleCar`，如在 `TestCars1` 中，还是 `Car`，如在 `TestCars2` 中。  相反，`car3` 在两种情况下都从 `Minivan` 类调用 `ShowDetails` 方法，无论它具有类型 `Minivan` 还是类型 `Car`。  
  
```c#  
// TestCars2  
// ----------  
// Four wheels and an engine.  
// Standard transportation.  
// ----------  
// Four wheels and an engine.  
// Standard transportation.  
// ----------  
// Four wheels and an engine.  
// Carries seven people.  
// ----------  
  
```  
  
 完成示例的方法 `TestCars3` 和 `TestCars4`。  这些方法直接调用 `ShowDetails`，首先从宣布具有类型 `ConvertibleCar` 和 `Minivan` \(`TestCars3`\) 的对象调用，然后从具有类型 `Car` \(`TestCars4`\) 的对象调用。  以下代码定义了这两种方法。  
  
```c#  
  
public static void TestCars3()  
{  
    System.Console.WriteLine("\nTestCars3");  
    System.Console.WriteLine("----------");  
    ConvertibleCar car2 = new ConvertibleCar();  
    Minivan car3 = new Minivan();  
    car2.ShowDetails();  
    car3.ShowDetails();  
}  
  
public static void TestCars4()  
{  
    System.Console.WriteLine("\nTestCars4");  
    System.Console.WriteLine("----------");  
    Car car2 = new ConvertibleCar();  
    Car car3 = new Minivan();  
    car2.ShowDetails();  
    car3.ShowDetails();  
}  
  
```  
  
 该方法产生下面的输出，它对应本主题中第一个示例的结果。  
  
```c#  
// TestCars3  
// ----------  
// A roof that opens up.  
// Carries seven people.  
  
// TestCars4  
// ----------  
// Standard transportation.  
// Carries seven people.  
  
```  
  
 以下代码显示了整个项目及其输出。  
  
```c#  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
  
namespace OverrideAndNew2  
{  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            // Declare objects of the derived classes and test which version  
            // of ShowDetails is run, base or derived.  
            TestCars1();  
  
            // Declare objects of the base class, instantiated with the  
            // derived classes, and repeat the tests.  
            TestCars2();  
  
            // Declare objects of the derived classes and call ShowDetails  
            // directly.  
            TestCars3();  
  
            // Declare objects of the base class, instantiated with the  
            // derived classes, and repeat the tests.  
            TestCars4();  
        }  
  
        public static void TestCars1()  
        {  
            System.Console.WriteLine("\nTestCars1");  
            System.Console.WriteLine("----------");  
  
            Car car1 = new Car();  
            car1.DescribeCar();  
            System.Console.WriteLine("----------");  
  
            // Notice the output from this test case. The new modifier is  
            // used in the definition of ShowDetails in the ConvertibleCar  
            // class.    
            ConvertibleCar car2 = new ConvertibleCar();  
            car2.DescribeCar();  
            System.Console.WriteLine("----------");  
  
            Minivan car3 = new Minivan();  
            car3.DescribeCar();  
            System.Console.WriteLine("----------");  
        }  
        // Output:  
        // TestCars1  
        // ----------  
        // Four wheels and an engine.  
        // Standard transportation.  
        // ----------  
        // Four wheels and an engine.  
        // Standard transportation.  
        // ----------  
        // Four wheels and an engine.  
        // Carries seven people.  
        // ----------  
  
        public static void TestCars2()  
        {  
            System.Console.WriteLine("\nTestCars2");  
            System.Console.WriteLine("----------");  
  
            var cars = new List<Car> { new Car(), new ConvertibleCar(),   
                new Minivan() };  
  
            foreach (var car in cars)  
            {  
                car.DescribeCar();  
                System.Console.WriteLine("----------");  
            }  
        }  
        // Output:  
        // TestCars2  
        // ----------  
        // Four wheels and an engine.  
        // Standard transportation.  
        // ----------  
        // Four wheels and an engine.  
        // Standard transportation.  
        // ----------  
        // Four wheels and an engine.  
        // Carries seven people.  
        // ----------  
  
        public static void TestCars3()  
        {  
            System.Console.WriteLine("\nTestCars3");  
            System.Console.WriteLine("----------");  
            ConvertibleCar car2 = new ConvertibleCar();  
            Minivan car3 = new Minivan();  
            car2.ShowDetails();  
            car3.ShowDetails();  
        }  
        // Output:  
        // TestCars3  
        // ----------  
        // A roof that opens up.  
        // Carries seven people.  
  
        public static void TestCars4()  
        {  
            System.Console.WriteLine("\nTestCars4");  
            System.Console.WriteLine("----------");  
            Car car2 = new ConvertibleCar();  
            Car car3 = new Minivan();  
            car2.ShowDetails();  
            car3.ShowDetails();  
        }  
        // Output:  
        // TestCars4  
        // ----------  
        // Standard transportation.  
        // Carries seven people.  
    }  
  
    // Define the base class, Car. The class defines two virtual methods,  
    // DescribeCar and ShowDetails. DescribeCar calls ShowDetails, and each derived  
    // class also defines a ShowDetails method. The example tests which version of  
    // ShowDetails is used, the base class method or the derived class method.  
    class Car  
    {  
        public virtual void DescribeCar()  
        {  
            System.Console.WriteLine("Four wheels and an engine.");  
            ShowDetails();  
        }  
  
        public virtual void ShowDetails()  
        {  
            System.Console.WriteLine("Standard transportation.");  
        }  
    }  
  
    // Define the derived classes.  
  
    // Class ConvertibleCar uses the new modifier to acknowledge that ShowDetails  
    // hides the base class method.  
    class ConvertibleCar : Car  
    {  
        public new void ShowDetails()  
        {  
            System.Console.WriteLine("A roof that opens up.");  
        }  
    }  
  
    // Class Minivan uses the override modifier to specify that ShowDetails  
    // extends the base class method.  
    class Minivan : Car  
    {  
        public override void ShowDetails()  
        {  
            System.Console.WriteLine("Carries seven people.");  
        }  
    }  
  
}  
  
```  
  
## 请参阅  
 [C\# 编程指南](../../../csharp/programming-guide/index.md)   
 [类和结构](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [使用 Override 和 New 关键字进行版本控制](../../../csharp/programming-guide/classes-and-structs/versioning-with-the-override-and-new-keywords.md)   
 [base](../../../csharp/language-reference/keywords/base.md)   
 [abstract](../../../csharp/language-reference/keywords/abstract.md)