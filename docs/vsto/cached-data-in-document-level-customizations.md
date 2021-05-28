---
title: ドキュメントレベルのカスタマイズにおけるキャッシュ データ
description: データをデータ キャッシュとして埋め込めるようにすることで、Visual Studio で、ドキュメントレベルのカスタマイズのビューからデータを分離する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data islands [Office development in Visual Studio]
- view [Office development in Visual Studio]
- caching data [Office development in Visual Studio], about caching data
- data caching [Office development in Visual Studio], about data caching
- data [Office development in Visual Studio], cache
- data [Office development in Visual Studio], document-level solutions
- document-level customizations [Office development in Visual Studio], data model
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f1c383b5367b2966b9fd082b2d47570264b4d191
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99955776"
---
# <a name="cached-data-in-document-level-customizations"></a>ドキュメントレベルのカスタマイズにおけるキャッシュ データ
  ドキュメントレベルのカスタマイズの主な目的は、Office ドキュメントのビューからデータを分離することです。 データとは、数字やテキストを含む、ドキュメントに格納されている情報を指します。 ビューは、ユーザー インターフェイスと Microsoft Office Word および Microsoft Office Excel のオブジェクト モデルを指します。

 Visual Studio では、データを *データ アイランド* (*データ キャッシュ* とも呼ばれます) として埋め込めるようにすることで、ドキュメントレベルのカスタマイズでビューのデータを分離します。 Word または Excel の起動なしで、データの読み取りや変更を直接行うことができます。 これは、Microsoft Office がインストールされていないサーバー上のドキュメントのデータを変更する必要がある場合に便利です。 Word と Excel は、クライアント環境での使用を目的としています。サーバー上で実行するように設計されていません。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 ドキュメントレベルのカスタマイズの詳細については、「[Office ソリューションの開発の概要 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)」と「[ドキュメントレベルのカスタマイズのアーキテクチャ](../vsto/architecture-of-document-level-customizations.md)」を参照してください。

## <a name="understand-the-cached-data-programming-model"></a>キャッシュされたデータ プログラミング モデルを理解する
 データ アイランドには、ソリューション内の特定の要件を満たす任意のオブジェクトを含めることができます。 これらのオブジェクトには、<xref:System.Data.DataSet> オブジェクト、<xref:System.Data.DataTable> オブジェクト、および <xref:System.Xml.Serialization.XmlSerializer> クラスによってシリアル化できるその他のオブジェクトが含まれます。 詳細については、「[キャッシュ データ](../vsto/caching-data.md)」を参照してください。

 キャッシュされたデータのビューを提供するには、ドキュメント上の Windows フォーム コントロールと *ホスト コントロール* をデータ アイランド内のオブジェクトにバインドできます。 データ アイランドとデータ バインド コントロールの間のデータ バインディングによって、2 つの同期が維持されます。 コントロールに依存しないデータに対する検証コードを追加することもできます。 詳細については、「[Office ソリューションのコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)」を参照してください。

 ホスト コントロールは、Excel および Word オブジェクト モデルのネイティブ オブジェクトの拡張バージョンです。 ネイティブ オブジェクトとは異なり、ホスト コントロールはマネージド データ オブジェクトに直接バインドできます。 詳細については、「[ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)」と「[Office ドキュメントでの Windows フォーム コントロールの概要](../vsto/windows-forms-controls-on-office-documents-overview.md)」を参照してください。

## <a name="access-cached-data-on-the-server"></a>サーバー上のキャッシュされたデータにアクセスする
 ドキュメント内のキャッシュされたデータにアクセスするには、<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> クラスを使用できます。 このクラスは、[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] の一部であり、Excel または Word の実行なしでサーバー上で使用できます。 キャッシュされたデータを変更した後にユーザーがドキュメントを開くと、そのデータにバインドされているすべてのコントロールが自動的に変更に同期され、更新されたデータがユーザーに表示されます。 詳細については、「[サーバー上のドキュメントのデータにアクセスする](../vsto/accessing-data-in-documents-on-the-server.md)」を参照してください。

 サーバー上のデータに書き込むために Excel と Word は必要ありません。クライアントで表示するためにのみ必要です。 Excel と Word をサーバーにインストールする必要もありません。 これにより、スケーラビリティが向上し、データ アイランドを含むドキュメントのバッチ処理を高速に実行できるようになります。

## <a name="data-caching-for-offline-use"></a>オフラインで使用するためのデータ キャッシュ
 データ アイランドにデータを格納すると、オフラインのシナリオに対応できます。 ユーザーが初めてドキュメントを開くかサーバーからドキュメントを要求すると、データ アイランドに最新のデータが格納されます。 データ アイランドがドキュメントにキャッシュされ、その後オフラインで使用できるようになります。 ライブ接続が使用できない場合でも、ユーザー (およびコード) はデータを操作できます。 ユーザーが再接続したときに、データに対する変更をサーバーのデータ ソースに反映させることができます。

## <a name="cached-data-and-custom-xml-parts-compared"></a>キャッシュされたデータとカスタム XML パーツの比較
 カスタム XML パーツは、ドキュメントに XML の任意の部分を格納する方法として、2007 Microsoft Office システムで導入されました。 カスタム XML パーツはデータ キャッシュと同じシナリオの多くで役に立ちますが、データ アイランドとカスタム XML パーツにはいくつかの違いがあります。 カスタム XML パーツの詳細については、「[カスタム XML パーツの概要](../vsto/custom-xml-parts-overview.md)」を参照してください。

 次の表に、相違点と類似点をいくつか示します。

|質問/特性|データ キャッシュ|カスタム XML パーツ|
|-|----------------|----------------------|
|どの Office アプリケーションでこれらを使用できますか?|次のアプリケーションのドキュメントレベルのカスタマイズ:<br /><br /> - Excel<br />- Word|次のアプリケーションのドキュメントレベルおよびアプリケーションレベルのソリューション:<br /><br /> - Excel<br />- PowerPoint<br />- Word|
|どのような種類のデータを格納できますか?|特定の要件を満たす、カスタマイズ アセンブリ内の任意のパブリック オブジェクト。 詳細については、「[キャッシュ データ](../vsto/caching-data.md)」を参照してください。|任意の XML データ。|
|Microsoft Office アプリケーションを起動せずにデータにアクセスできますか?|はい。[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] によって提供される <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> クラスを使用します。|はい。<xref:System.IO.Packaging> 名前空間のクラスを使用するか、Open XML Format SDK を使用します。|

## <a name="see-also"></a>こちらもご覧ください
- [Office ソリューションにおけるデータ](../vsto/data-in-office-solutions.md)
- [Visual Studio での Office ソリューションのアーキテクチャ](../vsto/architecture-of-office-solutions-in-visual-studio.md)
