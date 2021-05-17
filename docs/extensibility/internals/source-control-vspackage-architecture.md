---
title: ソース管理 VSPackage アーキテクチャ | Microsoft Docs
description: ソース管理パッケージ (ソース管理サービスとして Visual Studio に機能を提供する VSPackage) のアーキテクチャについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control packages, architecture
ms.assetid: 453125fc-23dc-49b1-8476-94581f05e6c7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4e9f19506c58f65f80900c08fe339c7478144546
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064229"
---
# <a name="source-control-vspackage-architecture"></a>ソース管理 VSPackage アーキテクチャ
ソース管理パッケージは、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE によって提供されるサービスを使用する VSPackage です。 見返りとして、ソース管理パッケージは、その機能性をソース管理サービスとして提供します。 また、ソース管理パッケージは、ソース管理を [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に統合するためのソース管理プラグインよりも汎用性が高い選択肢です。

 ソース管理プラグイン API を実装するソース管理プラグインは、厳格なコントラクトを順守します。 たとえば、プラグインは既定の [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ユーザー インターフェイス (UI) を置き換えることはできません。 さらに、ソース管理プラグイン API では、プラグインが独自のソース管理モデルを実装することはできません。 一方で、ソース管理パッケージは、これら両方の制限を克服します。 ソース管理パッケージは、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ユーザーのソース管理エクスペリエンスを完全に制御します。 さらに、ソース管理パッケージでは、独自のソース管理モデルとロジックを使用でき、すべてのソース管理関連ユーザー インターフェイスを定義できます。

## <a name="source-control-package-components"></a>ソース管理パッケージのコンポーネント
 アーキテクチャ図で示しているように、"ソース管理スタブ" という名前の [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] コンポーネントは、ソース管理パッケージを [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] と統合する VSPackage です。

 ソース管理スタブは、次のタスクを処理します。

- ソース管理のパッケージ登録に必要な共通の UI を提供します。

- ソース管理パッケージを読み込みます。

- ソース管理パッケージをアクティブまたは非アクティブに設定します。

  ソース管理スタブは、ソース管理パッケージのアクティブなサービスを探し、IDE から受信したすべてのサービス呼び出しをそのパッケージにルーティングします。

  ソース管理アダプター パッケージは、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] で提供される特別なソース管理パッケージです。 このパッケージは、ソース管理プラグイン API に基づいてソース管理プラグインをサポートするための中心的なコンポーネントです。 ソース管理プラグインがアクティブなプラグインである場合、ソース管理スタブはそのイベントをソース管理アダプター パッケージに送信します。 その後、ソース管理アダプター パッケージは、ソース管理プラグイン API を使用してソース管理プラグインと通信し、すべてのソース管理プラグインに共通である既定の UI も提供します。

  その一方で、ソース管理パッケージがアクティブなパッケージである場合、ソース管理スタブは [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] のソース管理パッケージ インターフェイスを使用してパッケージと直接通信します。 ソース管理パッケージは、その独自のソース管理 UI をホストする責任があります。

  ![ソース管理アーキテクチャのグラフィック](../../extensibility/internals/media/vsipsccarch.gif "VSIPSCCArch")

  ソース管理パッケージの場合、ソース管理コードまたは統合のための API は [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] によって用意されません。 これと対照的なのは、「[ソース管理プラグインを作成する](../../extensibility/internals/creating-a-source-control-plug-in.md)」で説明されているような、関数とコールバックの厳密なセットをソース管理プラグインで実装する必要があるアプローチです。

  他の VSPackage と同様に、ソース管理パッケージは `CoCreateInstance` を使用して作成できる COM オブジェクトです。 VSPackage は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage> を実装することによって、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE から自らを使用できるようにします。 インスタンスが作成されると、VSPackage はサイト ポインターと <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> インターフェイスを受け取ります。後者により、IDE で使用可能なサービスとインターフェイスへのアクセスが VSPackage に提供されます。

  VSPackage ベースのソース管理パッケージを作成するには、ソース管理プラグイン API ベースのプラグインを作成する場合よりも高度なプログラミング専門知識が必要です。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>
- [はじめに](../../extensibility/internals/getting-started-with-source-control-vspackages.md)
