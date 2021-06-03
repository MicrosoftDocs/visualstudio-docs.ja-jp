---
title: SharePoint ソリューションをローカルの SharePoint サイトに配置および発行する
titleSuffix: ''
description: 開発用コンピューターのローカル SharePoint サーバーに SharePoint ソリューションを配置または発行する方法を確認します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- deploying [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, deploying
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 22fe46e2876b14551637dd97712e1728816b020e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99913696"
---
# <a name="how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site"></a>方法: SharePoint ソリューションをローカルの SharePoint サイトに配置および発行する
  開発用コンピューターのローカル SharePoint サーバーに SharePoint ソリューションを配置または発行することができます。 配置プロセスにより、SharePoint サーバーに *.wsp* ファイルがコピーされ、ソリューションがインストールされて、機能がアクティブ化されます。 発行プロセスでは、 *.wsp* ファイルを SharePoint サーバーにコピーしてインストールするだけです。 SharePoint で有効にするには、手動でアクティブ化する必要があります。

## <a name="to-deploy-a-sharepoint-solution-to-the-local-sharepoint-server"></a>SharePoint ソリューションをローカルの SharePoint サーバーに配置するには

1. **ソリューション エクスプローラー** で、配置したいプロジェクトを選択します。

2. (メニュー バーで **[ビルド]** 、 **[ソリューションの配置]** の順に選択します)。

     *.wsp* ファイルが作成され、ローカルの SharePoint サーバーにインストールされます。 また、機能がアクティブ化されます。

## <a name="to-publish-a-sharepoint-solution-to-a-local-sharepoint-server"></a>SharePoint ソリューションをローカルの SharePoint サイトに発行する方法

1. **ソリューション エクスプローラー** で、発行する SharePoint プロジェクトのショートカット メニューを開き、 **[発行]** を選択します。

2. **[発行]** ダイアログ ボックスで、 **[ファイル システムに発行する]** オプション ボタンをクリックします。

3. **[ターゲットの場所]** テキスト ボックスにローカル パスを入力し、 **[発行]** を選択します。

     発行の進行状況が Visual Studio の **[出力]** ウィンドウに表示されます。 プロセスが終了すると、ソリューション ( *.wsp*) ファイルがローカルの SharePoint サーバーにインストールされます。 ただし、SharePoint で使用するには、アクティブにする必要があります。 ソリューション ファイルが既に存在する場合は、エラーが発生し、既存のファイルを上書きするかどうかを確認するメッセージが表示されます。 パッケージのアップグレードの詳細については、「[方法: リモート サーバー上で SharePoint ソリューションを配置、発行、およびアップグレードする](../sharepoint/how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server.md)」のリモート パッケージのアップグレードに関するセクションを参照してください。

## <a name="see-also"></a>関連項目
- [方法: リモート サーバー上で SharePoint ソリューションを配置、発行、およびアップグレードする](../sharepoint/how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server.md)
- [SharePoint ソリューション パッケージを作成する](../sharepoint/creating-sharepoint-solution-packages.md)
- [方法: SharePoint ソリューション パッケージをカスタマイズする](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)
- [方法: パッケージ デザイナーを使用してパッケージのフィーチャーおよび項目を追加および削除する](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)
