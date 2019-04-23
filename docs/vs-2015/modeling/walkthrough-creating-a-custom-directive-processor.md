---
title: 'チュートリアル: カスタム ディレクティブ プロセッサの作成 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- text templates, custom directive processors
- walkthroughs [text templates], directive processor
ms.assetid: b8f35a36-14e1-4467-8f5f-e01402af14d5
caps.latest.revision: 76
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 665c59e6881ec2e5924845dfc8dcc130b5044095
ms.sourcegitcommit: 53aa5a413717a1b62ca56a5983b6a50f7f0663b3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59663389"
---
# <a name="walkthrough-creating-a-custom-directive-processor"></a>チュートリアル: カスタム ディレクティブ プロセッサの作成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ディレクティブ プロセッサ * 作業コードを追加して、*生成された変換クラス*します。 *テキスト テンプレート*から*ディレクティブ*を呼び出す場合、テキスト テンプレートに記述したコードの残りの部分は、ディレクティブが提供する機能に依存する可能性があります。  

 独自のカスタム ディレクティブ プロセッサを記述できます。 これにより、テキスト テンプレートをカスタマイズすることができます。 カスタム ディレクティブ プロセッサを作成するには、<xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> または <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> を継承するクラスを作成します。  

 このチュートリアルでは、次のタスクについて説明します。  

-   カスタム ディレクティブ プロセッサの作成  

-   ディレクティブ プロセッサの登録  

-   ディレクティブ プロセッサのテスト  

## <a name="prerequisites"></a>必須コンポーネント  
 このチュートリアルを完了するための要件を次に示します。  

-   Visual Studio 2010  

-   Visual Studio 2010 SDK  

## <a name="creating-a-custom-directive-processor"></a>カスタム ディレクティブ プロセッサの作成  
 このチュートリアルでは、カスタム ディレクティブ プロセッサを作成します。 XML ファイルを読み取って <xref:System.Xml.XmlDocument> 変数に格納し、プロパティを通じてそれを公開するカスタム ディレクティブを追加します。 「ディレクティブ プロセッサのテスト」では、テキスト テンプレートでこのプロパティを使用して XML ファイルにアクセスします。  

 カスタム ディレクティブの呼び出しは、次のような形式で記述します。  

 `<#@ CoolDirective Processor="CustomDirectiveProcessor" FileName="<Your Path>DocFile.xml" #>`  

 カスタム ディレクティブ プロセッサは、生成された変換クラスに変数とプロパティを追加します。 これから記述するディレクティブでは、<xref:System.CodeDom> クラスを使用して、生成された変換クラスにエンジンによって追加されるコードを作成します。 <xref:System.CodeDom> クラスは、[!INCLUDE[vbprvb](../includes/vbprvb-md.md)] ディレクティブの `language` パラメーターで指定された言語に応じて、Visual C# または `template` でコードを作成します。 ディレクティブ プロセッサの言語とディレクティブ プロセッサにアクセスするテキスト テンプレートの言語は、同じでなくてもかまいません。  

 ディレクティブによって作成されるコードは次のようになります。  

```csharp  
private System.Xml.XmlDocument document0Value;  

public virtual System.Xml.XmlDocument Document0  
{  
  get  
  {  
    if ((this.document0Value == null))  
    {  
      this.document0Value = XmlReaderHelper.ReadXml(<FileNameParameterValue>);  
    }  
    return this.document0Value;  
  }  
}  
```  

```vb  
Private document0Value As System.Xml.XmlDocument  

Public Overridable ReadOnly Property Document0() As System.Xml.XmlDocument  
    Get  
        If (Me.document0Value Is Nothing) Then  
            Me.document0Value = XmlReaderHelper.ReadXml(<FileNameParameterValue>)  
        End If  
        Return Me.document0Value  
    End Get  
End Property  
```  

#### <a name="to-create-a-custom-directive-processor"></a>カスタム ディレクティブ プロセッサを作成するには  

1.  Visual Studio で、CustomDP という名前の C# クラス ライブラリ プロジェクトまたは Visual Basic クラス ライブラリ プロジェクトを作成します。  

    > [!NOTE]
    >  複数のコンピューターにディレクティブ プロセッサをインストールする場合は、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Extension (VSIX) プロジェクトを使用し、拡張機能に .pkgdef ファイルを追加することをお勧めします。 詳細については、「[カスタム ディレクティブ プロセッサの配置](../modeling/deploying-a-custom-directive-processor.md)」をご覧ください。  

2.  次のアセンブリへの参照を追加します。  

    -   **Microsoft.VisualStudio.TextTemplating.\*.0**  

    -   **Microsoft.VisualStudio.TextTemplating.Interfaces.\*.0**  

3.  **Class1** のコードを次のコードに置き換えます。 このコードによって、<xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> クラスを継承し、必要なメソッドを実装する CustomDirectiveProcessor クラスが定義されます。  

    ```csharp  
    using System;  
    using System.CodeDom;  
    using System.CodeDom.Compiler;  
    using System.Collections.Generic;  
    using System.Globalization;  
    using System.IO;  
    using System.Text;  
    using System.Xml;  
    using System.Xml.Serialization;  
    using Microsoft.VisualStudio.TextTemplating;  

    namespace CustomDP  
    {  
        public class CustomDirectiveProcessor : DirectiveProcessor  
        {  
            //this buffer stores the code that is added to the   
            //generated transformation class after all the processing is done   
            //---------------------------------------------------------------------  
            private StringBuilder codeBuffer;  

            //Using a Code Dom Provider creates code for the   
            //generated transformation class in either Visual Basic or C#.  
            //If you want your directive processor to support only one language, you  
            //can hard code the code you add to the generated transformation class.  
            //In that case, you do not need this field.  
            //--------------------------------------------------------------------------  
            private CodeDomProvider codeDomProvider;  

            //this stores the full contents of the text template that is being processed  
            //--------------------------------------------------------------------------  
            private String templateContents;  

            //These are the errors that occur during processing. The engine passes   
            //the errors to the host, and the host can decide how to display them,  
            //for example the host can display the errors in the UI  
            //or write them to a file.  
            //---------------------------------------------------------------------  
            private CompilerErrorCollection errorsValue;  
            public new CompilerErrorCollection Errors  
            {  
                get { return errorsValue; }  
            }  

            //Each time this directive processor is called, it creates a new property.  
            //We count how many times we are called, and append "n" to each new  
            //property name. The property names are therefore unique.  
            //-----------------------------------------------------------------------------  
            private int directiveCount = 0;  

            public override void Initialize(ITextTemplatingEngineHost host)  
            {  
                //we do not need to do any initialization work  
            }  

            public override void StartProcessingRun(CodeDomProvider languageProvider, String templateContents, CompilerErrorCollection errors)  
            {  
                //the engine has passed us the language of the text template  
                //we will use that language to generate code later  
                //----------------------------------------------------------  
                this.codeDomProvider = languageProvider;  
                this.templateContents = templateContents;  
                this.errorsValue = errors;  

                this.codeBuffer = new StringBuilder();  
            }  

            //Before calling the ProcessDirective method for a directive, the   
            //engine calls this function to see whether the directive is supported.  
            //Notice that one directive processor might support many directives.  
            //---------------------------------------------------------------------  
            public override bool IsDirectiveSupported(string directiveName)  
            {  
                if (string.Compare(directiveName, "CoolDirective", StringComparison.OrdinalIgnoreCase) == 0)  
                {  
                    return true;  
                }  
                if (string.Compare(directiveName, "SuperCoolDirective", StringComparison.OrdinalIgnoreCase) == 0)  
                {  
                    return true;  
                }  
                return false;  
            }  

            public override void ProcessDirective(string directiveName, IDictionary<string, string> arguments)  
            {  
                if (string.Compare(directiveName, "CoolDirective", StringComparison.OrdinalIgnoreCase) == 0)  
                {  
                    string fileName;  

                    if (!arguments.TryGetValue("FileName", out fileName))  
                    {  
                        throw new DirectiveProcessorException("Required argument 'FileName' not specified.");  
                    }  

                    if (string.IsNullOrEmpty(fileName))  
                    {  
                        throw new DirectiveProcessorException("Argument 'FileName' is null or empty.");  
                    }  

                    //Now we add code to the generated transformation class.  
                    //This directive supports either Visual Basic or C#, so we must use the  
                    //System.CodeDom to create the code.  
                    //If a directive supports only one language, you can hard code the code.  
                    //--------------------------------------------------------------------------  

                    CodeMemberField documentField = new CodeMemberField();  

                    documentField.Name = "document" + directiveCount + "Value";  
                    documentField.Type = new CodeTypeReference(typeof(XmlDocument));  
                    documentField.Attributes = MemberAttributes.Private;  

                    CodeMemberProperty documentProperty = new CodeMemberProperty();  

                    documentProperty.Name = "Document" + directiveCount;  
                    documentProperty.Type = new CodeTypeReference(typeof(XmlDocument));  
                    documentProperty.Attributes = MemberAttributes.Public;  
                    documentProperty.HasSet = false;  
                    documentProperty.HasGet = true;  

                    CodeExpression fieldName = new CodeFieldReferenceExpression(new CodeThisReferenceExpression(), documentField.Name);  
                    CodeExpression booleanTest = new CodeBinaryOperatorExpression(fieldName, CodeBinaryOperatorType.IdentityEquality, new CodePrimitiveExpression(null));  
                    CodeExpression rightSide = new CodeMethodInvokeExpression(new CodeTypeReferenceExpression("XmlReaderHelper"), "ReadXml", new CodePrimitiveExpression(fileName));  
                    CodeStatement[] thenSteps = new CodeStatement[] { new CodeAssignStatement(fieldName, rightSide) };  

                    CodeConditionStatement ifThen = new CodeConditionStatement(booleanTest, thenSteps);  
                    documentProperty.GetStatements.Add(ifThen);  

                    CodeStatement s = new CodeMethodReturnStatement(fieldName);  
                    documentProperty.GetStatements.Add(s);  

                    CodeGeneratorOptions options = new CodeGeneratorOptions();  
                    options.BlankLinesBetweenMembers = true;  
                    options.IndentString = "    ";  
                    options.VerbatimOrder = true;  
                    options.BracingStyle = "C";  

                    using (StringWriter writer = new StringWriter(codeBuffer, CultureInfo.InvariantCulture))  
                    {  
                        codeDomProvider.GenerateCodeFromMember(documentField, writer, options);  
                        codeDomProvider.GenerateCodeFromMember(documentProperty, writer, options);  
                    }  

                }//end CoolDirective  

                //One directive processor can contain many directives.  
                //If you want to support more directives, the code goes here...  
                //-----------------------------------------------------------------  
                if (string.Compare(directiveName, "supercooldirective", StringComparison.OrdinalIgnoreCase) == 0)  
                {  
                    //code for SuperCoolDirective goes here...  
                }//end SuperCoolDirective  

                //Track how many times the processor has been called.  
                //-----------------------------------------------------------------  
                directiveCount++;  

            }//end ProcessDirective  

            public override void FinishProcessingRun()  
            {  
                this.codeDomProvider = null;  

                //important: do not do this:  
                //the get methods below are called after this method   
                //and the get methods can access this field  
                //-----------------------------------------------------------------  
                //this.codeBuffer = null;  
            }  

            public override string GetPreInitializationCodeForProcessingRun()  
            {  
                //Use this method to add code to the start of the   
                //Initialize() method of the generated transformation class.  
                //We do not need any pre-initialization, so we will just return "".  
                //-----------------------------------------------------------------  
                //GetPreInitializationCodeForProcessingRun runs before the   
                //Initialize() method of the base class.  
                //-----------------------------------------------------------------  
                return String.Empty;  
            }  

            public override string GetPostInitializationCodeForProcessingRun()  
            {  
                //Use this method to add code to the end of the   
                //Initialize() method of the generated transformation class.  
                //We do not need any post-initialization, so we will just return "".  
                //------------------------------------------------------------------  
                //GetPostInitializationCodeForProcessingRun runs after the  
                //Initialize() method of the base class.  
                //-----------------------------------------------------------------  
                return String.Empty;  
            }  

            public override string GetClassCodeForProcessingRun()  
            {  
                //Return the code to add to the generated transformation class.  
                //-----------------------------------------------------------------  
                return codeBuffer.ToString();  
            }  

            public override string[] GetReferencesForProcessingRun()  
            {  
                //This returns the references that we want to use when   
                //compiling the generated transformation class.  
                //-----------------------------------------------------------------  
                //We need a reference to this assembly to be able to call   
                //XmlReaderHelper.ReadXml from the generated transformation class.  
                //-----------------------------------------------------------------  
                return new string[]  
                {  
                    "System.Xml",  
                    this.GetType().Assembly.Location  
                };  
            }  

            public override string[] GetImportsForProcessingRun()  
            {  
                //This returns the imports or using statements that we want to   
                //add to the generated transformation class.  
                //-----------------------------------------------------------------  
                //We need CustomDP to be able to call XmlReaderHelper.ReadXml  
                //from the generated transformation class.  
                //-----------------------------------------------------------------  
                return new string[]  
                {  
                    "System.Xml",  
                    "CustomDP"  
                };  
            }  
        }//end class CustomDirectiveProcessor  

        //-------------------------------------------------------------------------  
        // the code that we are adding to the generated transformation class   
        // will call this method  
        //-------------------------------------------------------------------------  
        public static class XmlReaderHelper  
        {  
            public static XmlDocument ReadXml(string fileName)  
            {  
                XmlDocument d = new XmlDocument();  

                using (XmlTextReader reader = new XmlTextReader(fileName))  
                {  
                    try  
                    {  
                        d.Load(reader);  
                    }  
                    catch (System.Xml.XmlException e)  
                    {  
                        throw new DirectiveProcessorException("Unable to read the XML file.", e);  
                    }  
                }  
                return d;  
            }  
        }//end class XmlReaderHelper  
    }//end namespace CustomDP  
    ```  

    ```vb  
    Imports System  
    Imports System.CodeDom  
    Imports System.CodeDom.Compiler  
    Imports System.Collections.Generic  
    Imports System.Globalization  
    Imports System.IO  
    Imports System.Text  
    Imports System.Xml  
    Imports System.Xml.Serialization  
    Imports Microsoft.VisualStudio.TextTemplating  

    Namespace CustomDP  

        Public Class CustomDirectiveProcessor  
        Inherits DirectiveProcessor  

            'this buffer stores the code that is added to the   
            'generated transformation class after all the processing is done   
            '---------------------------------------------------------------  
            Private codeBuffer As StringBuilder  

            'Using a Code Dom Provider creates code for the  
            'generated transformation class in either Visual Basic or C#.  
            'If you want your directive processor to support only one language, you  
            'can hard code the code you add to the generated transformation class.  
            'In that case, you do not need this field.  
            '--------------------------------------------------------------------------  
            Private codeDomProvider As CodeDomProvider  

            'this stores the full contents of the text template that is being processed  
            '--------------------------------------------------------------------------  
            Private templateContents As String  

            'These are the errors that occur during processing. The engine passes   
            'the errors to the host, and the host can decide how to display them,  
            'for example the host can display the errors in the UI  
            'or write them to a file.  
            '---------------------------------------------------------------------  
            Private errorsValue As CompilerErrorCollection  
            Public Shadows ReadOnly Property Errors() As CompilerErrorCollection  
                Get  
                    Return errorsValue  
                End Get  
            End Property  

            'Each time this directive processor is called, it creates a new property.  
            'We count how many times we are called, and append "n" to each new  
            'property name. The property names are therefore unique.  
            '--------------------------------------------------------------------------  
            Private directiveCount As Integer = 0  

            Public Overrides Sub Initialize(ByVal host As ITextTemplatingEngineHost)  

                'we do not need to do any initialization work  
            End Sub  

            Public Overrides Sub StartProcessingRun(ByVal languageProvider As CodeDomProvider, ByVal templateContents As String, ByVal errors As CompilerErrorCollection)  

                'the engine has passed us the language of the text template  
                'we will use that language to generate code later  
                '----------------------------------------------------------  
                Me.codeDomProvider = languageProvider  
                Me.templateContents = templateContents  
                Me.errorsValue = errors  

                Me.codeBuffer = New StringBuilder()  
            End Sub  

            'Before calling the ProcessDirective method for a directive, the   
            'engine calls this function to see whether the directive is supported.  
            'Notice that one directive processor might support many directives.  
            '---------------------------------------------------------------------  
            Public Overrides Function IsDirectiveSupported(ByVal directiveName As String) As Boolean  

                If String.Compare(directiveName, "CoolDirective", StringComparison.OrdinalIgnoreCase) = 0 Then  
                    Return True  
                End If  

                If String.Compare(directiveName, "SuperCoolDirective", StringComparison.OrdinalIgnoreCase) = 0 Then  
                    Return True  
                End If  

                Return False  
            End Function  

            Public Overrides Sub ProcessDirective(ByVal directiveName As String, ByVal arguments As IDictionary(Of String, String))  

                If String.Compare(directiveName, "CoolDirective", StringComparison.OrdinalIgnoreCase) = 0 Then  

                    Dim fileName As String  

                    If Not (arguments.TryGetValue("FileName", fileName)) Then  
                        Throw New DirectiveProcessorException("Required argument 'FileName' not specified.")  
                    End If  

                    If String.IsNullOrEmpty(fileName) Then  
                        Throw New DirectiveProcessorException("Argument 'FileName' is null or empty.")  
                    End If  

                    'Now we add code to the generated transformation class.  
                    'This directive supports either Visual Basic or C#, so we must use the  
                    'System.CodeDom to create the code.  
                    'If a directive supports only one language, you can hard code the code.  
                    '--------------------------------------------------------------------------  

                    Dim documentField As CodeMemberField = New CodeMemberField()  

                    documentField.Name = "document" & directiveCount & "Value"  
                    documentField.Type = New CodeTypeReference(GetType(XmlDocument))  
                    documentField.Attributes = MemberAttributes.Private  

                    Dim documentProperty As CodeMemberProperty = New CodeMemberProperty()  

                    documentProperty.Name = "Document" & directiveCount  
                    documentProperty.Type = New CodeTypeReference(GetType(XmlDocument))  
                    documentProperty.Attributes = MemberAttributes.Public  
                    documentProperty.HasSet = False  
                    documentProperty.HasGet = True  

                    Dim fieldName As CodeExpression = New CodeFieldReferenceExpression(New CodeThisReferenceExpression(), documentField.Name)  
                    Dim booleanTest As CodeExpression = New CodeBinaryOperatorExpression(fieldName, CodeBinaryOperatorType.IdentityEquality, New CodePrimitiveExpression(Nothing))  
                    Dim rightSide As CodeExpression = New CodeMethodInvokeExpression(New CodeTypeReferenceExpression("XmlReaderHelper"), "ReadXml", New CodePrimitiveExpression(fileName))  
                    Dim thenSteps As CodeStatement() = New CodeStatement() {New CodeAssignStatement(fieldName, rightSide)}  

                    Dim ifThen As CodeConditionStatement = New CodeConditionStatement(booleanTest, thenSteps)  
                    documentProperty.GetStatements.Add(ifThen)  

                    Dim s As CodeStatement = New CodeMethodReturnStatement(fieldName)  
                    documentProperty.GetStatements.Add(s)  

                    Dim options As CodeGeneratorOptions = New CodeGeneratorOptions()  
                    options.BlankLinesBetweenMembers = True  
                    options.IndentString = "    "  
                    options.VerbatimOrder = True  
                    options.BracingStyle = "VB"  

                    Using writer As StringWriter = New StringWriter(codeBuffer, CultureInfo.InvariantCulture)  

                        codeDomProvider.GenerateCodeFromMember(documentField, writer, options)  
                        codeDomProvider.GenerateCodeFromMember(documentProperty, writer, options)  
                    End Using  

                End If  'CoolDirective  

                'One directive processor can contain many directives.  
                'If you want to support more directives, the code goes here...  
                '-----------------------------------------------------------------  
                If String.Compare(directiveName, "supercooldirective", StringComparison.OrdinalIgnoreCase) = 0 Then  

                    'code for SuperCoolDirective goes here  
                End If 'SuperCoolDirective  

                'Track how many times the processor has been called.  
                '-----------------------------------------------------------------  
                directiveCount += 1  
            End Sub 'ProcessDirective  

            Public Overrides Sub FinishProcessingRun()  

                Me.codeDomProvider = Nothing  

                'important: do not do this:  
                'the get methods below are called after this method   
                'and the get methods can access this field  
                '-----------------------------------------------------------------  
                'Me.codeBuffer = Nothing  
            End Sub  

            Public Overrides Function GetPreInitializationCodeForProcessingRun() As String  

                'Use this method to add code to the start of the   
                'Initialize() method of the generated transformation class.  
                'We do not need any pre-initialization, so we will just return "".  
                '-----------------------------------------------------------------  
                'GetPreInitializationCodeForProcessingRun runs before the   
                'Initialize() method of the base class.  
                '-----------------------------------------------------------------  
                Return String.Empty  
            End Function  

            Public Overrides Function GetPostInitializationCodeForProcessingRun() As String  

                'Use this method to add code to the end of the   
                'Initialize() method of the generated transformation class.  
                'We do not need any post-initialization, so we will just return "".  
                '------------------------------------------------------------------  
                'GetPostInitializationCodeForProcessingRun runs after the  
                'Initialize() method of the base class.  
                '-----------------------------------------------------------------  
                Return String.Empty  
            End Function  

            Public Overrides Function GetClassCodeForProcessingRun() As String  

                'Return the code to add to the generated transformation class.  
                '-----------------------------------------------------------------  
                Return codeBuffer.ToString()  
            End Function  

            Public Overrides Function GetReferencesForProcessingRun() As String()  

                'This returns the references that we want to use when   
                'compiling the generated transformation class.  
                '-----------------------------------------------------------------  
                'We need a reference to this assembly to be able to call   
                'XmlReaderHelper.ReadXml from the generated transformation class.  
                '-----------------------------------------------------------------  
                Return New String() {"System.Xml", Me.GetType().Assembly.Location}  
            End Function  

            Public Overrides Function GetImportsForProcessingRun() As String()  

                'This returns the imports or using statements that we want to   
                'add to the generated transformation class.  
                '-----------------------------------------------------------------  
                'We need CustomDP to be able to call XmlReaderHelper.ReadXml  
                'from the generated transformation class.  
                '-----------------------------------------------------------------  
                Return New String() {"System.Xml", "CustomDP"}  
            End Function  
        End Class 'CustomDirectiveProcessor  

        '--------------------------------------------------------------------------  
        ' the code that we are adding to the generated transformation class   
        ' will call this method  
        '--------------------------------------------------------------------------  
        Public Class XmlReaderHelper  

            Public Shared Function ReadXml(ByVal fileName As String) As XmlDocument  

                Dim d As XmlDocument = New XmlDocument()  

                Using reader As XmlTextReader = New XmlTextReader(fileName)  

                    Try  
                        d.Load(reader)  

                    Catch e As System.Xml.XmlException  

                        Throw New DirectiveProcessorException("Unable to read the XML file.", e)  
                    End Try  
                End Using  

                Return d  
            End Function  
        End Class 'XmlReaderHelper  

    End Namespace  
    ```  

4.  [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]のみ、開く、**プロジェクト** メニューをクリック**CustomDP プロパティ**です。 **[アプリケーション]** タブの **[ルート名前空間]** から既定値 `CustomDP` を削除します。  

5.  **[ファイル]** メニューの **[すべてを保存]** をクリックします。  

6.  **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。  

### <a name="build-the-project"></a>プロジェクトのビルド  
 プロジェクトをビルドします。 **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。  

## <a name="registering-the-directive-processor"></a>ディレクティブ プロセッサの登録  
 テキスト テンプレートからディレクティブを呼び出す前に[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]、ディレクティブ プロセッサのレジストリ キーを追加する必要があります。  

> [!NOTE]
>  複数のコンピューターにディレクティブ プロセッサをインストールする場合は、アセンブリと .pkgdef ファイルを含む [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Extension (VSIX) を定義することをお勧めします。 詳細については、「[カスタム ディレクティブ プロセッサの配置](../modeling/deploying-a-custom-directive-processor.md)」をご覧ください。  

 ディレクティブ プロセッサのキーは次の場所のレジストリにあります。  

```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\*.0\TextTemplating\DirectiveProcessors  
```  

 64 ビット システムの場合、レジストリは次の場所にあります。  

```  
HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\VisualStudio\*.0\TextTemplating\DirectiveProcessors  
```  

 ここでは、この場所にカスタム ディレクティブ プロセッサのキーを追加します。  

> [!CAUTION]
>  レジストリを誤って編集すると、システムに重大な障害をもたらす可能性があります。 レジストリを変更する前に、コンピューター上の重要なデータをすべてバックアップしてください。  

#### <a name="to-add-a-registry-key-for-the-directive-processor"></a>ディレクティブ プロセッサのレジストリ キーを追加するには  

1. [スタート] メニューまたはコマンド ラインを使用して、`regedit` コマンドを実行します。  

2. **\software\microsoft\visualstudio\\\\*.0\TextTemplating\DirectiveProcessors** を参照し、ノードをクリックします。  

    64 ビット システムでは、**HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\VisualStudio\\\*.0\TextTemplating\DirectiveProcessors** を使います。  

3. CustomDirectiveProcessor という名前の新しいキーを追加します。  

   > [!NOTE]
   >  これは、カスタム ディレクティブの Processor フィールドで使用する名前です。 この名前は、ディレクティブの名前、ディレクティブ プロセッサ クラスの名前、またはディレクティブ プロセッサの名前空間と同じでなくてもかまいません。  

4. Class という名前の新しい文字列値を追加し、その新しい文字列に CustomDP.CustomDirectiveProcessor という値を設定します。  

5. CodeBase という名前の新しい文字列値を追加し、このチュートリアルで作成した CustomDP.dll のパスに一致する値を設定します。  

    たとえば、パスは、`C:\UserFiles\CustomDP\bin\Debug\CustomDP.dll` のようになります。  

    レジストリ キーの値は次のようになります。  

   |   名前    |  型  |                                   データ                                   |
   |-----------|--------|--------------------------------------------------------------------------|
   | (既定) | REG_SZ |                             (値が設定されていません)                              |
   |   クラス   | REG_SZ |                    CustomDP.CustomDirectiveProcessor                     |
   | CodeBase  | REG_SZ | <strong>\<ソリューションへのパス></strong>CustomDP\bin\Debug\CustomDP.dll |

    アセンブリを GAC に追加した場合は、値を次のように設定します。  

   |   名前    |  型  |               データ                |
   |-----------|--------|-----------------------------------|
   | (既定) | REG_SZ |          (値が設定されていません)          |
   |   クラス   | REG_SZ | CustomDP.CustomDirectiveProcessor |
   | Assembly  | REG_SZ |           CustomDP.dll            |

6. Visual Studio を再起動します。  

## <a name="testing-the-directive-processor"></a>ディレクティブ プロセッサのテスト  
 ディレクティブ プロセッサをテストするには、それを呼び出すテキスト テンプレートを記述する必要があります。  

 この例のテキスト テンプレートでは、ディレクティブを呼び出し、クラス ファイルのドキュメントを含む XML ファイルの名前を渡します。 詳細については、次を参照してください。 [XML ドキュメント コメント](http://msdn.microsoft.com/library/803b7f7b-7428-4725-b5db-9a6cff273199)します。  

 テキスト テンプレートでは、次に、ディレクティブによって作成された <xref:System.Xml.XmlDocument> プロパティを使用して XML をナビゲートし、ドキュメントのコメントを出力します。  

#### <a name="to-create-an-xml-file-for-use-in-testing-the-directive-processor"></a>ディレクティブ プロセッサのテストに使用する XML ファイルを作成するには  

1.  という名前のテキスト ファイルを作成する`DocFile.xml`任意のテキスト エディター (メモ帳など) を使用しています。  

    > [!NOTE]
    >  このファイルはどこに作成してもかまいません (C:\Test\DocFile.xml など)。  

2.  次の内容をテキスト ファイルに追加します。  

    ```  
    <?xml version="1.0"?>  
    <doc>  
        <assembly>  
            <name>xmlsample</name>  
        </assembly>  
        <members>  
            <member name="T:SomeClass">  
                <summary>Class level summary documentation goes here.</summary>  
                <remarks>Longer comments can be associated with a type or member through the remarks tag</remarks>  
            </member>  
            <member name="F:SomeClass.m_Name">  
                <summary>Store for the name property</summary>  
            </member>   
            <member name="M:SomeClass.#ctor">  
                <summary>The class constructor.</summary>   
            </member>  
            <member name="M:SomeClass.SomeMethod(System.String)">  
                <summary>Description for SomeMethod.</summary>  
                <param name="s">Parameter description for s goes here</param>  
                <seealso cref="T:System.String">You can use the cref attribute on any tag to reference a type or member and the compiler will check that the reference exists.</seealso>  
            </member>  
            <member name="M:SomeClass.SomeOtherMethod">  
                <summary>Some other method.</summary>  
                <returns>Return results are described through the returns tag.</returns>  
                <seealso cref="M:SomeClass.SomeMethod(System.String)">Notice the use of the cref attribute to reference a specific method</seealso>  
            </member>  
            <member name="M:SomeClass.Main(System.String[])">  
                <summary>The entry point for the application.</summary>  
                <param name="args">A list of command line arguments</param>  
            </member>  
            <member name="P:SomeClass.Name">  
                <summary>Name property</summary>  
                <value>A value tag is used to describe the property value</value>  
            </member>  
        </members>  
    </doc>  
    ```  

3.  ファイルを保存して閉じます。  

#### <a name="to-create-a-text-template-to-test-the-directive-processor"></a>テキスト テンプレートを作成してディレクティブ プロセッサをテストするには  

1.  Visual Studio で、TemplateTest という名前の C# クラス ライブラリ プロジェクトまたは Visual Basic クラス ライブラリ プロジェクトを作成します。  

2.  TestDP.tt という名前の新しいテキスト テンプレート ファイルを追加します。  

3.  TestDP.tt の**カスタム ツール** プロパティが、`TextTemplatingFileGenerator` に設定されているかを確認します。  

4.  TestDP.tt の内容を次のテキストに変更します。  

    > [!NOTE]
    >  文字列を置換することを確認 <`YOUR PATH>` DocFile.xml ファイルへのパス。  

     テキスト テンプレートの言語は、ディレクティブ プロセッサの言語と同じでなくてもかまいません。  

    ```csharp  
    <#@ assembly name="System.Xml" #>  
    <#@ template debug="true" #>  
    <#@ output extension=".txt" #>  

    <#  //This will call the custom directive processor. #>  
    <#@ CoolDirective Processor="CustomDirectiveProcessor" FileName="<YOUR PATH>\DocFile.xml" #>  

    <#  //Uncomment this line if you want to see the generated transformation class. #>  
    <#  //System.Diagnostics.Debugger.Break(); #>  

    <#  //This will use the results of the directive processor. #>  
    <#  //The directive processor has read the XML and stored it in Document0. #>  
    <#  
        XmlNode node = Document0.DocumentElement.SelectSingleNode("members");  

        foreach (XmlNode member in node.ChildNodes)  
        {  
            XmlNode name = member.Attributes.GetNamedItem("name");  
            WriteLine("{0,7}:  {1}", "Name", name.Value);  

            foreach (XmlNode comment in member.ChildNodes)  
            {  
                WriteLine("{0,7}:  {1}", comment.Name, comment.InnerText);  
            }  
            WriteLine("");  
        }  
    #>  

    <#  //You can call the directive processor again and pass it a different file. #>  
    <# //@ CoolDirective Processor="CustomDirectiveProcessor" FileName="<YOUR PATH>\<Your Second File>" #>  

    <#  //To use the results of the second directive call, use Document1. #>  
    <#  
        //XmlNode node2 = Document1.DocumentElement.SelectSingleNode("members");  

        //...  
    #>  
    ```  

    ```vb  
    <#@ assembly name="System.Xml" #>  
    <#@ template debug="true" language="vb" #>  
    <#@ output extension=".txt" #>  

    <#  'This will call the custom directive processor. #>  
    <#@ CoolDirective Processor="CustomDirectiveProcessor" FileName="<YOUR PATH>\DocFile.xml" #>  

    <#  'Uncomment this line if you want to see the generated transformation class. #>  
    <#  'System.Diagnostics.Debugger.Break() #>  

    <#  'This will use the results of the directive processor. #>  
    <#  'The directive processor has read the XML and stored it in Document0. #>  
    <#  
        Dim node as XmlNode = Document0.DocumentElement.SelectSingleNode("members")  

        Dim member As XmlNode  
        For Each member In node.ChildNodes  

            Dim name As XmlNode = member.Attributes.GetNamedItem("name")  
            WriteLine("{0,7}:  {1}", "Name", name.Value)  

            Dim comment As XmlNode  
            For Each comment In member.ChildNodes  
                WriteLine("{0,7}:  {1}", comment.Name, comment.InnerText)  
            Next  

            WriteLine("")  
        Next  
    #>  

    <#  'You can call the directive processor again and pass it a different file. #>  
    <# '@ CoolDirective Processor="CustomDirectiveProcessor" FileName="<YOUR PATH>\DocFileTwo.xml" #>  

    <#  'To use the results of the second directive call, use Document1. #>  
    <#  
        'node = Document1.DocumentElement.SelectSingleNode("members")  

        '...  
    #>  
    ```  

    > [!NOTE]
    >  この例では、`Processor` パラメーターの値は `CustomDirectiveProcessor` です。 `Processor` パラメーターの値は、プロセッサのレジストリ キーの名前に一致する必要があります。  

5.  **[ファイル]** メニューの **[すべてを保存]** をクリックします。  

#### <a name="to-test-the-directive-processor"></a>ディレクティブ プロセッサをテストするには  

1.  **ソリューション エクスプ ローラー**で TestDP.tt を右クリックし、**[カスタム ツールの実行]** をクリックします。  

     [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 、ユーザーに TestDP.txt が表示されません**ソリューション エクスプ ローラー**既定。 プロジェクトに割り当てられているすべてのファイルを表示するために、**[プロジェクト]** メニューを開き、**[すべてのファイルを表示]** をクリックします。  

2.  **ソリューション エクスプ ローラー**の中で、TestDP.txt ノードを展開し、エディターでそれを開くために TestDP.txt をダブルクリックします。  

     生成されたテキスト出力が表示されます。 出力の内容は次のようになります。  

    ```  
       Name:  T:SomeClass  
    summary:  Class level summary documentation goes here.  
    remarks:  Longer comments can be associated with a type or member through the remarks tag  

       Name:  F:SomeClass.m_Name  
    summary:  Store for the name property  

       Name:  M:SomeClass.#ctor  
    summary:  The class constructor.  

       Name:  M:SomeClass.SomeMethod(System.String)  
    summary:  Description for SomeMethod.  
      param:  Parameter description for s goes here  
    seealso:  You can use the cref attribute on any tag to reference a type or member and the compiler will check that the reference exists.  

       Name:  M:SomeClass.SomeOtherMethod  
    summary:  Some other method.  
    returns:  Return results are described through the returns tag.  
    seealso:  Notice the use of the cref attribute to reference a specific method  

       Name:  M:SomeClass.Main(System.String[])  
    summary:  The entry point for the application.  
      param:  A list of command line arguments  

       Name:  P:SomeClass.Name  
    summary:  Name property  
      value:  A value tag is used to describe the property value  
    ```  

## <a name="adding-html-to-generated-text"></a>生成されたテキストへの HTML の追加  
 カスタム ディレクティブ プロセッサをテストした後は、生成されたテキストに HTML を追加できます。  

#### <a name="to-add-html-to-the-generated-text"></a>生成されたテキストに HTML を追加するには  

1.  TestDP.tt 内のコードを次のコードに置き換えます。 HTML は強調表示されています。 文字列を置換することを確認`YOUR PATH`DocFile.xml ファイルへのパス。  

    > [!NOTE]
    >  追加された開くタグ (\<#) および閉じるタグ (#>) は HTML タグからステートメントのコードを分離しています。  

    ```csharp  
    <#@ assembly name="System.Xml" #>  
    <#@ template debug="true" #>  
    <#@ output extension=".htm" #>  

    <#  //this will call the custom directive processor #>  
    <#@ CoolDirective Processor="CustomDirectiveProcessor" FileName="<YOUR PATH>\DocFile.xml" #>  

    <#  //uncomment this line if you want to see the generated transformation class #>  
    <#  //System.Diagnostics.Debugger.Break(); #>  

    <html><body>  

    <#  //this will use the results of the directive processor #>  
    <#  //the directive processor has read the XML and stored it in Document0#>  
    <#  
        XmlNode node = Document0.DocumentElement.SelectSingleNode("members");  

        foreach (XmlNode member in node.ChildNodes)  
        {  
    #>  
    <h3>  
    <#      
            XmlNode name = member.Attributes.GetNamedItem("name");  
            WriteLine("{0,7}:  {1}", "Name", name.Value);  
    #>  
    </h3>  
    <#  
            foreach (XmlNode comment in member.ChildNodes)  
            {  
                WriteLine("{0,7}:  {1}", comment.Name, comment.InnerText);  
    #>  
    <br/>  
    <#  
            }  
        }  
    #>  
    </body></html>  
    ```  

    ```vb  
    <#@ assembly name="System.Xml" #>  
    <#@ template debug="true" language="vb" #>  
    <#@ output extension=".htm" #>  

    <#  'this will call the custom directive processor #>  
    <#@ CoolDirective Processor="CustomDirectiveProcessor" FileName="<YOUR PATH>\DocFile.xml" #>  

    <#  'uncomment this line if you want to see the generated transformation class #>  
    <#  'System.Diagnostics.Debugger.Break() #>  

    <html><body>  

    <#  'this will use the results of the directive processor #>  
    <#  'the directive processor has read the XML and stored it in Document0#>  
    <#  
        Dim node as XmlNode = Document0.DocumentElement.SelectSingleNode("members")  

        Dim member As XmlNode  
        For Each member In node.ChildNodes  
    #>  
    <h3>  
    <#      
            Dim name As XmlNode = member.Attributes.GetNamedItem("name")  
            WriteLine("{0,7}:  {1}", "Name", name.Value)  
    #>  
    </h3>  
    <#  
            Dim comment As XmlNode  
            For Each comment In member.ChildNodes  
                WriteLine("{0,7}:  {1}", comment.Name, comment.InnerText)  
    #>  
    <br/>  
    <#  
            Next  
        Next  
    #>  
    </body></html>  
    ```  

2.  **[ファイル]** メニューの **[TestDP.txt の保存]** をクリックします。  

3.  出力をブラウザーで表示するには、**ソリューション エクスプローラー**で TestDP.htm を右クリックし、**[ブラウザーで表示する]** をクリックします。  

     HTML 形式が適用される点を除き、出力は元のテキストと同じです。 各項目名は太字で表示されます。
