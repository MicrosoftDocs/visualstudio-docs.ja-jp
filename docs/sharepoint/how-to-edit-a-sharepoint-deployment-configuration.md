---
title: '方法: SharePoint の配置構成を編集する | Microsoft Docs'
description: SharePoint の配置構成を作成する、または既存の配置構成を変更する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.Project.DeploymentConfig
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
ms.openlocfilehash: 59354537f0c1f22534395da1e0ed3db3929a14a9
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99913643"
---
# <a name="how-to-edit-a-sharepoint-deployment-configuration"></a>方法: SharePoint の配置構成を編集する
  SharePoint の配置構成を作成する、または既存の配置構成を変更することができます。 たとえば、1 つの手順を実行したり、配置プロセスのステップの順序を変更したりできます。 組み込みの構成およびプログラムによって追加された構成は変更できないため、配置構成を作成または変更したい場合があります。

## <a name="create-a-sharepoint-deployment-configuration"></a>SharePoint の配置構成を作成する

#### <a name="to-create-a-sharepoint-deployment-configuration"></a>SharePoint の配置構成を作成するには

1. **ソリューション エクスプローラー** で、SharePoint プロジェクトを選択します。次に、メニュー バーで **[プロジェクト]** 、 _[ProjectName]_ **[プロパティ]** を選択します。

2. **[SharePoint]** タブで、 **[新規作成]** をクリックします。

     **[新しい配置構成の追加]** ダイアログ ボックスが開きます。

3. **[名前]** ボックスに、配置構成の名前を入力します。

4. **[利用可能な配置手順]** ウィンドウで、展開構成に追加する手順を選択し、( **>** ) ボタンを選択して、 **[OK]** ボタンを選択します。

    > [!NOTE]
    > 配置前コマンドまたは配置後コマンドを構成している場合、これらの手順は、カスタマイズされた展開構成に追加した場合にのみ実行されます。

## <a name="change-the-active-deployment-configuration"></a>アクティブな配置構成を変更する

#### <a name="to-change-the-active-deployment-configuration"></a>アクティブな配置構成を変更するには

1. **ソリューション エクスプローラー** で、SharePoint プロジェクトを選択します。次に、メニュー バーで **[プロジェクト]**  >  **\<*ProjectName*>[プロパティ]** を選択します。

2. **[SharePoint]** タブを選択します。

3. **[アクティブな配置構成]** 一覧のボックスで、使用する配置構成の名前を選択します。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
