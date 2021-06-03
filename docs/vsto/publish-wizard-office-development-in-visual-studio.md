---
title: 発行ウィザード (Visual Studio での Office 開発)
description: 発行ウィザードを使用して、指定した場所にソリューション ファイルをコピーしたり、マニフェスト ファイルを作成したり、Visual Studio でセットアップ プログラムを作成したりする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VST.ProjectProperties.PublishWizard
- VST.PublishWizard.Publish.2007System
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ClickOnce deployment [Office development in Visual Studio], Publish Wizard
- deploying applications [Office development in Visual Studio], Publish Wizard
- Office applications [Office development in Visual Studio], Publish Wizard
- Publish Wizard, Office solutions
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 29400e82dcd7b0d5cd9062679610b50bfaab191d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99971688"
---
# <a name="publish-wizard-office-development-in-visual-studio"></a>発行ウィザード (Visual Studio での Office 開発)
  指定した場所にソリューション ファイルをコピーしたり、マニフェスト ファイルを作成したり、セットアップ プログラムを作成したりするには、"**発行ウィザード**" を使用します。

 このウィザードにアクセスするには、 **[ビルド]** メニューの [***SolutionName* の発行]** を選択します。 **ソリューション エクスプローラー** から "**発行ウィザード**" にアクセスすることもできます。 プロジェクト ノードのショートカット メニューを開いて、 **[発行]** を選択します。

 以下の各セクションでは、このウィザードのページについて説明します。

## <a name="where-do-you-want-to-publish-the-application"></a>アプリケーションをどこに公開しますか?
 **[このアプリケーションを公開する場所を指定します]** (必須)。 発行場所は、"**発行ウィザード**" で、ビルドからマニフェスト、アセンブリ、一時証明書、その他のファイルなどのソリューション ファイルがコピーされるディレクトリです。 このディレクトリへの書き込みアクセス権が必要です。

 ディスク パス、ファイル共有、FTP サイト、または Web サイトの URL として場所を入力するか、 **[参照]** ボタンをクリックして場所を参照します。 パスは次の形式にすることができます。

- 標準の Windows 形式の相対または絶対パス (*C:\Deploy\MyApplication* や *\MyApplication* など)。

- 汎用名前付け規則 (UNC) パス ( *\\\ServerName\MyApplication\\* など)。

- Web サイトの URL (`http://www.contoso.com/MyApplication` など)。

  既定の発行場所は、IIS をインストールしている場合は *http://localhost/projectname/* で、IIS をインストールしていない場合は、publish\ ディレクトリです。

> [!NOTE]
> ターゲット コンピューターで Windows Vista が実行されている場合は、さらに考慮すべき点があります。 ローカル発行オプションを使用するには、Windows Vista コンピューターの管理者である必要があります。 また、IIS がインストールされているかどうかに関係なく、既定の場所は常に *publish\\* ディレクトリになります。

## <a name="what-is-the-default-installation-path-on-end-user-computers"></a>エンド ユーザーのコンピューター上での、既定のインストール パスを指定してください。
 インストール パスは省略可能です。 必要に応じて、後でインストール パスを設定できます。 詳細については、[Office ソリューションのインストール パスを変更する方法](/previous-versions/bb608626(v=vs.110))に関するページを参照してください。

 インストール パスの URL は、エンド ユーザーがカスタマイズをインストールするディレクトリです。 このディレクトリは、ソリューションで更新プログラムを確認するために使用するパスでもあります。 前のページの **[アプリケーションを公開する場所を指定します]** ボックスに入力したパスと同じパスでない限り、"**発行ウィザード**" ではこの場所にソリューションが配置されません。

 **[Web サイトから]** エンド ユーザーがソリューションをインストールする際に従う URL を指定します。

 **[UNC パスまたはファイル共有から]** エンド ユーザーがソリューションをインストールする際に従う UNC パスを指定します。

 **CD-ROM または DVD-ROM から** このオプションにはインストール パスは必要ありません。

 Visual Studio では CD または DVD に書き込まれません。 出力を CD または DVD に手動でコピーする必要があります。

## <a name="see-also"></a>関連項目
- [ClickOnce を使用して Office ソリューションを配置する](../vsto/deploying-an-office-solution-by-using-clickonce.md)
- [プロジェクト デザイナーの [発行] ページ &#40;Visual Studio での Office 開発&#41;](../vsto/publish-page-project-designer-office-development-in-visual-studio.md)
- [Office ソリューションを配置する](../vsto/deploying-an-office-solution.md)