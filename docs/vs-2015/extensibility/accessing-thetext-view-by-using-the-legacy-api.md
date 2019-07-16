---
title: レガシ API を使用してテキスト ビューへのアクセス |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - text view
ms.assetid: 8f751f72-c972-4be3-84ee-19c281e02e25
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8f9396e4523e38e7313efb5668c4680f551558ab
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68184947"
---
# <a name="accessing-thetext-view-by-using-the-legacy-api"></a>レガシ API を使用するテキスト ビューへのアクセス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

テキスト ビューは、テキスト バッファーに格納されているテキストのプレゼンテーションです。 テキスト ビューは、次のセクションで示すように、従来の API を使用してアクセスできます。  
  
## <a name="text-view-object"></a>テキスト ビュー オブジェクト  
 各ビューは、独自のテキスト バッファーに関連付けられていると、ビューは、バッファー内のデータでウィンドウを。 次の図は、キーによって表されるテキスト ビュー オブジェクトのインターフェイスを示しています。<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView>します。  
  
 ![Visual Studio テキスト ビュー オブジェクト](../extensibility/media/vstextview.gif "vstextview")  
テキスト ビュー オブジェクト  
  
 ビューは、バッファー内のテキストを表示する方法です。 ビューで確認できますが、バッファー内のテキストの正確な表現されないように、折り返し、および、アウトラインなどの機能が含まれます。  
  
 ビューには、他のサービスや着信するコマンドをインターセプトし、ビューの動作にする前に処理を実行するプロセスが有効になります。 これを行う最も一般的なサービスは、言語サービスです。 言語サービスは、ENTER キーをカスタムのインデントの動作またはツール ヒントを提供するためのコマンドをインターセプトする必要がありますなどが。  
  
## <a name="adding-functionality-to-the-text-view"></a>テキスト ビューへの機能の追加  
 特定のキーストロークを処理することによって、テキストの表示動作をカスタマイズできます。 実装する、キーストロークをインターセプトする<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter>オブジェクト、コマンド ターゲットを提供し、(<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>) モニターと切片コマンド。  
  
 テキスト ビューでは、コマンドのフィルターをシーケンシャルなアーキテクチャを使用します。 新しいコマンド フィルター (<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>オブジェクト) 呼び出しによって、シーケンスに追加された、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A>メソッド。  
  
 使用して、テキスト ビューのイベント通知が提供される、`T:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEvents`インターフェイス。 テキスト ビューへの変更の通知を受け取るクライアント オブジェクトをこのインターフェイスを実装します。 使用してテキスト ビューには、このインターフェイスを公開、<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer>ビューからの変更の通知を受信する、テキスト ビュー上のインターフェイス。  
  
## <a name="see-also"></a>関連項目  
 [レガシ API を使用してビューの設定の変更](../extensibility/changing-view-settings-by-using-the-legacy-api.md)   
 [グローバル設定を監視するためのテキスト マネージャーの使用](../extensibility/using-the-text-manager-to-monitor-global-settings.md)
