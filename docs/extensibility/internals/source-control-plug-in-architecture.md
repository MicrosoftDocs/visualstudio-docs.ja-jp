---
title: ソース管理プラグインのアーキテクチャ | Microsoft Docs
description: ソース管理プラグインを実装およびアタッチして、Visual Studio IDE にソース管理サポートを追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, architecture
ms.assetid: 35351d4c-9414-409b-98fc-f2023e2426b7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3fe51878603996044535b0abfb70302ef9027c03
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064255"
---
# <a name="source-control-plug-in-architecture"></a>アーキテクチャのソース管理プラグイン
ソース管理プラグインを実装およびアタッチして、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE) にソース管理サポートを追加することができます。 IDE では、適切に定義されたソース管理プラグイン API を使用してソース管理プラグインに接続します。 IDE では、ツール バーとメニュー コマンドで構成されるユーザー インターフェイス (UI) を提供して、ソース管理システムのバージョン管理機能を公開します。 ソース管理プラグインはソース管理機能を実装します。

## <a name="source-control-plug-in-resources"></a>ソース管理プラグインのリソース
 ソース管理プラグインは、バージョン管理アプリケーションを作成して [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE に接続するためのリソースを提供します。 ソース管理プラグインには API 仕様が含まれており、このプラグインを [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE に統合できるよう、ソース管理プラグインでこの仕様を実装する必要があります。 スケルトンのソース管理プラグインを実装し、ソース管理プラグイン API に準拠した重要な関数の実装例を示す (C++ で記述された) コード サンプルも含まれています。

 ソース管理プラグイン API の仕様では、任意のソース管理システムを選択して利用できますが、そのための条件として、ソース管理プラグイン API に準拠して実装された関数の必要なセットを含むソース管理 DLL を作成する必要があります。

## <a name="components"></a>Components
 図中のソース管理アダプター パッケージは IDE のコンポーネントであり、ソース管理操作に対するユーザーの要求を、ソース管理プラグインでサポートされている関数呼び出しに変換します。 この処理のために、IDE とソース管理プラグインの間で情報をやり取りする効果的な対話のしくみが両者に必要です。 この対話を実行するためには、両者が同じ言語を使用する必要があります。 このドキュメントで説明しているソース管理プラグイン API は、この情報交換のための共通語彙です。

 ![ソース コード管理のアーキテクチャ図](../../extensibility/internals/media/vs_sccsdk_plug_in_arch.gif "vs_sccsdk_plug_in_arch") VS とソース管理プラグイン間の相互作用を示すアーキテクチャ図

 アーキテクチャ図で示しているように、図中で "VS シェル" というラベルの付いた [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] シェルは、ユーザーの作業中のプロジェクトと関連コンポーネント (エディターやソリューション エクスプローラーなど) をホストします。 ソース管理アダプター パッケージは、IDE とソース管理プラグイン間の相互作用を処理します。 ソース管理アダプター パッケージは、独自のソース管理 UI を提供します。 これは、ソース管理操作のスコープを開始および定義するためにユーザーが操作する最上位の UI です。

 ソース管理プラグインは独自の UI を備えることができ、これは、図で示しているように 2 つの部分で構成される場合があります。 "ベンダー UI" というラベルの付いたボックスは、ソース管理プラグインの作成者が提供するカスタムのユーザー インターフェイス要素を表します。 これらは、ユーザーが高度なソース管理操作を呼び出したときに、ソース管理プラグインによって直接表示されます。 "ヘルパー UI" というラベルの付いたボックスは、IDE を通じて間接的に呼び出されるソース管理プラグイン UI 機能のセットです。 ソース管理プラグインは、IDE によって提供される特殊なコールバック関数を通じて、UI 関連のメッセージを IDE に渡します。 ヘルパー UI により、(多くの場合、 **[詳細設定]** ボタンの使用を通じて) IDE とのよりシームレスな統合が促進され、より統一性のあるエンドユーザー エクスペリエンスが実現します。

 ソース管理プラグインでは、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] シェルに変更を加えることはできません。つまり、ソース管理アダプター パッケージと、IDE によって提供されるソース管理 UI のどちらにも変更を加えることができません。 エンド ユーザーのための統合されたエクスペリエンスに寄与するさまざまなソース管理プラグイン API 関数の実装を通じて提供される柔軟性を最大限に活用する必要があります。 ソース管理プラグイン API のドキュメントのリファレンス セクションには、いくつかの高度なソース管理プラグインの機能に関する情報が含まれています。 以上の特徴を活かすために、ソース管理プラグインでは、その高度な機能を初期化中に IDE に対して宣言する必要があり、各機能用の特定の高度な関数を実装する必要があります。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../../extensibility/source-control-plug-ins.md)
- [用語集](../../extensibility/source-control-plug-in-glossary.md)
- [ソース管理プラグインの作成](../../extensibility/internals/creating-a-source-control-plug-in.md)
