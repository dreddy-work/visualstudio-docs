---
title: "Reference required to assembly &#39;&lt;assemblyidentity&gt;&#39; containing type &#39;&lt;typename&gt;&#39;, but a suitable reference could not be found due to possible circular references: &lt;referencedependencylist&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "bc30962"
  - "vbc30962"
helpviewer_keywords: 
  - "BC30962"
ms.assetid: 6f338158-bfb4-4cc0-bbf7-1111c708613c
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
translation.priority.ht: 
  - "de-de"
  - "es-es"
  - "fr-fr"
  - "it-it"
  - "ja-jp"
  - "ko-kr"
  - "ru-ru"
  - "zh-cn"
  - "zh-tw"
translation.priority.mt: 
  - "cs-cz"
  - "pl-pl"
  - "pt-br"
  - "tr-tr"
---
# Reference required to assembly &#39;&lt;assemblyidentity&gt;&#39; containing type &#39;&lt;typename&gt;&#39;, but a suitable reference could not be found due to possible circular references: &lt;referencedependencylist&gt;
An expression uses a type, such as a class, structure, interface, enumeration, or delegate, that is defined outside your project. However, your project reference to that assembly is part of a set of circular references.  
  
 When several projects have references among themselves, the references can be *circular*. For example, two projects can have references to each other. More generally, a chain of references from one project to the next can ultimately return to the starting project. In such cases, there is no final project at the end of the chain with which to resolve the reference.  
  
 To access a type defined in another assembly, the [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] compiler must have a reference to that assembly. This must be a single, unambiguous reference that does not cause circular references among projects.  
  
 **Error ID:** BC30962  
  
### To correct this error  
  
-   In your project properties, add a direct reference to the project producing the assembly that defines the type you are using.  
  
## See Also  
 [Managing references in a project](../ide/managing-references-in-a-project.md)   
 [NIB: Referencing Namespaces and Components](http://msdn.microsoft.com/en-us/568fa759-796b-44cd-bf5e-1cf8de6e38fd)   
 [NIB How to: Add or Remove References By Using the Add Reference Dialog Box](http://msdn.microsoft.com/en-us/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)   
 [NIB How to: Modify Project Properties and Configuration Settings](http://msdn.microsoft.com/en-us/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)   
 [Troubleshooting Broken References](../ide/troubleshooting-broken-references.md)