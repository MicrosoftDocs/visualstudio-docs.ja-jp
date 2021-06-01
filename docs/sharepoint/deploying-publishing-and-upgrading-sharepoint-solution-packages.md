---
title: SharePoint ソリューション パッケージの配置、発行、およびアップグレードを行う
description: SharePoint ソリューション パッケージの配置、発行、およびアップグレードを行います。 配置プロセスをカスタマイズします。 リモートまたはローカル サーバーにパッケージを発行します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.Project.SharePointProjectPropertyTab
- VS.SharePointTools.Project.Publishing
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
ms.openlocfilehash: cd0dfa3a12c675463c46e93aa0d5b25e8b4bd4b2
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99948857"
---
# <a name="deploy-publish-and-upgrade-sharepoint-solution-packages"></a>SharePoint ソリューション パッケージの配置、発行、およびアップグレードを行う
  Visual Studio で SharePoint ソリューションを開発した後、そのパッケージ (.wsp) ファイルをローカル SharePoint サーバーに配置するか、リモートまたはローカル SharePoint サーバーに発行できます。 ファイルを配置する場合は、パッケージファイル (.wsp) の配置方法をカスタマイズできます。

> [!NOTE]
> 現時点では、リモートの SharePoint サーバーに発行できるのは、サンドボックス化されたソリューションのみです。 詳細については、「[サンドボックス ソリューションの考慮事項](../sharepoint/sandboxed-solution-considerations.md)」を参照してください。

## <a name="deploy-publish-and-upgrade"></a>配置、発行、およびアップグレード
 "*配置*" とは、Visual Studio で SharePoint プロジェクトからビルドされた SharePoint ソリューション ファイルをローカル ホストにコピーすることを指します。 配置されるソリューションでは、インターネット インフォメーション サービス (IIS) プールのリサイクル、配置後のソリューションのアクティブ化などの配置手順を構成できます。 配置するには、 **[ビルド]** メニューの **[配置]** コマンドを使用します。 詳細については、「[方法: SharePoint の配置構成を編集する](../sharepoint/how-to-edit-a-sharepoint-deployment-configuration.md)」と「[方法: SharePoint ソリューションのローカル SharePoint サイトへの配置と発行を行う](../sharepoint/how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site.md)」を参照してください。

 "*発行*" とは、サンドボックス化された SharePoint ソリューション ファイルをリモート SharePoint サイト (別のシステムに配置されているサイト) にアップロードすることを指します。 SharePoint サンドボックス ソリューション ファイルをローカル SharePoint サイトに発行することもできますが、発行先のサイトがローカルであるかリモートであるかに関係なく、その配置手順を構成することはできません。

 "*アップグレード*" とは、既存のリモートまたはローカルに発行された SharePoint ソリューションを更新することを指します。 Visual Studio で SharePoint ソリューションを変更した後、ソリューションのパッケージ ファイル名を変更し、ソリューションを再発行します。ソリューションが正常に再発行された後、それをアップグレードします。 ローカルに発行されたソリューションを再発行する場合は、既存のソリューション ファイルを上書きできます。

## <a name="deploy-packages"></a>パッケージの配置
 テストとデバッグを目的として、開発用コンピューターの SharePoint サーバーにパッケージ ファイルを配置できます。 **[発行]** ダイアログ ボックスの **[ファイル システムに発行]** オプションボタンを選択することで、別のコンピューターにインストールできるパッケージ ファイルを作成することもできます。 パッケージが作成され、指定したローカル ファイル パスにコピーされます。 SharePoint ソリューションをローカル サーバーに配置するには、 **[ビルド]** メニューの **[配置]** を使用します。 詳細については、「[SharePoint ソリューションのローカル SharePoint サイトへの配置と発行を行う](../sharepoint/how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site.md)」を参照してください。

 リスト定義を配置する方法、イベント レシーバーを追加する方法、およびフィーチャー デザイナーとパッケージ デザイナーを使用する方法については、「[チュートリアル: プロジェクト タスク リスト定義を配置する](../sharepoint/walkthrough-deploying-a-project-task-list-definition.md)」を参照してください。

## <a name="customize-the-deployment-process"></a>配置プロセスをカスタマイズする
 次の表は、SharePoint ソリューションのデバッグと配置を行うときに使用できる 2 つの配置構成を示しています。

|デプロイの構成|説明|
|------------------------------|-----------------|
|Default|既定の配置構成。 次の配置手順が実行されます。<br /><br /> 1. 配置前コマンドを実行する。<br />2. IIS アプリケーション プールをリサイクルする。<br />3. ソリューションを取り消す。<br />4. ソリューションを追加する。<br />5. 機能をアクティブ化する。<br />6. 配置後コマンドを実行する。<br /><br /> パッケージがアンインストールされると、次の取り消し手順が実行されます。<br /><br /> 1. IIS アプリケーション プールをリサイクルする。<br />2. ソリューションを取り消す。|
|アクティブ化なし|この配置構成では、[既定] の構成と同じ手順が実行されますが、アクティブ化手順はスキップされます。|

 独自の配置構成を作成して、1 つの手順を完了したり、配置プロセス手順の順序を変更したりすることができます。 詳細については、「[方法:SharePoint の配置構成を編集する](../sharepoint/how-to-edit-a-sharepoint-deployment-configuration.md)」を参照してください。

 配置の前後に実行するコマンドを追加することもできます。 詳細については、「[方法: SharePoint 配置コマンドを設定する](../sharepoint/how-to-set-sharepoint-deployment-commands.md)」を参照してください。

## <a name="publish-packages-to-a-remote-or-local-server"></a>リモートまたはローカル サーバーにパッケージを発行する
 サンドボックス化された SharePoint ソリューションをリモート サーバーに発行するには、メニュー バーで **[ビルド]** 、 **[発行]** の順に選択します。 **[発行]** ダイアログ ボックスで **[SharePoint サイトに発行]** を選択し、リモート サーバーの URL (`https://someremoteserver.sharepoint.microsoftonline.com` など) を指定します。

 SharePoint ソリューションをローカル サーバーに発行するには、 **[発行]** ダイアログ ボックスで、 **[ファイル システムに発行]** オプションを選択し、ローカル システム パスを指定します。

 ソリューションが SharePoint に正常に発行されると、**ソリューション ギャラリー** にソリューションが表示され、アクティブ化できるようになります。 詳細については、「[方法: リモート サーバー上で SharePoint ソリューションの配置、発行、およびアップグレードを行う](../sharepoint/how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server.md)」を参照してください。

### <a name="upgrade-published-packages"></a>発行済みのパッケージをアップグレードする
 SharePoint プロジェクトの発行後に Visual Studio で何らかの変更を行った場合は、変更を含めるように発行済みのパッケージをアップグレードする必要があります。 正常にアップグレードするには、パッケージの名前が一意である必要があります。 SharePoint サイトで同じ名前のパッケージが見つかった場合 (既存のアプリケーションを更新するときに発生する可能性があります)、ファイル名の競合を警告するエラー メッセージが表示され、パッケージの名前を変更できます。 再発行すると、SharePoint サイトに新しいパッケージが表示され、アップグレードできます。 アップグレードされるパッケージでは、古いパッケージのデータを使用してソリューションが更新された後、SharePoint でソリューションがアクティブ化されます。 詳細については、「[方法: リモート サーバー上で SharePoint ソリューションの配置、発行、およびアップグレードを行う](../sharepoint/how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server.md)」を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
