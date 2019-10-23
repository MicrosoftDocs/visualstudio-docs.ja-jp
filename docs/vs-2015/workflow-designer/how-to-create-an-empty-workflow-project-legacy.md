---
title: '方法: 空のワークフロープロジェクトを作成する (レガシ) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- projects, empty workflow
- empty workflow projects
- workflows, empty workflow projects
ms.assetid: f81b9cf2-9adb-47a2-936b-cb1851614e19
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d24baf48f74a7e18ee7bb4922ad989fd8e03a38a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662737"
---
# <a name="how-to-create-an-empty-workflow-project-legacy"></a>方法: 空のワークフロー プロジェクトを作成する (レガシ)
[!INCLUDE[wfd1](../includes/wfd1-md.md)] が備えている従来の [!INCLUDE[vs2010](../includes/vs2010-md.md)]を使用して空のワークフロー プロジェクトを作成するには、次の手順を実行します。 [!INCLUDE[wfd2](../includes/wfd2-md.md)] または [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] を対象とする必要がある場合は、従来の[!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]を使用します。

### <a name="to-create-an-empty-workflow-project"></a>空のワークフロー プロジェクトを作成するには

1. Visual Studio を起動します。

2. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** を選択します。

     **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

3. レガシデザイナーにアクセスするには、 **[新しいプロジェクト]** ウィンドウの上部にあるドロップダウンリストの **[.NET Framework 3.0]** オプションまたは **[.NET Framework 3.5]** オプションを選択します。

    > [!NOTE]
    > @No__t_0 の既定のオプションは **.NET Framework 4**です。 このオプションは、[!INCLUDE[wf](../includes/wf-md.md)] を対象とする [!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)] アプリケーションを作成する場合に使用され、従来のデザイナーは使用しません。

4. **[プロジェクトの種類]** ペインで、 C# ビジュアル または Visual Basic ( **[その他の言語]** の下) を選択し、 **[ワークフロー]** を選択します。

5. **[テンプレート]** ペインで、 **[空のワークフロープロジェクト]** を選択します。

6. **[名前]** ボックスに、プロジェクトのわかりやすい名前を入力します。

7. **[場所]** ボックスに、プロジェクトを保存するディレクトリを入力するか、 **[参照]** をクリックして移動します。

     プロジェクト用にソリューションディレクトリを作成する場合は、 **[ソリューションのディレクトリを作成]** する チェックボックスをオンにして、 **[ソリューション名]** ボックスに名前を入力します。

8. **[OK]** をクリックします。

## <a name="see-also"></a>参照
 [従来のワークフロー プロジェクトの作成](../workflow-designer/creating-legacy-workflow-projects.md)