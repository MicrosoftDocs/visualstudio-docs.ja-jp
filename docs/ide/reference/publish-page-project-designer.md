---
title: "[発行] ページ (プロジェクト デザイナー) | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- Microsoft.VisualStudio.Publish.ClickOnceProvider.Dialog.PropertyPage
helpviewer_keywords:
- Project Designer, Publish page
- Publish page in Project Designer
author: gewarren
ms.author: gewarren
manager: ghogen
ms.workload:
- multiple
ms.openlocfilehash: d9f050662ed38814920e17b36f77bf6795aabfa9
ms.sourcegitcommit: 238cd48787391aa0ed1eb684f3f04e80f7958705
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2018
---
# <a name="publish-page-project-designer"></a>[発行] ページ (プロジェクト デザイナー)
**プロジェクト デザイナー** の **[発行]** ページは、ClickOnce 配置用のプロパティを構成する場合に使用します。  
  
 この **[発行]** ページにアクセスするには、 **ソリューション エクスプローラー**でプロジェクト ノードを選択し、 **[プロジェクト]** メニューの **[プロパティ]**をクリックします。 **プロジェクト デザイナー** が表示されたら、 **[発行]** タブをクリックします。  
  
> [!NOTE]
>  ここで説明するいくつかの ClickOnce プロパティは、**[ビルド]** メニューの **[発行ウィザード]** または、このページの **[発行ウィザード]** ボタンをクリックして設定することも可能です。  
  
## <a name="uielement-list"></a>UIElement の一覧  
 **発行フォルダーの場所**  
 アプリケーションが発行される場所を指定します。 ドライブ パス (`C:\deploy\myapplication`)、ファイル共有 (`\\server\myapplication`)、または FTP サーバー (`ftp://ftp.microsoft.com/myapplication`) にすることができます。 **[発行場所]** ボックスでは、テキストは参照 (**[...]**) ボタンが機能する順番で並んでいる必要があります。  
   
 **インストール フォルダーの URL**  
 任意。 ユーザーがアプリケーションをインストールする Web サイトを指定します。 これは、アプリケーションがステージング サーバーに発行されるなど、 **発行場所**と異なる場合のみ必要です。  
  
 **インストール モードと設定**  
 ( **[アプリケーションはオンラインでのみ利用できる]** が選択されている場合) アプリケーションが **発行場所** から直接実行されるかどうかを指定します。または ( **[アプリケーションはオフラインでも利用できる]** が選択されている場合) インストールされ、 **[スタート]** メニューおよび **[コントロール パネル]** の **[プログラム追加と削除]** に追加されるかどうかを指定します。  
  
 WPF Web ブラウザー アプリケーションなどのようなアプリケーションは、オンラインでのみ利用できるため、 **[アプリケーションはオフラインでも利用できる]** は無効です。  
  
 **アプリケーション ファイル**  
 [アプリケーション ファイル] ダイアログ ボックスを開きます。これは、個々のファイルをどのようにまたどこにインストールするかを指定します。  
  
 **必須コンポーネント**  
 [必須コンポーネント] ダイアログ ボックスを開きます。これは、アプリケーションと共にインストールする .NET Framework などの必須のコンポーネントを指定するために使用します。  
  
 **更新**  
 [アプリケーションの更新] ダイアログ ボックスを開きます。これは、アプリケーションの更新の動作の指定に使用します。 **[アプリケーションはオンラインでのみ利用できる]** が選択されている場合は、使用できません。  
  
 **オプション**  
 [発行オプション] ダイアログ ボックスを開きます。これは、その他の高度な発行のオプションを指定するために使用します。  
  
 **バージョンの発行**  
 アプリケーションのバージョンの発行番号が設定されます。バージョン番号を変更すると、アプリケーションが更新プログラムとして発行されます。 **メジャー**、 **マイナー**、 **ビルド**、 **リビジョン**のバージョンの発行のそれぞれの最大値は、<xref:System.UInt16.MaxValue>で許可されている 65355 ( <xref:System.Version>) です。  
  
 ClickOnce を使用してアプリケーションの複数のバージョンをインストールすると、以前のバージョンのアプリケーションは、指定した発行場所の Archive というフォルダーに移されます。 以前のバージョンがこのようにアーカイブされることで、インストール ディレクトリが以前のバージョンのフォルダーから分離されます。  
  
 **発行ごとにリビジョンを自動的にインクリメントする**  
 任意。 このオプションが選択されている場合 (既定)、バージョンの発行番号の **[リビジョン]** 部分は、アプリケーションが発行されるたびに 1 ずつインクリメントされます。 これにより、そのアプリケーションが更新プログラムとして発行されます。  
  
 **発行ウィザード**  
 発行ウィザードを開きます。 発行ウィザードの完了は、 **[ビルド]** メニューで **[発行]** コマンドを実行するのと同じ効果があります。  
  
 **今すぐ発行**  
 現在の設定を使用して、アプリケーションを発行します。 **[発行ウィザード]** の **[完了]** ボタンと同じです。  
  
## <a name="see-also"></a>参照  
 [ClickOnce アプリケーションの発行](../../deployment/publishing-clickonce-applications.md)   
 [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)   
 [方法: Visual Studio がファイルをコピーする場所を指定する](../../deployment/how-to-specify-where-visual-studio-copies-the-files.md)   
 [方法: エンド ユーザーがインストールを開始する場所を指定する](../../deployment/how-to-specify-the-location-where-end-users-will-install-from.md)   
 [方法: テクニカル サポートのリンクを指定する](../../deployment/how-to-specify-a-link-for-technical-support.md)   
 [方法: ClickOnce のオフラインまたはオンラインのインストール モードを指定する](../../deployment/how-to-specify-the-clickonce-offline-or-online-install-mode.md)   
 [方法 : CD インストールの自動開始を有効にする](../../deployment/how-to-enable-autostart-for-cd-installations.md)   
 [方法: ClickOnce の発行バージョンを設定する](../../deployment/how-to-set-the-clickonce-publish-version.md)   
 [方法: ClickOnce の発行バージョンを自動的にインクリメントする](../../deployment/how-to-automatically-increment-the-clickonce-publish-version.md)   
 [方法: ClickOnce で発行されるファイルを指定する](../../deployment/how-to-specify-which-files-are-published-by-clickonce.md)   
 [方法: ClickOnce アプリケーションと共に必須コンポーネントをインストールする](../../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)   
 [方法 : ClickOnce アプリケーションの更新プログラムを管理する](../../deployment/how-to-manage-updates-for-a-clickonce-application.md)   
 [方法: ClickOnce アプリケーションの発行言語を変更する](../../deployment/how-to-change-the-publish-language-for-a-clickonce-application.md)   
 [方法 : ClickOnce アプリケーションのスタート メニューの名前を指定する](../../deployment/how-to-specify-a-start-menu-name-for-a-clickonce-application.md)   
 [方法: ClickOnce アプリケーションの発行ページを指定する](../../deployment/how-to-specify-a-publish-page-for-a-clickonce-application.md)   
 [ClickOnce のセキュリティと配置](../../deployment/clickonce-security-and-deployment.md)
