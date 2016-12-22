---
title: "区域性对字符串的影响 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "区域设置, 对字符串的作用"
  - "字符串 [Visual Basic], 区域设置依赖"
ms.assetid: c4664444-ee0d-47bf-bef1-eaa3c54bdd7f
caps.latest.revision: 20
caps.handback.revision: 20
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# 区域性对字符串的影响 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

此帮助页讨论 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 如何使用区域性信息来执行字符串转换和比较。  
  
## 何时使用特定于区域性的字符串  
 通常，应该对提供给用户和从用户输入中读取的所有数据使用特定于区域性的字符串，而对应用程序的内部数据使用区域性固定的字符串。  
  
 例如，如果应用程序要求用户以字符串形式输入日期，则应预计到用户会根据各自的区域性对字符串进行格式设置，因此，应用程序应适当地转换字符串。  如果应用程序随后在其用户界面中呈现日期，则应按照用户的区域性来呈现。  
  
 但是，如果应用程序将日期上载到中央服务器，则应依据某个特定的区域性来设置字符串格式，以防止在可能不同的日期格式间出现混淆。  
  
## 区分区域性的函数  
 所有 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 字符串转换函数（除 `Str` 和 `Val` 函数外）都使用应用程序的区域性信息，以确保转换和比较适合于应用程序用户的区域性。  
  
 在运行于具有不同区域性设置的计算机上的应用程序中成功使用字符串转换函数的关键在于：了解哪些函数使用特定的区域性设置，哪些函数使用当前区域性设置。  请注意，应用程序的区域性设置默认情况下是从操作系统的区域性设置中继承的。  有关更多信息，请参见 <xref:Microsoft.VisualBasic.Strings.Asc%2A>、<xref:Microsoft.VisualBasic.Strings.AscW%2A>、<xref:Microsoft.VisualBasic.Strings.Chr%2A>、<xref:Microsoft.VisualBasic.Strings.ChrW%2A>、<xref:Microsoft.VisualBasic.Strings.Format%2A>、<xref:Microsoft.VisualBasic.Conversion.Hex%2A>、<xref:Microsoft.VisualBasic.Conversion.Oct%2A> 和 [类型转换函数](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)。  
  
 在字符串和数字之间进行转换时，`Str`（将数字转换为字符串）以及 `Val`（将字符串转换为数字）函数不使用应用程序的区域性信息。  相反，它们只将句点 \(.\) 识别为有效的小数点分隔符。  与这些函数类似的可识别区域性的函数包括：  
  
-   **使用当前区域性的转换。** `CStr` 和 `Format` 函数将数字转换为字符串，而 `CDbl` 和 `CInt` 函数将字符串转换为数字。  
  
-   **使用特定区域性的转换。**每个数字对象都有一个将数字转换为字符串的 `ToString(IFormatProvider)` 方法，以及一个将字符串转换为数字的 `Parse(String, IFormatProvider)` 方法。  例如，`Double` 类型提供了 <xref:System.Double.ToString%28System.IFormatProvider%29> 和 <xref:System.Double.Parse%28System.String%2CSystem.IFormatProvider%29> 方法。  
  
 有关更多信息，请参见 <xref:Microsoft.VisualBasic.Conversion.Str%2A> 和 <xref:Microsoft.VisualBasic.Conversion.Val%2A>。  
  
## 使用特定区域性  
 假设您正在开发一个将日期（设置为字符串格式）发送到 Web 服务的应用程序。  在这种情况下，应用程序必须为字符串转换使用特定区域性。  为了阐述原因，请考虑一下使用日期的 <xref:System.DateTime.ToString> 方法的结果：如果应用程序使用该方法来设置日期“2005 年 7 月 4 日”的格式，在使用美国英语 \(en\-US\) 区域性运行时，它将返回“7\/4\/2005 12:00:00 AM”，但在使用德语 \(de\-DE\) 区域性运行时，它将返回“04.07.2005 00:00:00”。  
  
 在需要采用特定区域性格式执行字符串转换时，应使用 [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] 内置的 `CultureInfo` 类。  通过将区域性的名称传递到 <xref:System.Globalization.CultureInfo.%23ctor%2A> 构造函数，您可以为某个特定区域性创建新的 `CultureInfo` 对象。  <xref:System.Globalization.CultureInfo> 类的“帮助”页中列出了支持的区域性名称。  
  
 或者，您可以从 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName> 属性中获取固定区域性的实例。  虽然固定区域性基于英语区域性，但也存在一些差异。  例如，固定区域性指定 24 小时制，而不是 12 小时制。  
  
 若要将日期转换为与区域性对应的字符串，请将 <xref:System.Globalization.CultureInfo> 对象传递到日期对象的 <xref:System.DateTime.ToString%28System.IFormatProvider%29> 方法。  例如，无论应用程序的区域性设置如何，以下代码都会显示“07\/04\/2005 00:00:00”。  
  
 [!code-vb[VbVbalrConcepts#1](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/codesnippet/VisualBasic/how-culture-affects-strings_1.vb)]  
  
> [!NOTE]
>  将总是依据英语区域性解释日期文本。  
  
## 比较字符串  
 在以下两种很重要的情况下，需要进行字符串比较：  
  
-   **对数据进行排序，以便向用户显示。**使用基于当前区域性的运算，以使字符串正确排序。  
  
-   **确定两个应用程序内部字符串是否完全匹配（通常用于安全目的）。**使用不考虑当前区域性的运算。  
  
 使用 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] <xref:Microsoft.VisualBasic.Strings.StrComp%2A> 函数可以执行这两种类型的比较。  指定可选参数 `Compare` 可控制比较的类型：对于大多数输入和输出，可指定 `Text`，如果要确定是否完全匹配，可指定 `Binary`。  
  
 `StrComp` 函数返回一个整数，该整数指示所比较的两个字符串之间基于排序顺序的关系。  正数结果值指示第一个字符串大于第二个字符串。  负数结果指示第一个字符串较小，而零指示两个字符串相等。  
  
 [!code-vb[VbVbalrStrings#22](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/how-culture-affects-strings_2.vb)]  
  
 也可以使用 [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] 中与 `StrComp` 函数对应的 <xref:System.String.Compare%2A?displayProperty=fullName> 方法。  这是基字符串类的静态重载方法。  下面的示例阐释如何使用此方法：  
  
 [!code-vb[VbVbalrStrings#48](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/how-culture-affects-strings_3.vb)]  
  
 为了更细致地控制比较的执行方式，您可以使用 <xref:System.String.Compare%2A> 方法的附加重载。  利用 <xref:System.String.Compare%2A?displayProperty=fullName> 方法，您可以使用 `comparisonType` 参数来指定要使用哪种比较方式。  
  
||||  
|-|-|-|  
|`comparisonType` 参数的值|比较类型|何时使用|  
|`Ordinal`|基于字符串组成部分字节数的比较。|在比较以下各项时使用此值：区分大小写的标识符、与安全相关的设置或者字节数必须完全匹配的其他非语言标识符。|  
|`OrdinalIgnoreCase`|基于字符串组成部分字节数的比较。<br /><br /> `OrdinalIgnoreCase` 使用固定区域性信息来确定两个字符在什么情况下只是大小写不同。|在比较以下各项时使用此值：不区分大小写的标识符、与安全相关的设置以及 Windows 中存储的数据。|  
|`CurrentCulture` 或 `CurrentCultureIgnoreCase`|基于字符串在当前区域性中的解读的比较。|在比较以下各项时使用这些值：向用户显示的数据、大多数用户输入以及需要语言学解读的其他数据。|  
|`InvariantCulture` 或 `InvariantCultureIgnoreCase`|基于字符串在固定区域性中的解读的比较。<br /><br /> 此类型与 `Ordinal` 和 `OrdinalIgnoreCase` 不同，因为固定区域性将其接受范围外的字符视为等效的固定字符。|只有在比较持久数据或显示需要固定排序顺序的语言相关数据时，才使用这些值。|  
  
### 安全注意事项  
 如果应用程序根据比较或大小写转换运算的结果制定安全决策，则运算应使用 <xref:System.String.Compare%2A?displayProperty=fullName> 方法，并为 `comparisonType` 参数传递 `Ordinal` 或 `OrdinalIgnoreCase`。  
  
## 请参阅  
 <xref:System.Globalization.CultureInfo>   
 [字符串介绍 \(Visual Basic\)](../../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)   
 [类型转换函数](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)