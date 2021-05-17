---
title: オートメーション モデルへの投稿 | Microsoft Docs
description: VSPackage を設計するとき、一連のガイドラインに従って、Visual Studio オートメーション モデルに投稿する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK]
ms.assetid: 44de482d-93c8-41a4-843c-cefda995a03e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 44da0c91eb425cbd558aea4335447f9293684b90
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057040"
---
# <a name="contribute-to-the-automation-model"></a>オートメーション モデルへの投稿
Visual Studio には、環境をカスタマイズするための一連のオートメーション インターフェイスが用意されています。 オートメーション モデルはオブジェクト モデルであり、エンド ユーザーはこれを使用して Visual Studio のアドインと拡張機能を作成できるようになります。

 また、オートメーション モデルへの投稿は、VSPackage の開発者に適しています。これにより、VSPackage のエンド ユーザーはアドインを作成できるようになります。また、エンド ユーザーが [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] で VSPackage を使用するときに、通常、一貫したユーザー モデル エクスペリエンスを提供できます。

 エンド ユーザー エクスペリエンスの一貫性を確保するために、VSPackage の設計時に一連のガイドラインに従うことができ、そうすることで VSPackage のオートメーション モデルを [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のアイデアに準拠させることができます。

## <a name="in-this-section"></a>このセクションの内容
- [オートメーション モデルの概要](../../extensibility/internals/automation-model-overview.md)

 共通環境の主要なファセットを制御するオブジェクトの関連グループとしてオートメーション モデルを定義します。 この一連のオブジェクトが、オートメーション モデルの図に示されます。

- [VSPackage でのオートメーションの提供](../../extensibility/internals/providing-automation-for-vspackages.md)

 VSPackage のオートメーションを実現する 2 つの主な方法について説明します。

- [プロジェクト オブジェクトの公開](../../extensibility/internals/exposing-project-objects.md)

 VSPackage 固有のオブジェクトを作成するためのステップバイステップの手順を示します。

- [プロジェクトのモデリング](../../extensibility/internals/project-modeling.md)

 新しいプロジェクト タイプのオートメーションを作成するために必要な標準プロジェクト オブジェクトについて説明し、プロジェクト オートメーションが従うパスを図示します。 このトピックでは、クラスの宣言と実装の一覧も示します。

- [イベントの公開](../../extensibility/internals/exposing-events-in-the-visual-studio-sdk.md)

 オートメーション モデルのイベントを作成するためのステップバイステップの手順を示します。

- [オプション ページのオートメーションのサポート](../../extensibility/internals/automation-support-for-options-pages.md)

 `DTE.Properties` オブジェクトを拡張することによって、 **[ツール]** メニューの VSPackage のカスタム **[オプション]** ダイアログ ボックスのプロパティをサポートするために、オートメーション オブジェクトを返す方法について説明します。

- [コードへのオートメーションの提供](../../extensibility/internals/providing-automation-for-code.md)

 コードのオートメーション モデルは作成する必要がないことを説明します。 ただし、このトピックには、コード モデルについて深い洞察が得られる情報を提供するリンクが用意されています。

- [方法: ウィンドウへのオートメーションの提供](../../extensibility/internals/how-to-provide-automation-for-windows.md)

 ウィンドウでオートメーション オブジェクトを使用できるようにしたいが、環境で既製のオートメーション オブジェクトが提供されていない場合は、常に、オートメーションの提供が推奨されることを説明します。 ツール ウィンドウとドキュメント ウィンドウのオートメーションについて説明します。

- [オートメーション モデルの使用](../../extensibility/internals/using-the-automation-model.md)

 オートメーション コンシューマーが初期のプロジェクト オートメーション オブジェクトを取得する方法を示す 2 つのコード例を提供します。

- [構成および SelectedItem オブジェクトのためのオートメーション](../../extensibility/internals/automation-for-configuration-and-selecteditem-objects.md)

 構成および SelectedItem オブジェクトのオートメーションに関する情報を提供します。

## <a name="reference"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> VSPackage が DTE オートメーション オブジェクト モデルにどのように参加するかを示すコード サンプルを提供します。 パラメーター、戻り値、および選択した説明を示します。
