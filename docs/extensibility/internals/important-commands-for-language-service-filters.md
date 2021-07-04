---
title: 言語サービス フィルターの重要なコマンド | Microsoft Docs
description: Visual Studio でフル機能の言語サービス フィルターを作成するときにサポートする必要がある重要なコマンドについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- language services, filters
- language services, commands to support
ms.assetid: 4948c494-3d4d-4f50-b3f9-959e73f90e4d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8dd5f65248411a7ea6b892d5b4c800718456339f
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899057"
---
# <a name="important-commands-for-language-service-filters"></a>言語サービス フィルターの重要なコマンド
フル機能の言語サービス フィルターを作成する場合は、次のコマンドの処理について検討してください。 コマンド識別子の完全なリストは、マネージ コードの場合は <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> 列挙型で、アンマネージド [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] コードの場合は Stdidcmd.h ヘッダー ファイルで定義されます。 Stdidcmd.h ファイルは、*Visual Studio SDK のインストール パス*\VisualStudioIntegration\Common\Inc にあります。

## <a name="commands-to-handle"></a>処理するコマンド

> [!NOTE]
> 次の表のすべてのコマンドについてフィルター処理を行うことは必須ではありません。

|コマンド|説明|
|-------------|-----------------|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|ユーザーが右クリックすると送信されます。 このコマンドは、ショートカット メニューを表示するタイミングであることを示します。 このコマンドを処理しない場合、テキスト エディターは、言語固有のコマンドを含まない既定のショートカット メニューを表示します。 独自のコマンドをこのメニューに含めるには、このコマンドを処理して独自にショートカット メニューを表示します。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|通常、ユーザーが Ctrl + J キーを押すと送信されます。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> の <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> メソッドを呼び出して、ステートメント入力候補ボックスを表示します。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|ユーザーが文字を入力すると送信されます。 このコマンドを監視して、トリガー文字が入力されたタイミングを判断したり、ステートメント入力候補、メソッド ヒント、およびテキスト マーカー (構文の色分け、かっこの一致、エラーマーカーなど) を提供したりします。 ステートメント入力候補については <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> の <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> メソッドを、メソッド ヒントについては <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow> の <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow.SetMethodData%2A> メソッドを呼び出します。 テキスト マーカーをサポートするには、このコマンドを監視し、入力された文字に呼応してマーカーを更新する必要があるかどうかを判断します。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|ユーザーが Enter キーを押すと送信されます。 このコマンドを監視して、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> の <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A> メソッドを呼び出してメソッド ヒント ウィンドウを閉じるタイミングを判断します。 既定では、このコマンドはテキスト ビューによって処理されます。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|ユーザーが Backspace キーを押すと送信されます。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> の <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData.OnDismiss%2A> メソッドを呼び出してメソッド ヒント ウィンドウを閉じるタイミングを判断するために監視します。 既定では、このコマンドはテキスト ビューによって処理されます。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|メニューまたはショートカット キーから送信されます。 パラメーター情報を使用してヒント ウィンドウを更新するには、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> の <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateTipWindow%2A> メソッドを呼び出します。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|ユーザーがマウス カーソルを変数に合わせて (変数の位置まで動かして) **[編集]** メニューの **[IntelliSense]** から **[クイック ヒント]** を選択すると送信されます。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> の <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateTipWindow%2A> メソッドを呼び出して、変数の型をヒントに返します。 デバッグがアクティブな場合、ヒントには変数の値も表示されます。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|通常、ユーザーが Ctrl + Space キーを押すと送信されます。 このコマンドは、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> の <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> メソッドを呼び出すよう言語サービスに指示します。|
|<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID><br /><br /> <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>|メニュー (通常は、 **[編集]** メニューの **[詳細設定]** の **[選択範囲のコメント]** または **[選択範囲のコメントを解除]** ) から送信されます。 <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> は、選択したテキストをユーザーがコメント アウトすることを示します。<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> は、選択したテキストをユーザーがコメント解除することを示します。 これらのコマンドは、言語サービスによる実装のみが可能です。|

## <a name="see-also"></a>関連項目
- [従来の言語サービスの開発](../../extensibility/internals/developing-a-legacy-language-service.md)
