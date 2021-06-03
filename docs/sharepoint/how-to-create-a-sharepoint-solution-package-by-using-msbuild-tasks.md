---
title: MSBuild タスクを使用して SharePoint ソリューション パッケージを作成する
description: 開発用コンピューターでコマンド ライン MSBuild タスクを使用して、SharePoint ソリューション パッケージ (.wsp) をビルド、クリーン、検証する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: f4c1d2e986b6a810cc568efd9577be87a38fdefb
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99873542"
---
# <a name="how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks"></a>方法: MSBuild タスクを使用して SharePoint ソリューション パッケージを作成する
  開発用コンピューターでコマンド ライン MSBuild タスクを使用して、SharePoint パッケージ ( *.wsp*) をビルド、クリーン、検証することができます。 これらのコマンドを使用して、ビルド コンピューターで Team Foundation Server を使用してビルド プロセスを自動化することもできます。

## <a name="build-a-sharepoint-package"></a>SharePoint パッケージをビルドする

#### <a name="to-build-a-sharepoint-package"></a>SharePoint パッケージをビルドするには

1. Windows の **[スタート]** メニューで、 **[すべてのプログラム]**  >  **[アクセサリ]**  >  **[コマンド プロンプト]** の順に選択します。

2. SharePoint プロジェクトが配置されているディレクトリに移動します。

3. 次のコマンドを入力して、プロジェクトのパッケージを作成します。 *ProjectFileName* をプロジェクトの名前で置き換えます。

    ```cmd
    msbuild /t:Package ProjectFileName
    ```

     たとえば、次のコマンドのいずれかを実行して、ListDefinition1 という名前の SharePoint プロジェクトをパッケージ化することができます。

    ```cmd
    msbuild /t:Package ListDefinition1.vbproj
    msbuild /t:Package ListDefinition1.csproj
    ```

## <a name="clean-a-sharepoint-package"></a>SharePoint パッケージをクリーンする

#### <a name="to-clean-a-sharepoint-package"></a>SharePoint パッケージをクリーンするには

1. コマンド プロンプト ウィンドウを開きます。

2. SharePoint プロジェクトが配置されているディレクトリに移動します。

3. 次のコマンドを入力して、プロジェクトのパッケージをクリーンします。 *ProjectFileName* をプロジェクトの名前で置き換えます。

    ```cmd
    msbuild /t:CleanPackage ProjectFileName
    ```

     たとえば、次のコマンドのいずれかを実行して、ListDefinition1 という名前の SharePoint プロジェクトをクリーンすることができます。

    ```cmd
    msbuild /t:CleanPackage ListDefinition1.vbproj
    msbuild /t:CleanPackage ListDefinition1.csproj
    ```

## <a name="validate-a-sharepoint-package"></a>SharePoint パッケージを検証する

#### <a name="to-validate-a-sharepoint-package"></a>SharePoint パッケージを検証するには

1. コマンド プロンプト ウィンドウを開きます。

2. SharePoint プロジェクトが配置されているディレクトリに移動します。

3. 次のコマンドを入力して、プロジェクトのパッケージを検証します。 *ProjectFileName* をプロジェクトの名前で置き換えます。

    ```cmd
    msbuild /t:ValidatePackage ProjectFileName
    ```

     たとえば、次のコマンドのいずれかを実行して、ListDefinition1 という名前の SharePoint プロジェクトを検証することができます。

    ```cmd
    msbuild /t:ValidatePackage ListDefinition1.vbproj
    msbuild /t:ValidatePackage ListDefinition1.csproj
    ```

## <a name="set-properties-in-a-sharepoint-package"></a>SharePoint パッケージのプロパティを設定する

#### <a name="to-set-a-property-in-a-sharepoint-package"></a>SharePoint パッケージのプロパティを設定するには

1. コマンド プロンプト ウィンドウを開きます。

2. SharePoint プロジェクトが配置されているディレクトリに移動します。

3. 次のコマンドを入力して、プロジェクトのパッケージのプロパティを設定します。 *PropertyName* を、設定するプロパティで置き換えます。

    ```cmd
    msbuild /property:PropertyName=Value
    ```

     たとえば、次のコマンドを実行して警告レベルを設定できます。

    ```cmd
    msbuild /property:WarningLevel = 2
    ```

## <a name="see-also"></a>関連項目
- [SharePoint フィーチャーを作成する](../sharepoint/creating-sharepoint-features.md)
- [方法: SharePoint 機能をカスタマイズする](../sharepoint/how-to-customize-a-sharepoint-feature.md)
- [方法: SharePoint 機能の項目を追加および削除する](../sharepoint/how-to-add-and-remove-items-to-sharepoint-features.md)
