---
title: 簡略化された埋め込み |Microsoft Docs
description: ドキュメント ビュー オブジェクトが Visual Studio の子である場合にエディターで有効にできる、簡略化された埋め込みについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - simple view embedding
ms.assetid: f1292478-a57d-48ec-8c9e-88a23f04ffe5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: dca3b0c11c916a1fc47e4687bfeeabee35bcdfb4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056377"
---
# <a name="simplified-embedding"></a>簡略化された埋め込み
簡略化された埋め込みは、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] がドキュメント ビュー オブジェクトの親 (つまり子になる) であり、そのウィンドウ コマンドを処理するために <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> インターフェイスが実装されている場合に、エディターで有効になります。 簡略化された埋め込みエディターでは、アクティブなコントロールをホストできません。 簡略化された埋め込みを使用してエディターを作成するために使用するオブジェクトを次の図に示します。

 ![簡略化された埋め込みエディターの図](../extensibility/media/vssimplifiedembeddingeditor.gif "vsSimplifiedEmbeddingEditor") 簡略化された埋め込みを備えたエディター

> [!NOTE]
> この図のオブジェクトのうち、標準的なファイルベースのエディターを作成するために必要なのは `CYourEditorFactory` オブジェクトだけです。 カスタム エディターを作成する場合は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> を実装する必要はありません。エディター独自のプライベートの永続化メカニズムを備えることになる可能性があるからです。 ただし、カスタム エディター以外の場合は、これを行う必要があります。

 簡略化された埋め込みを備えたエディターを作成するために実装されるすべてのインターフェイスは、`CYourEditorDocument` オブジェクトに含まれています。 ただし、ドキュメント データの複数のビューをサポートするには、次の表に示すように、インターフェイスを別のデータに分割し、オブジェクトを表示します。

|インターフェイス|インターフェイスの場所|用途|
|---------------|---------------------------|---------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>|View|親ウィンドウへの接続を提供します。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|View|コマンドを処理します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser>|View|ステータス バーを更新できるようにします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxUser>|View|**ツールボックス** 項目を有効にします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsFileChangeEvents>|データ|ファイルが変更されたときに通知を送信します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>|データ|ファイルの種類に対して名前を付けて保存機能を有効にするために使用します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2>|データ|ドキュメントの永続性を有効にします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocDataFileChangeControl>|データ|再読み込みのトリガーなど、ファイル変更イベントの抑制を許可します。|
