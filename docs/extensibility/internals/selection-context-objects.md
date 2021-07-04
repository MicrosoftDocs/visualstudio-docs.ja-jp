---
title: 選択コンテキスト オブジェクト | Microsoft Docs
description: Visual Studio IDE でグローバル選択コンテキスト オブジェクトを使用して IDE に表示する内容を決定する仕組みの詳細について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- selection, tracking
- selection, context objects
ms.assetid: 7308ea8f-a42c-47e5-954e-7dee933dce7a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b0c97108eaba426a4def4c1052d3adc7348eb88b
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898488"
---
# <a name="selection-context-objects"></a>コンテキスト オブジェクトの選択
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE) では、グローバル選択コンテキスト オブジェクトを使用して、IDE に表示する内容を決定します。 IDE の各ウィンドウは、自身の選択コンテキスト オブジェクトをグローバル選択コンテキストにプッシュできます。 IDE では、あるウィンドウにフォーカスがあるときに、そのウィンドウの値でグローバル選択コンテキストを更新します。 詳細については、「[ユーザーへのフィードバック](../../extensibility/internals/feedback-to-the-user.md)」を参照してください。

 IDE 内のウィンドウ フレームまたはサイトのそれぞれに、<xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> という名前のサービスがあります。 ウィンドウ フレームに配置されている VSPackage によって作成されたオブジェクトは、`QueryService` メソッドを呼び出して <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> インターフェイスへのポインターを取得する必要があります。

 フレーム ウィンドウでは、開始時に、自身の選択コンテキスト情報の一部をグローバル選択コンテキストに伝達しないようにすることができます。 この機能は、空の選択内容で開始する必要があるツール ウィンドウに役立ちます。

 グローバル選択コンテキストを変更すると、VSPackage で監視できるイベントがトリガーされます。 VSPackage では、`IVsTrackSelectionEx` インターフェイスと <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection> インターフェイスを実装することで、次のタスクを実行できます。

- 階層内の現在アクティブなファイルを更新します。

- 特定の種類の要素に対する変更を監視します。 たとえば、VSPackage で特別な **[プロパティ]** ウィンドウを使用している場合は、アクティブな **[プロパティ]** ウィンドウで変更を監視し、必要に応じて独自の特別なウィンドウを再起動できます。

  次のシーケンスは、選択の追跡の典型的な例を示しています。

1. IDE が、新しく開かれたウィンドウから選択コンテキストを取得し、グローバル選択コンテキストにプッシュします。 選択コンテキストで HIERARCHY_DONTPROPAGATE または SELCONTAINER_DONTPROPAGATE が使用されている場合、その情報はグローバル コンテキストに伝達されません。 詳細については、「[ユーザーへのフィードバック](../../extensibility/internals/feedback-to-the-user.md)」を参照してください。

2. 通知イベントが、それを要求したすべての VSPackage にブロードキャストされます。

3. VSPackage は、受信したイベントに対応して、階層の更新、ツールの再アクティブ化、他の類似したタスクなどのアクティビティを実行します。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection>
- [Visual Studio での階層](../../extensibility/internals/hierarchies-in-visual-studio.md)
- [IDE での選択と通貨](../../extensibility/internals/selection-and-currency-in-the-ide.md)
- [プロジェクトの種類](../../extensibility/internals/project-types.md)
