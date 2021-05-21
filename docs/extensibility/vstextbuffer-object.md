---
title: VSTextBuffer オブジェクト | Microsoft Docs
description: VSTextBuffer オブジェクトは、一般にファイルに関連付けられている Unicode テキストのストリームを表します。 この記事では、VSTextBuffer のインターフェイスを一覧で紹介します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VSTextBuffer
helpviewer_keywords:
- VSTextBuffer object, reference
- views [Visual Studio SDK], VSTextBuffer object
ms.assetid: c5f94b45-7249-4e1f-a53d-1d2a1c61e0ef
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a72491b118e0a51454181734a8fe388c2f7e851e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062188"
---
# <a name="vstextbuffer-object"></a>VSTextBuffer オブジェクト
テキスト バッファー オブジェクトは、一般にファイルに関連付けられている Unicode テキストのストリームを表します。 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> オブジェクトは、ウィザードのように、コア エディターのコンテキスト外で使用できます。

 `VSTextBuffer` のインターフェイスを次の表に示します。

|Method|説明|
|------------|-----------------|
|[IOleCommandTarget](/windows/desktop/api/docobj/nn-docobj-iolecommandtarget)|標準の OLE インターフェイス。 バッファー内の元に戻すとやり直しの処理に使用されます。|
|[IPersistFile](/windows/desktop/api/objidl/nn-objidl-ipersistfile)|標準の OLE インターフェイス。|
|[IPersistStream](/windows/desktop/api/objidl/nn-objidl-ipersiststream)|標準の OLE インターフェイス。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompoundAction>|複合アクション (つまり、1 つの元に戻すとやり直しの単位にグループ化されたアクション) の作成を可能にします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData>|テキスト バッファーによって管理されるドキュメント データの保持を可能にします。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>|基本的なサービスを提供します。多くのクライアントから使用されます。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextFind>|バッファーを検索するために使用されます。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines>|2 次元座標を使用して読み取りと書き込みの機能を提供します。 `IVsTextBuffer` から継承されます。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStream>|1 次元座標を使用して読み取りと書き込みの機能を提供します。 `IVsTextBuffer` から継承されます。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextScanner>|バッファー内のテキストに対する高速でストリーム指向のシーケンシャル アクセスを提供します。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsUserData>|プロパティの汎用コレクションへのアクセスを提供します。 最も重要なプロパティは、バッファーの名前、つまりモニカーです。 GUID を作成してキーとして使用することにより、このインターフェイスを使用して独自のランダム データをバッファーに格納できます。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer>|イベントの接続ポイントをサポートします。|

## <a name="remarks"></a>解説
 通常、`VSTextBuffer` は、`IVsTextBuffer` に対する `QueryInterface` の呼び出しによって検出されます。 詳細については、[テキスト バッファー](/previous-versions/visualstudio/visual-studio-2015/extensibility/accessing-the-text-buffer-by-using-the-legacy-api?preserve-view=true&view=vs-2015)に関するページを参照してください。

## <a name="see-also"></a>こちらもご覧ください
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>
- <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView>
- [図形の編集](https://www.microsoft.com/download/details.aspx?id=55984)