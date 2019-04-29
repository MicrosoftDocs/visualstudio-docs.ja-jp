---
title: 使用して、サービスを提供します |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- examples [Visual Studio SDK], services
- Visual Studio, services
- services
ms.assetid: c0b415ba-b825-4da0-9faf-8a60a663e302
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 36f49d4e1ebaa6d8e15e43b821af56204739cb07
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62798966"
---
# <a name="using-and-providing-services"></a>サービスの使用と提供
サービスは、2 つの Vspackage の間のコントラクトです。 1 つの VSPackage では、別の VSPackage を使用するためのインターフェイスの特定のセットを提供します。 たとえば、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]を提供、<xref:Microsoft.VisualStudio.Shell.Interop.SVsActivityLog>サービスすべての VSPackage に読み込みます。 このサービスの提供、<xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog>インターフェイスで、アクティビティ ログに書き込むことができます。 詳細については、「[方法 :アクティビティ ログを使用して、](../extensibility/how-to-use-the-activity-log.md)します。

 Vspackage を使用して、独自のサービスを提供できます、<xref:Microsoft.VisualStudio.Shell.Interop.IProfferService>インターフェイス.

 Visual Studio では、次などの重要なサービスを提供します。

|IDE のサービス|説明|
|-----------------|-----------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>|IDE へのアクセスは、基本的な機能、Vspackage、およびレジストリを使用した処理をサービスを提供します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>|基本的なウィンドウ操作およびツールとドキュメント ウィンドウを作成する機能など、IDE での UI 関連の機能を提供します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>|プロジェクトの列挙、新しいプロジェクトの作成、およびプロジェクトの変更を監視する機能など、基本のソリューションに関連する機能を提供します。|

## <a name="in-this-section"></a>このセクションの内容
- [サービスの基本情報](../extensibility/internals/service-essentials.md)Visual Studio サービスの重要な要素を表示します。

- [方法: サービスを取得](../extensibility/how-to-get-a-service.md)を要求する方法について説明します (使用する) サービス。

- [方法: サービスを提供](../extensibility/how-to-provide-a-service.md)サービスを提供する方法について説明します。

- [方法: 非同期の Visual Studio サービスを提供](../extensibility/how-to-provide-an-asynchronous-visual-studio-service.md)非同期のサービスを提供する方法について説明します。

- [方法: サービスのトラブルシューティング](../extensibility/how-to-troubleshoot-services.md)にソリューションを示し、一般的な問題について説明します。

## <a name="related-sections"></a>関連項目
- [Visual Studio SDK](../extensibility/visual-studio-sdk.md)