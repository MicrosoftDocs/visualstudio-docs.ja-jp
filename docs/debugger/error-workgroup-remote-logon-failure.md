---
title: エラー :ワークグループ リモート ログオン エラー |Microsoft Docs
ms.date: 11/04/2016
ms.topic: troubleshooting
f1_keywords:
- vs.debug.error.workgroup_remote_logon_failure
dev_langs:
- CSharp
- VB
- FSharp
- JScript
- C++
helpviewer_keywords:
- logon failure, remote debugging
- remote debugging, logon failure
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 1b197913abecbaf2ff74913a41720f464646fc67
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2019
ms.locfileid: "53848049"
---
# <a name="error-workgroup-remote-logon-failure"></a>エラー :ワークグループ リモート ログオン エラー
このエラーには、次のメッセージが表示されます。  
  
 ログオン エラー: 不明なユーザー名、または不適切なパスワードです。  
  
 **原因**  
  
 このエラーは、ワークグループのコンピューターからデバッグしているときにリモート コンピューターに接続しようとすると発生することがあります。 以下の原因が考えられます。  
  
-   名前とパスワードが一致するアカウントがリモート コンピューター上に存在しない。  
  
-   Visual Studio コンピューターとリモート コンピューターの両方がワークグループに存在する場合、リモート コンピューターの **[ローカル セキュリティ ポリシー]** 設定の既定値によって、このエラーが発生することがあります。 **[ローカル セキュリティ ポリシー]** 設定の既定値は **[Guest のみ - ローカル ユーザーが Guest として認証する]** です。 このセットアップでデバッグするには、リモート コンピューターの設定を **[クラシック - ローカル ユーザーがローカル ユーザーとして認証する]** に変更する必要があります。  
  
> [!NOTE]
>  次のタスクを実行するには、管理者権限が必要です。  
  
### <a name="to-open-the-local-security-policy-window"></a>[ローカル セキュリティ ポリシー] ウィンドウを開くには  
  
1.  **secpol.msc** Microsoft 管理コンソール スナップインを開始します。 Windows Search、[ファイル名を指定して実行] ボックス、またはコマンド プロンプトで「secpol.msc」と入力します。  
  
### <a name="to-add-user-rights-assignments"></a>ユーザー権限の割り当てを追加するには  
  
1.  **[ローカル セキュリティ ポリシー]** ウィンドウを開きます。  
  
2.  **[ローカル ポリシー]** フォルダーを展開します。  
  
3.  **[ユーザー権利の割り当て]** をクリックします。  
  
4.  **[ポリシー]** 列の **[プログラムのデバッグ]** をダブルクリックして、**[ローカル セキュリティ ポリシーの設定]** ダイアログ ボックスに現在のローカル グループ ポリシーの割り当てを表示します。  
  
     ![ローカル セキュリティ ポリシーのユーザー権限](../debugger/media/dbg_err_localsecuritypolicy_userrightsdebugprograms.png "DBG_ERR_LocalSecurityPolicy_UserRightsDebugPrograms")  
  
5.  新しいユーザーを追加するには、**[ユーザーまたはグループの追加]** をクリックします。  
  
### <a name="to-change-the-sharing-and-security-model"></a>共有とセキュリティ モデルを変更するには  
  
1.  **[ローカル セキュリティ ポリシー]** ウィンドウを開きます。  
  
2.  **[ローカル ポリシー]** フォルダーを展開します。  
  
3.  **[セキュリティ オプション]** をクリックします。  
  
4.  **ポリシー**列をダブルクリックして**ネットワーク アクセス。ローカル アカウントの共有とセキュリティ モデル**します。  
  
5.  **ネットワーク アクセス。ローカル アカウントの共有とセキュリティ モデル** ダイアログ ボックスに、値を変更**クラシック - ローカル ユーザー自身として認証** をクリックし、**適用**ボタンをクリックします。  
  
     ![ローカル セキュリティ ポリシーのセキュリティ オプション](../debugger/media/dbg_err_localsecuritypolicy_securityoptions_networkaccess.png "DBG_ERR_LocalSecurityPolicy_SecurityOptions_NetworkAccess")  
  
## <a name="see-also"></a>「  
 [リモート デバッグ エラーとトラブルシューティング](../debugger/remote-debugging-errors-and-troubleshooting.md)   
 [Remote Debugging](../debugger/remote-debugging.md)