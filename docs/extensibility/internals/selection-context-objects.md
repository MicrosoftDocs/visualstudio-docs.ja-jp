---
title: コンテキスト オブジェクトの選択 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- selection, tracking
- selection, context objects
ms.assetid: 7308ea8f-a42c-47e5-954e-7dee933dce7a
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ef76f417fe2b4371c73d78bbb90b0bd48470746a
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66318634"
---
# <a name="selection-context-objects"></a>コンテキスト オブジェクトの選択
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]統合開発環境 (IDE) が何を IDE に表示するかを判断するグローバルの選択コンテキスト オブジェクトを使用します。 IDE では、各ウィンドウは、独自の選択コンテキスト オブジェクトの選択のグローバル コンテキストにプッシュを持つことができます。 IDE は、そのウィンドウにフォーカスがあるウィンドウから値を持つグローバルの選択コンテキストを更新します。 詳細については、次を参照してください。[ユーザーへのフィードバック](../../extensibility/internals/feedback-to-the-user.md)します。

 ウィンドウ フレームまたは IDE でのサイトごとと呼ばれるサービス<xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection>します。 ウィンドウ フレームに配置されている VSPackage によって作成されたオブジェクトを呼び出す必要があります、`QueryService`へのポインターを取得するメソッド、<xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection>インターフェイス。

 フレーム ウィンドウには、開始するときに、グローバルの選択コンテキストを伝達されてから、選択コンテキスト情報の特定の部分を保持できます。 この機能は、空の選択範囲を開始する可能性のあるツール ウィンドウに便利です。

 Vspackage を監視するグローバルの選択コンテキストのトリガー イベントを変更します。 Vspackage が実装することで、次のタスクを実行できます`IVsTrackSelectionEx`と<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection>インターフェイス。

- 階層内の現在アクティブなファイルを更新します。

- 特定の種類の要素への変更を監視します。 例では、VSPackage が特別なを使用している場合、**プロパティ**ウィンドウで、アクティブな変更を監視できます**プロパティ**ウィンドウし、必要な場合に自分を再起動します。

  次の順序は、選択の追跡の一般的な手順を示しています。

1. IDE では、新しく開かれたウィンドウから選択コンテキストを取得し、グローバルの選択コンテキスト内に配置します。 HIERARCHY_DONTPROPAGATE または SELCONTAINER_DONTPROPAGATE を選択コンテキストを使用する場合、グローバルなコンテキストにその情報は反映されません。 詳細については、次を参照してください。[ユーザーへのフィードバック](../../extensibility/internals/feedback-to-the-user.md)します。

2. 通知イベントは、それらを要求したすべての VSPackage にブロードキャストされます。

3. VSPackage は、階層には、ツール、またはその他の同様のタスクを再アクティブ化の更新などのアクティビティを実行することによって受信イベントに対して動作します。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection>
- [Visual Studio での階層](../../extensibility/internals/hierarchies-in-visual-studio.md)
- [IDE での選択と通貨](../../extensibility/internals/selection-and-currency-in-the-ide.md)
- [プロジェクト タイプ](../../extensibility/internals/project-types.md)