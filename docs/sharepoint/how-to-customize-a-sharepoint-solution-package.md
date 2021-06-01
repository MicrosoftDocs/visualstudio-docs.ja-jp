---
title: '方法: SharePoint ソリューション パッケージをカスタマイズする | Microsoft Docs'
description: SharePoint ソリューション パッケージ (.wsp) を作成およびカスタマイズするには、パッケージ デザイナーを使用します。 パッケージ化されたマニフェスト ファイルを表示または上書きします。 マニフェスト テンプレートを変更します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.RAD.PackageDesignerAdvanced
- VS.SharePointTools.RAD.PackageDesigner.Manifest
- VS.SharePointTools.RAD.PackageDesignerProperties
- VS.SharePointTools.RAD.PackageDesigner.SwitchView
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, packages
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 149e99a3ba86f1eec22d90618abfd8972ed68e97
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99959897"
---
# <a name="how-to-customize-a-sharepoint-solution-package"></a>方法: SharePoint ソリューション パッケージをカスタマイズする
  パッケージ デザイナーを使用して、パッケージ ( *.wsp*) を作成およびカスタマイズできます。 たとえば、SharePoint プロジェクトの項目と機能を追加したり、ソリューションの配置時に Web サーバーをリセットするかどうかを指定したり、配置サーバーの種類を設定したりできます。

## <a name="open-the-package-designer"></a>パッケージ デザイナーを開く

#### <a name="to-open-the-package-designer"></a>パッケージ デザイナーを開くには

- **ソリューション エクスプローラー** で、 **[パッケージ]** をダブルクリックするか、 **[パッケージ]** のショートカット メニューで **[ビュー デザイナー]** を選択します。

## <a name="view-the-packaged-manifestffile"></a>パッケージ化された manifestfFile を表示する
 パッケージ デザイナーを使用して、パッケージ化されたマニフェスト ファイルを変更および生成できます。 その後、Visual Studio でこのファイルの XML コードを表示できます。

#### <a name="to-view-the-xml-source-file"></a>XML ソース ファイルを表示するには

1. **パッケージ デザイナー** で、 **[マニフェスト]** を選択します。

#### <a name="to-view-the-packaged-manifest-file-by-using-solution-explorer"></a>ソリューション エクスプローラーを使用してパッケージ化されたマニフェスト ファイルを表示するには

1. **ソリューション エクスプローラー** で、**[すべてのファイルを表示]** をクリックします。

2. [パッケージ] を展開し、Package.package を展開します。次に、*Package.Template.xml* ファイルを開きます。

    > [!NOTE]
    > パッケージ テンプレートのマニフェスト XML ファイルを開くと、ファイルは自動的に検証されます。[エラー一覧] ウィンドウに表示される警告は無視してかまいません。

## <a name="change-the-manifest-template"></a>マニフェスト テンプレートを変更する
 パッケージ化されたマニフェスト ファイルの XML コードは、Visual Studio の XML エディターまたは [マニフェスト テンプレート] ペインで変更できます。 XML コードに対する変更は、パッケージのパッケージ化されたマニフェスト ファイルにマージされます。

#### <a name="to-change-the-manifest-template-by-using-the-xml-editor"></a>XML エディターを使用してマニフェスト テンプレートを変更するには

1. **パッケージ デザイナー** で **[マニフェスト]** タブを選択します。 **[編集オプション]** ノードを展開し、 **[XML エディターで開く]** リンクをクリックします。

     XML への変更は、パッケージ化されたマニフェスト ファイルにマージされます。

#### <a name="to-change-the-manifest-template-by-using-the-manifest-template-pane"></a>[マニフェスト テンプレート] ペインを使用してマニフェスト テンプレートを変更するには

1. **パッケージ デザイナー** で **[マニフェスト]** タブを選択します。 **[編集オプション]** ノードを展開し、[マニフェスト テンプレート] ペインに表示される XML を変更します。

     XML への変更は、 **[パッケージ マニフェストのプレビュー]** ペインに表示されます。

## <a name="overwrite-the-packaged-manifest-file"></a>パッケージ化されたマニフェスト ファイルを上書きする
 パッケージ デザイナーを無効にして、*manifest.xml* ファイルを手動で作成できます。 この手順を初めて実行すると、パッケージ デザイナーの現在の設定がパッケージ テンプレート XML ファイルに保存されます。 その後、XML コードを変更または上書きできます。

> [!NOTE]
> パッケージ デザイナーが無効になっているときに、XML ファイル内の SharePoint プロジェクトの項目と機能を追加または削除した場合、これらのプロジェクトの項目と機能はパッケージ化されません。

#### <a name="to-overwrite-packaged-manifest-file-by-disabling-the-designer"></a>デザイナーを無効にすることでパッケージ化されたマニフェスト ファイルを上書きするには

1. **パッケージ デザイナー** で、 **[マニフェスト]** タブを選択します。

2. **[編集オプション]** ノードを展開し、 **[生成された XML を上書きし、XML エディターでマニフェストを編集します]** リンクを選択し、 **[はい]** ボタンを選択します。

     現在のパッケージ化されたマニフェスト ファイルでテンプレートが更新されます。

## <a name="enable-the-package-designer"></a>パッケージ デザイナーを有効にする
 パッケージ デザイナーを再度有効にして、*manifest.xml* ファイルをカスタマイズできます。

#### <a name="to-re-enable-the-designer"></a>デザイナーを再度有効にするには

1. **パッケージ デザイナー** で、 **[マニフェストの編集を破棄してデザイナーを再有効化します]** リンクを選択し、 **[はい]** ボタンを選択します。

     テンプレートは元のテキストで更新され、XML に対する変更はすべて失われます。

## <a name="see-also"></a>こちらもご覧ください
- [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
