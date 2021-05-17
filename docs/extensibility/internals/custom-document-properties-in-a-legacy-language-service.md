---
title: 従来の言語サービスのカスタム ドキュメントのプロパティ
description: 従来の言語サービスの一環として、Visual Studio のプロパティ ウィンドウに表示されるカスタム ドキュメントのプロパティを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- custom document properties, language services [managed package framework]
- document properties, custom
- language services [managed package framework], custom document properties
ms.assetid: cc714a67-b33e-4440-9203-3c90f648bd9c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1e154ba5e6ce4c85f597957b1d6704ca341b3c4d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091150"
---
# <a name="custom-document-properties-in-a-legacy-language-service"></a>従来の言語サービスのカスタム ドキュメントのプロパティ
ドキュメントのプロパティは、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の **[プロパティ]** ウィンドウに表示できます。 プログラミング言語には、通常、個々のソース ファイルに関連付けられたプロパティはありません。 ただし、XML では、エンコード、スキーマ、およびスタイル シートに影響するドキュメントのプロパティがサポートされています。

## <a name="discussion"></a>ディスカッション
 言語にカスタム ドキュメントのプロパティが必要な場合は、<xref:Microsoft.VisualStudio.Package.DocumentProperties> クラスからクラスを派生させ、派生クラスに必要なプロパティを実装する必要があります。

 また、通常、ドキュメントのプロパティはソース ファイル自体に格納されます。 これには、言語サービスでソース ファイルのプロパティ情報を解析して **[プロパティ]** ウィンドウに表示することと、 **[プロパティ]** ウィンドウでドキュメントのプロパティが変更されたときにソース ファイルを更新することが必要です。

## <a name="customize-the-documentproperties-class"></a>DocumentProperties クラスをカスタマイズする
 カスタム ドキュメントのプロパティをサポートするには、<xref:Microsoft.VisualStudio.Package.DocumentProperties> クラスからクラスを派生させ、必要な数だけプロパティを追加する必要があります。 また、ユーザー属性を指定して、それらを **[プロパティ]** ウィンドウの表示で整理する必要もあります。 プロパティに `get` アクセサーしかない場合は、 **[プロパティ]** ウィンドウに読み取り専用として表示されます。 プロパティに `get` および `set` アクセサーの両方がある場合、プロパティは **[プロパティ]** ウィンドウでも更新できます。

### <a name="example"></a>例
 2 つのプロパティ、`Filename` および `Description` が示されている、<xref:Microsoft.VisualStudio.Package.DocumentProperties> から派生したクラスの例を次に示します。 プロパティが更新されると、<xref:Microsoft.VisualStudio.Package.LanguageService> クラスのカスタム メソッドが呼び出されて、プロパティがソース ファイルに書き込まれます。

```csharp
using System.ComponentModel;
using Microsoft.VisualStudio.Package;

namespace TestLanguagePackage
{
    class TestDocumentProperties : DocumentProperties
    {
        private string m_filename;
        private string m_description;

        public TestDocumentProperties(CodeWindowManager mgr)
            : base(mgr)
        {
        }

        // Helper function to initialize this property without
        // going through the FileName property (which does a lot
        // more than we need when the filename is set).
        public void SetFileName(string filename)
        {
            m_filename = filename;
        }

        // Helper function to initialize this property without
        // going through the Description property (which does a lot
        // more than we need when the description is set).
        public void SetDescription(string description)
        {
            m_description = description;
        }

        ////////////////////////////////////////////////////////////
        // The document properties

        [CategoryAttribute("General")]
        [DescriptionAttribute("Name of the file")]
        [DisplayNameAttribute("Filename")]
        public string FileName
        {
            get { return m_filename; }
            set
            {
               if (value != m_filename)
               {
                    m_filename = value;
                    SetPropertyValue("Filename", m_filename);
               }
            }
        }

        [CategoryAttribute("General")]
        [DescriptionAttribute("Description of the file")]
        [DisplayNameAttribute("Description")]
        public string Description
        {
            get { return m_description; }
            set
            {
                if (value != m_description)
                {
                    m_description = value;
                    SetPropertyValue("Description", m_description);
                }
            }
        }

        ///////////////////////////////////////////////////////////
        // Private methods.

        private void SetPropertyValue(string propertyName, string propertyValue)
        {
            Source src = this.GetSource();
            if (src != null)
            {
                TestLanguageService service = src.LanguageService as TestLanguageService;
                if (service != null)
                {
                    // Set the property in to the source file.
                    service.SetPropertyValue(src, propertyName, propertyValue);
                }
            }
        }
    }
}
```

## <a name="instantiate-the-custom-documentproperties-class"></a>カスタムの DocumentProperties クラスをインスタンス化する
 カスタム ドキュメントのプロパティのクラスをインスタンス化するには、ご使用のバージョンの <xref:Microsoft.VisualStudio.Package.LanguageService> クラスで <xref:Microsoft.VisualStudio.Package.LanguageService.CreateDocumentProperties%2A> メソッドをオーバーライドして、<xref:Microsoft.VisualStudio.Package.DocumentProperties> クラスの単一インスタンスを返す必要があります。

### <a name="example"></a>例

```csharp
using System.ComponentModel;
using Microsoft.VisualStudio.Package;

namespace TestLanguagePackage
{
    class TestLanguageService : LanguageService
    {
        private TestDocumentProperties m_documentProperties;

        public override DocumentProperties CreateDocumentProperties(CodeWindowManager mgr)
        {
            if (m_documentProperties == null)
            {
                m_documentProperties = new TestDocumentProperties(mgr);
            }
            return m_documentProperties;
        }
    }
}
```

## <a name="properties-in-the-source-file"></a>ソース ファイル内のプロパティ
 通常、ドキュメントのプロパティはソース ファイルに固有であるため、値はソース ファイル自体に格納されます。 これには、これらのプロパティを定義するために、言語パーサーまたはスキャナーからのサポートが必要です。 たとえば、XML ドキュメントのプロパティは、ルート ノードに格納されます。 ルート ノードの値は、 **[プロパティ]** ウィンドウの値が変更されると変更され、ルート ノードはエディターで更新されます。

### <a name="example"></a>例
 この例では、次のように、ソース ファイルの最初の 2 行に、特殊なコメント ヘッダーに埋め込まれたプロパティ `Filename` および `Description` を格納します。

```
//!Filename = file.testext
//!Description = A sample file
```

 この例では、ソース ファイルの最初の 2 行からドキュメントのプロパティを取得して設定するために必要な 2 つのメソッドと、ユーザーがソース ファイルを直接変更した場合にプロパティがどのように更新されるかを示しています。 ここで示した例の `SetPropertyValue` メソッドは、「*DocumentProperties クラスをカスタマイズする*」セクションで示すように、`TestDocumentProperties` クラスから呼び出されたものと同じです。

 この例では、スキャナーを使用して、最初の 2 行のトークンの種類を判別します。 この例は、説明のみを目的としています。 この状況に対するより一般的なアプローチは、ソース ファイルをいわゆる解析ツリーに解析することです。このツリーの各ノードには、特定のトークンに関する情報が含まれています。 ルート ノードには、ドキュメントのプロパティが含まれています。

```csharp
using System.ComponentModel;
using Microsoft.VisualStudio.Package;

namespace TestLanguagePackage
{
    // TokenType.Comment is the last item in that enumeration.
    public enum TestTokenTypes
    {
        DocPropertyLine = TokenType.Comment + 1,
        DocPropertyName,
        DocPropertyAssign,
        DocPropertyValue
    }

    class TestLanguageService : LanguageService
    {
        // Search this many lines from the beginning for properties.
        private static int maxLinesToSearch = 2;

        private TestDocumentProperties m_documentProperties;

        // Called whenever a full parsing operation has completed.
        public override void OnParseComplete(ParseRequest req)
        {
            if (m_documentProperties != null)
            {
                Source src = GetSource(req.View);
                if (src != null)
                {
                    string value = GetPropertyValue(src, "Filename");
                    m_documentProperties.SetFileName(value);

                    value = GetPropertyValue(src, "Description");
                    m_documentProperties.SetDescription(value);

                    // Update the Properties Window.
                    m_documentProperties.Refresh();
                }
            }
        }

        // Retrieves the specified property value from the given source.
        public string GetPropertyValue(Source src, string propertyName)
        {
            string propertyValue = "";

            if (src != null)
            {
                IVsTextColorState colorState = src.ColorState;
                if (colorState != null)
                {
                    string      line;
                    TokenInfo[] lineInfo = null;
                    int         i;

                    for (i = 0; i < maxLinesToSearch; i++)
                    {
                        line     = src.GetLine(i);
                        lineInfo = src.GetColorizer().GetLineInfo(
                                                        src.GetTextLines(),
                                                        i,
                                                        colorState);
                        if (lineInfo == null)
                        {
                            continue;
                        }
                        if (lineInfo[0].Type != (TokenType)TestTokenTypes.DocPropertyLine)
                        {
                            // Not a property line.
                            continue;
                        }
                        TokenInfo valueInfo = new TokenInfo();
                        int tokenIndex = -1;
                        for (tokenIndex = 0;
                             tokenIndex < lineInfo.Length;
                             tokenIndex++)
                        {
                            if (lineInfo[tokenIndex].Type == (TokenType)TestTokenTypes.DocPropertyName)
                            {
                                break;
                            }
                        }
                        if (tokenIndex >= lineInfo.Length)
                        {
                            // No property name on the line.
                            continue;
                        }
                        string name = src.GetText(i,
                                                  lineInfo[tokenIndex].StartIndex,
                                                  i,
                                                  lineInfo[tokenIndex].EndIndex + 1);
                        if (name != null)
                        {
                            if (String.Compare(name, propertyName, true) == 0)
                            {
                                for ( ;
                                     tokenIndex < lineInfo.Length;
                                     tokenIndex++)
                                {
                                    if (lineInfo[tokenIndex].Type == (TokenType)TestTokenTypes.DocPropertyValue)
                                    {
                                        break;
                                    }
                                }
                                if (tokenIndex < lineInfo.Length)
                                {
                                    propertyValue = src.GetText(i,
                                                          lineInfo[tokenIndex].StartIndex,
                                                          i,
                                                          lineInfo[tokenIndex].EndIndex + 1);
                                }
                                break;
                            }
                        }
                    }
                }
            }
            return propertyValue;
        }

        // Sets the specified property into the given source file.
        // Called from the TestDocumentProperties class.
        public void SetPropertyValue(Source src, string propertyName, string propertyValue)
        {
            string newLine;

            if (propertyName == null || propertyName == "")
            {
                // No property name, so nothing to do
                return;
            }
            if (propertyValue == null)
            {
                propertyValue = "";
            }
            // This is the line to be inserted.
            newLine = String.Format("//!{0} = {1}", propertyName, propertyValue);

            // First, find the line on which the property belongs.
            // If line is found, replace it.
            // Otherwise, insert the line at the beginning of the file.
            if (src != null)
            {
                IVsTextColorState colorState = src.ColorState;
                if (colorState != null)
                {
                    int         lineNumber = -1;
                    string      line;
                    TokenInfo[] lineInfo   = null;
                    int         i;

                    for (i = 0; i < maxLinesToSearch; i++)
                    {
                        line     = src.GetLine(i);
                        lineInfo = src.GetColorizer().GetLineInfo(
                                                        src.GetTextLines(),
                                                        i,
                                                        colorState);
                        if (lineInfo == null)
                        {
                            continue;
                        }
                        if (lineInfo[0].Type != (TokenType)TestTokenTypes.DocPropertyLine)
                        {
                            // Not a property line
                            continue;
                        }
                        TokenInfo valueInfo = new TokenInfo();
                        int tokenIndex = -1;
                        for (tokenIndex = 0;
                             tokenIndex < lineInfo.Length;
                             tokenIndex++)
                        {
                            if (lineInfo[tokenIndex].Type == (TokenType)TestTokenTypes.DocPropertyName)
                            {
                                break;
                            }
                        }
                        if (tokenIndex >= lineInfo.Length)
                        {
                            // No property name on the line.
                            continue;
                        }
                        string name = src.GetText(i,
                                                  lineInfo[tokenIndex].StartIndex,
                                                  i,
                                                  lineInfo[tokenIndex].EndIndex + 1);
                        if (name != null)
                        {
                            if (String.Compare(name, propertyName, true) == 0)
                            {
                                lineNumber = i;
                                break;
                            }
                        }
                    }

                    // Set up an undo context that also handles the insert/replace.
                    EditArray editArray = new EditArray(src,
                                                        true,
                                                        "Update Property");
                    if (editArray != null)
                    {
                        TextSpan span = new TextSpan();
                        if (lineNumber != -1)
                        {
                            // Replace line.
                            int lineLength = 0;
                            src.GetTextLines().GetLengthOfLine(lineNumber,
                                                               out lineLength);
                            span.iStartLine  = lineNumber;
                            span.iStartIndex = 0;
                            span.iEndLine    = lineNumber;
                            span.iEndIndex   = lineLength;
                        }
                        else
                        {
                            // Insert new line.
                            span.iStartLine  = 0;
                            span.iStartIndex = 0;
                            span.iEndLine    = 0;
                            span.iEndIndex   = 0;
                            newLine += "\n";
                        }
                        editArray.Add(new EditSpan(span, newLine));
                        editArray.ApplyEdits();
                    }
                }
            }
        }
    }
}
```

## <a name="see-also"></a>関連項目
- [従来の言語サービスの機能](../../extensibility/internals/legacy-language-service-features1.md)
