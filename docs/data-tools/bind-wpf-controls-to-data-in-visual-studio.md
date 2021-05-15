---
title: データへの WPF コントロールのバインド - パート 1
description: データに WPF コントロールをバインドします。 これらのデータバインド コントロールを作成するには、Visual Studio で [データ ソース] ウィンドウから WPF デザイナーに項目をドラッグします。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- data [WPF], displaying
- WPF, data binding in Visual Studio
- WPF data binding [Visual Studio]
- displaying data, WPF
- WPF [WPF], data
- WPF Designer, data binding
- data binding, WPF
ms.assetid: e05a1e0c-5082-479d-bbc9-d395b0bc6580
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 137d8970ebfc70dcf102fa70d7bcf18d81677535
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99859269"
---
# <a name="bind-wpf-controls-to-data-in-visual-studio"></a>Visual Studio でデータに WPF コントロールをバインドする

データを [!INCLUDE[TLA#tla_titlewinclient](../data-tools/includes/tlasharptla_titlewinclient_md.md)] コントロールにバインドすることで、アプリケーションのユーザーに対してデータを表示できます。 これらのデータバインド コントロールを作成するには、Visual Studio で **[データ ソース]** ウィンドウから [!INCLUDE[wpfdesigner_current_short](../data-tools/includes/wpfdesigner_current_short_md.md)]に項目をドラッグします。 このトピックでは、データ バインド [!INCLUDE[TLA#tla_titlewinclient](../data-tools/includes/tlasharptla_titlewinclient_md.md)] アプリケーションの作成に使用できる最も一般的なタスク、ツール、およびクラスについて説明します。

Visual Studio でのデータバインド コントロールの作成方法に関する一般的な情報については、「[Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)」をご覧ください。 [!INCLUDE[TLA#tla_titlewinclient](../data-tools/includes/tlasharptla_titlewinclient_md.md)] データ バインディングの詳細については、「[データ バインディングの概要](/dotnet/desktop-wpf/data/data-binding-overview)」を参照してください。

## <a name="tasks-involved-in-binding-wpf-controls-to-data"></a>データへの WPF コントロールのバインドに関連するタスク

次の表に、**[データ ソース]** ウィンドウから [!INCLUDE[wpfdesigner_current_short](../data-tools/includes/wpfdesigner_current_short_md.md)] に項目をドラッグすることで実行できるタスクを示します。

|タスク|詳細情報|
|----------| - |
|データ バインド コントロールを作成する。<br /><br /> 既存のコントロールをデータにバインドする。|[データセットへの WPF コントロールのバインド](../data-tools/bind-wpf-controls-to-a-dataset.md)|
|親子のリレーションシップを持つ関連データを表示するコントロールを作成する。あるコントロールの親データ レコードを選択すると、その選択レコードに関連する子データが別のコントロールに表示されるようにします。|[WPF アプリケーションで関連データを表示する](../data-tools/display-related-data-in-wpf-applications.md)|
|あるテーブルの外部キー フィールドの値に基づいて、別のテーブルの情報を表示する *ルックアップ テーブル* を作成する。|[WPF アプリケーションでルックアップ テーブルを作成する](../data-tools/create-lookup-tables-in-wpf-applications.md)|
|コントロールをデータベース内のイメージにバインドする。|[データベースの画像にコントロールをバインドする](../data-tools/bind-controls-to-pictures-from-a-database.md)|

## <a name="valid-drop-targets"></a>有効なドロップ ターゲット

**[データ ソース]** ウィンドウ内の項目は、[!INCLUDE[wpfdesigner_current_short](../data-tools/includes/wpfdesigner_current_short_md.md)] の有効なドロップ ターゲットにのみドラッグできます。 有効なドロップ ターゲットの種類は、主にコンテナーとコントロールの 2 つです。 コンテナーとは、通常はコントロールを含むユーザー インターフェイス要素です。 たとえば、グリッドやウィンドウはコンテナーです。

## <a name="generated-xaml-and-code"></a>生成される XAML およびコード

**[データ ソース]** ウィンドウから [!INCLUDE[wpfdesigner_current_short](../data-tools/includes/wpfdesigner_current_short_md.md)]に項目をドラッグすると、Visual Studio によって、新しいデータバインド コントロールを定義する (または、既存のコントロールをデータ ソースにバインドする) [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] が生成されます。 一部のデータ ソースでは、Visual Studio によって、データ ソースにデータを入力するコードも分離コード ファイルに生成されます。

次の表に、Visual Studio で **[データ ソース]** ウィンドウの各データ ソースに対して生成される [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] とコードを示します。

| データ ソース | コントロールをデータ ソースにバインドする XAML の生成 | データ ソースにデータを読み込むコードの生成 |
| - | - | - |
| データセット | はい | はい |
| [!INCLUDE[adonet_edm](../data-tools/includes/adonet_edm_md.md)] | はい | はい |
| サービス | はい | いいえ |
| Object | はい | いいえ |

### <a name="datasets"></a>データセット

**[データ ソース]** ウィンドウからデザイナーにテーブルまたは列をドラッグすると、Visual Studio によって、次の処理を行う [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] が生成されます。

- 項目をドラッグした先のコンテナーのリソースに、データセットと新しい <xref:System.Windows.Data.CollectionViewSource> を追加する。 <xref:System.Windows.Data.CollectionViewSource> は、データセットのデータの移動と表示に使用できるオブジェクトです。

- コントロールのデータ バインディングを作成する。 デザイナーの既存のコントロールに項目をドラッグすると、XAML により、その項目にコントロールがバインドされます。 コンテナーに項目をドラッグすると、XAML により、ドラッグした項目に対して選択されたコントロールが作成され、そのコントロールが項目にバインドされます。 コントロールは、新しい <xref:System.Windows.Controls.Grid> 内に作成されます。

Visual Studio は、分離コード ファイルに次の変更も加えます。

- コントロールを格納する <xref:System.Windows.FrameworkElement.Loaded> 要素の [!INCLUDE[TLA2#tla_ui](../data-tools/includes/tla2sharptla_ui_md.md)] イベント ハンドラーを作成する。 イベント ハンドラーは、テーブルにデータを読み込み、コンテナーのリソースから <xref:System.Windows.Data.CollectionViewSource> を取得して、最初のデータ項目を現在の項目にします。 <xref:System.Windows.FrameworkElement.Loaded> イベント ハンドラーが既に存在する場合は、Visual Studio によって、このコードがその既存のイベント ハンドラーに追加されます。

### <a name="entity-data-models"></a>エンティティ データ モデル

**[データ ソース]** ウィンドウからデザイナーにエンティティまたはエンティティ プロパティをドラッグすると、Visual Studio によって、次の処理を行う [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] が生成されます。

- 項目をドラッグした先のコンテナーのリソースに、新しい <xref:System.Windows.Data.CollectionViewSource> を追加する。 <xref:System.Windows.Data.CollectionViewSource> は、エンティティのデータの移動と表示に使用できるオブジェクトです。

- コントロールのデータ バインディングを作成する。 デザイナーの既存のコントロールに項目をドラッグすると、[!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] により、その項目にコントロールがバインドされます。 コンテナーに項目をドラッグすると、[!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] により、ドラッグした項目に対して選択されたコントロールが作成され、そのコントロールが項目にバインドされます。 コントロールは、新しい <xref:System.Windows.Controls.Grid> 内に作成されます。

Visual Studio は、分離コード ファイルに次の変更も加えます。

- デザイナーにドラッグされたエンティティ (または、デザイナーにドラッグされたプロパティを含むエンティティ) のクエリを返す新しいメソッドを追加する。 新しいメソッドの名前は `Get<EntityName>Query` です。`\<EntityName>` はエンティティの名前です。

- コントロールを格納する <xref:System.Windows.FrameworkElement.Loaded> 要素の [!INCLUDE[TLA2#tla_ui](../data-tools/includes/tla2sharptla_ui_md.md)] イベント ハンドラーを作成する。 このイベント ハンドラーは、`Get<EntityName>Query` メソッドを呼び出してエンティティにデータを入力し、コンテナーのリソースから <xref:System.Windows.Data.CollectionViewSource> を取得して、最初のデータ項目を現在の項目にします。 <xref:System.Windows.FrameworkElement.Loaded> イベント ハンドラーが既に存在する場合は、Visual Studio によって、このコードがその既存のイベント ハンドラーに追加されます。

### <a name="services"></a>サービス

**[データ ソース]** ウィンドウからデザイナーにサービス オブジェクトまたはプロパティをドラッグすると、Visual Studio によって、データバインド コントロールを作成する (または、既存のコントロールをオブジェクトまたはプロパティにバインドする) [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] が生成されます。 ただし、プロキシ サービス オブジェクトにデータを入力するコードは生成されません。 このコードは、ユーザーが手動で記述する必要があります。 これを行う方法を示す例については、「[WCF データ サービスへの WPF コントロールのバインド](../data-tools/bind-wpf-controls-to-a-wcf-data-service.md)」をご覧ください。

Visual Studio は、次の処理を行う XAML を生成します。

- 項目をドラッグした先のコンテナーのリソースに、新しい <xref:System.Windows.Data.CollectionViewSource> を追加する。 <xref:System.Windows.Data.CollectionViewSource> は、サービスから返されるオブジェクトのデータの移動と表示に使用できるオブジェクトです。

- コントロールのデータ バインディングを作成する。 デザイナーの既存のコントロールに項目をドラッグすると、[!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] により、その項目にコントロールがバインドされます。 コンテナーに項目をドラッグすると、[!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] により、ドラッグした項目に対して選択されたコントロールが作成され、そのコントロールが項目にバインドされます。 コントロールは、新しい <xref:System.Windows.Controls.Grid> 内に作成されます。

### <a name="objects"></a>オブジェクト

**[データ ソース]** ウィンドウからデザイナーにオブジェクトまたはプロパティをドラッグすると、Visual Studio によって、データバインド コントロールを作成する (または、既存のコントロールをオブジェクトまたはプロパティにバインドする) [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] が生成されます。 ただし、オブジェクトにデータを入力するコードは生成されません。 このコードは、ユーザーが手動で記述する必要があります。

> [!NOTE]
> カスタム クラスはパブリックである必要があり、既定では、パラメーターなしのコンストラクターが必要です。 構文に "ドット" が含まれる入れ子になったクラスにすることはできません。 詳細については、「[WPF における XAML とカスタム クラス](/dotnet/framework/wpf/advanced/xaml-and-custom-classes-for-wpf)」をご覧ください。

Visual Studio によって、次の処理を行う [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] が生成されます。

- 項目をドラッグした先のコンテナーのリソースに、新しい <xref:System.Windows.Data.CollectionViewSource> を追加する。 <xref:System.Windows.Data.CollectionViewSource> は、オブジェクトのデータの移動と表示に使用できるオブジェクトです。

- コントロールのデータ バインディングを作成する。 デザイナーの既存のコントロールに項目をドラッグすると、XAML により、その項目にコントロールがバインドされます。 コンテナーに項目をドラッグすると、XAML により、ドラッグした項目に対して選択されたコントロールが作成され、そのコントロールが項目にバインドされます。 コントロールは、新しい <xref:System.Windows.Controls.Grid> 内に作成されます。

## <a name="see-also"></a>関連項目

- [Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)
