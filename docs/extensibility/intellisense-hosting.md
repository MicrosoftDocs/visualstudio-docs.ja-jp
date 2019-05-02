---
title: IntelliSense のホスティング |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - IntelliSense hosting
ms.assetid: 20c61f8a-d32d-47e2-9c67-bf721e2cbead
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6e4f6ae0f2df20cefefb8a086fbd383d98a6d5cd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62910625"
---
# <a name="intellisense-hosting"></a>IntelliSense をホストしています。
Visual Studio では、IntelliSense のホストを使用できます。 Visual Studio テキスト エディターでホストされていないコードに対して IntelliSense を提供する IntellSense をホストしていることができます。

## <a name="intellisense-hosting-usage"></a>IntelliSense のホスティングの使用状況
 Visual Studio で、入力候補のセットとテキスト バッファーにアクセスできる任意のコードは、どこからでも windows の IntelliSense を取得できます、ユーザー インターフェイス (UI) にします。 このサンプル シナリオの一部がで補完、**ウォッチ**ウィンドウまたは [ブレークポイントのプロパティ] ウィンドウの条件フィールド。

### <a name="implementation-interfaces"></a>インターフェイスの実装

#### <a name="ivsintellisensehost"></a>IVsIntellisenseHost
 IntelliSense のポップアップ ウィンドウをホストする任意の UI コンポーネントをサポートする必要があります、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost>インターフェイス。 既定のコア エディターのテキスト ビューには、株式が含まれています。<xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost>インターフェイスの現在の IntelliSense 機能を保持する実装。 ほとんどの場合、メソッド、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost>表す何のサブセットが実装されているインターフェイス、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>インターフェイス。 サブセットには、IntelliSense UI 処理、カレットおよび選択操作、および単純なテキストの置換機能が含まれています。 さらに、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost>インターフェイスを使用する別の IntelliSense"subject"と「コンテキスト」件名コンテキストが使用されているテキスト バッファーに直接存在しないが、IntelliSense が提供できるようにします。

#### <a name="ivsintellisensehostgethostflags"></a>IVsIntellisenseHost.GetHostFlags
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost>インターフェイス プロバイダーを実装する必要があります、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.GetHostFlags%2A>をクライアントが判別 IntelliSense の種類、ホストの機能を有効にするメソッドをサポートしています。

 定義されている、ホスト フラグ[IntelliSenseHostFlags](../extensibility/intellisensehostflags.md)、以下にまとめます。

|IntelliSense ホスト フラグ|説明|
|----------------------------|-----------------|
|IHF_READONLYCONTEXT|読み取り専用と編集が、件名のテキスト内でのみが発生したコンテキスト バッファーは、したがって、フラグを設定します。|
|IHF_NOSEPERATESUBJECT|設定フラグつまりをある IntelliSense の別のサブジェクトはありません。 サブジェクトに存在するコンテキスト バッファーなど、従来の<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>IntelliSense システム。|
|IHF_SINGLELINESUBJECT|件名がないこのフラグは設定で単一行の編集のようにできる、複数の行、**ウォッチ**ウィンドウ。|
|IHF_FORCECOMMITTOCONTEXT|このフラグを設定し、コンテキスト バッファーを更新する必要がある場合、ホストは、読み取り専用フラグが無視されるコンテキスト バッファーを続行するために編集を使用できます。|
|IHF_OVERTYPE|編集 (サブジェクトまたはコンテキスト) では、上書きモードで行う必要があります。|

#### <a name="ivsintellisensehostbeforecompletorcommit-and-ivsintellisensehostaftercompletorcommit"></a>IVsIntellisenseHost.BeforeCompletorCommit と IVsIntellisenseHost.AfterCompletorCommit
 前に、と後のテキストがコミットされ、前処理および後処理を有効にする、これらのコールバック メソッドが完了ウィンドウによって呼び出されます。

#### <a name="ivsintellisensecompletor"></a>IVsIntellisenseCompletor
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseCompletor>インターフェイスは、統合開発環境 (IDE) で使用される標準の完了ウィンドウの共同作成可能なバージョン。 すべて<xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost>インターフェイスがこの completor インターフェイスを使用して IntelliSense をすばやく実装できます。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.TextManager.Interop>