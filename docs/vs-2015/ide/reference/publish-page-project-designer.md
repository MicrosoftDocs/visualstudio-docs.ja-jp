﻿---
title: '[発行] ページ (プロジェクト デザイナー) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- Microsoft.VisualStudio.Publish.ClickOnceProvider.Dialog.PropertyPage
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Project Designer, Publish page
- Publish page in Project Designer
ms.assetid: 153527c6-8b95-4003-8e8e-03a489d0a629
caps.latest.revision: 37
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 15fd3f1b93378adba0579b6de50d0e779a09ac5a
ms.sourcegitcommit: 53aa5a413717a1b62ca56a5983b6a50f7f0663b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59658215"
---
# <a name="publish-page-project-designer"></a>[発行] ページ (プロジェクト デザイナー)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

**プロジェクト デザイナー** の **[発行]** ページは、ClickOnce 配置用のプロパティを構成する場合に使用します。  
  
 この **[発行]** ページにアクセスするには、 **ソリューション エクスプローラー**でプロジェクト ノードを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。 **プロジェクト デザイナー** が表示されたら、 **[発行]** タブをクリックします。  
  
> [!NOTE]
>  ここで説明するいくつかの ClickOnce プロパティは、**[ビルド]** メニューの **[発行ウィザード]** または、このページの **[発行ウィザード]** ボタンをクリックして設定することも可能です。  
  
## <a name="uielement-list"></a>UIElement の一覧  
 **発行フォルダーの場所**  
 アプリケーションが発行される場所を指定します。 ドライブ パス (`C:\deploy\myapplication`)、ファイル共有 (`\\server\myapplication`)、FTP サーバー (`ftp://ftp.microsoft.com/myapplication`)、または Web サイト (`http://www.microsoft.com/myapplication`) にすることができます。 **[発行場所]** ボックスでは、テキストは参照 (**[...]**) ボタンが機能する順番で並んでいる必要があります。  
  
 既定の発行場所は、IIS をインストールしている場合は `http://localhost/<projectname>/` で、IIS をインストールしていない場合は、 `publish\` ディレクトリです。 コンピューターが Windows Vista を実行している場合、IIS がインストールされているかどうかにかかわらず、既定は常に `publish\` です。  
  
 **インストール フォルダーの URL**  
 任意。 ユーザーがアプリケーションをインストールする Web サイトを指定します。 これは、アプリケーションがステージング サーバーに発行されるなど、 **発行場所**と異なる場合のみ必要です。  
  
 **インストール モードと設定**  
 ( **[アプリケーションはオンラインでのみ利用できる]** が選択されている場合) アプリケーションが **発行場所** から直接実行されるかどうかを指定します。または ( **[アプリケーションはオフラインでも利用できる]** が選択されている場合) インストールされ、 **[スタート]** メニューおよび **[コントロール パネル]** の **[プログラム追加と削除]** に追加されるかどうかを指定します。  
  
 WPF Web ブラウザー アプリケーションなどのようなアプリケーションは、オンラインでのみ利用できるため、 **[アプリケーションはオフラインでも利用できる]** は無効です。  
  
 **アプリケーション ファイル**  
 [Application Files Dialog Box](http://msdn.microsoft.com/b06dff3a-b87a-4caf-996b-7a4acf8137a8)を開きます。これは、個々のファイルをどのようにまたどこにインストールするかを指定します。  
  
 **必須コンポーネント**  
 [Prerequisites Dialog Box](../../ide/reference/prerequisites-dialog-box.md)を開きます。これは、アプリケーションと共にインストールする .NET Framework などの必須のコンポーネントを指定するために使用します。  
  
 **更新**  
 [Application Updates Dialog Box](http://msdn.microsoft.com/8eca8743-8e68-4d04-bfd5-4dc0a9b2934f)を開きます。これは、アプリケーションの更新の動作の指定に使用します。 **[アプリケーションはオンラインでのみ利用できる]** が選択されている場合は、使用できません。  
  
 **オプション**  
 [Publish Options Dialog Box](http://msdn.microsoft.com/fd9baa1b-7311-4f9e-8ffb-ae50cf110592)を開きます。これは、その他の高度な発行のオプションを指定するために使用します。  
  
 **バージョンの発行**  
 アプリケーションのバージョンの発行番号が設定されます。バージョン番号を変更すると、アプリケーションが更新プログラムとして発行されます。 **メジャー**、 **マイナー**、 **ビルド**、 **リビジョン**のバージョンの発行のそれぞれの最大値は、<xref:System.UInt16.MaxValue>で許可されている 65355 ( <xref:System.Version>) です。  
  
 ClickOnce を使用してアプリケーションの複数のバージョンをインストールすると、以前のバージョンのアプリケーションは、指定した発行場所の Archive というフォルダーに移されます。 以前のバージョンがこのようにアーカイブされることで、インストール ディレクトリが以前のバージョンのフォルダーから分離されます。  
  
 **発行ごとにリビジョンを自動的にインクリメントする**  
 任意。 このオプションが選択されている場合 (既定)、バージョンの発行番号の **[リビジョン]** 部分は、アプリケーションが発行されるたびに 1 ずつインクリメントされます。 これにより、そのアプリケーションが更新プログラムとして発行されます。  
  
 **発行ウィザード**  
 [Publish Wizard](http://msdn.microsoft.com/fc6abebd-13d6-48e4-a567-fbc52dad0872)を開きます。 発行ウィザードの完了は、 **[ビルド]** メニューで **[発行]** コマンドを実行するのと同じ効果があります。  
  
 **今すぐ発行**  
 現在の設定を使用して、アプリケーションを発行します。 **[発行ウィザード]** の **[完了]** ボタンと同じです。  
  
## <a name="see-also"></a>関連項目
 [ClickOnce アプリケーションの発行](../../deployment/publishing-clickonce-applications.md)   
 [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行します。](../../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)   
 [方法: Visual Studio がファイルをコピーする場所を指定します。](../../deployment/how-to-specify-where-visual-studio-copies-the-files.md)   
 [方法: エンドユーザーがからインストールする場所を指定します。](../../deployment/how-to-specify-the-location-where-end-users-will-install-from.md)   
 [方法: テクニカル サポートのリンクを指定します。](../../deployment/how-to-specify-a-link-for-technical-support.md)   
 [方法: 指定の ClickOnce のオフラインまたはオンライン モードのインストール](../../deployment/how-to-specify-the-clickonce-offline-or-online-install-mode.md)   
 [方法: CD インストールの自動開始を有効にします。](../../deployment/how-to-enable-autostart-for-cd-installations.md)   
 [方法: 発行バージョンを設定、ClickOnce](../../deployment/how-to-set-the-clickonce-publish-version.md)   
 [方法: 発行のバージョンに自動的にインクリメント、ClickOnce](../../deployment/how-to-automatically-increment-the-clickonce-publish-version.md)   
 [方法: ClickOnce で発行されるファイルを指定します。](../../deployment/how-to-specify-which-files-are-published-by-clickonce.md)   
 [方法: ClickOnce アプリケーションと共に必須コンポーネントをインストールします。](../../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)   
 [方法: ClickOnce アプリケーションの更新プログラムを管理します。](../../deployment/how-to-manage-updates-for-a-clickonce-application.md)   
 [方法: 変更、ClickOnce アプリケーションの発行の言語](../../deployment/how-to-change-the-publish-language-for-a-clickonce-application.md)   
 [方法: ClickOnce アプリケーションのスタート メニューの名前を指定します。](../../deployment/how-to-specify-a-start-menu-name-for-a-clickonce-application.md)   
 [方法: ClickOnce アプリケーションの発行ページを指定します。](../../deployment/how-to-specify-a-publish-page-for-a-clickonce-application.md)   
 [ClickOnce のセキュリティと配置](../../deployment/clickonce-security-and-deployment.md)
