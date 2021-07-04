---
title: ユーザー アカウントでワーカー プロセスを実行する | Microsoft Docs
description: Visual Studio でユーザー アカウントを使用し、ASP.NET ワーカー プロセス (aspnet_wp.exe または w3wp.exe) を実行できるようにコンピューターを設定します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- user accounts, aspnet_wp.exe
- ASP.NET, debugging Web applications
- tools, aspnet_wp.exe
- ASP.NET, tools
- aspnet_wp.exe
ms.assetid: b58e97b1-e62a-4318-aea4-52276ea20735
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 752d09a0d0c6fe49e49e1298d475c90c86991836
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112384643"
---
# <a name="how-to-run-the-worker-process-under-a-user-account"></a>方法: ユーザー アカウントでワーカー プロセスを実行する
ユーザー アカウントを使用して [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] ワーカー プロセス (aspnet_wp.exe または w3wp.exe) を実行できるようにコンピューターを設定するには、次の手順を実行します。

 > [!IMPORTANT]
 > Windows Server 2008 R2 以降、各アプリケーション プールの ID として [ApplicationPoolIdentity](/iis/manage/configuring-security/application-pool-identities) を使用することが推奨されます。

## <a name="procedure"></a>プロシージャ

#### <a name="to-run-aspnet_wpexe-under-a-user-account"></a>ユーザー アカウントで aspnet_wp.exe を実行するには

1. コンピューターでランタイムをインストールしたパスの CONFIG フォルダーにある machine.config ファイルを開きます。

2. &lt;processModel&gt; セクションを見つけ、user 属性と password 属性を、aspnet_wp.exe を実行するユーザー アカウントの名前とパスワードに変更します。

3. machine.config ファイルを保存します。

4. [!INCLUDE[winxpsvr](../debugger/includes/winxpsvr_md.md)] では、既定で、IIS 6.0 がインストールされます。 対応するワーカー プロセスは w3wp.exe です。aspnet_wp.exe をワーカー プロセスとして IIS 6.0 モードで実行するには、次の手順を実行します。

   1. **[スタート]** ボタンをクリックし、 **[管理ツール]** をポイントして、 **[インターネット インフォメーション サービス (IIS) マネージャー]** をクリックします。

   2. **[インターネット インフォメーション サービス]** ダイアログ ボックスの **[Web サイト]** フォルダーを右クリックし、 **[プロパティ]** を選択します。

   3. **[Web サイトのプロパティ]** ダイアログ ボックスの **[サービス]** を選択します。

   4. **[IIS 6.0 プロセス分離モードで WWW サービスを実行する]** をオンにします。

   5. **[プロパティ]** ダイアログ ボックスを閉じ、 **[インターネット サービス マネージャー]** を閉じます。

5. Windows のコマンド プロンプトを開き、次を実行してサーバーをリセットします。

   ```cmd
   iisreset
   ```

   または

   ```cmd
   net stop iisadmin /y
   net start w3svc
   ```

6. [Temporary [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Files] フォルダーを探します。このフォルダーは、[CONFIG] フォルダーと同じパスにあります。 [Temporary [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Files] フォルダーを右クリックし、ショートカット メニューの **[プロパティ]** をクリックします。

7. **[Temporary ASP.NET Files のプロパティ]** ダイアログ ボックスで、 **[セキュリティ]** タブをクリックします。

8. **[詳細設定]** をクリックします。

9. **[Temporary ASP.Net Files のセキュリティの詳細設定]** ダイアログ ボックスで、 **[追加]** をクリックします。

    **[ユーザー、コンピューターまたはグループの選択]** ダイアログ ボックスが表示されます。

10. **[選択するオブジェクト名を入力してください]** ボックスに、ユーザー名を入力して、 **[OK]** をクリックします。 ユーザー名は、次の形式で入力する必要があります: ドメイン名\ユーザー名。

11. **[Temporary ASP.NET Files のアクセス許可のエントリ]** ダイアログ ボックスで、ユーザーに **フル コントロール** を付与し、 **[OK]** をクリックして **[Temporary ASP.NET Files のアクセス許可のエントリ]** ダイアログ ボックスを閉じます。

12. **[セキュリティ]** ダイアログ ボックスが表示され、システム フォルダーのアクセス許可を本当に変更するかどうかの確認が求められます。 **[はい]** をクリックします。

13. **[OK]** をクリックして、 **[Temporary ASP.NET Files のプロパティ]** ダイアログ ボックスを閉じます。

## <a name="see-also"></a>関連項目
- [ASP.NET アプリケーションをデバッグする](../debugger/how-to-enable-debugging-for-aspnet-applications.md)
- [ASP.NET のデバッグ: システム要件](../debugger/aspnet-debugging-system-requirements.md)
