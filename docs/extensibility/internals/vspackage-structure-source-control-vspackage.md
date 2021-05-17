---
title: VSPackage 構造 (ソース管理 VSPackage) | Microsoft Docs
description: ソース管理実装者に Visual Studio と統合するための VSPackage に関するガイドラインを提供するソース管理パッケージ SDK について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, structure
- source control packages, VSPackage overview
ms.assetid: 92722be7-b397-48c3-a7a7-0b931a341961
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ae037e3bda4ca09ee11969325b67ff0f8323722d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060693"
---
# <a name="vspackage-structure-source-control-vspackage"></a>VSPackage 構造 (ソース管理 VSPackage)

ソース管理パッケージ SDK は、ソース管理実装者が自分のソース管理機能を Visual Studio 環境と統合できるようにする VSPackage を作成するためのガイドラインを提供します。 VSPackage は、パッケージがそのレジストリ エントリでアドバタイズしているサービスに基づいて、通常は Visual Studio 統合開発環境 (IDE) によって必要に応じて読み込まれる COM コンポーネントです。 すべての VSPackage が <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage> を実装する必要があります。 VSPackage では通常、Visual Studio IDE によって提供されるサービスを消費し、独自のいくつかのサービスを提供します。

VSPackage では、そのメニュー項目を宣言し、.vsct ファイル経由で既定の項目の状態を確立します。 VSPackage が読み込まれるまで、Visual Studio IDE には、この状態のメニュー項目が表示されます。 その後、VSPackage の実装の <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> メソッドが呼び出されて、メニュー項目が有効または無効になります。

## <a name="source-control-package-characteristics"></a>ソース管理パッケージの特性

ソース管理 VSPackage は、Visual Studio に緊密に統合されています。 VSPackage のセマンティクスには、次のものが含まれます。

- VSPackage であることによって実装されるインターフェイス (`IVsPackage` インターフェイス)

- UI コマンドの実装 (.vsct ファイルと <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイスの実装)

- Visual Studio による VSPackage の登録

ソース管理 VSPackage は、次の他の Visual Studio エンティティと通信する必要があります。

- プロジェクト

- エディター

- ソリューション

- Windows

- 実行中のドキュメント テーブル

### <a name="visual-studio-environment-services-that-may-be-consumed"></a>消費される可能性がある Visual Studio 環境サービス

<xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>

SVsRegisterScciProvider サービス

<xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>

### <a name="vsip-interfaces-implemented-and-called"></a>実装されて呼び出される VSIP インターフェイス

ソース管理パッケージは VSPackage であるため、Visual Studio に登録されている他の VSPackage と直接対話できます。 ソース管理のすべての機能を提供するために、ソース管理 VSPackage は、プロジェクトまたはシェルによって提供されるインターフェイスに対応できます。

Visual Studio のプロジェクトが Visual Studio IDE 内のプロジェクトとして認識されるには、必ず <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3> を実装する必要があります。 ただし、このインターフェイスは、ソース管理のために十分に特化されているわけではありません。 ソース管理下にあることが期待されるプロジェクトでは <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2> を実装します。 このインターフェイスは、プロジェクトの内容をクエリしたり、プロジェクトにグリフやバインドの情報 (ソース管理下にあるプロジェクトのサーバーの場所とディスクの場所の間の接続を確立するために必要な情報) を提供したりするために、ソース管理 VSPackage によって使用されます。

ソース管理 VSPackage では <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2> を実装します。それにより、プロジェクトはソース管理に自身を登録し、自身の状態のグリフを取得できるようになります。

ソース管理 VSPackage で考慮する必要があるインターフェイスの完全な一覧については、「[関連サービスとインターフェイス](../../extensibility/internals/related-services-and-interfaces-source-control-vspackage.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [デザイン要素](../../extensibility/internals/source-control-vspackage-design-elements.md)
- [関連サービスとインターフェイス](../../extensibility/internals/related-services-and-interfaces-source-control-vspackage.md)
