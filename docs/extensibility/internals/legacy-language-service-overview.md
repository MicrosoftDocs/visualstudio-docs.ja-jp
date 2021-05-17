---
title: 従来の言語サービスの概要 | Microsoft Docs
description: Visual Studio の従来の言語サービスと、マネージド パッケージ フレームワーク (MPF) 言語サービス クラスでサポートされている機能について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], about language services
ms.assetid: bb44e27b-d228-463c-b2cf-cd5c24c7c1b5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 236fc2a2923ffd0829f74ab56a119ff81b29cd7f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061174"
---
# <a name="legacy-language-service-overview"></a>従来の言語サービスの概要
言語サービスでは、特定の [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 機能を実装できるエディター サポートを提供します。 マネージド パッケージ フレームワーク (MPF) 言語サービス クラスでは、頻繁に使用される機能に対する完全なサポートと、その他の機能に対する部分的なサポートを提供します。

## <a name="fully-supported-features-in-the-mpf"></a>MPF で完全にサポートされている機能
 MPF 言語サービス クラスでは、次の機能をサポートしています。

- 構文の強調表示

- アウトライン

- コードのブロックのコメント化

- かっこの一致

- コード スニペット

- カスタム ドキュメントのプロパティ

- IntelliSense のパラメーター ヒント

- IntelliSense のクイック ヒント

- IntelliSense のメンバー補完

- IntelliSense の単語補完

## <a name="partially-supported-features-in-the-mpf"></a>MPF で部分的にサポートされている機能
 MPF では、次の機能について部分的なサポートのみを提供します。 つまり、MPF によって呼び出されるメソッドを実装する必要があります。

- コードの再フォーマット。 再フォーマットを実装するコードはユーザーが提供します。

- 有効なコード スパンの識別によるブレークポイントの検証。 コード スパンを識別するコードはユーザーが提供します。

- 変数を表示するためのデバッガーの **[自動変数]** ウィンドウのサポート。 ウィンドウに何を表示するかを決定するコードはユーザーが提供します。

- 型とメンバーの間をすばやく移動するための **ナビゲーション バー** のサポート。 ユーザーは、**ナビゲーション バー** のコンボ ボックスの一覧を設定するヘルパー クラスを実装して返します。

## <a name="implementation"></a>実装
 言語サービス自体と、使用する言語でサポートする言語サービス機能を実装するには、いくつかの手順を完了する必要があります。 これらの手順については、次の各トピックで説明します。

- [従来の言語サービスの実装](../../extensibility/internals/implementing-a-legacy-language-service2.md)

- [従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)

- [従来の言語サービスでの構文の配色変更](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)

- [従来の言語サービスでのかっこの一致](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)

- [従来の言語サービスのアウトライン](../../extensibility/internals/outlining-in-a-legacy-language-service.md)

- [従来の言語サービスのコメント コード](../../extensibility/internals/commenting-code-in-a-legacy-language-service.md)

- [従来の言語サービスの再フォーマット コード](../../extensibility/internals/reformatting-code-in-a-legacy-language-service.md)

- [従来の言語サービスのカスタム ドキュメント プロパティ](../../extensibility/internals/custom-document-properties-in-a-legacy-language-service.md)

- [従来の言語サービスでのコード スニペットのサポート](../../extensibility/internals/support-for-code-snippets-in-a-legacy-language-service.md)

- [従来の言語サービスでのナビゲーション バーのサポート](../../extensibility/internals/support-for-the-navigation-bar-in-a-legacy-language-service.md)

- [従来の言語サービスでの単語補完](../../extensibility/internals/word-completion-in-a-legacy-language-service.md)

- [従来の言語サービスでのメンバー補完](../../extensibility/internals/member-completion-in-a-legacy-language-service.md)

- [従来の言語サービスのパラメーター ヒント](../../extensibility/internals/parameter-info-in-a-legacy-language-service2.md)

- [従来の言語サービスのクイック ヒント](../../extensibility/internals/quick-info-in-a-legacy-language-service.md)

- [従来の言語サービスでの自動変数ウィンドウのサポート](../../extensibility/internals/support-for-the-autos-window-in-a-legacy-language-service.md)

- [従来の言語サービスでのブレークポイントの検証](../../extensibility/internals/validating-breakpoints-in-a-legacy-language-service.md)

## <a name="see-also"></a>関連項目
- [従来の言語サービスの実装](../../extensibility/internals/implementing-a-legacy-language-service1.md)
- [従来の言語サービスの機能拡張](../../extensibility/internals/legacy-language-service-extensibility.md)
