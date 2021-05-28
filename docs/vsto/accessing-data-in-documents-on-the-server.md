---
title: サーバー上のドキュメント内のデータにアクセスする
description: Microsoft Office Word や Microsoft Office Excel のオブジェクト モデルを使用せずに、ドキュメント レベルのカスタマイズ内のデータに対してプログラミングを行う方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Office development in Visual Studio], accessing on server
- data access [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 0df6aef3c83d66b84f569e85e953fde8a3f0e16c
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826773"
---
# <a name="access-data-in-documents-on-the-server"></a>サーバー上のドキュメント内のデータにアクセスする
  Microsoft Office Word や Microsoft Office Excel のオブジェクト モデルを使用せずに、ドキュメント レベルのカスタマイズ内のデータに対してプログラミングを行うことができます。 つまり、Word や Excel がインストールされていないサーバー上のドキュメントに含まれているデータにアクセスできるということです。 たとえば、サーバー上 (たとえば、[!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] ページ内) のコードによって、ドキュメント内のデータをカスタマイズし、カスタマイズされたドキュメントをエンド ユーザーに送信することもできます。 エンド ユーザーがドキュメントを開くと、ソリューション アセンブリ内のデータ バインド コードによって、カスタマイズされたデータがドキュメントにバインドされます。 これが可能なのは、ドキュメント内のデータがユーザー インターフェイスから分離されているためです。 詳細については、「[ドキュメント レベルのカスタマイズのキャッシュ データ](../vsto/cached-data-in-document-level-customizations.md)」を参照してください。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="cache-data-for-use-on-a-server"></a>サーバーで使用するためのデータをキャッシュする
 データ オブジェクトをドキュメント内にキャッシュするには、デザイン時にオブジェクトを <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> 属性でマークするか、実行時にホスト項目の `StartCaching` メソッドを使用します。 データ オブジェクトをドキュメント内にキャッシュすると、[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] によってオブジェクトがシリアル化され、ドキュメント内に格納される XML 文字列になります。 オブジェクトをキャッシュするには、オブジェクトが特定の要件を満たしている必要があります。 詳細については、「[キャッシュ データ](../vsto/caching-data.md)」を参照してください。

 サーバー側のコードでは、データ キャッシュ内の任意のデータ オブジェクトを操作できます。 キャッシュされたデータ インスタンスにバインドされているコントロールはユーザー インターフェイスと同期されるため、データに対して行われたすべてのサーバー側の変更は、クライアントでドキュメントを開いたときに自動的に表示されます。

## <a name="access-data-in-the-cache"></a>キャッシュ内のデータにアクセスする
 キャッシュ内のデータには、Office の外部のアプリケーション (たとえば、コンソール アプリケーション、Windows フォーム アプリケーション、Web ページなど) からアクセスすることができます。 キャッシュされたデータにアクセスするアプリケーションは、完全に信頼されている必要があります。部分信頼の Web アプリケーションでは、Office ドキュメントにキャッシュされたデータに対して、挿入、取得、変更の操作を行うことができません。

 データ キャッシュには、<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> クラスの <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A> プロパティによって公開されるコレクションの階層を通じてアクセスできます。

- <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A> プロパティは、ドキュメント レベルのカスタマイズ内にキャッシュされているすべてのデータを格納した <xref:Microsoft.VisualStudio.Tools.Applications.CachedData> を返します。

- <xref:Microsoft.VisualStudio.Tools.Applications.CachedData> にはそれぞれ、1 つまたは複数の <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataHostItem> オブジェクトが格納されます。 <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataHostItem> には、1 つのクラス内で定義されている、すべてのキャッシュ データ オブジェクトが格納されます。

- <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataHostItem> にはそれぞれ、1 つまたは複数の <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem> オブジェクトが格納されます。 <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem> は、1 つのキャッシュ データ オブジェクトを表します。

  次のコード例は、Excel ブック プロジェクトの `Sheet1` クラス内のキャッシュされた文字列にアクセスする方法を示したものです。 この例は、<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.Save%2A> メソッド用に提供されている、より長い例の一部分です。

  :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_ServerDocument/Form1.cs" id="Snippet12":::
  :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_ServerDocument/Form1.vb" id="Snippet12":::

## <a name="modify-data-in-the-cache"></a>キャッシュ内のデータを変更する
 キャッシュされたデータ オブジェクトに変更を加えるには、通常、次の手順を実行します。

1. キャッシュされたオブジェクトの XML 表現を、オブジェクトの新規インスタンスへと逆シリアル化します。 XML にアクセスするには、キャッシュされたデータ オブジェクトを表す <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem> の <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem.Xml%2A> プロパティを使用します。

2. このコピーに変更を加えます。

3. 次のいずれかのオプションを使用して、変更されたオブジェクトをデータ キャッシュへと再びシリアル化します。

    - 変更を自動的にシリアル化したい場合は、<xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem.SerializeDataInstance%2A> メソッドを使用します。 このメソッドでは、データ キャッシュ内の、<xref:System.Data.DataSet>、<xref:System.Data.DataTable> および型指定されたデータセット オブジェクトをシリアル化するために、**DiffGram** 形式が使用されます。 **DiffGram** 形式を使用することで、オフライン ドキュメントのデータ キャッシュに対する変更がサーバーに正しく送信されます。

    - キャッシュされたデータを変更するために独自のシリアル化を実行したい場合は、<xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem.Xml%2A> プロパティに操作を直接記述することができます。 <xref:System.Data.Common.DataAdapter> を使用してデータベースを更新し、<xref:System.Data.DataSet>、<xref:System.Data.DataTable>、または型指定されたデータセット内のデータに加えられた変更を反映する場合は、**DiffGram** 形式を指定してください。 そうしなかった場合、<xref:System.Data.Common.DataAdapter> では、既存の行を変更するのではなく、新しい行を追加することでデータベースが更新されます。

### <a name="modify-data-without-deserializing-the-current-value"></a>現在の値を逆シリアル化せずにデータを変更する
 場合によっては、最初に現在の値を逆シリアル化せずに、キャッシュされたオブジェクトの値を変更する必要が生じることもあります。 たとえば、単純型のオブジェクト (文字列や整数など) の値を変更する場合や、サーバー上のドキュメントにキャッシュされた <xref:System.Data.DataSet> を初期化する場合には、この操作を行う可能性があります。 このような場合には、キャッシュされたオブジェクトの現在の値を最初に逆シリアル化せずに、<xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem.SerializeDataInstance%2A> メソッドを使用します。

 次のコード例は、Excel ブック プロジェクトの `Sheet1` クラス内のキャッシュされた文字列の値を変更する方法を示したものです。 この例は、<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.Save%2A> メソッド用に提供されている、より長い例の一部分です。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_ServerDocument/Form1.cs" id="Snippet11":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_ServerDocument/Form1.vb" id="Snippet11":::

### <a name="modify-null-values-in-the-data-cache"></a>データ キャッシュ内の null 値を変更する
 ドキュメントを保存して閉じる際、値が **null** のオブジェクトはデータ キャッシュに格納されません。 この制限事項は、キャッシュされたデータを変更する際に、次のような影響をもたらします。

- データ キャッシュ内のオブジェクトを 1 つでも **null** 値に設定すると、ドキュメントを開くときにデータ キャッシュ内のすべてのオブジェクトが自動的に **null** に設定され、ドキュメントを保存して閉じるときにはデータ キャッシュ全体がクリアされます。 つまり、キャッシュされたオブジェクトがすべてデータ キャッシュから削除され、<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A> コレクションは空になります。

- データ キャッシュ内に **null** オブジェクトがあるソリューションをビルドする場合、ドキュメントが初めて開かれる前に <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> クラスを使ってそれらのオブジェクトを初期化したい場合は、データ キャッシュ内のすべてのオブジェクトを初期化する必要があります。 一部のオブジェクトだけを初期化すると、ドキュメントを開いたときにすべてのオブジェクトが **null** に設定され、ドキュメントを保存して閉じたときにはデータ キャッシュ全体がクリアされます。

## <a name="access-typed-datasets-in-the-cache"></a>キャッシュ内の型指定されたデータセットにアクセスする
 Office ソリューションと、Office の外部のアプリケーション (Windows フォーム アプリケーションや [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] プロジェクトなど) の両方から、型指定されたデータセットのデータにアクセスする場合は、両方のプロジェクトで参照される別のアセンブリに、型指定されたデータセットを定義する必要があります。 **データ ソース構成** ウィザードまたは **データセット デザイナー** を使って、型指定されたデータセットを各プロジェクトに追加した場合、.NET Framework では、2 つのプロジェクト内の型指定されたデータセットが異なる型として扱われます。 型指定されたデータセットの作成について詳しくは、「[Visual Studio でデータセットを作成および構成する](../data-tools/create-and-configure-datasets-in-visual-studio.md)」をご覧ください。

## <a name="see-also"></a>こちらもご覧ください

- [サーバー上のドキュメント内のデータにアクセスする](../vsto/accessing-data-in-documents-on-the-server.md)
- [ドキュメント レベルのカスタマイズのキャッシュ データ](../vsto/cached-data-in-document-level-customizations.md)