---
title: usings の生成
ms.date: 02/19/2019
ms.topic: reference
author: kendrahavens
ms.author: kehavens
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 0ce1b620a6d8aba7e4aea767745891dff6d9f869
ms.sourcegitcommit: cd91a8a4f6086cda9ba6948be25864fc7d6b8e44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2019
ms.locfileid: "59537505"
---
# <a name="generate-usings-in-visual-studio"></a>Visual Studio で usings を生成する

このコード生成は以下に適用されます。

- C#

**概要:** コピーして貼り付けたコードに対して、必要なインポートまたは [using ステートメント](/dotnet/csharp/language-reference/keywords/using-statement)をすぐに追加できます。

**条件:** プロジェクトや他のソース内のさまざまな場所からコードをコピーして、それを新しいコードに貼り付けることは、一般的な方法です。 このクイック アクションによって、コピーして貼り付けたコードで不足しているインポート ステートメントが検索され、それらを追加するように求められます。

**理由:** クイック アクションにより必要なインポートが自動的に追加されるため、コードに必要な `using` ステートメントを手動でコピーする必要はありません。

## <a name="generate-usings-refactoring"></a>usings リファクタリングの生成

1. 必要な `using` ステートメントを含めずに、ファイルからコードをコピーして新しいものに貼り付けます。 その結果として発生するエラーには、コードの修正が付随します。これにより足りない `using` ステートメントが追加されます。

    > [!NOTE] 
    > この提案は **[ツール] > [オプション] > [テキスト エディター] > [C#] > [詳細] > [ディレクティブを使用する]** で有効にする必要があります。

2. Ctrl + . キーを選択します **[クイック アクションとリファクタリング]** メニューが開きます。

    ![usings の生成](media/generate-using-codefix.png)

3. **[using \<your reference\>]\(using <参照>)** を選択し、足りない参照を追加します。

    ![usings 生成の結果](media/generate-using-result.png)

## <a name="see-also"></a>関連項目

- [コード生成](../code-generation-in-visual-studio.md)
- [変更のプレビュー](../../ide/preview-changes.md)
- [.NET 開発者向けのヒント](../../ide/visual-studio-2017-for-dotnet-developers.md)
