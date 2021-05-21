---
title: 新しいデータ ソースの追加
description: Visual Studio で新しいデータ ソースを追加します。 データ ソースとは、データ ストアに接続し、データを .NET アプリケーションで使用できるようにする .NET オブジェクトです。
ms.custom: SEO-VS-2020
ms.date: 11/21/2018
ms.topic: how-to
f1_keywords:
- vs.datasource.datasourcefieldspicker
helpviewer_keywords:
- data [Visual Studio], data sources
- data sources
ms.assetid: ed28c625-bb89-4037-bfde-cfa435d182a2
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: b6e42681d2c25162df22af9711d47b71ba155d67
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99867439"
---
# <a name="add-new-data-sources"></a>新しいデータ ソースの追加

:::moniker range="vs-2019"
> [!NOTE]
> この記事で説明する機能は、.NET Framework Windows フォームおよび WPF 開発に適用されます。 Visual Studio 2019 (およびそれ以前のバージョン) では、これらの機能は、WPF と Windowsフォームのどちらについても、.NET Core 開発ではサポートされていません。
:::moniker-end

Visual Studio の .NET データ ツールのコンテキストでは、"*データ ソース*" という用語は、データ ストアに接続し、データを .NET アプリケーションで使用できるようにする .NET オブジェクトを指します。 Visual Studio デザイナーでは、データ ソースの出力を使用して、 **[データ ソース]** ウィンドウからデータベース オブジェクトをドラッグ アンド ドロップしたときにデータをフォームにバインドする定型コードを生成できます。 この種のデータ ソースとして、次のものを使用できます。

- なんらかのデータベースに関連付けられている Entity Framework モデルのクラス。

- なんらかのデータベースに関連付けられているデータセット。

- Windows Communication Foundation (WCF) データ サービスや REST サービスなどのネットワーク サービスを表すクラス。

- SharePoint サービスを表すクラス。

- ソリューション内のクラスまたはコレクション。

> [!NOTE]
> データ バインディング機能、データセット、Entity Framework、LINQ to SQL、WCF、または SharePoint を使用していない場合、"データ ソース" の概念は適用されません。 SQLCommand オブジェクトを使用してデータベースに直接接続し、データベースと直接通信するだけです。

データ ソースは、Windows フォームまたは Windows Presentation Foundation アプリケーションで **データ ソース構成ウィザード** を使用して作成および編集します。 Entity Framework の場合、まずエンティティ クラスを作成し、 **[プロジェクト]**  >  **[新しいデータ ソースの追加]** の順に選択して、このウィザードを開始します (詳細については、この記事で後述します)。

![データ ソース構成ウィザード](../data-tools/media/data-source-configuration-wizard.png)

## <a name="data-sources-window"></a>[データ ソース] ウィンドウ

データ ソースを作成すると、 **[データ ソース]** ツール ウィンドウに表示されます。

> [!TIP]
> **[データ ソース]** ウィンドウを開くには、自分のプロジェクトが開いていることを確認し、**Shift** + **Alt** + **D** キーを押すか、 **[表示]**  >  **[その他のウィンドウ]**  >  **[データ ソース]** の順に選択します。

データ ソースは、 **[データ ソース]** ウィンドウからフォームのデザイン サーフェイスまたはコントロールにドラッグできます。 これにより、データ ストアのデータを表示する定型コードが生成されます。

次の図は、Windows フォームにドロップされたデータセットを示しています。 アプリケーションで **F5** キーを押すと、基になるデータベースのデータがフォームのコントロールに表示されます。

![データ ソースのドラッグ操作](../data-tools/media/raddata-data-source-drag-operation.png)

## <a name="data-source-for-a-database-or-a-database-file"></a>データベースまたはデータベース ファイルのデータ ソース

データベースまたはデータベース ファイルのデータ ソースとして使用するデータセットまたは Entity Framework モデルを作成できます。

### <a name="dataset"></a>データセット

データセットをデータ ソースとして作成するには、 **[プロジェクト]**  >  **[新しいデータ ソースの追加]** の順に選択して、**データ ソース構成ウィザード** を実行します。 データ ソースの種類として **[データベース]** を選択し、プロンプトに従って、新規または既存のデータベース接続、あるいはデータベース ファイルを指定します。

### <a name="entity-classes"></a>エンティティ クラス

Entity Framework モデルをデータ ソースとして作成するには:

1. **Entity Data Model ウィザード** を実行して、エンティティ クラスを作成します。 **[プロジェクト]**  >  **[新しい項目の追加]**  >  **[ADO.NET Entity Data Model]** の順に選択します。

   ![新しい Entity Framework モデル プロジェクト項目](../data-tools/media/raddata-new-entity-framework-model-project-item.png)

1. モデルを生成する方法を選択します。

   ![エンティティ データ モデル ウィザード](../data-tools/media/raddata-entity-data-model-wizard.png)

1. モデルをデータ ソースとして追加します。 **[オブジェクト]** カテゴリを選択すると、生成されたクラスが **データ ソース構成ウィザード** に表示されます。

   ![エンティティ クラスが表示されたデータ ソース構成ウィザード](../data-tools/media/raddata-data-source-configuration-wizard-with-entity-classes.png)

## <a name="data-source-for-a-service"></a>サービスのデータ ソース

サービスからデータ ソースを作成するには、**データ ソース構成ウィザード** を実行し、データ ソースの種類として **[サービス]** を選択します。 これは、 **[サービス参照の追加]** ダイアログ ボックスへのショートカットです。ここには、**ソリューション エクスプローラー** でプロジェクトを右クリックして **[サービス参照の追加]** を選択することでアクセスすることもできます。

サービスからデータ ソースを作成すると、Visual Studio によりサービス参照がプロジェクトに追加されます。 また、サービスから返されるオブジェクトに対応するプロキシ オブジェクトも作成されます。 たとえば、データセットを返すサービスは、プロジェクト内でデータセットとして表現され、特定の型を返すサービスは、プロジェクト内で、返される型として表現されます。

次の種類のサービスからデータ ソースを作成できます。

- [WCF Data Services](/dotnet/framework/data/wcf/wcf-data-services-overview)

- [WCF サービス](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)

- Web サービス

    > [!NOTE]
    > **[データ ソース]** ウィンドウに表示される項目は、サービスから返されるデータによって異なります。 サービスによっては、**データ ソース構成ウィザード** でバインドできるオブジェクトを作成するための十分な情報を提供しないものもあります。 たとえば、サービスから型指定されていないデータセットが返される場合、ウィザードを完了しても、 **[データ ソース]** ウィンドウには項目が表示されません。 これは、型指定されていないデータセットからはスキーマが提供されず、したがってウィザードでデータ ソースを作成するための十分な情報が得られないためです。

## <a name="data-source-for-an-object"></a>オブジェクトのデータ ソース

1 つ以上のパブリック プロパティを公開する任意のオブジェクトからデータ ソースを作成できます。それには、**データ ソース構成ウィザード** を実行し、データ ソースの種類として **[オブジェクト]** を選択します。 オブジェクトのすべてのパブリック プロパティは、**[データ ソース]** ウィンドウに表示されます。 Entity Framework を使用しており、モデルが生成されている場合、ここには、自分のアプリケーションのデータ ソースであるエンティティ クラスが表示されます。

**[データ オブジェクトの選択]** ページで、ツリー ビューのノードを展開して、バインド先のオブジェクトを見つけます。 ツリー ビューには、プロジェクトのノードと、プロジェクトによって参照されるアセンブリおよび他のプロジェクトのノードが含まれています。

ツリー ビューに表示されていないアセンブリまたはプロジェクトのオブジェクトにバインドする場合は、 **[参照の追加]** をクリックし、 **[参照の追加] ダイアログ ボックス** を使用して、アセンブリまたはプロジェクトへの参照を追加します。 参照を追加すると、そのアセンブリまたはプロジェクトがツリー ビューに追加されます。

> [!NOTE]
> オブジェクトがツリー ビューに表示される前に、オブジェクトを含むプロジェクトをビルドすることが必要な場合があります。

> [!NOTE]
> ドラッグ アンド ドロップ データ バインディングをサポートするには、<xref:System.ComponentModel.ITypedList> または <xref:System.ComponentModel.IListSource> インターフェイスを実装するオブジェクトに既定のコンストラクターが必要です。 これがない場合、Visual Studio はデータ ソース オブジェクトをインスタンス化できないので、デザイン サーフェイスに項目をドラッグするとエラーが表示されます。

## <a name="data-source-for-a-sharepoint-list"></a>SharePoint リストのデータ ソース

**データ ソース構成ウィザード** を実行し、データ ソースの種類として **[SharePoint]** を選択すると、SharePoint リストからデータ ソースを作成できます。 SharePoint では、WCF Data Services を介してデータを公開します。そのため、SharePoint データ ソースの作成は、サービスからのデータ ソースの作成と同じです。 **データ ソース構成ウィザード** で **[SharePoint]** 項目をクリックすると、**[サービス参照の追加]** ダイアログ ボックスが表示されます。このダイアログ ボックスで、SharePoint サーバーを指定することにより SharePoint データ サービスに接続します。 これには SharePoint SDK が必要です。

## <a name="see-also"></a>関連項目

- [.NET 用の Visual Studio データ ツール](../data-tools/visual-studio-data-tools-for-dotnet.md)
