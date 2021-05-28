---
title: SharePoint ソリューション パッケージの作成 | Microsoft Docs
description: パッケージ デザイナーを使用して、SharePoint ソリューションの配置パッケージを作成およびカスタマイズします。 パッケージング ツール、デザイナー オプション、およびフォルダー構造について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, packages
- packages [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 423fcaf54d1d46ddf92352f4ff8bdbb637bbe514
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99949091"
---
# <a name="create-sharepoint-solution-packages"></a>SharePoint ソリューション パッケージを作成する
  配置パッケージを作成したりカスタマイズしたりするには、パッケージ デザイナーを使用します。 たとえば、SharePoint のプロジェクト項目およびフィーチャーの追加、IIS サーバーのリセット、フィーチャーのアクティブ化スコープの設定、フィーチャーの依存関係の特定などを行うことができます。 このデザイナーでは、マニフェスト (個々のパッケージを記述した XML ファイル) を生成することもできます。

## <a name="packaging-tools"></a>パッケージ化ツール
 **パッケージ デザイナー** を使用して、パッケージをカスタマイズしたりマニフェストを生成したりできます。 SharePoint のプロジェクト項目の追加、Web サーバーのリセットの構成、および配置用サーバーの種類の設定を行うことができます。 詳細については、「[方法: パッケージ デザイナーを使用してパッケージの機能と項目を追加および削除する](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)」を参照してください。

 また、**パッケージング エクスプローラー** を使用して、パッケージ ファイル ( *.wsp*) 内の機能と項目を変更できます。 詳細については、「[方法: パッケージング エクスプローラーを使用してパッケージの機能と項目を追加および削除する](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-packaging-explorer.md)」を参照してください。

 Visual Studio および MSBuild を使用して、SharePoint ソリューションを配置するためのパッケージ ( *.wsp*) ファイルを作成できます。 SharePoint の配置に必要なマニフェスト ファイルはこのプロセスで生成されます。 詳細については、「[方法: MSBuild タスクを使用して SharePoint ソリューション パッケージを作成する](../sharepoint/how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks.md)」を参照してください。

## <a name="package-designer-options"></a>パッケージ デザイナーのオプション
 次の表は、**パッケージ デザイナー** を使用してカスタマイズできる、SharePoint パッケージのプロパティの一覧です。

|パッケージ デザイナーのプロパティ|既定の設定に関する説明|
|-------------------------------|------------------------------------|
|名前|必須。 パッケージの既定の名前は *ProjectName* に設定されます。|
|[Web サーバーのリセット]|省略可能。 SharePoint サーバーに *.wsp* ファイルがインストールされた後に Web サーバーを再起動する場合に選択します。|
|配置サーバーの種類|省略可能。 パッケージをホストするサーバーの種類を表します。 設定されていない場合、既定では WebFrontEnd エンドになります。<br /><br /> ApplicationServer: サービスをホストするサーバーを表します。<br /><br /> WebFrontEnd: Web サイトをホストするサーバーを表します。|
|[ソリューション内の項目]|パッケージに追加できるすべての SharePoint プロジェクト項目およびフィーチャーを表します。|
|[パッケージ内の項目]|省略可能。 パッケージ内の配置対象の SharePoint プロジェクト項目およびフィーチャーを表します。|

## <a name="configure-the-packaging-process"></a>パッケージ化プロセスを構成する
 Visual Studio で SharePoint ソリューションを開発した後に、プロジェクトをパッケージ化する方法をカスタマイズすることができます。

 次の表に、 *.wsp* ファイルの作成方法をカスタマイズするために使用できる 2 つの MSBuild ターゲットを示します。

|Target|説明|
|------------|-----------------|
|BeforeLayout|ファイルが中間ディレクトリにコピーされる直前にタスクを実行するターゲット。 パッケージ ファイル ( *.wsp*) を作成する前に、ファイルに変更を加えることができます。|
|AfterLayout|ファイルが中間ディレクトリにコピーされた直後にタスクを実行するターゲット。|

 詳細については、「[方法: MSBuild ターゲットを使用して SharePoint ソリューション パッケージをカスタマイズする](../sharepoint/how-to-customize-a-sharepoint-solution-package-by-using-msbuild-targets.md)」を参照してください。

## <a name="packaging-architecture"></a>パッケージ化のアーキテクチャ
 Visual Studio で SharePoint パッケージ ( *.wsp*) を作成すると、次の手順が実行されます。

1. パッケージの物理構造と意味構造が正しいことを確認するために、フィーチャーおよびパッケージが検証されます。

2. パッケージ内のフィーチャー、プロジェクト項目、およびパッケージ ファイルが列挙されます。 パッケージおよびフィーチャーのマニフェスト ファイルが変換されて、配置およびアクティブ化に必要な情報がすべて追加されます。 トークンは完全修飾値に置き換えられます。

3. カスタマイズ可能な BeforeLayout MSBuild ターゲットが実行されます。 この手順を作成して、 *.wsp* ファイルの作成前に、パッケージに独自の変更を適用できます。

4. 列挙されたファイルが中間ディレクトリにコピーされます。

5. カスタマイズ可能な AfterLayout MSBuild ターゲットが実行されます。 この手順を作成して、 *.wsp* ファイルの作成前に、パッケージに独自の変更を適用できます。

6. 中間ディレクトリのファイルが *.wsp* ファイルに追加されます。

## <a name="package-folder-structure"></a>パッケージ フォルダーの構造
 SharePoint プロジェクトをパッケージ化すると、*SolutionFolder\bin\\\<BuildConfiguration>* フォルダーに *.wsp* ファイルが自動的に作成されます。 たとえば、ソリューションが *C:\Visual Studio 2013\Projects\ListDefinition1* にあり、ビルド構成が [リリース] に設定されている場合、 *.wsp* ファイルは *C:\Visual Studio 2013\Projects\ListDefinition1\bin\Release* に置かれます。

## <a name="see-also"></a>こちらもご覧ください
- [方法: SharePoint ソリューション パッケージをカスタマイズする](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)
- [方法: パッケージ デザイナーを使用してパッケージの機能と項目を追加および削除する](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)
- [方法: MSBuild タスクを使用して SharePoint ソリューション パッケージを作成する](../sharepoint/how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks.md)
- [方法: MSBuild タスクを使用して SharePoint ソリューション パッケージを作成する](../sharepoint/how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks.md)
- [方法: MSBuild ターゲットを使用して SharePoint ソリューション パッケージをカスタマイズする](../sharepoint/how-to-customize-a-sharepoint-solution-package-by-using-msbuild-targets.md)
