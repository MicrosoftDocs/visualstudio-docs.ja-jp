---
title: カスタム ログ ファイルの場所を設定する (ClickOnce 配置エラー)
description: ClickOnce ですべての配置に対して保持されるアクティブ化ログ ファイルについて説明します。これには、ClickOnce 配置のインストールと初期化に関するエラーが記録されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- troubleshooting ClickOnce deployments
- ClickOnce deployment, troubleshooting
- ClickOnce deployment, error logging
ms.assetid: 77424414-7f0e-4b99-94bb-ea130de92d09
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: e527e1aec630faadec6e594f944a6715028c6d82
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99885054"
---
# <a name="how-to-set-a-custom-log-file-location-for-clickonce-deployment-errors"></a>方法: ClickOnce 配置エラー用にカスタム ログ ファイルの場所を設定する
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] では、すべての配置のアクティブ化ログ ファイルが保持されます。 これらのログには、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置のインストールと初期化に関連するエラーが記録されます。 既定では、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] によって、配置のアクティブ化ごとに 1 つのログ ファイルが作成されます。 これらのログ ファイルは、Temporary Internet Files フォルダーに格納されます。 アクティブ化エラーが発生すると、配置のログ ファイルがユーザーに表示されます。ユーザーは、発生したエラーのダイアログ ボックスで **[詳細]** をクリックします。

 レジストリ エディター (**regedit.exe**) を使用してカスタム ログ ファイルのパスを設定することで、特定のクライアントのこの動作を変更できます。 この場合、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] によって、すべての配置のアクティブ化の成功と失敗が 1 つのファイルに記録されます。

> [!CAUTION]
> レジストリ エディタの使用を誤ると、オペレーティング システムの再インストールが必要になるような深刻な問題を引き起こす可能性があります。 問題が発生する可能性のあることを十分に認識したうえで利用してください。

> [!NOTE]
> ログ ファイルが大きくなりすぎないように、場合によってはログ ファイルを切り捨てるか削除する必要があります。

 次の手順では、1 つのクライアントのカスタム ログ ファイルの場所を設定する方法を説明します。

### <a name="to-set-a-custom-log-file-location"></a>カスタム ログ ファイルの場所を設定するには

1. **Regedit.exe** を開きます。

2. `HKCU\Software\Classes\Software\Microsoft\Windows\CurrentVersion\Deployment` ノードに移動します。

3. 文字列値 `LogFilePath` を、選択したカスタム ログの場所の完全なパスとファイル名に設定します。

     この場所は、ユーザーが書き込みアクセス権を持つディレクトリ内である必要があります。 たとえば、Windows Vista では、次のフォルダー構造を作成し、`LogFilePath` を *C:\Users\\\<username>Documents\Logs\ClickOnce\installation.log* に設定します。

## <a name="see-also"></a>関連項目
- [ClickOnce 配置のトラブルシューティング](../deployment/troubleshooting-clickonce-deployments.md)