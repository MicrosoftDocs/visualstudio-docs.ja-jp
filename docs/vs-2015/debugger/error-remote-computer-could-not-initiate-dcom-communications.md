---
title: エラー :リモート コンピューターは DCOM 通信を開始できませんでした。Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.error.unmarshal_callback_failed
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: bbba0766-2502-4ef1-a75d-bf1f0db39e37
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b8ddec2bdec09da1f1175b59c94db31841a1453f
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65697339"
---
# <a name="error-remote-computer-could-not-initiate-dcom-communications"></a>エラー :リモート コンピューターは DCOM 通信を初期化できませんでした
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

リモート コンピューターがローカル コンピューターと通信しようとしたときに DCOM エラーが発生しました。 ローカル コンピューターは、  
  
 Visual Studio を実行しているコンピューターです。 このエラーが発生する原因は複数あります。  
  
- ローカル マシンのファイアウォールが有効になっていない。  
  
- リモート マシンからローカル マシンへの Windows 認証が機能していない。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1. ローカル コンピューターの Windows ファイアウォールが有効にされている場合は、次を参照してください。[設定 Up the Remote Tools のデバイスで](https://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c)ローカル デバッグのファイアウォールを構成する方法についてはします。  
  
2. リモート サーバーからローカル コンピューターのファイル共有を開いてみて Windows 認証をテストします。  
  
3. Windows 認証を復元するために、両方のコンピューターを再起動してみます。 Kerberos エラーがないかどうかローカル コンピューターとリモート コンピューターのイベント ログを確認し、既知の問題がないかどうかドメイン管理者に問い合わせてください。  
  
## <a name="see-also"></a>関連項目  
 [デバイスのリモート ツールのセットアップ](https://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c)
