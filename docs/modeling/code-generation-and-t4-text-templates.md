---
title: "Code Generation and T4 Text Templates | Microsoft Docs"
ms.custom: ""
ms.date: "11/04/2016"
ms.prod: "visual-studio-tfs-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "vs-devops-techdebt"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "VS.ToolsOptionsPages.TextTemplating.TextTemplating"
helpviewer_keywords: 
  - "generating text"
  - ".tt files"
  - "code generation"
  - "text templates"
  - "generating code"
ms.assetid: 74a0a748-5b11-4999-8bea-49572967827d
caps.latest.revision: 82
author: "alancameronwills"
ms.author: "awills"
manager: "douge"
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
# Code Generation and T4 Text Templates
In [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], a *T4 text template* is a mixture of text blocks and control logic that can generate a text file. The control logic is written as fragments of program code in [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] or [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]. In Visual Studio 2015 Update 2 and later, you can use C# version 6.0 features in T4 templates directives. The generated file can be text of any kind, such as a Web page, or a resource file, or program source code in any language.  
  
 There are two kinds of T4 text templates:  
  
 **Run time T4 text templates** ('preprocessed' templates) are executed in your application to produce text strings, typically as part of its output.  
 For example, you could create a template to define an HTML page:  
  
```  
<html><body>  
 The date and time now is: <#= DateTime.Now #>  
</body></html>  
```  
  
 Notice that the template resembles the generated output. The similarity of the template to the resulting output helps you avoid mistakes when you want to change it.  
  
 In addition, the template contains fragments of program code. You can use these fragments to repeat sections of text, to make conditional sections, and to show data from your application.  
  
 To generate the output, your application calls a function that is generated by the template. For example:  
  
```c#  
string webResponseText = new MyTemplate().TransformText();  
  
```  
  
 Your application can run on a computer that does not have [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] installed.  
  
 To create a run-time template, add a **Preprocessed text template** file to your project. Alternatively, you can add a plain text file and set its **Custom Tool** property to **TextTemplatingFilePreprocessor**.  
  
 For more information, see [Run-Time Text Generation with T4 Text Templates](../modeling/run-time-text-generation-with-t4-text-templates.md). For more information about the syntax of templates, see [Writing a T4 Text Template](../modeling/writing-a-t4-text-template.md).  
  
 **Design-time T4 text templates** are executed in [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] to define part of the source code and other resources of your application.  
 Typically you would use several templates that read the data in a single input file or database, and generate some of your `.cs`, `.vb`, or other source files. Each template generates one file. They are executed within [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] or [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)].  
  
 For example, your input data could be an XML file of configuration data. Whenever you edit the XML file during development, the text templates would regenerate part of the application code. One of the templates could resemble the following example:  
  
```  
<#@ output extension=".txt" #>  
<#@ assembly name="System.Xml" #>  
<#  
 System.Xml.XmlDocument configurationData = ...; // Read a data file here.  
#>  
namespace Fabrikam.<#= configurationData.SelectSingleNode("jobName").Value #>  
{  
  ... // More code here.   
}  
  
```  
  
 Dependent on the values in the XML file, the generated `.cs` file would resemble the following:  
  
```  
namespace Fabrikam.FirstJob  
{  
  ... // More code here.   
}  
```  
  
 As another example, the input could be a diagram of workflow in a business activity. When the users change their business workflow, or when you start work with new users who have a different workflow, it is easy to regenerate the code to fit the new model.  
  
 Design-time templates make it quicker and more reliable to change the configuration when the requirements change. Typically the input is defined in terms of business requirements, as in the workflow example. This makes it easier to discuss the changes with your users. Design-time templates are therefore a useful tool in an agile development process.  
  
 To create a design-time template, add a **Text Template** file to your project. Alternatively, you can add a plain text file and set its **Custom Tool** property to **TextTemplatingFileGenerator**.  
  
 For more information, see [Design-Time Code Generation by using T4 Text Templates](../modeling/design-time-code-generation-by-using-t4-text-templates.md). For more information about the syntax of templates, see [Writing a T4 Text Template](../modeling/writing-a-t4-text-template.md).  
  
> [!NOTE]
>  The term *model* is sometimes used to describe data read by one or more templates. The model can be in any format, in any kind of file or database. It does not have to be a UML model or a Domain-Specific Language model. 'Model' just indicates that the data can be defined in terms of the business concepts, rather than resembling the code.  
  
 The text template transformation feature is named *T4*.  
  
## In This Section  
 [Run-Time Text Generation with T4 Text Templates](../modeling/run-time-text-generation-with-t4-text-templates.md)  
 In any application that generates text files, precompiled text templates are an easy and reliable method of defining the text. However, this method cannot be used for text templates that change at run time.  
  
 [Design-Time Code Generation by using T4 Text Templates](../modeling/design-time-code-generation-by-using-t4-text-templates.md)  
 Generating code and other resources from a model lets you update your application by updating the model.  
  
 [Code Generation in a Build Process](../modeling/code-generation-in-a-build-process.md)  
 If you have installed [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] Visualization and Modeling SDK, you can ensure the generated software keeps up to date with changes in the model.  
  
 [Writing a T4 Text Template](../modeling/writing-a-t4-text-template.md)  
 The syntax of a text template file.  
  
 [Walkthrough: Generating Code by using Text Templates](../modeling/walkthrough-generating-code-by-using-text-templates.md)  
 A demonstration of one way to use code generation.  
  
 [Debugging a T4 Text Template](../modeling/debugging-a-t4-text-template.md)  
 How to debug text templates, and some common text template errors.  
  
 [Generating Files with the TextTransform Utility](../modeling/generating-files-with-the-texttransform-utility.md)  
 The command-line tool that you can use to run text template transformations.  
  
 [Customizing T4 Text Transformation](../modeling/customizing-t4-text-transformation.md)  
 How to write directive processors and custom templating hosts for your own data sources.  
  
## See Also  
 [Generate files from a UML model](../modeling/generate-files-from-a-uml-model.md)   
 [Generating Code from a Domain-Specific Language](../modeling/generating-code-from-a-domain-specific-language.md)