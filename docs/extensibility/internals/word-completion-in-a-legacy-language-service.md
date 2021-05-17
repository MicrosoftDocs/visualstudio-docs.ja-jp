---
title: 従来の言語サービスでの単語補完 | Microsoft Docs
description: Visual Studio SDK の従来の言語サービスでは、単語補完をサポートできます。 VSPackage で従来の言語サービスを実装する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], IntelliSense Complete Word
- IntelliSense, Complete Word
- Complete Word
ms.assetid: 0ace5ac3-f9e1-4e6d-add4-42967b1f96a6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 360778e4dbc89130e8a533640fefb188047fe8ca
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074081"
---
# <a name="word-completion-in-a-legacy-language-service"></a>従来の言語サービスでの単語補完
単語補完では、部分的に入力された単語の不足している文字を補います。 補完候補が 1 つしかない場合は、補完文字が入力されると、その単語が完成します。 単語の一部が複数の候補に一致する場合は、補完候補の一覧が表示されます。 補完文字は、識別子に使用されない任意の文字にすることができます。

 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能の新しい実装方法では MEF 拡張機能が使用されます。 詳細については、「[エディターと言語サービスの拡張](../../extensibility/extending-the-editor-and-language-services.md)」を参照してください。

> [!NOTE]
> 新しいエディターの API をできるだけ早く使い始めることをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

## <a name="implementation-steps"></a>実装手順

1. ユーザーが **IntelliSense** メニューから **[入力候補]** を選択すると、<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> コマンドが言語サービスに送信されます。

2. <xref:Microsoft.VisualStudio.Package.ViewFilter> クラスでは、コマンドをキャッチし、解析理由 <xref:Microsoft.VisualStudio.Package.ParseReason> で <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> メソッドを呼び出します。

3. 次に、<xref:Microsoft.VisualStudio.Package.Source> クラスでは <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> メソッドを呼び出して単語補完候補の一覧を取得し、<xref:Microsoft.VisualStudio.Package.CompletionSet> クラスを使用してツール ヒントの一覧に単語を表示します。

    一致する単語が 1 つしかない場合、<xref:Microsoft.VisualStudio.Package.Source> クラスでは単語を補完します。

   また、識別子の最初の文字が入力されたときにスキャナーからトリガー値 <xref:Microsoft.VisualStudio.Package.TokenTriggers> が返される場合、<xref:Microsoft.VisualStudio.Package.Source> クラスではこれを検出し、解析理由 <xref:Microsoft.VisualStudio.Package.ParseReason> で <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> メソッドを呼び出します。 この場合、パーサーではメンバー選択文字の存在を検出し、メンバーの一覧を提供する必要があります。

## <a name="enabling-support-for-the-complete-word"></a>入力候補のサポートを有効にする
 単語補完のサポートを有効にするには、言語パッケージに関連付けられた <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> ユーザー属性に渡される `CodeSense` 名前付きパラメーターを設定します。 これにより、<xref:Microsoft.VisualStudio.Package.LanguagePreferences> クラスの <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A> プロパティが設定されます。

 単語補完を操作するには、解析理由値 <xref:Microsoft.VisualStudio.Package.ParseReason> に応じて、パーサーから宣言の一覧が返される必要があります。

## <a name="implementing-complete-word-in-the-parsesource-method"></a>ParseSource メソッドに入力候補を実装する
 単語補完の場合、<xref:Microsoft.VisualStudio.Package.Source> クラスでは <xref:Microsoft.VisualStudio.Package.AuthoringScope> クラスの <xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDeclarations%2A> メソッドを呼び出して、単語の一致候補の一覧を取得します。 <xref:Microsoft.VisualStudio.Package.Declarations> クラスから派生したクラスでこの一覧を実装する必要があります。 実装する必要のあるメソッドの詳細については、<xref:Microsoft.VisualStudio.Package.Declarations> クラスを参照してください。

 一覧に 1 つの単語だけが含まれている場合、<xref:Microsoft.VisualStudio.Package.Source> クラスでは単語の一部の代わりにその単語を自動的に挿入します。 一覧に複数の単語が含まれている場合、<xref:Microsoft.VisualStudio.Package.Source> クラスではユーザーが適切な選択肢を選択できるツール ヒントの一覧を提示します。

 「[従来の言語サービスでのメンバー補完](../../extensibility/internals/member-completion-in-a-legacy-language-service.md)」にある <xref:Microsoft.VisualStudio.Package.Declarations> クラス実装の例も参照してください。
