---
title: サービスの使用と提供 |Microsoft Docs
description: VSPackage による提供と使用のために Visual Studio IDE によって提供されるサービスについて説明します。 これらの記事では、サービスを取得、提供する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- examples [Visual Studio SDK], services
- Visual Studio, services
- services
ms.assetid: c0b415ba-b825-4da0-9faf-8a60a663e302
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b3f5e99b946514ebd3064441e9d2265be31e968a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060199"
---
# <a name="using-and-providing-services"></a>サービスの使用と提供
サービスは、2 つの VSPackage 間のコントラクトです。 ある VSPackage により、別の VSPackage で使用するインターフェイスの特定のセットが提供されます。 たとえば、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] により、読み込まれるすべての VSPackage に <xref:Microsoft.VisualStudio.Shell.Interop.SVsActivityLog> サービスが提供されます。 このサービスから、アクティビティ ログへの書き込みに使用できる <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog> インターフェイスが提供されます。 詳細については、「[方法: アクティビティ ログを使用する](../extensibility/how-to-use-the-activity-log.md)」を参照してください。

 VSPackage では、<xref:Microsoft.VisualStudio.Shell.Interop.IProfferService> インターフェイスを使用して独自のサービスを提供できます。

 Visual Studio には、次のような重要なサービスが用意されています。

|IDE サービス|説明|
|-----------------|-----------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>|基本機能、VSPackage、レジストリを扱う IDE サービスへのアクセスを提供します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>|ツールとドキュメント ウィンドウを作成する機能など、IDE の基本的なウィンドウ機能と UI 関連の機能を提供します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>|プロジェクトの列挙、新しいプロジェクトの作成、プロジェクトの変更の監視など、ソリューションに関連する基本的な機能を提供します。|

## <a name="in-this-section"></a>このセクションの内容
- [サービスの基本](../extensibility/internals/service-essentials.md)では、Visual Studio サービスの重要な要素を示します。

- [方法: サービスを取得する](../extensibility/how-to-get-a-service.md)では、サービスを要求 (使用) する方法について説明します。

- [方法: サービスを提供する](../extensibility/how-to-provide-a-service.md)では、サービスを提供する方法について説明します。

- [方法: 非同期の Visual Studio サービスを提供する](../extensibility/how-to-provide-an-asynchronous-visual-studio-service.md)では、非同期サービスを提供する方法について説明します。

- [方法: サービスのトラブルシューティング](../extensibility/how-to-troubleshoot-services.md)では、一般的な問題について説明し、それらの解決策を示します。

## <a name="related-sections"></a>関連項目
- [Visual Studio SDK](../extensibility/visual-studio-sdk.md)
