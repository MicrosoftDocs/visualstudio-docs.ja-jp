---
title: ClickOnce アプリケーションの発行 | Microsoft Docs
description: 発行ウィザードを使用して ClickOnce アプリケーションを初めて発行する方法について説明します。 以降の変更は、プロジェクト デザイナーの [発行] ページで行います。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- Microsoft.VisualStudio.Publish.ClickOnceProvider.Dialog.Options
- Microsoft.VisualStudio.Publish.ClickOnceProvider.PublishWizard.Help
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, publishing
- ClickOnce applications, publishing
- applications [Visual Studio], ClickOnce deployment
- deploying applications [ClickOnce], publishing ClickOnce applications
ms.assetid: eb6dfe79-f54c-4331-8e36-073688e70973
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: fa9e94bf124888d05b6393a4821b5db61181871c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99927575"
---
# <a name="publish-clickonce-applications"></a>ClickOnce アプリケーションの発行
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを最初に発行するときに、発行ウィザードを使用して発行プロパティを設定できます。 このウィザードで設定できるのはプロパティの一部のみです。その他のプロパティはすべて、既定値に設定されます。

 それ以降に発行プロパティを変更するには、**プロジェクト デザイナー** の **[発行]** ページを使用します。

## <a name="publish-wizard"></a>発行ウィザード
 発行ウィザードを使用して、アプリケーションを発行するときの基本的な設定を指定できます。 たとえば、次の発行プロパティが含まれます。

- 発行フォルダーの場所 - Visual Studio がファイルをコピーする場所 (ローカル コンピューター、ネットワーク ファイル共有、FTP サーバー、または Web サイト)。

- インストール フォルダーの場所 - エンド ユーザーがインストールを開始する場所 (ネットワーク ファイル共有、FTP サーバー、Web サイト、CD/DVD)。

- オンラインまたはオフラインの可用性 - エンド ユーザーがネットワーク接続でアプリケーションにアクセスできるかどうか。

- 更新間隔 - 新しい更新プログラムをアプリケーションがチェックする頻度。

  詳細については、「[方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)」を参照してください。

## <a name="publish-page"></a>ページの発行
 **プロジェクト デザイナー** の **[発行]** ページは、ClickOnce 配置用のプロパティを構成する場合に使用します。 次の表にトピックを示します。

|タイトル|説明|
|-----------|-----------------|
|[方法: Visual Studio がファイルをコピーする場所を指定する](../deployment/how-to-specify-where-visual-studio-copies-the-files.md)|Visual Studio がアプリケーション ファイルとマニフェストを配置する場所を設定する方法について説明します。|
|[方法: エンド ユーザーがインストールを開始する場所を指定する](../deployment/how-to-specify-the-location-where-end-users-will-install-from.md)|ユーザーがアプリケーションをダウンロードし、インストールするためにアクセスする場所を設定する方法について説明します。|
|[方法: ClickOnce のオフラインまたはオンラインのインストール モードを指定する](../deployment/how-to-specify-the-clickonce-offline-or-online-install-mode.md)|アプリケーションをオフラインまたはオンラインで使用できるかどうかを設定する方法について説明します。|
|[方法: ClickOnce の発行するバージョンを設定する](../deployment/how-to-set-the-clickonce-publish-version.md)|発行するアプリケーションを更新プログラムとして扱うかどうかを指定する、ClickOnce の **[発行するバージョン]** プロパティの設定方法について説明します。|
|[方法: ClickOnce の発行するバージョンを自動的にインクリメントする](../deployment/how-to-automatically-increment-the-clickonce-publish-version.md)|アプリケーションを発行するたびに、**PublishVersion** のリビジョン番号を自動的にインクリメントする方法について説明します。|

 詳細については、「[[発行] ページ (プロジェクト デザイナー)](../ide/reference/publish-page-project-designer.md)」を参照してください

### <a name="application-files-dialog-box"></a>[アプリケーション ファイル] ダイアログ ボックス
 このダイアログ ボックスでは、発行、動的ダウンロード、および更新のために、プロジェクト内のファイルを分類する方法を指定できます。 このダイアログ ボックスには、既定では除外されないプロジェクト ファイル、またはダウンロード グループのあるプロジェクト ファイルを一覧にしたグリッドが含まれています。

 ファイルの除外、ファイルに対するデータ ファイルや必須コンポーネントのマーク、および Visual Studio UI で条件付きインストールを実行するためのファイル グループの作成を行うには、「[方法: ClickOnce で発行されるファイルを指定する](../deployment/how-to-specify-which-files-are-published-by-clickonce.md)」を参照してください。 また、Mage.exe を使用してデータ ファイルにマークすることもできます。 詳しくは、「[方法: ClickOnce アプリケーションにデータ ファイルを含める](../deployment/how-to-include-a-data-file-in-a-clickonce-application.md)」をご覧ください。

### <a name="prerequisites-dialog-box"></a>[必須コンポーネント] ダイアログ ボックス
 このダイアログ ボックスでは、必須コンポーネントとしてインストールするコンポーネントおよびそのインストール方法を指定します。 詳細については、「[方法: ClickOnce アプリケーションと共に必須コンポーネントをインストールする](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)」および「[[必須コンポーネント] ダイアログ ボックス](../ide/reference/prerequisites-dialog-box.md)」を参照してください。

### <a name="application-updates-dialog-box"></a>[アプリケーションの更新] ダイアログ ボックス
 このダイアログ ボックスでは、アプリケーションのインストール時に更新プログラムをチェックする方法を指定します。 詳細については、「[方法: ClickOnce アプリケーションの更新プログラムを管理する](../deployment/how-to-manage-updates-for-a-clickonce-application.md)」を参照してください。

### <a name="publish-options-dialog-box"></a>[発行オプション] ダイアログ ボックス
 [発行オプション] ダイアログ ボックスでは、アプリケーションの配置オプションを指定します。

|タイトル|説明|
|-|-|
|[方法: ClickOnce アプリケーションの発行言語を変更する](../deployment/how-to-change-the-publish-language-for-a-clickonce-application.md)|言語およびカルチャを指定してローカライズ版と対応付ける方法について説明します。|
|[方法: ClickOnce アプリケーションのスタート メニューの名前を指定する](../deployment/how-to-specify-a-start-menu-name-for-a-clickonce-application.md)|ClickOnce アプリケーションの表示名を変更する方法について説明します。|
|[方法: テクニカル サポートのリンクを指定する](../deployment/how-to-specify-a-link-for-technical-support.md)|**[サポート URL]** プロパティを設定する方法について説明します。このプロパティには、ユーザーがアプリケーションに関する情報を取得するためにアクセスする Web ページまたはファイル共有を指定します。|
|[方法: ClickOnce 配置で個々の必要条件にサポート URL を指定する](../deployment/how-to-specify-a-support-url-for-individual-prerequisites-in-a-clickonce-deployment.md)|各必要条件の個別のサポート URL が含まれるようにアプリケーション マニフェストを手動で変更する方法を説明します。|
|[方法: ClickOnce アプリケーションの発行ページを指定する](../deployment/how-to-specify-a-publish-page-for-a-clickonce-application.md)|既定の Web ページ (publish.htm) とアプリケーションを生成および発行する方法について説明します。|
|[方法: ClickOnce の既定の Web ページをカスタマイズする](../deployment/how-to-customize-the-default-web-page-for-a-clickonce-application.md)|アプリケーションと共に自動的に生成および発行された Web ページをカスタマイズする方法について説明します。|
|[方法: CD インストールの自動開始を有効にする](../deployment/how-to-enable-autostart-for-cd-installations.md)|メディアを挿入したときに ClickOnce アプリケーションが自動的に起動するように、自動開始を有効にする方法について説明します。|

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[方法: ClickOnce アプリケーションのファイルの関連付けを作成する](../deployment/how-to-create-file-associations-for-a-clickonce-application.md)|ClickOnce アプリケーションにファイル名の拡張子のサポートを追加する方法について説明します。|
|[方法: オンライン ClickOnce アプリケーションでクエリ文字列を取得する](../deployment/how-to-retrieve-query-string-information-in-an-online-clickonce-application.md)|ClickOnce アプリケーションの実行用 URL に渡されるパラメーターを取得する方法を説明します。|
|[方法: デザイナーを使用して ClickOnce アプリケーションの URL アクティベーションを無効にする](../deployment/how-to-disable-url-activation-of-clickonce-applications-by-using-the-designer.md)|デザイナーを使用して、ユーザーが **[スタート]** メニューからアプリケーションを起動するように強制する方法について説明します。|
|[方法: ClickOnce アプリケーションの URL アクティべーションを無効にする](../deployment/how-to-disable-url-activation-of-clickonce-applications.md)|ユーザーが **[スタート]** メニューからアプリケーションを起動するように強制する方法について説明します。|
|[チュートリアル: デザイナーを使用し、ClickOnce 配置 API で必要に応じてアセンブリをダウンロードする](../deployment/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer.md)|デザイナーを使用して、アプリケーションで初めて使用するときにのみアプリケーション アセンブリをダウンロードする方法を説明します。|
|[チュートリアル : ClickOnce 配置 API を使用して必要に応じてアセンブリをダウンロードする](../deployment/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api.md)|アプリケーションで初めて使用するときにのみアプリケーション アセンブリをダウンロードする方法を説明します。|
|[チュートリアル : ClickOnce 配置 API を使用して必要に応じてサテライト アセンブリをダウンロードする](../deployment/walkthrough-downloading-satellite-assemblies-on-demand-with-the-clickonce-deployment-api.md)|サテライト アセンブリをオプションとしてマークする方法、および現在のカルチャ設定にクライアント コンピューターが必要とするアセンブリのみをダウンロードする方法について説明します。|
|[チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)|.NET Framework ユーティリティを使用して ClickOnce アプリケーションを配置する方法を説明します。|
|[チュートリアル: 再署名が不要で商標を保持する ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-app-no-re-signing-required.md)|.NET Framework ユーティリティを使用して、マニフェストに再署名せずに ClickOnce アプリケーションを配置する方法について説明します。|
|[方法: プロジェクトを構成してターゲット プラットフォームを設定する](../ide/how-to-configure-projects-to-target-platforms.md)|プロジェクトの **[対象の CPU]** プロパティまたは **[プラットフォーム ターゲット]** プロパティを変更して、64 ビット プロセッサ用に発行する方法について説明します。|
|[チュートリアル: ClickOnce アプリケーションを複数の .NET Framework バージョンで実行できるようにする](/previous-versions/dd996998(v=vs.100))|複数バージョンの .NET Framework で ClickOnce アプリケーションのインストールと実行を行う方法について説明します。|
|[チュートリアル: ClickOnce アプリケーションのカスタム インストーラーの作成](../deployment/walkthrough-creating-a-custom-installer-for-a-clickonce-application.md)|カスタム インストーラーを作成し、ClickOnce アプリケーションをインストールする方法について説明します。|
|[方法: Visual スタイルが有効になっている WPF アプリケーションを公開する](../deployment/how-to-publish-a-wpf-application-with-visual-styles-enabled.md)|Visual スタイルが有効になっている WPF アプリケーションを発行しようとしたときに表示されるエラーを解決する手順について説明します。|

## <a name="see-also"></a>関連項目
- [ClickOnce のセキュリティと配置](../deployment/clickonce-security-and-deployment.md)
- [ClickOnce に関するリファレンス](../deployment/clickonce-reference.md)