---
title: 従来の言語サービスでのコードの再フォーマット | Microsoft Docs
description: Visual Studio の従来の言語サービスでのソース コードの再フォーマットのサポートを有効にする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- reformatting code, supporting in language services [managed package framework]
- language services [managed package framework], reformatting code
ms.assetid: 08bb3375-8fef-4f4e-9efa-0d7333bab0eb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e8dc10e4def3e4725bb4f64041cdb17146b9d84d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060862"
---
# <a name="reformatting-code-in-a-legacy-language-service"></a>従来の言語サービスの再フォーマット コード

[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、インデントと空白の使用を正規化することによって、ソース コードを再フォーマットできます。 これには、各行の先頭へのスペースまたはタブの挿入または削除、行間への新しい行の追加、スペースのタブへの置き換え、またはタブのスペースへの置き換えを含めることができます。

> [!NOTE]
> 改行文字を挿入または削除すると、ブレークポイントやブックマークなどのマーカーに影響を与える場合がありますが、スペースやタブの追加または削除はマーカーに影響を与えません。

ユーザーは、 **[編集]** メニューの **[詳細]** メニューから **[選択範囲のフォーマット]** または **[ドキュメントのフォーマット]** を選択することによって、再フォーマット操作を開始できます。 また、コード スニペットまたは特定の文字が挿入されたときに、再フォーマット操作をトリガーすることもできます。 たとえば、C# で右中かっこを入力すると、対応する左中かっこと右中かっこの間のすべての文字が適切なレベルに自動的にインデントされます。

[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] が言語サービスに **[選択範囲のフォーマット]** または **[ドキュメントのフォーマット]** コマンドを送信すると、<xref:Microsoft.VisualStudio.Package.ViewFilter> クラスは <xref:Microsoft.VisualStudio.Package.Source> クラスの <xref:Microsoft.VisualStudio.Package.Source.ReformatSpan%2A> メソッドを呼び出します。 フォーマットをサポートするには、<xref:Microsoft.VisualStudio.Package.Source.ReformatSpan%2A> メソッドをオーバーライドし、独自のフォーマット コードを指定する必要があります。

## <a name="enabling-support-for-reformatting"></a>再フォーマットのサポートの有効化

フォーマットをサポートするには、VSPackage を登録するときに、<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> の `EnableFormatSelection` パラメーターを `true` に設定する必要があります。 これにより、<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableFormatSelection%2A> プロパティが `true` に設定されます。 <xref:Microsoft.VisualStudio.Package.ViewFilter.CanReformat%2A> メソッドは、このプロパティの値を返します。 true を返した場合、<xref:Microsoft.VisualStudio.Package.ViewFilter> クラスは <xref:Microsoft.VisualStudio.Package.Source.ReformatSpan%2A> を呼び出します。

## <a name="implementing-reformatting"></a>再フォーマットの実装

再フォーマットを実装するには、<xref:Microsoft.VisualStudio.Package.Source> クラスからクラスを派生させ、<xref:Microsoft.VisualStudio.Package.Source.ReformatSpan%2A> メソッドをオーバーライドする必要があります。 <xref:Microsoft.VisualStudio.TextManager.Interop.TextSpan> オブジェクトは、フォーマットするスパンを記述し、<xref:Microsoft.VisualStudio.Package.EditArray> オブジェクトは、そのスパンに加えられた編集を保持します。 このスパンがドキュメント全体である場合があることに注意してください。 ただし、スパンに加えられた変更は複数存在する可能性があるため、すべての変更を 1 つのアクションで元に戻せる必要があります。 これを行うには、<xref:Microsoft.VisualStudio.Package.CompoundAction> オブジェクトですべての変更をラップします (このトピックの「CompoundAction クラスの使用」セクションを参照)。

### <a name="example"></a>例

次の例では、コンマの後にタブがあるか、またはコンマが行の最後にある場合を除き、選択範囲内のすべてのコンマの後に必ず 1 つのスペースが存在するようにします。 行内の最後のコンマの後にある末尾のスペースは削除されます。 このメソッドが <xref:Microsoft.VisualStudio.Package.Source.ReformatSpan%2A> メソッドからどのように呼び出されるかを確認するには、このトピックの「CompoundAction クラスの使用」セクションを参照してください。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft VisualStudio.TextManager.Interop;

namespace MyLanguagePackage
{
    class MySource : Source
    {
        private void DoFormatting(EditArray mgr, TextSpan span)
        {
            // Make sure there is one space after every comma unless followed
            // by a tab or comma is at end of line.
            IVsTextLines pBuffer = GetTextLines();
            if (pBuffer != null)
            {
                int    startIndex = span.iStartIndex;
                int    endIndex   = 0;
                string line       = "";
                // Loop over all lines in span
                for (int i = span.iStartLine; i <= span.iEndLine; i++)
                {
                    if (i < span.iEndLine)
                    {
                        pBuffer.GetLengthOfLine(i, out endIndex);
                    }
                    else
                    {
                        endIndex = span.iEndIndex;
                    }
                    pBuffer.GetLineText(i, startIndex, i, endIndex, out line);

                    if (line.Length > 0)
                    {
                        int index = 0;
                        // Loop over all commas in line
                        while ((index = line.IndexOf(',', index)) != -1)
                        {
                            int spaceIndex = index + 1;
                            // Determine how many spaces after comma
                            while (spaceIndex < line.Length && line[spaceIndex] == ' ')
                            {
                                ++spaceIndex;
                            }

                            int      spaceCount      = spaceIndex - (index + 1);
                            string   replacementText = " ";
                            bool     fDoEdit         = true;
                            TextSpan editTextSpan    = new TextSpan();

                            editTextSpan.iStartLine  = i;
                            editTextSpan.iEndLine    = i;
                            editTextSpan.iStartIndex = index + 1;

                            if (spaceIndex == line.Length)
                            {
                                if (spaceCount > 0)
                                {
                                    // Delete spaces after a comma at end of line
                                    editTextSpan.iEndIndex = spaceIndex;
                                    replacementText = "";
                                }
                                else
                                {
                                    // Otherwise, do not add spaces if comma is
                                    // at end of line.
                                    fDoEdit = false;
                                }
                            }
                            else if (spaceCount == 0)
                            {
                                if (spaceIndex < line.Length && line[spaceIndex] == '\t')
                                {
                                    // Do not insert space if a tab follows
                                    // a comma.
                                    fDoEdit = false;
                                }
                                else
                                {
                                    // No space after comma so add a space.
                                    editTextSpan.iEndIndex = index + 1;
                                }
                            }
                            else if (spaceCount > 1)
                            {
                                // More than one space after comma, replace
                                // with a single space.
                                editTextSpan.iEndIndex = spaceIndex;
                            }
                            else
                            {
                                // Single space after a comma and not at end
                                // of the line, leave it alone.
                                fDoEdit = false;
                            }
                            if (fDoEdit)
                            {
                                // Add edit operation
                                mgr.Add(new EditSpan(editTextSpan, replacementText));
                            }
                            index = spaceIndex;
                        }
                    }
                    startIndex = 0; // All subsequent lines start at 0
                }
                // Apply all edits
                mgr.ApplyEdits();
            }
        }
    }
}
```

## <a name="using-the-compoundaction-class"></a>CompoundAction クラスの使用

コードのセクションで実行されたすべての再フォーマットを 1 つのアクションで元に戻せる必要があります。 これは、<xref:Microsoft.VisualStudio.Package.CompoundAction> クラスを使用して実現できます。 このクラスでは、テキスト バッファーでの一連の編集操作を 1 つの編集操作にラップします。

### <a name="example"></a>例

<xref:Microsoft.VisualStudio.Package.CompoundAction> クラスを使用する方法の例を次に示します。 `DoFormatting` メソッドの例については、このトピックの「フォーマットのサポートの実装」セクションにある例を参照してください。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft VisualStudio.TextManager.Interop;

namespace MyLanguagePackage
{
    class MySource : Source
    {
        public override void ReformatSpan(EditArray mgr, TextSpan span)
        {
            string description = "Reformat code";
            CompoundAction ca = new CompoundAction(this, description);
            using (ca)
            {
                ca.FlushEditActions();      // Flush any pending edits
                DoFormatting(mgr, span);    // Format the span
            }
        }
    }
}
```

## <a name="see-also"></a>関連項目

- [従来の言語サービスの機能](legacy-language-service-features1.md)
