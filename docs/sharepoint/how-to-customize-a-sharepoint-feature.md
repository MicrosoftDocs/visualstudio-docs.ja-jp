---
title: '方法: SharePoint フィーチャーをカスタマイズする | Microsoft Docs'
description: Visual Studio で SharePoint フィーチャーをカスタマイズします。 ソリューション エクスプローラーまたは SharePoint パッケージ エクスプローラーで新しいフィーチャーを追加すると、フィーチャー デザイナーが開きます。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.RAD.FeatureDesigner.SwitchView
- VS.SharePointTools.RAD.featureDesigner.Manifest
- VS.SharePointTools.RAD.FeatureDesignerProperties
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, features
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 0604b6497920e1e6df0a792ce758519f425ac155
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99959949"
---
# <a name="how-to-customize-a-sharepoint-feature"></a>方法: SharePoint フィーチャーをカスタマイズする
  SharePoint フィーチャーは、Visual Studio のフィーチャー デザイナーを使用して作成およびカスタマイズできます。 たとえば、フィーチャー スコープを設定し、その他のフィーチャーを依存関係として追加することができます。 既定では、ソリューション エクスプローラーまたは SharePoint パッケージ エクスプローラーで新しいフィーチャーを追加すると、フィーチャー デザイナーが開きます。

## <a name="opening-the-feature-designer"></a>フィーチャー デザイナーを開く
 フィーチャー デザイナーを使用して、SharePoint プロジェクト項目をフィーチャーに追加または削除できます。

#### <a name="to-open-the-feature-designer"></a>フィーチャー デザイナーを開くには

1. **ソリューション エクスプローラー** で、 **[フィーチャー]** を展開します。

2. *Feature1* 項目をダブルクリックするか、*Feature1* 項 目のショートカット メニューを開いて、 **[デザイナーの表示]** を選択します。

## <a name="view-the-packaged-manifest-file"></a>パッケージ化されたマニフェスト ファイルを表示する
 フィーチャー デザイナーを使用して、フィーチャーのパッケージ化されたマニフェスト ファイル (*feature.xml*) を変更および生成できます。 その後、Visual Studio でこのファイルの XML コードを表示できます。

#### <a name="to-view-the-packaged-manifest-file"></a>パッケージ化されたマニフェスト ファイルを表示するには

1. **フィーチャー デザイナー** で、 **[マニフェスト]** タブを選択します。

#### <a name="to-view-the-packaged-manifest-file-by-using-solution-explorer"></a>ソリューション エクスプローラーを使用してパッケージ化されたマニフェスト ファイルを表示するには

1. **ソリューション エクスプローラー** で、 **[すべてのファイルを表示]** アイコンを選択します。

2. [Features] を展開し、[FeatureName]、[FeatureName.feature] の順に展開して、 *\<FeatureName>.Template.xml* ファイルを開きます。

    > [!NOTE]
    > フィーチャー テンプレートのマニフェスト XML ファイルを開くと、ファイルは自動的に検証されます。[エラー一覧] ウィンドウに表示される警告は無視してかまいません。

## <a name="change-the-manifest-template"></a>マニフェスト テンプレートを変更する
 フィーチャー マニフェスト ファイルの XML コードは、Visual Studio の XML エディターまたは [マニフェスト テンプレート] ウィンドウで変更できます。 XML コードに対する変更は、フィーチャーのパッケージ化されたマニフェスト ファイルにマージされます。 たとえば、フィーチャー プロパティをカスタマイズするためにマニフェスト テンプレートを変更する場合があります。

#### <a name="to-change-the-manifest-template-by-using-the-xml-editor"></a>XML エディターを使用してマニフェスト テンプレートを変更するには

1. **フィーチャー デザイナー** で **[マニフェスト]** タブを選択し、 **[編集オプション]** ノードを展開して、 **[XML エディターで開く]** リンクをクリックします。

     XML への変更は、パッケージ化されたマニフェスト ファイルにマージされます。

#### <a name="to-change-the-manifest-template-by-using-the-manifest-template-pane"></a>[マニフェスト テンプレート] ウィンドウを使用してマニフェスト テンプレートを変更するには

1. **フィーチャー デザイナー** で **[マニフェスト]** タブを選択します。 **[編集オプション]** ノードを展開し、[マニフェスト テンプレート] ウィンドウに表示される XML を変更します。

     XML への変更は、 **[パッケージ マニフェストのプレビュー]** ウィンドウに表示されます。

## <a name="overwrite-the-packaged-manifest-file"></a>パッケージ化されたマニフェスト ファイルを上書きする
 フィーチャー デザイナーを無効にして、*feature.xml* ファイルを手動で作成することができます。 この手順を初めて実行すると、フィーチャー デザイナーの現在の設定がフィーチャー テンプレート XML ファイルに保存されます。 その後、XML コードを変更または上書きできます。

> [!NOTE]
> フィーチャー デザイナーが無効になっているときに、XML ファイル内の SharePoint プロジェクト項目を追加または削除した場合、これらのプロジェクト項目はパッケージ化されません。

#### <a name="to-overwrite-packaged-manifest-file-by-disabling-the-designer"></a>デザイナーを無効にすることでパッケージ化されたマニフェスト ファイルを上書きするには

1. **フィーチャー デザイナー** で、 **[マニフェスト]** タブを選択します。

2. **[編集オプション]** ノードを展開し、 **[生成された XML を上書きし、XML エディターでマニフェストを編集します]** リンクを選択し、 **[はい]** ボタンを選択します。

     現在のパッケージ化されたマニフェスト ファイルでテンプレートが更新されます。

## <a name="enable-the-feature-designer"></a>フィーチャー デザイナーを有効にする
 フィーチャー デザイナーを再度有効にして、*feature.xml* ファイルをカスタマイズすることができます。

#### <a name="to-re-enable-the-designer"></a>デザイナーを再度有効にするには

1. **フィーチャー デザイナー** で、 **[マニフェストの編集を破棄してデザイナーを再有効化します]** リンクを選択し、 **[はい]** ボタンを選択します。

2. テンプレートは元のテキストで更新され、XML に対する変更はすべて失われます。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
