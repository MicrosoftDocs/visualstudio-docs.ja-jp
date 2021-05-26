---
title: Visual Studio 2015 SDK でのソース管理の新機能 | Microsoft Docs
description: ソース管理 VSPackage の機能について説明した後、その実装手順の概要を確認します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- what's new [Visual Studio SDK], source control
- source control [Visual Studio SDK], what's new
ms.assetid: bcf85418-18fb-4824-9dae-d14bf3d56a77
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: da10750629fcdae66ab8456b3074c07f44e3cf05
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069063"
---
# <a name="whats-new-in-source-control-for-the-visual-studio-2015-sdk"></a>Visual Studio 2015 SDK でのソース管理の新機能

[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] では、ソース管理 VSPackage を実装することによって、緊密に統合されたソース管理ソリューションを提供できます。 このセクションでは、ソース管理 VSPackage の機能について説明した後、その実装手順の概要について説明しますします。

## <a name="the-source-control-vspackage"></a>ソース管理 VSPackage

Visual Studio では、2 種類のソース管理ソリューションをサポートしています。 すべてのバージョンの Visual Studio で、ソース管理プラグイン API ベースのプラグインを引き続き統合できます。 また、高レベルの複雑さと自律性を必要とするソース管理ソリューションに適した、緊密に統合された [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] パスを提供する、ソース管理のための VSPackage を作成することもできます。

VSPackage を使用すると、ほぼすべての種類の機能を Visual Studio に追加できます。 ソース管理 VSPackage は、ユーザーに表示される UI からソース管理システムとのバックエンド通信まで、Visual Studio の完全なソース管理機能を提供します。

ソース管理 VSPackage の実装には、"オール オア ナッシング" の戦略が要求されます。 ソース管理 VSPackage の作成者は、ソース管理機能全体だけでなく、Visual Studio と正常に統合するためにすべてのパッケージに必要なインターフェイスをカバーするために、多数のソース管理インターフェイスと新しい UI 要素 (ダイアログ ボックス、メニュー、ツール バー) の実装に多大な労力を投資する必要があります。

次の手順は、ソース管理パッケージを実装するために必要な作業の一般的な概要を示しています。 詳細については、[ソース管理 VSPackage の作成](../../extensibility/internals/creating-a-source-control-vspackage.md)に関するページを参照してください。

1. プライベート ソース管理サービスを提供する VSPackage を作成します。

2. Visual Studio によって提供されるソース管理関連のサービスにインターフェイス (<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> や <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider> インターフェイスなど) を実装します。

3. ソース管理 VSPackage を登録します。

4. すべてのソース管理 UI (メニュー項目、ダイアログ ボックス、ツール バー、コンテキスト メニューなど) を実装します。

5. ソース管理関連のすべてのイベントが、アクティブであり、かつ VSPackage によって処理される必要があるときにソース管理 VSackage に渡されます。

6. ソース管理 VSPackage では、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3> インターフェイスを実装するイベントや (<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> インターフェイスによって実装される) TPD (Track Project Document) イベントなどのイベントをリッスンし、必要なアクションを実行する必要があります。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>
- [概要](../../extensibility/internals/source-control-integration-overview.md)
- [ソース管理 VSPackage の作成](../../extensibility/internals/creating-a-source-control-vspackage.md)
