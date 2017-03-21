---
title: "互操作性疑难解答 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "程序集 [Visual Basic]"
  - "程序集 [Visual Basic], 部署"
  - "COM 互操作, 疑难解答"
  - "COM 对象, 疑难解答"
  - "互操作程序集"
  - "互操作, 部署程序集"
  - "互操作, 安装共享组件的程序集"
  - "互操作, 共享组件"
  - "互操作性, 共享组件"
  - "互操作性, 疑难解答"
  - "共享组件, 与程序集联合使用"
  - "互操作性疑难解答"
  - "Visual Basic 疑难解答, 互操作性"
ms.assetid: b324cc1e-b03c-4f39-aea6-6a6d5bfd0e37
caps.latest.revision: 21
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 21
---
# 互操作性疑难解答 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

在兼容 COM 和 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)]的托管代码之间时，可能会遇到以下一个或多个常见问题。  
  
##  <a name="vbconinteroperabilitymarshalinganchor1"></a> 互操作封送处理  
 有时，您可能需要使用不是 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)]的数据类型。  互操作程序集处理 COM 对象的工作，但是，您可能必须控件使用的数据类型，则在向 COM 公开托管对象时。  例如，结构在类库中的字符串必须指定 `BStr` 非托管类型发送到 Visual Basic 6.0 和早期版本创建的 COM 对象。  在这种情况下，可以使用 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 特性使托管类型显示为非托管类型。  
  
##  <a name="vbconinteroperabilitymarshalinganchor2"></a> 导出固定长度的字符串传递到非托管代码  
 在 Visual Basic 6.0 和早期版本中，字符串传递给 COM 对象导出为字节序列，不带 null 终止字符。  为了与其他语言兼容，在导出字符串时， [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong-md.md)] ，包括一终止字符。  最好的方法来解决此不兼容性将导出缺少终止字符作为数组 `Byte` 或 `Char`的字符串。  
  
##  <a name="vbconinteroperabilitymarshalinganchor3"></a> 导出继承层次结构  
 托管类层次结构展平，当公开为 COM 对象。  例如，因此，如果您定义具有成员的基类，然后继承以公开为 COM 对象的派生类，在 COM 对象使用该派生类不能使用继承成员的客户端的基类。  ，仅当基类也是作为 COM 对象创建，基类成员可以从 COM 对象仅捕获作为基类的实例，然后单击。  
  
## 重载方法  
 尽管您可以将 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)]创建重载方法，但 COM 不支持。  当包含重载的方法时的类公开为 COM 对象，新方法名称为重载的方法生成。  
  
 例如，请考虑包含 `Synch` 两个重载方法的类。  当类公开为 COM 对象时，新生成的方法名可能为 `Synch` 和 `Synch_2`。  
  
 重命名可能会 COM 对象的使用者两个问题。  
  
1.  客户端可能预见不到生成的方法名。  
  
2.  ，在新重载添加到类或其基类时，在作为 COM 对象公开的类生成的方法名可能更改。  这可能导致版本控制问题。  
  
 若要解决这两个问题，请为每个方法一个唯一名称，而不是使用重载，那么，当您开发将公开为 COM 对象的对象。  
  
##  <a name="vbconinteroperabilitymarshalinganchor4"></a> 对于通过 Interop 程序集使用 COM 对象  
 您几乎使用互操作程序集，则 COM 对象的托管代码替换它们表示。  但是，因为它们是包装类，并不实际的 COM 对象，所以使用 interop 程序集与标准程序集之间的一些差异。  这些不同之处包括类和数据类型风险参数和返回值的。  
  
##  <a name="vbconinteroperabilitymarshalinganchor5"></a> 作为接口和类公开的类  
 不同于标准程序集中的类， COM 类在互操作程序集公开为接口和一个表示 COM 类的类。  接口名称与相同的 COM 类。  interop 类的名称是否与原 COM 类，但是，包含单词 “追加的类。  例如，假设您具有引用的项。 COM 对象的互操作程序集。  如果 COM 类被命名为 `MyComClass`， IntelliSense 和对象浏览器显示接口名为 `MyComClass` ，类命名为 `MyComClassClass`。  
  
##  <a name="vbconinteroperabilitymarshalinganchor6"></a> 创建 .NET framework 类的实例  
 通常，您创建 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 类的实例使用 `New` 语句用类名。  让 COM 类由 interop 程序集是可用于接口的 `New` 语句的这一情况。  除非您使用 `Inherits` 语句的 COM 类，您可以使用接口就象类。  下面的代码在具有对 Microsoft ActiveX Data Objects 2.8 Library COM 对象的项目演示如何创建 `Command` 对象:  
  
 [!code-vb[VbVbalrInterop#20](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/troubleshooting-interoperability_1.vb)]  
  
 但是，因此，如果使用 COM 类为基础为一个派生类，如下面的代码必须使用表示 COM 类的 interop 类，例如:  
  
 [!code-vb[VbVbalrInterop#21](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/troubleshooting-interoperability_2.vb)]  
  
> [!NOTE]
>  互操作程序集隐式实现表示 COM 类的接口。  不应尝试使用 `Implements` 语句实现这些接口或将导致错误。  
  
##  <a name="vbconinteroperabilitymarshalinganchor7"></a> 参数和返回值的数据类型  
 不同于标准程序集的成员，互操作程序集的成员可以与原始对象声明中所用的数据类型。  尽管互操作程序集将 COM 类型隐式转换为兼容的公共语言运行时类型，应注意双方用于阻止运行时错误的数据类型。  例如，在 Visual Basic 6.0 和早期版本创建的 COM 对象，类型 `Integer` 的值假定 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort-md.md)] 等效的类型， `Short`。  建议您使用对象浏览器来检查导入成员的特性，在使用它们。  
  
##  <a name="vbconinteroperabilitymarshalinganchor8"></a> 模块级 COM 方法  
 创建 COM 类的实例使用 `New` 关键字然后调用对象的方法使用大多数 COM 对象。  此规则的例外情况涉及包含 `AppObj` 或 `GlobalMultiUse` COM 类的 COM 对象。  此类类似于 [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong-md.md)] 类的模块级方法。  Visual Basic 6.0 和早期版本第一次隐式创建实例的调用这些对象的方法。  例如，在 Visual Basic 6.0 可以添加对 Microsoft DAO 3.6 对象库和调用 `DBEngine` 方法，而无需首先创建一个实例:  
  
```  
Dim db As DAO.Database  
' Open the database.  
Set db = DBEngine.OpenDatabase("C:\nwind.mdb")  
' Use the database object.  
```  
  
 [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong-md.md)] 要求必须始终创建 COM 对象的实例，然后才能使用其方法。  若要使用这些方法在 [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong-md.md)]，声明所需类的变量并使用 new 关键字分配给对象变量。  可以使用 `Shared` 关键字，如果要确保时，只有一个类实例创建。  
  
 [!code-vb[VbVbalrInterop#23](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/troubleshooting-interoperability_3.vb)]  
  
##  <a name="vbconinteroperabilitymarshalinganchor9"></a> 在事件处理程序的未处理错误  
 一个常见互操作问题在处理 COM 对象所引发的事件处理程序涉及错误。  使用 `On Error` 或 `Try...Catch...Finally` 语句，，因此，除非您明确检查错误此类错误被忽略。  例如，下面的示例摘自具有对 Microsoft ActiveX Data Objects 2.8 Library COM 对象的 [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong-md.md)] 项目。  
  
 [!code-vb[VbVbalrInterop#24](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/troubleshooting-interoperability_4.vb)]  
  
 此示例引发错误按预期方式工作。  但是，在中，如果尝试相同的示例，而无需 `Try...Catch...Finally` 块，该错误将被忽略，就象使用了 `OnError Resume Next` 语句。  如果没有错误处理，被零除将导致失败。  由于这种错误从不引发未经处理的异常错误，务必要在事件处理程序使用某种形式的异常处理机制从 COM 对象所引发的事件。  
  
### 理解 COM 互操作错误  
 如果没有错误处理机制，互操作调用通常生成提供的信息的错误。  只要有可能，那么，当事件发生时，使用结构化错误处理提供更多信息。  ，在调试应用程序时，此控件尤其建立的。  例如:  
  
 [!code-vb[VbVbalrInterop#25](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/troubleshooting-interoperability_5.vb)]  
  
 您可以通过检查异常对象的内容找到很多信息描述、 HRESULT 和 COM 错误源。  
  
##  <a name="vbconinteroperabilitymarshalinganchor10"></a> Activex 控件问题  
 使用 Visual Basic 6.0 一起使用 [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong-md.md)] 一起使用，而不会遇到的大多数 Activex 控件。  例外主要在于容器上包含其他控件的控件或控件。  无法与 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)]使用较早的控件的一些示例如下:  
  
-   Microsoft forms 2.0 frame 控件  
  
-   Up\-Down 控件，也称作数值调节钮控件  
  
-   Sheridan tab 控件  
  
 对于不受支持的 Activex 控件问题少量的工作区。  您可以分次迁移现有控件绑定到 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)] ，如果您拥有原始的源代码。  否则，可以检查与软件供应商控件的更新.NET 兼容版本替换不受支持的 Activex 控件。  
  
##  <a name="vbconinteroperabilitymarshalinganchor11"></a> 按址传递控件的只读属性  
 ，当您通过某些旧 Activex 控件 `ReadOnly` 属性作为 `ByRef` 参数传递到其他过程时，[!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong-md.md)] 有时会引发 COM 错误 \(如 “error 0x800A017F CTL\_E\_SETNOTSUPPORTED”。  类似的从 Visual Basic 6.0 过程调用不会引发错误，并且，将参数，如同按值传递一样。  在 [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong-md.md)] 看到的错误消息是 COM 的对象尝试更改没有属性 `Set` 程序的属性。  
  
 如果可以访问调用的过程，可以防止此错误使用 `ByVal` 关键字声明接受 `ReadOnly` 特性的参数。  例如:  
  
 [!code-vb[VbVbalrInterop#26](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/troubleshooting-interoperability_6.vb)]  
  
 如果您无权访问其源代码的调用的过程，可以强制按值传递属性。添加额外的括号在调用程序附近。  例如，在具有对 Microsoft ActiveX Data Objects 2.8 Library COM 对象的项目中，可以使用:  
  
 [!code-vb[VbVbalrInterop#27](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/troubleshooting-interoperability_7.vb)]  
  
##  <a name="vbconinteroperabilitymarshalinganchor12"></a> 部署公开 Interop 的程序集  
 部署公开 COM 接口的程序集带来了一些特殊的难题。  例如，在中，当不同的应用程序引用同一个 COM 程序集，一个潜在问题。  这种情况很常见的，在安装新版本程序集，而另一应用程序仍在使用程序集的早期版本。  如果卸载共享 DLL 的程序集，则可能会无意中使其对于其他程序集不可用。  
  
 若要避免此问题，应将共享的程序集添加到全局程序集 \(GAC\)缓存并使用组件的 MergeModule。  如果您在全局程序集缓存中安装应用程序，应将其安装到 CommonFilesFolder 在一个特定于版本的子目录。  
  
 不共享的程序集应并行位于与调用应用程序的目录。  
  
## 请参阅  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [COM 互操作](../../../visual-basic/programming-guide/com-interop/index.md)   
 [Tlbimp.exe（类型库导入程序）](../Topic/Tlbimp.exe%20\(Type%20Library%20Importer\).md)   
 [Tlbexp.exe（类型库导出程序）](../Topic/Tlbexp.exe%20\(Type%20Library%20Exporter\).md)   
 [演练：用 COM 对象实现继承](../../../visual-basic/programming-guide/com-interop/walkthrough-implementing-inheritance-with-com-objects.md)   
 [Inherits 语句](../../../visual-basic/language-reference/statements/inherits-statement.md)   
 [全局程序集缓存](../Topic/Global%20Assembly%20Cache.md)