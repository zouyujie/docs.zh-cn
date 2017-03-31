---
title: "如何：捕捉非 CLS 异常 | Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- exceptions [C#], non-CLS
ms.assetid: db4630b3-5240-471a-b3a7-c7ff6ab31e8d
caps.latest.revision: 8
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 3515ecab379a0e910cdd5ba82a4a39b085cc816f
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-catch-a-non-cls-exception"></a>如何：捕捉非 CLS 异常
包括 C++/CLI 在内的某些 .NET 语言允许对象引发并非派生自 <xref:System.Exception> 的异常。 这类异常被称为非 CLS 异常或非异常。**** 无法在 [!INCLUDE[csprcs](../../../csharp/includes/csprcs_md.md)] 中引发非 CLS 异常，但有两种方式可以捕获它们：  
  
-   在作为 <xref:System.Runtime.CompilerServices.RuntimeWrappedException> 的 `catch (Exception e)` 块内。  
  
     默认情况下，[!INCLUDE[csprcs](../../../csharp/includes/csprcs_md.md)] 程序集将非 CLS 异常作为包装的异常捕获。 如果需要访问原始异常，请使用此方法，可通过 <xref:System.Runtime.CompilerServices.RuntimeWrappedException.WrappedException%2A> 属性访问它。 本主题的后续过程将解释如何通过此方式捕获异常。  
  
-   在位于 `catch (Exception)` 或 `catch (Exception e)` 块之后的常规 catch 块（未指定异常类型的 catch 块）之中。  
  
     如果为了响应非 CLS 异常需要执行某些操作（如写入日志文件），且无需访问异常信息时，请使用此方法。 默认情况下，公共语言运行时包装所有异常。 要禁用此行为，请将此程序集级别属性添加到代码中，通常位于 AssemblyInfo.cs 文件：`[assembly: RuntimeCompatibilityAttribute(WrapNonExceptionThrows = false)]`。  
  
### <a name="to-catch-a-non-cls-exception"></a>要捕捉非 CLS 异常  
  
1.  在 `catch(Exception e) block` 中使用 `as` 关键字测试 `e` 是否可被强制转换为 <xref:System.Runtime.CompilerServices.RuntimeWrappedException>。  
  
2.  通过 <xref:System.Runtime.CompilerServices.RuntimeWrappedException.WrappedException%2A> 属性访问原始异常。  
  
## <a name="example"></a>示例  
 下面示例显示如何捕捉以 C++/CLR 编写的类库所引发的非 CLS 异常。 请注意，在此示例中，[!INCLUDE[csprcs](../../../csharp/includes/csprcs_md.md)] 客户端代码预先已知道被引发的异常类型是 <xref:System.String?displayProperty=fullName>。 可以将 <xref:System.Runtime.CompilerServices.RuntimeWrappedException.WrappedException%2A> 属性强制转换回原始类型，只要可以从你的代码访问该类型。  
  
```  
// Class library written in C++/CLR.  
   ThrowNonCLS.Class1 myClass = new ThrowNonCLS.Class1();  
  
   try  
   {  
    // throws gcnew System::String(  
    // "I do not derive from System.Exception!");  
    myClass.TestThrow();   
   }  
  
   catch (Exception e)  
   {  
    RuntimeWrappedException rwe = e as RuntimeWrappedException;  
    if (rwe != null)      
    {  
      String s = rwe.WrappedException as String;  
      if (s != null)  
      {  
        Console.WriteLine(s);  
      }  
    }  
    else  
    {  
       // Handle other System.Exception types.  
    }  
   }             
```  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Runtime.CompilerServices.RuntimeWrappedException>   
 [异常和异常处理](../../../csharp/programming-guide/exceptions/index.md)
