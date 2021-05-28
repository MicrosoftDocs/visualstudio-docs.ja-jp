---
title: MSBuild ターゲットを使用して SharePoint ソリューション パッケージをカスタマイズする
titleSuffix: ''
description: コマンド プロンプトで MSBuild ターゲットを使用して、Visual Studio で SharePoint ソリューション パッケージ ファイル (.wsp) を作成する方法をカスタマイズします。
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
ms.openlocfilehash: b4d181a6310e1ff924f060e906093d3c28d60ede
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99959923"
---
# <a name="how-to-customize-a-sharepoint-solution-package-by-using-msbuild-targets"></a>方法: MSBuild ターゲットを使用して SharePoint ソリューション パッケージをカスタマイズする
  MSBuild ターゲットをコマンド プロンプトで使用することによって、Visual Studio で SharePoint パッケージファイル ( *.wsp*) を作成する方法をカスタマイズできます。 たとえば、MSBuild のプロパティをカスタマイズして、パッケージ化する中間ディレクトリと、列挙されたファイルを指定する MSBuild 項目グループを変更できます。

## <a name="customize-and-run-msbuild-targets"></a>MSBuild ターゲットをカスタマイズして実行する
 BeforeLayout および AfterLayout ターゲットをカスタマイズする場合は、パッケージ レイアウトの前に、パッケージ化されるファイルの追加、削除、変更などのタスクを実行できます。

#### <a name="to-customize-the-beforelayout-target"></a>BeforeLayout ターゲットをカスタマイズするには

1. メモ帳などのエディターを開き、次のコードを追加します。

   ```xml
   <Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
     <Target Name="BeforeLayout">
       <Message Importance="high" Text="In the BeforeLayout Target"></Message>
     </Target>
   </Project>
   ```

    この例では、このターゲットのパッケージ化の前にメッセージを表示します。

2. ファイルに「**CustomLayout.SharePoint.targets**」という名前を付け、SharePoint プロジェクト用のフォルダーに保存します。

3. プロジェクトを開き、そのショートカット メニューを開き、 **[プロジェクトのアンロード]** を選択します。

4. **ソリューション エクスプローラー** で、プロジェクトのショートカット メニューを開き、 **[ *\<ProjectName>.vbproj* の編集]** または **[ *\<ProjectName>.csproj* の編集]** を選択します。

5. プロジェクト ファイルの末尾付近にある `Import` 行の後ろに、次の行を追加します。

   ```xml
   <Import Project="CustomLayout.SharePoint.targets" />
   ```

6. プロジェクト ファイルを保存して閉じます。

7. **ソリューション エクスプローラー** で、プロジェクトのショートカット メニューを開き、 **[プロジェクトの再ロード]** をクリックします。

   プロジェクトを発行すると、パッケージ化が開始される前に、メッセージが出力に表示されます。

#### <a name="to-customize-the-afterlayout-target"></a>AfterLayout ターゲットをカスタマイズするには

1. メニュー バーで、 **[ファイル]**  >  **[開く]**  >  **[ファイル]** を選択します。

2. **[ファイルを開く]** ダイアログ ボックスで、プロジェクト フォルダーに移動します。CustomLayout.target ファイルを選択して、 **[開く]** ボタンをクリックします。

3. `</Project>` タグの直前に、次のコードを追加します。

   ```xml
   <Target Name="AfterLayout">
     <Message Importance="high" Text="In the AfterLayout Target"></Message>
   </Target>
   ```

    この例では、このターゲットがパッケージ化された後でメッセージを表示します。

4. ターゲット ファイルを保存して閉じます。

5. Visual Studio を再起動した後、プロジェクトを開きます。

   プロジェクトを発行すると、パッケージ化の開始前に BeforeLayout メッセージが表示され、パッケージ化の終了後に AfterLayout メッセージが表示されます。

## <a name="see-also"></a>こちらもご覧ください
- [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
