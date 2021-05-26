---
title: 従来の言語サービスの機能 1 |Microsoft Docs
description: マネージド パッケージ フレームワーク (MPF) 言語サービスでサポートされている Visual Studio の機能について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework]
ms.assetid: a646e4f0-767d-4cd1-8e1a-9a2aa210a1b7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2bb5169eeb53aa16d0827cdf50cb50d0db34d996
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074519"
---
# <a name="legacy-language-service-features-1"></a>従来の言語サービスの機能 1
マネージド パッケージ フレームワーク (MPF) 言語サービスでは、構文の強調表示、IntelliSense、ブレークポイントの検証などの 1 つまたは複数の [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の機能をサポートできます。 各機能を他の機能とは独立して実装することもできますが、スキャナーだけを必要とする構文の強調表示を除いて、すべてパーサーとスキャナーが必要です。

## <a name="in-this-section"></a>このセクションの内容
- [従来の言語サービスでのかっこの一致](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)

 言語ペアの一致 (かっこの一致とも呼ばれます) をサポートするために必要な事項について説明します。

- [従来の言語サービスのコメント コード](../../extensibility/internals/commenting-code-in-a-legacy-language-service.md)

 選択したコードのコメントとコメント解除をサポートするために必要な事項について説明します。

- [従来の言語サービスのカスタム ドキュメント プロパティ](../../extensibility/internals/custom-document-properties-in-a-legacy-language-service.md)

 ソース ファイルに埋め込まれているドキュメント プロパティをサポートするために必要な事項について説明します。

- [従来の言語サービスのアウトライン](../../extensibility/internals/outlining-in-a-legacy-language-service.md)

 非表示領域の実装によってアウトラインをサポートするために必要な事項について説明します。

- [従来の言語サービスの再フォーマット コード](../../extensibility/internals/reformatting-code-in-a-legacy-language-service.md)

 コードの再フォーマットをサポートするために必要な事項について説明します。

- [従来の言語サービスでのコード スニペットのサポート](../../extensibility/internals/support-for-code-snippets-in-a-legacy-language-service.md)

 コード スニペット (挿入して編集できるコードのセグメント) をサポートするために必要な事項について説明します。

- [従来の言語サービスのパラメーター ヒント](../../extensibility/internals/parameter-info-in-a-legacy-language-service2.md)

 メソッドが入力されたときにメソッド シグネチャを表示するための IntelliSense パラメーター ヒントの操作をサポートするために必要な事項について説明します。

- [従来の言語サービスのクイック ヒント](../../extensibility/internals/quick-info-in-a-legacy-language-service.md)

 識別子に関する情報を表示するための IntelliSense クイックヒント操作をサポートするために必要な事項について説明します。

- [従来の言語サービスでのメンバー補完](../../extensibility/internals/member-completion-in-a-legacy-language-service.md)

 リストから名前空間のメンバーを選択するための IntelliSense メンバー補完操作をサポートするために必要な事項について説明します。

- [従来の言語サービスでの単語補完](../../extensibility/internals/word-completion-in-a-legacy-language-service.md)

 部分的に入力された単語を補完するための IntelliSense の入力候補操作をサポートするために必要な事項について説明します。

- [従来の言語サービスでの自動変数ウィンドウのサポート](../../extensibility/internals/support-for-the-autos-window-in-a-legacy-language-service.md)

 デバッグ中に言語サービスで **[自動変数]** ウィンドウをサポートするために実行できることについて説明します。

- [従来の言語サービスでのナビゲーション バーのサポート](../../extensibility/internals/support-for-the-navigation-bar-in-a-legacy-language-service.md)

 エディター ビューの上部にある "**ナビゲーション バー**" を使用して、そのビューに表示されるファイル内の任意の種類またはメンバーにすばやく移動できるようにする方法について説明します。

- [従来の言語サービスでの構文の配色変更](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)

 ソース コードの構文の強調表示をサポートするために必要な事項について説明します。

- [従来の言語サービスでのブレークポイントの検証](../../extensibility/internals/validating-breakpoints-in-a-legacy-language-service.md)

 デバッガーの外部でのブレークポイントの検証をサポートするために言語サービスで実行できることについて説明します。

## <a name="related-sections"></a>関連項目
- [従来の言語サービスのパーサーとスキャナー](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)

 マネージド パッケージ フレームワークを使用する言語サービスのすべての機能を実装するために必要なパーサーとスキャナーについて説明します。

- [従来の言語サービスの実装](../../extensibility/internals/implementing-a-legacy-language-service2.md)

 MPF を使用して言語サービスを実装するために必要な事項について説明します。

- [従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)

 MPF ベースの言語サービスを [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に登録するために必要な手順について説明します。

- [IntelliSense の使用](../../ide/using-intellisense.md)

 IntelliSense によって言語参照に簡単にアクセスできるようにする方法について説明します。

- [従来の言語サービスの実装](../../extensibility/internals/implementing-a-legacy-language-service1.md)

 マネージド パッケージ フレームワーク (MPF) を使用して、完全な機能を備えた言語サービスをマネージド コードで実装する方法について説明します。
