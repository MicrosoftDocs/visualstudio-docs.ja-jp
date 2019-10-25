---
title: ソース管理プラグインのアーキテクチャ |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, architecture
ms.assetid: 35351d4c-9414-409b-98fc-f2023e2426b7
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6f06f023a46fc9bc417e9630613a716f8dd448d2
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72723443"
---
# <a name="source-control-plug-in-architecture"></a>アーキテクチャのソース管理プラグイン
ソース管理プラグインを実装してアタッチすることによって、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE) にソース管理サポートを追加できます。 IDE は、適切に定義されたソース管理プラグイン API を使用してソース管理プラグインに接続します。 IDE では、ツールバーとメニューコマンドで構成されるユーザーインターフェイス (UI) を提供することによって、ソース管理システムのバージョン管理機能を公開しています。 ソース管理プラグインは、ソース管理機能を実装します。

## <a name="source-control-plug-in-resources"></a>ソース管理プラグインのリソース
 ソース管理プラグインには、バージョン管理アプリケーションを作成して [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE に接続するためのリソースが用意されています。 ソース管理プラグインには、ソース管理プラグインによって実装され、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE に統合できるようにする必要がある API 仕様が含まれています。 また、ソース管理プラグイン API に準拠しC++た重要な関数の実装をデモンストレーションするスケルトンソース管理プラグインを実装するコードサンプル (で記述) も含まれています。

 ソース管理プラグイン api 仕様を使用すると、ソース管理プラグイン API に従って実装されている必要な関数のセットを使用してソース管理 DLL を作成する場合に、任意のソース管理システムを利用できます。

## <a name="components"></a>コンポーネント
 この図のソース管理アダプターパッケージは、ソース管理操作に対するユーザーの要求を、ソース管理プラグインによってサポートされる関数呼び出しに変換する IDE のコンポーネントです。 これを行うには、ide とソース管理プラグインに、IDE とプラグインの間で情報をやり取りする効果的なダイアログが必要です。 このダイアログを実行するには、どちらも同じ言語を話す必要があります。 このドキュメントに記載されているソース管理プラグイン API は、この exchange の一般的な語彙です。

 ![ソースコード管理アーキテクチャの図](../../extensibility/internals/media/vs_sccsdk_plug_in_arch.gif "vs_sccsdk_plug_in_arch")VS とソース管理プラグイン間の相互作用を示すアーキテクチャ図

 アーキテクチャダイアグラムに示されているように、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] シェルは、図で VS shell というラベルが付けられ、ユーザーの作業プロジェクトと関連コンポーネント (エディターやソリューションエクスプローラーなど) をホストします。 ソース管理アダプターパッケージは、IDE とソース管理プラグイン間の相互作用を処理します。 ソース管理アダプターパッケージには、独自のソース管理 UI が用意されています。 これは、ソース管理操作のスコープを開始および定義するために、ユーザーが操作する最上位の UI です。

 ソース管理プラグインは独自の UI を持つことができ、図に示すように2つの部分で構成される場合があります。 "Vendor UI" というラベルが付いたボックスは、ソース管理プラグインの作成者が提供するカスタムユーザーインターフェイス要素を表します。 これらは、ユーザーが高度なソース管理操作を呼び出したときに、ソース管理プラグインによって直接表示されます。 "ヘルパー UI" というラベルの付いたボックスは、IDE を通じて間接的に呼び出されるソース管理プラグインの UI 機能のセットです。 ソース管理プラグインは、IDE によって提供される特殊なコールバック関数を使用して、UI 関連のメッセージを IDE に渡します。 ヘルパー UI を使用すると、IDE とのシームレスな統合が容易になり (多くの場合、 **[詳細設定**] ボタンを使用)、エンドユーザーエクスペリエンスが統一されます。

 ソース管理プラグインは、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] シェルに変更を加えることはできず、その結果、ソース管理アダプターパッケージまたは IDE によって提供されるソース管理 UI のいずれかに変更を加えることはできません。 エンドユーザーの統合されたエクスペリエンスに寄与するさまざまなソース管理プラグイン API 関数の実装によって提供される柔軟性を最大限に活用する必要があります。 ソース管理プラグイン API ドキュメントのリファレンスセクションには、いくつかの高度なソース管理プラグイン機能に関する情報が含まれています。 これらの機能を利用するには、ソース管理プラグインは初期化中に IDE に高度な機能を宣言する必要があり、機能ごとに特定の高度な機能を実装する必要があります。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../../extensibility/source-control-plug-ins.md)
- [用語集](../../extensibility/source-control-plug-in-glossary.md)
- [ソース管理プラグインの作成](../../extensibility/internals/creating-a-source-control-plug-in.md)