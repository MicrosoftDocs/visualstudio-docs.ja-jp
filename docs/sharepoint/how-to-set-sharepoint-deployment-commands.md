---
title: '方法: SharePoint の配置コマンドを設定する | Microsoft Docs'
description: SharePoint の配置前コマンドと配置後コマンドを設定して、配置プロセスをカスタマイズする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, deploying
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 72938f316be22cd9b2eab2d7dab893c9370fb0ad
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99965851"
---
# <a name="how-to-set-sharepoint-deployment-commands"></a>方法: SharePoint の配置コマンドを設定する
  配置前コマンドと配置後コマンドを設定することによって、配置プロセスをカスタマイズすることができます。 これらのコマンドは、Visual Studio から SharePoint ソリューションをデバッグするときに、他の配置操作の前後に実行されます。

### <a name="to-add-a-pre-deployment-command"></a>配置前コマンドを追加するには

1. メニュー バーで、 **[プロジェクト]**  >  **[\<*ProjectName*> プロパティ]** を選択します。

2. **[SharePoint]** タブを選択します。

3. **[配置前コマンド ライン]** テキスト ボックスに、MS-DOS または MSBuild コマンドを入力して、この手順をカスタマイズします。

     たとえば、配置が完了する前にディレクトリの内容を一覧表示するには、「**dir**」と入力します。

### <a name="to-add-a-post-deployment-command"></a>配置後コマンドを追加するには

1. メニュー バーで、 **[プロジェクト]**  >  **[\<*ProjectName*> プロパティ]** を選択します。

2. **[SharePoint]** タブを選択します。

3. **[配置後コマンド ライン]** テキスト ボックスに、MS-DOS または MSBuild コマンドを入力して、この手順をカスタマイズします。

     たとえば、配置が完了した後にディレクトリの内容を一覧表示するには、「**dir**」と入力します。 MSBuild 変数を使用してビルド ディレクトリからアセンブリをコピーするには、「**copy $(TargetPath) c:\DeploymentDirectory**」と入力します。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
