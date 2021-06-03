---
title: SharePoint ソリューションのセキュリティ | Microsoft Docs
description: SharePoint アプリケーションのセキュリティを強化するために Visual Studio に組み込まれている機能について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- security [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, security
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 588b2af3672851bf7f452287d8383aa2d319347d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99881582"
---
# <a name="security-for-sharepoint-solutions"></a>SharePoint ソリューションのセキュリティ
  [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] には、SharePoint アプリケーションのセキュリティを強化するために、次の機能が組み込まれています。

## <a name="safe-control-entries"></a>安全なコントロール エントリ
 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] で作成されるすべての SharePoint プロジェクト項目には、安全なコントロールのコレクションを表す **安全なコントロール エントリ** プロパティがあります。 その **安全** サブプロパティを使用すると、セキュリティで保護されていると見なされるコントロールを指定できます。 詳細については、「[プロジェクト項目でのパッケージ化と配置の情報を提供する](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)」と「[安全な Web パーツの指定](/previous-versions/office/developer/sharepoint2003/dd583154(v=office.11)#specifying-safe-web-parts)」を参照してください。

## <a name="allowpartiallytrustedcallers-attribute"></a>AllowPartiallyTrustedCallers 属性
 既定では、ランタイム コード アクセス セキュリティ (CAS) システムによって完全に信頼されているアプリケーションのみが、共有マネージド コード アセンブリにアクセスできます。 完全に信頼されたアセンブリを AllowPartiallyTrustedCallers 属性でマークすると、部分的に信頼されたアセンブリからアクセスできるようになります。

 AllowPartiallyTrustedCallers 属性は、システムのグローバル アセンブリ キャッシュ ([!INCLUDE[TLA2#tla_gac](../sharepoint/includes/tla2sharptla-gac-md.md)]) に配置されていない SharePoint ソリューションに追加されます。 これには、サンドボックス ソリューションや SharePoint アプリケーションの Bin ディレクトリに配置されたソリューションが含まれます。 詳細については、「[Microsoft .NET Framework バージョン 1 のセキュリティの変更点](/previous-versions/msp-n-p/ff921345(v=pandp.10))」と「[SharePoint Foundation で Web パーツを展開する](/previous-versions/office/developer/sharepoint-2010/cc768621(v=office.14))」を参照してください。

## <a name="safe-against-script-property"></a>スクリプトに対して安全プロパティ
 "*スクリプト インジェクション*" は、悪意のある可能性があるコードをコントロールや Web ページに挿入することです。 SharePoint 2010 サイトをスクリプト インジェクションから保護するため、既定では共同作成者は Web パーツまたはそのプロパティを表示または編集できません。 この動作は、SafeAgainstScript という名前の SafeControl 属性によって制御されます。 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] では、プロジェクト項目の **安全なコントロール エントリ** のサブプロパティである **スクリプトに対して安全** にこの属性を設定します。 詳細については、「[プロジェクト項目でのパッケージ化と配置の情報を提供する](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)」と「[方法: コントロールを安全なコントロールとしてマークする](../sharepoint/how-to-mark-controls-as-safe-controls.md)」を参照してください。

## <a name="vista-and-windows-7-user-account-control"></a>Vista と Windows 7 のユーザー アカウント制御
 [!INCLUDE[windowsver](../sharepoint/includes/windowsver-md.md)] と [!INCLUDE[win7](../sharepoint/includes/win7-md.md)] には、ユーザー アカウント制御 (UAC) と呼ばれるセキュリティ機能が組み込まれています。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] および [!INCLUDE[windowsver](../sharepoint/includes/windowsver-md.md)] のシステム上の [!INCLUDE[win7](../sharepoint/includes/win7-md.md)] で SharePoint ソリューションを開発する場合は、UAC により、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] をシステム管理者として実行することが求められます。 **[スタート]** メニューから、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] のショートカット メニューを開いた後、 **[管理者として実行]** を選択します。

 常に管理者として実行するように [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] のショートカットを構成するには、そのショートカット メニューを開いて **[プロパティ]** を選択し、 **[プロパティ]** ダイアログ ボックスの **[詳細設定]** ボタンを選択してから、 **[管理者として実行]** チェック ボックスをオンにします。

 詳細については、「[Windows Vista でのユーザー アカウント制御の理解と構成](/previous-versions/windows/it-pro/windows-vista/cc709628(v=ws.10))」 と [Windows 7 のユーザー アカウント制御に関する記事](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731416(v=ws.10))をご覧ください。

## <a name="sharepoint-permissions-considerations"></a>SharePoint の権限に関する考慮事項
 SharePoint ソリューションを開発するには、SharePoint ソリューションを実行し、デバッグするために十分な権限が必要です。 SharePoint ソリューションをテストする前に、次の手順に従って必要な権限を取得してください。

1. 自分のユーザー アカウントをシステムの管理者として追加します。

2. 自分のユーザー アカウントを SharePoint サーバーのファーム管理者として追加します。

    1. SharePoint 2010 サーバーの全体管理で、 **[ファーム管理者グループの管理]** リンクを選択します。

    2. **[ファーム管理者]** ページで、 **[新規作成]** メニュー オプションを選択します

3. 自分のユーザー アカウントを WSS_ADMIN_WPG グループに追加します。

## <a name="additional-security-resources"></a>追加のセキュリティ リソース
 セキュリティに関する問題の詳細については、次を参照してください。

### <a name="visual-studio-security"></a>Visual Studio のセキュリティ

- [セキュリティとユーザー アクセス許可](/previous-versions/visualstudio/visual-studio-2010/ms165099(v=vs.100))

- [ネイティブ コードと .NET Framework コードのセキュリティ](/previous-versions/visualstudio/visual-studio-2010/1787tk12(v=vs.100))

- [.NET Framework におけるセキュリティ](/previous-versions/dotnet/netframework-4.0/fkytk30f(v=vs.100))

### <a name="sharepoint-security"></a>SharePoint のセキュリティ

- [SharePoint Foundation の管理とセキュリティ](/previous-versions/office/developer/sharepoint-2010/ee537811(v=office.14))

- [SharePoint セキュリティ リソース センター](/sharepoint/dev/)

- [SharePoint Foundation の Web パーツをセキュリティで保護する](/previous-versions/office/developer/sharepoint-2010/cc768613(v=office.14))

- [Web アプリケーションのセキュリティの向上: 脅威と対策](/previous-versions/msp-n-p/ff649874(v=pandp.10))

### <a name="general-security"></a>一般的なセキュリティ

- [MSDN セキュリティ開発ライフサイクル](https://www.microsoft.com/msrc?rtc=1)

- [セキュリティで保護された ASP.NET アプリケーションの構築: 認証、認可、セキュリティで保護された通信](/previous-versions/msp-n-p/ff649100(v=pandp.10))

## <a name="see-also"></a>関連項目

- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)