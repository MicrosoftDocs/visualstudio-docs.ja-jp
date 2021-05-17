---
title: 従来の言語サービスのパラメーター ヒント 2 | Microsoft Docs
description: 従来の言語サービスでメソッドが入力されたときにメソッド シグネチャを表示するための IntelliSense パラメーター ヒントの操作をサポートする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense, Parameter Info tool tip
- language services [managed package framework], IntelliSense Parameter Info
- Parameter Info (IntelliSense), supporting in language services [managed package framework]
ms.assetid: a117365d-320d-4bb5-b61d-3e6457b8f6bc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0488c9d6570d9ed127c5b021ddfcf7d74f0dd856
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062929"
---
# <a name="parameter-info-in-a-legacy-language-service-2"></a>従来の言語サービスのパラメーター ヒント 2
IntelliSense パラメーター ヒントは、ユーザーがメソッド パラメーター リストのパラメーター リスト開始文字 (通常は始めかっこ) を入力したときに、メソッドのシグネチャを表示するツールヒントです。 各パラメーターが入力され、パラメーターの区切り記号 (通常はコンマ) が入力されると、ツールヒントが更新され、次のパラメーターが太字で表示されます。

 Managed Package Framework (MPF) クラスでは、パラメーター ヒントのツールヒントの管理をサポートします。 パーサーでは、パラメーターの開始文字、パラメーターの次の文字、パラメーターの終了文字を検出する必要があり、メソッド シグネチャとそれに関連付けられたパラメーターのリストを提供する必要があります。

 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能の新しい実装方法では MEF 拡張機能が使用されます。 詳細については、「[エディターと言語サービスの拡張](../../extensibility/extending-the-editor-and-language-services.md)」を参照してください。

> [!NOTE]
> 新しいエディターの API をできるだけ早く使い始めることをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

## <a name="implementation"></a>実装
 パーサーでは、パラメーター リストの開始文字 (多くの場合、始めかっこ) を検出したときに、トリガー値 <xref:Microsoft.VisualStudio.Package.TokenTriggers> を設定する必要があります。 パラメーターの区切り記号 (多くの場合、コンマ) を検出したときに、<xref:Microsoft.VisualStudio.Package.TokenTriggers> トリガーを設定する必要があります。 これにより、パラメーター ヒントのツールヒントが更新され、次のパラメーターが太字で表示されます。 パーサーは、パラメーター リストの終了文字 (多くの場合、終わりかっこ) を検出したときに、トリガー値 <xref:Microsoft.VisualStudio.Package.TokenTriggers> を設定する必要があります。

 <xref:Microsoft.VisualStudio.Package.TokenTriggers> トリガー値は、<xref:Microsoft.VisualStudio.Package.Source.MethodTip%2A> メソッドの呼び出しを開始します。このメソッドは、<xref:Microsoft.VisualStudio.Package.ParseReason> を解析の理由として、<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> メソッド パーサーを呼び出します。 パーサーで、パラメーター リストの開始文字より前の識別子が認識されたメソッド名であると判断されると、<xref:Microsoft.VisualStudio.Package.AuthoringScope> オブジェクト内の一致するメソッド シグネチャのリストが返されます。 メソッド シグネチャが見つかった場合は、パラメーター ヒントのツールヒントが表示され、リストの最初のシグネチャが示されます。 このツールヒントは、さらに多くのシグネチャが入力されたときに更新されます。 パラメーター リストの終了文字が入力されると、パラメーター ヒントのツールヒントがビューから削除されます。

> [!NOTE]
> 確実にパラメーター ヒントのツールヒントが適切に書式設定されるようにするには、<xref:Microsoft.VisualStudio.Package.Methods> クラスのプロパティをオーバーライドして適切な文字を指定する必要があります。 基底の <xref:Microsoft.VisualStudio.Package.Methods> クラスでは、C# スタイルのメソッド シグネチャを前提としています。 これを実行する方法の詳細については、<xref:Microsoft.VisualStudio.Package.Methods> クラスを参照してください。

## <a name="enabling-support-for-the-parameter-info"></a>パラメーター ヒントのサポートの有効化
 パラメーター ヒントのツールヒントをサポートするには、<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> の `ShowCompletion` 名前付きパラメーターを `true` に設定する必要があります。 言語サービスでは、<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A> プロパティからこのレジストリ エントリの値を読み取ります。

 また、パラメーター ヒントのツールヒントを表示するには、<xref:Microsoft.VisualStudio.Package.LanguagePreferences.ParameterInformation%2A> プロパティを `true` に設定する必要があります。

### <a name="example"></a>例
 パラメーター リスト文字を検出し、適切なトリガーを設定する簡単な例を次に示します。 この例は、説明のみを目的としています。 テキスト行でトークンを識別して返すメソッド `GetNextToken` がスキャナーに含まれていることを想定しています。 このコード例では、単純に、正しい種類の文字が表示されるたびにトリガーを設定します。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestScanner : IScanner
    {
        private Lexer lex;
        private const char parameterListStartChar = '(';
        private const char parameterListEndChar   = ')';
        private const char parameterNextChar      = ',';

        public bool ScanTokenAndProvideInfoAboutIt(TokenInfo tokenInfo,
                                                   ref int state)
        {
            bool foundToken = false
            string token = lex.GetNextToken();
            if (token != null)
            {
                foundToken = true;
                char c = token[0];
                if (Char.IsPunctuation(c))
                {
                    tokenInfo.Type = TokenType.Operator;
                    tokenInfo.Color = TokenColor.Keyword;
                    tokenInfo.EndIndex = index;

                    if (c == parameterListStartChar)
                    {
                        tokenInfo.Trigger |= TokenTriggers.ParameterStart;
                    }
                    else if (c == parameterListNextChar)
                    {
                        tokenInfo.Trigger |= TokenTriggers.ParameterNext;
                    else if (c == parameterListEndChar)
                    {
                        tokenInfo.Trigger |= TokenTriggers.ParameterEnd;
                    }
                }
            return foundToken;
        }
    }
}
```

## <a name="supporting-the-parameter-info-tooltip-in-the-parser"></a>パーサーでのパラメーター ヒントのツールヒントのサポート
 <xref:Microsoft.VisualStudio.Package.Source> クラスでは、パラメーター ヒントのツールヒントが表示され更新されるときに、<xref:Microsoft.VisualStudio.Package.AuthoringScope> および <xref:Microsoft.VisualStudio.Package.AuthoringSink> のクラスのコンテンツについて何からの想定を行います。

- パーサーには、パラメーター リストの開始文字が入力されたときに <xref:Microsoft.VisualStudio.Package.ParseReason> が与えられます。

- <xref:Microsoft.VisualStudio.Package.ParseRequest> オブジェクトに指定された場所は、パラメーター リストの開始文字の直後にあります。 パーサーでは、その位置で利用可能なすべてのメソッド宣言のシグネチャを収集し、お使いのバージョンの <xref:Microsoft.VisualStudio.Package.AuthoringScope> オブジェクトのリストに格納する必要があります。 このリストには、メソッド名、メソッドの型 (または戻り値の型)、使用可能なパラメーターのリストが含まれています。 このリストは、後からパラメーター ヒントのツールヒントにメソッド シグネチャまたはシグネチャを表示するために検索されます。

  パーサーでは、<xref:Microsoft.VisualStudio.Package.ParseRequest> オブジェクトで指定された行を解析して、入力されたメソッドの名前と、ユーザーによるパラメーター入力の進行状況を収集する必要があります。 これを行うには、メソッドの名前を <xref:Microsoft.VisualStudio.Package.AuthoringSink> オブジェクトの <xref:Microsoft.VisualStudio.Package.AuthoringSink.StartName%2A> メソッドに渡し、パラメーター リストの開始文字が解析されたときに <xref:Microsoft.VisualStudio.Package.AuthoringSink.StartParameters%2A> メソッドを呼び出し、パラメーター リストの次の文字が解析されたときに <xref:Microsoft.VisualStudio.Package.AuthoringSink.NextParameter%2A> メソッドを呼び出し、最後にパラメーター リストの終了文字が解析されたときに <xref:Microsoft.VisualStudio.Package.AuthoringSink.EndParameters%2A> メソッドを呼び出します。 これらのメソッド呼び出しの結果は、パラメーター ヒントのツールヒントを適切に更新するために <xref:Microsoft.VisualStudio.Package.Source> クラスで使用されます。

### <a name="example"></a>例
 ユーザーが入力する可能性のあるテキスト行を次に示します。 行の下の数値は、行のその位置でパーサーが行うステップを示します (解析が左から右に進むと想定)。 ここでは、"testfunc" メソッド シグネチャを含むメソッド シグネチャに対して、行より前のすべてが既に解析されていることを前提としています。

```
testfunc("a string",3);
     ^^          ^ ^
     12          3 4
```

 パーサーによって実行されるステップを次に示します。

1. パーサーは、テキスト "testfunc" を使用して <xref:Microsoft.VisualStudio.Package.AuthoringSink.StartName%2A> を呼び出します。

2. パーサーは <xref:Microsoft.VisualStudio.Package.AuthoringSink.StartParameters%2A> を呼び出します。

3. パーサーは <xref:Microsoft.VisualStudio.Package.AuthoringSink.NextParameter%2A> を呼び出します。

4. パーサーは <xref:Microsoft.VisualStudio.Package.AuthoringSink.EndParameters%2A> を呼び出します。
