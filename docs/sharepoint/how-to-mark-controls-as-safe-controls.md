---
title: '方法: コントロールを安全なコントロールとしてマークする | Microsoft Docs'
description: アセンブリを追加するときに、SharePoint プロジェクト項目の "安全なコントロール エントリ" プロパティまたはパッケージ デザイナーで、コントロールを安全なコントロールとしてマークします。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, safe controls
- SharePoint development in Visual Studio, advanced packaging tools
- safe controls [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: bf7e2f2c5b0de59a5f1cac91f0df9cefbf15bda8
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99964707"
---
# <a name="how-to-mark-controls-as-safe-controls"></a>方法: コントロールを安全なコントロールとしてマークする
  セキュリティのために、SharePoint では、スクリプト インジェクションから保護されている Web コントロールと保護されていない Web コントロールが区別されます。 保護されたコントロール (*安全なコントロール*) は、信頼されていないユーザーがアクセスできます。 パッケージにアセンブリを追加するときに、SharePoint プロジェクト項目の "安全なコントロール エントリ" プロパティまたは "**パッケージ デザイナー**" で、コントロールを安全としてマークすることができます。 詳細については、「

- [web.config ファイルの設定の変更](/previous-versions/office/developer/sharepoint-2007/bb802890(v=office.12))に関するページ、および[安全なコントロールとしての Web パーツ アセンブリの登録](/previous-versions/office/developer/sharepoint2003/dd587360(v=office.11))に関するページを参照してください。

> [!IMPORTANT]
> これらの手順は、説明を目的としています。 コントロールを安全としてマークするのは、コントロールが安全であることが確実である場合のみにしてください。

## <a name="marking-safe-controls-in-the-safe-control-entries-property"></a>"安全なコントロール エントリ" プロパティでコントロールを安全としてマークする

#### <a name="to-mark-controls-as-safe-or-unsafe-in-the-safe-control-entries-property"></a>"安全なコントロール エントリ" プロパティでコントロールを安全または安全でないとしてマークするには

1. 視覚的 Web パーツ プロジェクトを使用して SharePoint ソリューションを作成します。

2. 2 つのコントロール (テキスト ボックスとボタン) を Web パーツに追加します。 これらの名前は、それぞれ既定値の TextBox1 と Button1 のままにします。

3. Web パーツの "**安全なコントロール エントリ**" プロパティに 2 つのエントリを追加します。 これを行うには、 **[プロパティ]** ウィンドウの **[安全なコントロール エントリ]** プロパティの横にある省略記号 (![ASP.NET モバイル デザイナーの省略記号](../sharepoint/media/mwellipsis.gif "ASP.NET モバイル デザイナー楕円")) ボタンをクリックします。

     **[安全なコントロール エントリ]** ダイアログ ボックスが表示されます。

4. **[安全なコントロール エントリ]** ダイアログ ボックスで、 **[追加]** ボタンを 2 回クリックして、 **[メンバー]** ウィンドウに 2 つの安全なコントロール エントリ (1 つはボタン用、もう 1 つはテキスト ボックス用) を追加します。

5. 1 つ目の安全なコントロール エントリを選択してから、 **[安全]** プロパティの値を **[False]** に、その **[型名]** プロパティを **[Button1]** に、その **[スクリプトに対して安全]** プロパティを **[False]** に変更します。

     この手順では、ボタン コントロールが安全でないコントロールとして識別されます。

6. 一覧で 2 つ目の安全なコントロール エントリを選択します。 **[安全]** プロパティの値を **[True]** のままにして、その **[型名]** プロパティを **[TextBox1]** に設定し、その **[スクリプトに対して安全]** プロパティを **[True]** に設定します。

     これでテキスト ボックス コントロールが、スクリプト インジェクションに対して安全なコントロールとしてマークされました。

7. **[OK]** をクリックしてダイアログ ボックスを閉じます。

## <a name="marking-safe-controls-in-the-package-designer"></a>パッケージ デザイナーでの安全なコントロールとしてマークする

#### <a name="to-mark-controls-as-safe-or-unsafe-in-the-package-designer"></a>パッケージ デザイナーでコントロールを安全または安全でないとしてマークするには

1. 視覚的 Web パーツ プロジェクトを使用して SharePoint ソリューションを作成します。

2. 2 つのコントロール (テキスト ボックスとボタン) を Web パーツに追加します。 これらの名前は、それぞれ既定値の TextBox1 と Button1 のままにします。

     コントロールの名前空間は、後で使用するため、メモしておいてください。

3. メニュー バーで **[ビルド]**  >  **[ソリューションのビルド]** を選択してプロジェクトをビルドします。

4. 別の SharePoint ソリューションを作成します。

5. **ソリューション エクスプローラー** で、*Package.Package* ファイルのショートカット メニューを開き、 **[開く]** をクリックして **パッケージ デザイナー** を開きます。

6. **パッケージ デザイナー** で、 **[詳細設定]** タブを選択します。

7. **[追加アセンブリ]** で **[追加]** ボタンを選択し、一覧の **[既存のアセンブリの追加]** を選択します。

8. **[既存のアセンブリの追加]** ダイアログ ボックスで、 **[ソース パス]** の横にある省略記号 (![ASP.NET モバイル デザイナーの省略記号](../sharepoint/media/mwellipsis.gif "ASP.NET モバイル デザイナー楕円")) ボタンを選択します。

9. 手順 1 で作成した SharePoint ソリューションからアセンブリを選択し、 **[開く]** を選択します。

10. この例では、 **[配置ターゲット]** オプションを GlobalAssemblyCache のままにします。

     この手順により、アセンブリがシステムのグローバル アセンブリ キャッシュ (GAC) に配置されます。 アセンブリを Web アプリケーション (Bin) フォルダーに配置する場合は、代わりにそのオプションを選択します。 詳細については、「[SharePoint Foundation で Web パーツを配置する](/previous-versions/office/developer/sharepoint-2010/cc768621(v=office.14))」を参照してください。

11. **[安全なコントロール]** ボックスで、 **[新しい項目を追加するにはここをクリックします]** を選択します。

12. 次の表のプロパティの値を入力します。

    |プロパティ名|値|
    |-------------------|-----------|
    |名前空間|コントロールの完全修飾名前空間 (**BdcModelProject1.VisualWebPart1** など)。|
    |種類名|ボタン 1|
    |アセンブリ名|厳密なアセンブリ名 (Microsoft.Office.SharePoint.ClientExtensions, Version=14.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c など)。|
    |Safe|**[安全]** チェック ボックスをオフにします。|
    |スクリプトに対して安全|**[スクリプトに対して安全]** チェック ボックスをオフのままにします。|

    > [!NOTE]
    > **パッケージ デザイナー** の **[詳細設定]** タブで追加したアセンブリの **[アセンブリ名]** の値をトークンにすることはできません。これは厳密な名前付きアセンブリである必要があります。 詳しくは、「[厳密な名前付きアセンブリの作成と使用](/previous-versions/dotnet/netframework-4.0/xwb8f617(v=vs.100))」をご覧ください。

13. **Tab** キーを押して、別の安全なコントロール エントリを作成します。

14. **[新しい項目を追加するにはここをクリックします]** ボタンをもう一度選択します。

15. 次の表のプロパティの値を入力します。

    |プロパティ名|値|
    |-------------------|-----------|
    |名前空間|コントロールの完全修飾名前空間 (**BdcModelProject1.VisualWebPart1** など)。|
    |種類名|TextBox1|
    |アセンブリ名|厳密なアセンブリ名 (Microsoft.Office.SharePoint.ClientExtensions, Version=14.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c など)。|
    |Safe|**[安全]** チェック ボックスをオンにします。|
    |スクリプトに対して安全|**[スクリプトに対して安全]** チェック ボックスをオンにします。|

16. **Tab** キーを押してから、 **[OK]** ボタンを選択してダイアログ ボックスを閉じます。

## <a name="see-also"></a>関連項目
- [プロジェクト項目でのパッケージ化と配置の情報を提供する](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)
- [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
