---
title: SharePoint ソリューションのデバッグ | Microsoft Docs
description: Visual Studio デバッガーを使用して SharePoint ソリューションをデバッグします。 F5 キーのデバッグおよび配置プロセス、デバッグ ワークフロー、およびフィーチャー イベント レシーバーのデバッグについて説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.Project.WebConfigModificationDialog
- VS.SharePointTools.Project.DebuggingNotEnabled
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, debugging
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f1a6abfbafcbafb9daa52fdc6af85156700efef7
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99948948"
---
# <a name="debug-sharepoint-solutions"></a>SharePoint ソリューションをデバッグする
  SharePoint ソリューションは、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] デバッガーを使用してデバッグできます。 デバッグを開始すると、プロジェクト ファイルが [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によって SharePoint サーバーに配置され、SharePoint サイトのインスタンスが Web ブラウザーで開きます。 以下のセクションでは、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で SharePoint アプリケーションをデバッグする方法について説明します。

- [デバッグの有効化](#enable-debugging)

- [F5 キーのデバッグおよび配置プロセス](#f5-debug-and-deployment-process)

- [SharePoint プロジェクトのフィーチャー](#sharepoint-project-features)

- [デバッグ ワークフロー](#debug-workflows)

- [フィーチャー イベント レシーバーのデバッグ](#debug-feature-event-receivers)

- [拡張デバッグ情報の有効化](#enable-enhanced-debugging-information)

## <a name="enable-debugging"></a>デバッグの有効化
 SharePoint ソリューションを [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で初めてデバッグするとき、デバッグを有効にするように web.config ファイルが構成されていないことを警告するダイアログ ボックスが表示されます。 web.config ファイルは SharePoint サーバーのインストール時に作成されます。 詳細については、「[Web.config ファイルを使用して作業する](/previous-versions/office/developer/sharepoint-2010/ms460914(v=office.14))」を参照してください。このダイアログ ボックスでは、デバッグせずにプロジェクトを実行するか、デバッグを有効にするように web.config ファイルを編集するかを、選択できるようになっています。 前者を選択した場合、プロジェクトは通常どおりに実行されます。 後者を選択した場合、web.config ファイルは次のように構成されます。

- 呼び出し履歴は有効にする (`CallStack="true"`)

- [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] のカスタム エラーは無効にする (`<customErrors mode="Off" />`)

- コンパイル デバッグは有効にする (`<compilation debug="true">`)

  結果として生成される web.config ファイルは、次のとおりです。

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <configuration>
        ...
        <SharePoint>
            <SafeMode MaxControls="200"
                CallStack="true"
                DirectFileDependencies="10"
                TotalFileDependencies="50"
                AllowPageLevelTrace="false">
                ...
            </SafeMode>
        ...
        </SharePoint>
        <system.web>
            ...
            <customErrors mode="Off" />
            ...
            <compilation debug="true">
            ...
            </compilation>
            ...
        </system.web>
        ...
    </configuration>
```

 変更を元に戻し、デバッグを無効にするには、web.config ファイルで、次の [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] を変更します。

- 呼び出し履歴は無効にする (`CallStack="false"`)

- [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] のカスタム エラーは有効にする (`<customErrors mode="On" />`)

- コンパイル デバッグは無効にする (`<compilation debug="false">`)

## <a name="f5-debug-and-deployment-process"></a>F5 キーのデバッグおよび配置プロセス
 SharePoint プロジェクトをデバッグ モードで実行するとき、SharePoint の配置プロセスによって、次のタスクが実行されます。

1. カスタマイズ可能な配置前コマンドが実行されます。

2. [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] コマンドを使用して、Web ソリューション パッケージ (.wsp) ファイルが作成されます。 この .wsp ファイルには、すべての必要なファイルおよびフィーチャーが含まれます。 詳細については、「[ソリューションの概要](/previous-versions/office/developer/sharepoint-2010/aa543214(v=office.14))」を参照してください。

3. SharePoint ソリューションがファーム ソリューションである場合は、指定されたサイトの [!INCLUDE[TLA2#tla_iis5](../sharepoint/includes/tla2sharptla-iis5-md.md)] の [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] アプリケーション プールがリサイクルされます。 この段階で、[!INCLUDE[TLA2#tla_iis5](../sharepoint/includes/tla2sharptla-iis5-md.md)] のワーカー プロセスによってロックされたファイルが解放されます。

4. 以前のバージョンのパッケージが既に存在する場合は、.wsp ファイル内の以前のバージョンのフィーチャーおよびファイルが取り消されます。 この段階で、フィーチャーが非アクティブ化され、ソリューション パッケージがアンインストールされた後に、ソリューション パッケージが SharePoint サーバーから削除されます。

5. .wsp ファイル内の最新のバージョンのフィーチャーおよびファイルがインストールされます。 この段階で、SharePoint サーバーにソリューションが追加され、インストールされます。

6. ワークフローの場合は、ワークフロー アセンブリがインストールされます。 その場所は、 *[アセンブリの場所]* プロパティを使用して変更できます。

7. スコープがサイトまたは Web の場合は、SharePoint でプロジェクトのフィーチャーがアクティブ化されます。 ファーム スコープおよび Web アプリケーション スコープのフィーチャーはアクティブ化されません。

8. ワークフローの場合は、**SharePoint カスタマイズ ウィザード** で選択した SharePoint ライブラリ、リスト、またはサイトにワークフローが関連付けられます。

   > [!NOTE]
   > この関連付けは、ウィザードで **[ワークフローを自動的に関連付ける]** を選択した場合にのみ行われます。

9. カスタマイズ可能な配置後コマンドが実行されます。

10. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] デバッガーを [!INCLUDE[sharepointShort](../sharepoint/includes/sharepointshort-md.md)] プロセス (*w3wp.exe*) にアタッチします。 プロジェクトの種類で *[サンドボックス ソリューション]* プロパティを変更でき、その値が **true** に設定されている場合、デバッガーは別のプロセス (*SPUCWorkerProcess.exe*) にアタッチされます。 詳細については、「[サンドボックス ソリューションに関する考慮事項](../sharepoint/sandboxed-solution-considerations.md)」を参照してください。

11. SharePoint ソリューションがファーム ソリューションである場合は、JavaScript デバッガーが開始されます。

12. 適切なライブラリ、リスト、またはサイト ページが Web ブラウザーに表示されます。

    タスクが 1 つ完了するたびに、ステータス メッセージが [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] の出力ウィンドウに表示されます。 タスクを完了できなかった場合は、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] の [エラー一覧] ウィンドウにエラー メッセージが表示されます。

## <a name="sharepoint-project-features"></a>SharePoint プロジェクトのフィーチャー
 フィーチャーは、サイト定義を使用することによってサイトの変更を単純化する、移植性のあるモジュール式の機能単位です。 これは、特定のスコープに対してアクティブ化でき、ユーザーが特定の目的またはタスクを達成するのを支援する [!INCLUDE[sharepointShort](../sharepoint/includes/sharepointshort-md.md)] (WSS) 要素のパッケージでもあります。 テンプレートはフィーチャーとして配置されます。

 プロジェクトをデバッグ モードで実行すると、配置プロセスにより、 *%COMMONPROGRAMFILES%\Microsoft Shared\web server extensions\14\TEMPLATE\FEATURES* の *feature* ディレクトリにフォルダーが作成されます。 フィーチャーには、"*プロジェクト名* _Feature *x* という形式の名前が付きます (TestProject_Feature1 など)。

 feature ディレクトリに作成された、ソリューションのフォルダーには、"*フィーチャー定義*" ファイルと "*ワークフロー定義*" ファイルが格納されます。 フィーチャー定義ファイル (Feature.xml) には、プロジェクトのフィーチャーに含まれているファイルについて記述されています。プロジェクト定義ファイル (*Elements.xml*) には、プロジェクト テンプレートについて記述されています。 *Elements.xml* は **ソリューション エクスプローラー** に表示されますが、Feature.xml はフィーチャー パッケージの作成時に生成されます。 これらの種類のファイルの詳細については、「[SharePoint プロジェクトとプロジェクト項目テンプレート](../sharepoint/sharepoint-project-and-project-item-templates.md)」を参照してください。

## <a name="debug-workflows"></a>デバッグ ワークフロー
 ワークフロー プロジェクトをデバッグすると、その種類に応じたワークフロー テンプレートが [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によってライブラリまたはリストに追加されます。 このワークフロー テンプレートは手動で開始できるほか、項目を追加または更新することによって開始することもできます。 これで、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] を使用してワークフローをデバッグできます。

> [!NOTE]
> その他のアセンブリに参照を追加する場合は、アセンブリがグローバル アセンブリ キャッシュ ([!INCLUDE[TLA2#tla_gac](../sharepoint/includes/tla2sharptla-gac-md.md)]) にインストールされていることを確認してください。 そうしないと、ワークフロー ソリューションは失敗します。 アセンブリをインストールする方法については、「[ドキュメントまたはアイテムでワークフローを手動で起動する](https://support.office.com/article/Manually-start-a-workflow-on-a-document-or-item-5C106E0E-6FF2-4A75-AF99-F01653BC7963)」を参照してください。

 ただし、配置プロセスでは、ワークフローは開始されません。 SharePoint Web サイトからワークフローを開始する必要があります。 Microsoft Office Word 2010 などのクライアント アプリケーションや別個のサーバー側のコードを使用して、ワークフローを開始することもできます。 **SharePoint カスタマイズ ウィザード** が指定するアプローチのいずれかを使用してください。

 たとえば、ワークフローの手動での開始を許可した場合は、ライブラリまたはリスト内のアイテムから、ワークフローを直接開始します。 ワークフローを手動で開始する方法の詳細については、「[ドキュメントまたはアイテムでワークフローを手動で起動する](https://support.office.com/article/Manually-start-a-workflow-on-a-document-or-item-5C106E0E-6FF2-4A75-AF99-F01653BC7963)」を参照してください。

## <a name="debug-feature-event-receivers"></a>フィーチャー イベント レシーバーのデバッグ
 既定では、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint アプリケーションを実行すると、そのフィーチャーが SharePoint サーバー上で自動的にアクティブ化されます。 ただし、フィーチャー イベント レシーバーをデバッグする際は、このことが問題になります。[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によってアクティブ化されたフィーチャーは、デバッガーとは異なるプロセスで実行されるためです。 つまり、ブレークポイントなどの一部のデバッグ機能が正常に機能しなくなるということです。

 SharePoint でフィーチャーが自動的にアクティブ化される動作を無効にし、フィーチャー イベント レシーバーが適切にデバッグされるようにするには、プロジェクトの **[アクティブな配置構成]** プロパティの値を **[アクティブ化しない]** に設定してからデバッグを実行します。 そのうえで、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で SharePoint アプリケーションのデバッグを開始してから、SharePoint でフィーチャーを手動でアクティブ化します。 フィーチャーをアクティブ化するには、SharePoint の **[サイトの操作]** メニューの **[サイトの設定]** をクリックし、 **[サイト フィーチャーの管理]** リンクをクリックして、フィーチャーの横にある **[アクティブ化]** をクリックします。その後、通常どおりにデバッグを続けます。

## <a name="enable-enhanced-debugging-information"></a>拡張デバッグ情報の有効化
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] プロセス (devenv.exe)、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint ホスト プロセス (*vssphost4.exe*)、SharePoint、および WCF レイヤー間の相互作用がときには複雑であるため、ビルドや配置などの実行中に発生したエラーを診断することが困難な場合があります。 拡張デバッグ情報を有効にすると、こうしたエラーが解決しやすくなります。 これを行うには、まず Windows レジストリで次のレジストリ キーに移動します。

 **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\11.0\SharePointTools**

 "EnableDiagnostics" **REG_DWORD** 値が存在しない場合は、手動で作成します。 "EnableDiagnostics" の値を "1" に設定します。

 このキー値を 1 に設定すると、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] の実行時にプロジェクト システム エラーが発生するたびに、 **[出力]** ウィンドウにスタック トレース情報が表示されます。 強化されたデバッグ情報を無効にするには、EnableDiagnostics を 0 に戻すか、この値を削除します。

 その他の SharePoint レジストリ キーの詳細については、「[Visual Studio での SharePoint ツールの拡張機能のデバッグ](../sharepoint/debugging-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションのトラブルシューティング](../sharepoint/troubleshooting-sharepoint-solutions.md)
