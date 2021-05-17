---
title: 詳細ログ ファイルを指定する (ClickOnce 配置)
description: Clickonce 配置のインストール、初期化、更新、アンインストールについて ClickOnce によって管理されるアクティビティ ログの詳細度を指定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- logs, ClickOnce deployment
- ClickOnce deployment, logging
ms.assetid: 0807a28d-2e40-4a51-ab10-308d808ded6b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 7adb711c77f4bb2dead3190d40065e148760b034
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99887472"
---
# <a name="how-to-specify-verbose-log-files-for-clickonce-deployments"></a>方法: ClickOnce 配置用の詳細ログ ファイルを指定する
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] では、すべての配置について、アクティビティ ログ ファイルが管理されます。 これらのログでは、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置のインストール、初期化、更新、アンインストールに関連する詳細が文書化されます。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] からこれらのログ ファイルに書き込まれる詳細を増やすには、レジストリ エディター (*regedit.exe*) を使用して詳細レベルを指定します。

> [!CAUTION]
> レジストリ エディターの使用を誤ると、オペレーティング システムの再インストールが必要になる可能性がある深刻な問題を引き起こすおそれがあります。 問題が発生する可能性のあることを十分に認識したうえで利用してください。

 次の手順で、現在のユーザーの [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ログ ファイルの詳細レベルを指定する方法について説明します。 詳細レベルを引き下げるには、このレジストリ値を削除します。

### <a name="to-specify-verbose-log-files"></a>詳細ログ ファイルを指定するには

1. *Regedit.exe* を開きます。

2. ノード **HKEY_CURRENT_USER\Software\Classes\Software\Microsoft\Windows\CurrentVersion\Deployment** に移動します。

3. 必要に応じて、`LogVerbosityLevel` という名前の新しい文字列値を作成します。

4. `LogVerbosityLevel` の値を `1` に設定します。

## <a name="see-also"></a>関連項目
- [ClickOnce 配置のトラブルシューティング](../deployment/troubleshooting-clickonce-deployments.md)