---
title: '方法: マスター ページまたはテーマをインポートする | Microsoft Docs'
description: SharePoint デザイナーでマスター ページとテーマのテンプレートを作成し、Visual Studio にインポートして、SharePoint サイトのページに一貫性のある外観を与えます。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, importing items
- importing items [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 331ae3964de40e6590345aadae59776fe37f467a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99913672"
---
# <a name="how-to-import-a-master-page-or-theme"></a>方法: マスター ページまたはテーマをインポートする
  マスター ページとテーマを作成して使用することで、SharePoint サイトのページに一貫した外観を与えることができます。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] では、これらの要素のテンプレートは提供されませんが、SharePoint デザイナーで作成して [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] にインポートすることができます。 テーマの詳細については、Microsoft Web サイトの「[文書パーツ: ページとユーザー インターフェイス](/previous-versions/office/developer/sharepoint-2010/ee539040(v=office.14))」を参照してください。

### <a name="to-import-a-master-page-or-theme"></a>マスター ページまたはテーマをインポートするには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で、SharePoint プロジェクトを作成するか開きます。

     SharePoint プロジェクトを作成する方法の詳細については、「[SharePoint プロジェクトとプロジェクト項目テンプレート](../sharepoint/sharepoint-project-and-project-item-templates.md)」を参照してください。

2. メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** の順に選択します。

3. **[新しい項目の追加]** ダイアログ ボックスで、 **[SharePoint]** ノードを展開し、 **[2010]** ノードを選択します。

4. SharePoint テンプレートの一覧で、 **[モジュール]** テンプレートを選択し、モジュールの名前を指定します。

     モジュールには、SharePoint で指定した場所に配置するためのファイル (マスター ページやテーマ ファイルなど) が含まれています。

5. モジュールで、*Sample.txt* という名前の既定のファイルを削除します。

6. [モジュール] ノードを選択します。

7. メニューバーで、 **[プロジェクト]**  >  **[既存の項目の追加]** の順に選択し、マスター ページまたはテーマ ファイルを選択します。

     マスター ページ ファイルの拡張子は .master で、テーマ ファイルの拡張子は .thmx です。

8. マスター ページを追加した場合は、モジュールのプロパティで、 **[配置競合の解決]** 設定を **[自動]** に変更します。

    > [!NOTE]
    > マスター ページの名前が、既定のマスター ページまたはカスタム マスター ページとしてマークされている既存のマスター ページの名前と同じである場合に、エラーが発生することがあります。 この問題を解決する方法の詳細については、「[チュートリアル: イメージを備えたカスタム マスター ページおよびサイト ページのインポート](../sharepoint/walkthrough-import-a-custom-master-page-and-site-page-with-an-image.md)」を参照してください。

9. モジュールで *Elements.xml* を開きます。

     追加したマスター ページまたはテーマを参照するように *Elements.xml* ファイルを更新する必要があります。

10. マスター ページの場合は、既存のモジュール マークアップを次のマークアップに置き換えます。

    ```xml
    <Module Name="[Module Name]" Url="_catalogs/masterpage">
        <File Path="[Module Name]\[Master Page Name].master"
          Url="[Master Page Name].master" Type="GhostableInLibrary" />
    </Module>
    ```

     テーマの場合は、既存のモジュール マークアップを次のマークアップに置き換えます。

    ```xml
    <Module Name="[Module Name]" Url="_catalogs/theme"
        <File Path="[Module Name]\[Theme Name].thmx" Url="[Theme
          Name].thmx" Type="GhostableInLibrary" />
    </Module>
    ```

     プレースホルダーの値は、モジュールの実際の名前とマスター ページまたはテーマに置き換えてください。

     `Type="GhostableInLibrary"` 属性は、アイテムがコンテンツ データベースに追加されることを示し、モジュールの `Url` 属性は、SharePoint コンテンツ データベース内のファイルを格納する場所を指定します。

11. マスター ページの配置スコープを変更するには、**ソリューション エクスプローラー** の機能デザイナーで機能ファイルを開き、 **[スコープ]** リストの一覧から新しい配置スコープを選択します。

     値が **Web** の場合は、プロジェクトで現在指定されている Web サイトにのみマスター ページが適用されることを意味します。 値が **Site** の場合は、すべてのサブサイトとルート Web を含む、現在のサイト コレクションにマスター ページが適用されることを意味します。 その他の値は適用されません。

    > [!NOTE]
    > テーマはサイト コレクション レベルにのみ適用されるため、テーマのスコープを **Site** 以外に設定しないことをお勧めします。 テーマがサブサイトで使用されている場合、エラーが発生することがあります。

12. メニュー バーで **[ビルド]**  >  **[ソリューションの配置]** の順に選択します。

13. ファイルが正しく配置されているかどうかを確認するには、SharePoint サイトを開き、 **[サイトの操作]** メニューを選択し、 **[サイトの設定]** コマンドを選択して、 **[マスター ページ]** リンクまたは **[テーマ]** リンクを選択します。

     マスター ページまたはテーマの一覧が表示され、インポートしたマスター ページまたはテーマのいずれかが含まれます。

## <a name="see-also"></a>関連項目
- [マスター ページ](/previous-versions/office/developer/sharepoint-2010/ms443795(v=office.14))
- [既存の SharePoint サイトからの項目のインポート](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)
- [SharePoint のページを作成する](../sharepoint/creating-pages-for-sharepoint.md)
- [モジュールを使用してソリューションにファイルを含める](../sharepoint/using-modules-to-include-files-in-the-solution.md)
