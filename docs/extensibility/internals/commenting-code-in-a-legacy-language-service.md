---
title: 従来の言語サービスでのコードのコメント | Microsoft Docs
description: Visual Studio の従来の言語サービスでのコードのコメントのサポートを提供する、マネージド パッケージ フレームワーク (MPF) クラスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- comments, supporting in language services [managed package framework]
- language services [managed package framework], commenting code
ms.assetid: 9600d6f0-e2b6-4fe0-b935-fb32affb97a4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c712f1458aa182abcf9e10bee6c6cf90e11b194d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057105"
---
# <a name="comment-code-in-a-legacy-language-service"></a>従来の言語サービスでのコードのコメント
プログラミング言語では、通常、コードに注釈を付けたり、コメントを付けたりするための手段が提供されます。 コメントは、コードに関する追加情報を提供するテキストのセクションですが、コンパイル時または解釈時には無視されます。

 マネージド パッケージ フレームワーク (MPF) クラスは、選択したテキストのコメントとコメント解除のサポートを提供します。

## <a name="comment-styles"></a>コメントのスタイル
コメントには、次の 2 つの一般的なスタイルがあります。

1. 行コメントでは、コメントは 1 行にあります。

2. ブロック コメントでは、コメントには複数の行を含めることができます。

行 コメントには、単一の開始文字 (または複数の文字) がありますが、ブロック コメントには開始文字と終了文字の両方があります。 たとえば、C# では、行コメントは `//` で始まり、ブロック コメントは `/*` で始まり、`*/` で終わります。

ユーザーが **[編集]**  >  **[詳細]** メニューから **[選択範囲のコメント]** コマンドを選択すると、 コマンドは <xref:Microsoft.VisualStudio.Package.Source> クラスの <xref:Microsoft.VisualStudio.Package.Source.CommentSpan%2A> メソッドにルーティングされます。 ユーザーが **[選択のコメント解除]** コマンドを選択すると、コマンドは <xref:Microsoft.VisualStudio.Package.Source.UncommentSpan%2A> メソッドにルーティングされます。

## <a name="support-code-comments"></a>コードのコメントのサポート
 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> の `EnableCommenting` 名前付きパラメーターを使用して、言語サービスでコードのコメントをサポートすることができます。 これにより、<xref:Microsoft.VisualStudio.Package.LanguagePreferences> クラスの <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCommenting%2A> プロパティが設定されます。 言語サービス機能の設定の詳細については、[従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)に関するページを参照してください。

 また、<xref:Microsoft.VisualStudio.Package.Source.GetCommentFormat%2A> メソッドをオーバーライドして、言語のコメント文字を含む <xref:Microsoft.VisualStudio.Package.CommentInfo> 構造体を返す必要があります。 C# スタイルの行コメント文字が既定です。

### <a name="example"></a>例
 <xref:Microsoft.VisualStudio.Package.Source.GetCommentFormat%2A> メソッドの実装例を示します。

```csharp
using Microsoft.VisualStudio.Package;

namespace MyLanguagePackage
{
    class MySource : Source
    {
        public override CommentInfo GetCommentFormat() {
            CommentInfo info = new CommentInfo();
            info.LineStart       = "//";
            info.BlockStart      = "/*";
            info.BlockEnd        = "*/";
            info.UseLineComments = true;
            return info;
        }
    }
}
```

## <a name="see-also"></a>関連項目
- [従来の言語サービスの機能](../../extensibility/internals/legacy-language-service-features1.md)
- [従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)
