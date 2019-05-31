---
title: ソース管理 VSPackage アーキテクチャ |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control packages, architecture
ms.assetid: 453125fc-23dc-49b1-8476-94581f05e6c7
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c05ae692a364d4e7a81a017d376dd820ade56b73
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66322502"
---
# <a name="source-control-vspackage-architecture"></a>ソース管理 VSPackage アーキテクチャ
ソース管理パッケージとは、VSPackage を使用するサービスを[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]IDE を提供します。 代わりに、ソース管理パッケージのソース管理のサービスとしての機能を提供します。 さらに、ソース管理パッケージには、ソース管理プラグインをソース管理を統合するためのより汎用性の高い代替[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]します。

 ソース管理プラグインのソース管理プラグイン API を実装する、コントラクトの厳密な保管します。 たとえば、プラグインを置き換えることはできません、既定[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ユーザー インターフェイス (UI)。 さらに、ソース管理プラグイン API は、独自のソース管理モデルを実装するプラグイン、できません。 ただし、ソース管理パッケージでは、これらの制限の両方は解決します。 ソース管理パッケージのソース コントロールのエクスペリエンスを完全に制御を持つ、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ユーザー。 また、ソース管理パッケージは、独自のソース管理モデルと、ロジックを使用でき、すべてのソース コントロールに関連するユーザー インターフェイスを定義できます。

## <a name="source-control-package-components"></a>ソース管理パッケージのコンポーネント
 アーキテクチャの図に示すように、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ソース コントロールのスタブをという名前のコンポーネントを使用してソース管理パッケージを統合する VSPackage は、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]します。

 ソース コントロールのスタブは、次のタスクを処理します。

- ソース管理パッケージ登録のために必要な一般的な UI を提供します。

- ソース管理パッケージを読み込みます。

- ソース管理パッケージをアクティブまたは非アクティブとして設定します。

  ソース コントロールのスタブは、ソース管理パッケージのアクティブなサービスを検索し、そのパッケージを IDE から受信したすべてのサービス呼び出しをルーティングします。

  コントロール アダプターのソースのパッケージは、特殊なソース管理パッケージを[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]を提供します。 このパッケージは、ソース管理プラグインをソース管理プラグイン API に基づくをサポートするための中核となるコンポーネントです。 ソース管理プラグインがプラグインのアクティブな場合、ソース コントロールのスタブは、ソース コントロール アダプターのパッケージにそのイベントを送信します。 さらに、ソース コントロール アダプターのパッケージを使用して、ソース管理プラグイン API を使用して、ソース管理プラグインの通信も、既定値はすべてソース管理プラグインの一般的な UI を提供します。

  ソース管理パッケージは、アクティブなパッケージが、その一方で、ソース コントロールのスタブと直接通信する、パッケージを使用して、[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]パッケージのソース管理のインターフェイスします。 ソース管理パッケージは、独自のソース管理 UI をホストします。

  ![ソース コントロールのアーキテクチャのグラフィック](../../extensibility/internals/media/vsipsccarch.gif "VSIPSCCArch")

  ソース管理パッケージの[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]コントロールのソース コードまたは統合のための API が用意されていません。 説明されているアプローチとは対照的[をソース管理プラグインを作成する](../../extensibility/internals/creating-a-source-control-plug-in.md)ソース管理プラグインが厳密な一連の関数とコールバックの実装にします。

  ソース管理パッケージとは、COM オブジェクトを使用して作成できるすべての VSPackage のような`CoCreateInstance`します。 VSPackage、自体利用できるように、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]実装することによって IDE<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>します。 VSPackage が、サイトのポインターを受け取るインスタンスが作成されると、および<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>VSPackage アクセス、利用可能なサービスと、IDE でインターフェイスを提供するインターフェイス。

  ソース管理プラグイン API ベースを作成するよりもより高度なプログラミングの専門知識を必要とソース管理 VSPackage に基づくパッケージの書き込みプラグイン。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>
- [作業の開始](../../extensibility/internals/getting-started-with-source-control-vspackages.md)