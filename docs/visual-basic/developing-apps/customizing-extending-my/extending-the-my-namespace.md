---
title: "扩展 Visual Basic 中的 My 命名空间 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.AddingMyExtensions"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "My 命名空间"
  - "My 命名空间, 自定义"
  - "My 命名空间, 扩展"
ms.assetid: 808e8617-b01c-4135-8b21-babe87389e8e
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# 扩展 Visual Basic 中的 My 命名空间
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

Visual Basic 中的 `My` 命名空间公开了一些属性和方法，您可以利用这些属性和方法来轻松使用 .NET Framework 强大功能。  `My` 命名空间可以简化常见编程问题，它通常可将一个困难的任务简化为一行代码。  此外，`My` 命名空间可完全扩展，使您可以自定义 `My` 的行为，并可向其层次结构添加新服务，从而满足特定应用程序需求。  本主题将讨论如何自定义 `My` 命名空间的现有成员，以及如何将自己的自定义类添加到 `My` 命名空间中。  
  
 **主题内容**  
  
-   [自定义现有 My 命名空间成员](#customizing)  
  
-   [向 My 对象添加成员](#addingtoobjects)  
  
-   [向 My 命名空间添加自定义对象](#addingcustom)  
  
-   [向 My 命名空间添加成员](#addingtonamespace)  
  
-   [向自定义 My 对象添加事件](#addingevents)  
  
-   [设计准则](#design)  
  
-   [为 My 设计类库](#designing)  
  
-   [打包和部署扩展](#packaging)  
  
##  <a name="customizing"></a> 自定义现有 My 命名空间成员  
 Visual Basic 中的 `My` 命名空间公开了有关应用程序、计算机等的常用信息。  有关 `My` 命名空间中对象的完整列表，请参见 [My 引用](../../../visual-basic/language-reference/keywords/my-reference.md)。  您可能需要自定义 `My` 命名空间的现有成员，以使它们能更好地满足您应用程序的需求。  `My` 命名空间中的对象的任何属性，只要不是只读，则就可设置为自定义值。  
  
 例如，假定您经常使用 `My.User` 对象来访问运行您应用程序的用户的当前安全上下文。  但是，您公司使用自定义用户对象来公开公司内部用户的其他信息和功能。  在这种情况下，您可以将 `My.User.CurrentPrincipal` 属性的默认值替换为您自己的自定义主体对象的实例，如下面的示例中所示。  
  
 [!code-vb[VbVbcnExtendingMy#1](../../../visual-basic/developing-apps/customizing-extending-my/codesnippet/visualbasic/extending-the-my-namespace_1.vb)]  
  
 设置 `My.User` 对象的 `CurrentPrincipal` 属性，更改应用程序运行时所用的标识。  然后，`My.User` 对象就会返回新指定用户的相关信息。  
  
##  <a name="addingtoobjects"></a> 向 My 对象添加成员  
 从 `My.Application` 和 `My.Computer` 返回的类型定义为 `Partial` 类。  因此，您可以通过创建名称为 `MyApplication` 或 `MyComputer` `Partial` 的类来扩展 `My.Application` 和 `My.Computer` 对象。  该类不能为 `Private` 类。  如果将该类指定为 `My` 命名空间的部分，则可添加将要包括到 `My.Application` 或 `My.Computer` 对象的属性和方法。  
  
 例如，下面的示例将名称为 `DnsServerIPAddresses` 的属性添加到了 `My.Computer` 对象。  
  
 [!code-vb[VbVbcnExtendingMy#2](../../../visual-basic/developing-apps/customizing-extending-my/codesnippet/visualbasic/extending-the-my-namespace_2.vb)]  
  
##  <a name="addingcustom"></a> 向 My 命名空间添加自定义对象  
 虽然 `My` 命名空间提供了许多常见编程任务的解决方案，但是您还可能会遇到 `My` 命名空间未提供其解决方案的任务。  例如，您的应用程序可能需要访问自定义目录服务以获取用户数据，或者需要使用默认情况下不与 Visual Basic 一起安装的程序集。  如果出现这种情况，您就可扩展 `My` 命名空间，以将自定义解决方案包含到特定于您环境的常规任务中。  `My` 命名空间扩展方便，可轻松添加新成员，从而满足不断增长的应用程序需求。  此外，您还可以将 `My` 命名空间扩展作为 Visual Basic 模板，部署到其他开发人员的开发环境中。  
  
###  <a name="addingtonamespace"></a> 向 My 命名空间添加成员  
 由于 `My` 是一个命名空间，与其他所有命名空间类似；因此，您只需添加模块并指定 `My` 的 `Namespace`，就可向其中添加顶级属性。  使用 `HideModuleName` 特性可以批注模块，如下面的示例中所示。  `HideModuleName` 特性可确保 IntelliSense 显示 `My` 命名空间的成员时不显示模块名称。  
  
 [!code-vb[VbVbcnExtendingMy#3](../../../visual-basic/developing-apps/customizing-extending-my/codesnippet/visualbasic/extending-the-my-namespace_3.vb)]  
  
 若要向 `My` 命名空间添加成员，则请根据需要向模块添加属性。  对于添加到 `My` 命名空间的每个属性，请添加类型为 `ThreadSafeObjectProvider(Of T)` 的私有字段；其中，类型是您的自定义属性所返回的类型。  此字段用于创建线程安全对象实例，您的自定义属性将通过调用 `GetInstance` 方法来返回该实例。  这样，访问扩展属性的每个线程就可接收其自己的返回类型的实例。  下面的示例将类型为 `SampleExtension`、名称为 `SampleExtension` 的属性添加到了 `My` 命名空间：  
  
 [!code-vb[VbVbcnExtendingMy#4](../../../visual-basic/developing-apps/customizing-extending-my/codesnippet/visualbasic/extending-the-my-namespace_4.vb)]  
  
##  <a name="addingevents"></a> 向自定义 My 对象添加事件  
 您可以使用 `My.Application` 对象，通过扩展 `My` 命名空间中的 `MyApplication` 分部类来公开您的自定义 `My` 对象的事件。  对于基于 Windows 的项目，您可以在**解决方案资源管理器**中，双击项目的**“我的项目”**节点。  在 Visual Basic**“项目设计器”**中，单击 `Application` 选项卡，然后单击 `View Application Events` 按钮。  然后，将会创建一个名称为 ApplicationEvents.vb 的新文件。  该文件中包含下面的用于扩展 `MyApplication` 类的代码。  
  
 [!code-vb[VbVbcnExtendingMy#5](../../../visual-basic/developing-apps/customizing-extending-my/codesnippet/visualbasic/extending-the-my-namespace_5.vb)]  
  
 您可以通过将自定义事件处理程序添加到 `MyApplication` 类，来为您的自定义 `My` 对象添加事件处理程序。  您可以利用自定义事件，来添加当添加、移除事件处理程序或引发事件时要执行的代码。  注意，仅当用户为了处理事件而添加了代码时，自定义事件的 `AddHandler` 代码才会运行。  例如，请考虑上一节中的 `SampleExtension` 对象，该对象具有一个 `Load` 事件，且您要为该对象添加自定义事件处理程序。  下面的代码示例演示了名称为 `SampleExtensionLoad` 的自定义事件处理程序，当发生 `My.SampleExtension.Load` 事件时，将会调用该自定义事件处理程序。  当为了处理新的 `My.SampleExtensionLoad` 事件而添加代码时，将执行此自定义事件代码的 `AddHandler` 部分。  代码示例中包含有 `MyApplication_SampleExtensionLoad` 方法，目的是给出一个处理 `My.SampleExtensionLoad` 事件的事件处理程序的示例。  注意，在编辑 ApplicationEvents.vb 文件时，如果选中位于“代码编辑器”上方的下拉列表中的**“我的应用程序事件”**选项，则 `SampleExtensionLoad` 事件将可用。  
  
 [!code-vb[VbVbcnExtendingMy#6](../../../visual-basic/developing-apps/customizing-extending-my/codesnippet/visualbasic/extending-the-my-namespace_6.vb)]  
  
##  <a name="design"></a> 设计准则  
 开发 `My` 命名空间的扩展时，请遵循下面的准则，以帮助您将您的扩展组件的维护成本降到最低。  
  
-   **只包含扩展逻辑。** `My` 命名空间扩展中包含的逻辑应只包括公开 `My` 命名空间中所需功能时要用到的代码。  由于您的扩展将作为源代码驻留在用户项目中，更新扩展组件将带来高昂的维护成本，因此如果可能，请避免更新扩展组件。  
  
-   **最大限度地减少项目假设。**创建 `My` 命名空间的扩展时，请不要假定一组引用、项目级导入或特定编译器设置（例如，将 `Option Strict` 设置为 off）。  相反，要最小化依赖项，并使用 `Global` 关键字完全限定所有类型引用。  同时，还要确保编译扩展时，`Option Strict` 为 on，从而将扩展中的错误降到最少。  
  
-   **隔离扩展代码。**将代码置于单个文件中，可使您的扩展轻松部署为 Visual Studio 项模板。  有关更多信息，请参见本主题后面的“打包和部署扩展”。  将所有 `My` 命名空间扩展代码置于项目中的单个文件或文件夹中，还将有助于用户查找 `My` 命名空间扩展。  
  
##  <a name="designing"></a> 为 My 设计类库  
 对于多数对象模型，某些设计模式在 `My` 命名空间中运转正常，但其他设计模式则不然。  设计 `My` 命名空间的扩展时，请考虑下面的原则：  
  
-   **无状态方法。** `My` 命名空间中的方法应提供特定任务的完整解决方案。  请确保传递给方法的参数值要提供完成特定任务所需的所有输入。  避免创建依赖于先前状态的方法，例如到资源的打开连接。  
  
-   **全局实例。**只有 `My` 命名空间中维护的状态对于项目是全局性的。  例如，`My.Application.Info` 可封装整个应用程序中共享的状态。  
  
-   **简单参数类型。**为简单起见，请避免使用复杂的参数类型。  请创建不带参数输入或带简单的参数输入类型（如字符串、基元类型等）的方法。  
  
-   **工厂方法。**在某些类型的实例化过程中，会遇到不可避免的困难。  将工厂方法作为 `My` 命名空间的扩展提供，这样您就可更容易地发现并使用此类类型。  `My.Computer.FileSystem.OpenTextFileReader` 便是一个非常有效的工厂方法示例。  .NET Framework 中有多种流类型。  通过明确指定文本文件，`OpenTextFileReader` 可帮助用户理解要使用哪个流。  
  
 这些准则并不排除类库的常规设计原则。  相反，它们只是一些建议，专门针对使用 Visual Basic 和 `My` 命名空间的开发者进行了优化。  有关创建类库的常规设计原则的信息，请参见[Framework 设计准则](../Topic/Framework%20Design%20Guidelines.md)。  
  
##  <a name="packaging"></a> 打包和部署扩展  
 您可将 `My` 命名空间扩展包含在 Visual Studio 项目模板中，或者将您的扩展打包并部署为 Visual Studio 项模板。  您在将 `My` 命名空间扩展打包为 Visual Studio 项模板时，可以利用 Visual Basic 提供的其他功能。  您可以利用这些功能，在项目引用特定程序集时包含扩展；用户可以利用这些功能，通过使用 Visual Basic 项目设计器的**“My 扩展”**页，显式添加您的 `My` 命名空间扩展。  
  
 有关如何部署 `My` 命名空间扩展的详细信息，请参见[打包和部署自定义 My 扩展](../../../visual-basic/developing-apps/customizing-extending-my/packaging-and-deploying-custom-my-extensions.md)。  
  
## 请参阅  
 [打包和部署自定义 My 扩展](../../../visual-basic/developing-apps/customizing-extending-my/packaging-and-deploying-custom-my-extensions.md)   
 [扩展 Visual Basic 应用程序模型](../../../visual-basic/developing-apps/customizing-extending-my/extending-the-visual-basic-application-model.md)   
 [自定义 My 中可用的对象](../../../visual-basic/developing-apps/customizing-extending-my/customizing-which-objects-are-available-in-my.md)   
 [“项目设计器”\-\>“My 扩展”页](/visual-studio/ide/reference/my-extensions-page-project-designer-visual-basic)   
 [“项目设计器”, “应用程序”页 \(Visual Basic\)](/visual-studio/ide/reference/application-page-project-designer-visual-basic)   
 [分部](../../../visual-basic/language-reference/modifiers/partial.md)