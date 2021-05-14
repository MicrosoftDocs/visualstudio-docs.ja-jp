---
title: データにコントロールをバインドする
description: Visual Studio でデータにコントロールをバインドします。 [データ ソース] ウィンドウから項目をドラッグして、データバインド コントロールを作成します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- data, displaying
- data sources, displaying data
- Data Sources window
- displaying data
ms.assetid: be8b6623-86a6-493e-ab7a-050de4661fd6
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: a237d07af14cd6f31af300eff050c8952fd9840e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99859347"
---
# <a name="bind-controls-to-data-in-visual-studio"></a>Visual Studio でのデータへのコントロールのバインド

データをコントロールにバインドすることで、アプリケーションのユーザーに対してデータを表示できます。 これらのデータバインド コントロールを作成するには、Visual Studio で **[データ ソース]** ウィンドウからデザイン サーフェイスまたはサーフェイス上のコントロールに項目をドラッグします。

ここでは、データ バインディング コントロールを作成するために使用できるデータ ソースについて説明します。 また、データ バインディングに関連する一般的なタスクについても説明します。 データバインド コントロールの作成方法の詳細については、「[Visual Studio でのデータへの Windows フォーム コントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)」および「[Visual Studio でデータに WPF コントロールをバインドする](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)」をご覧ください。

## <a name="data-sources"></a>データ ソース

データ バインディングのコンテキストでは、データ ソースは、ユーザー インターフェイスにバインドできるメモリ内のデータを表します。 具体的に言うと、データ ソースは、Entity Framework クラス、データセット、.NET プロキシ オブジェクトにカプセル化されたサービス エンドポイント、LINQ to SQL クラス、あるいは任意の .NET オブジェクトまたはコレクションです。 一部のデータ ソースでは、**[データ ソース]** ウィンドウから項目をドラッグすることによりデータ バインディング コントロールを作成できますが、その他のデータ ソースではできません。 サポートされるデータ ソースを次の表に示します。

| データ ソース | **Windows フォーム デザイナー** でのドラッグ アンド ドロップのサポート | **WPF デザイナー** でのドラッグ アンド ドロップのサポート | **Silverlight デザイナー** でのドラッグ アンド ドロップのサポート |
| - | - | - | - |
| データセット | はい | はい | いいえ |
| エンティティ データ モデル | 可<sup>1</sup> | はい | はい |
| LINQ to SQL クラス | いいえ<sup>2</sup> | いいえ<sup>2</sup> | いいえ<sup>2</sup> |
| サービス ([!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)]、WCF サービス、および Web サービスを含む) | はい | はい | はい |
| Object | はい | はい | はい |
| SharePoint | はい | はい | はい |

1. **Entity Data Model** ウィザードを使用してモデルを生成し、それらのオブジェクトをデザイナーにドラッグします。

2. LINQ to SQL クラスは、**[データ ソース]** ウィンドウに表示されません。 ただし、LINQ to SQL クラスに基づく新しいオブジェクト データ ソースを追加し、それらのオブジェクトをデザイナーにドラッグして、データ バインディング コントロールを作成できます。 詳細については、[LINQ to SQL クラスを作成する方法 (O/R デザイナー) のチュートリアル](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)をご覧ください。

## <a name="data-sources-window"></a>[データ ソース] ウィンドウ

データ ソースは、**[データ ソース]** ウィンドウ内の項目としてプロジェクトで利用できます。 このウィンドウは、フォームのデザイン サーフェイスがプロジェクトのアクティブ ウィンドウである場合に表示されます。また、 **[表示]**  >  **[その他のウィンドウ]**  >  **[データ ソース]** を選択して開くこともできます (プロジェクトが開いている場合)。 このウィンドウから項目をドラッグして、基になるデータにバインドされたコントロールを作成できます。また、右クリックしてデータ ソースを構成することもできます。

![[データ ソース] ウィンドウ](../data-tools/media/raddata-data-sources-window.png)

**[データ ソース]** ウィンドウに表示されるデータ型ごとに、項目をデザイナーにドラッグしたときに既定のコントロールが作成されます。 **[データ ソース]** ウィンドウから項目をドラッグする前に、作成されるコントロールを変更できます。 詳細については、「[[データ ソース] ウィンドウからドラッグしたときに作成されるコントロールを設定する](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)」をご覧ください。

## <a name="tasks-involved-in-binding-controls-to-data"></a>データへのコントロールのバインドに関連するタスク

次の表に、コントロールをデータにバインドするために実行する最も一般的なタスクを示します。

|タスク|詳細情報|
|----------| - |
|**[データ ソース]** ウィンドウを開く。|エディターでデザイン サーフェイスを開き、 **[表示]**  >  **[データ ソース]** を選択する。|
|プロジェクトにデータ ソースを追加する。|[新しいデータ ソースの追加](../data-tools/add-new-data-sources.md)|
|**[データ ソース]** ウィンドウからデザイナーに項目をドラッグしたときに作成されるコントロールを設定する。|[[データ ソース] ウィンドウからドラッグしたときに作成されるコントロールを設定する](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)|
|**[データ ソース]** ウィンドウの項目に関連付けられるコントロールのリストを変更する。|[[データ ソース] ウィンドウにカスタム コントロールを追加する](../data-tools/add-custom-controls-to-the-data-sources-window.md)|
|データ バインド コントロールを作成する。|[Visual Studio でのデータへの Windows フォーム コントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)<br /><br /> [Visual Studio でデータに WPF コントロールをバインドする](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)|
|オブジェクトまたはコレクションにバインドする。|[Visual Studio でオブジェクトをバインドする](../data-tools/bind-objects-in-visual-studio.md)|
|UI に表示されるデータをフィルター処理する。|[Windows フォーム アプリケーションのデータのフィルター処理および並べ替えを行う](../data-tools/filter-and-sort-data-in-a-windows-forms-application.md)|
|コントロールのキャプションをカスタマイズする。|[Visual Studio がデータ バインド コントロールのキャプションを作成する方法をカスタマイズする](../data-tools/customize-how-visual-studio-creates-captions-for-data-bound-controls.md)|

## <a name="see-also"></a>関連項目

- [.NET 用の Visual Studio データ ツール](../data-tools/visual-studio-data-tools-for-dotnet.md)
- [Windows フォームでのデータ バインディング](/dotnet/framework/winforms/windows-forms-data-binding)
