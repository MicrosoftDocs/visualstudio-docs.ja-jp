---
title: '方法: ClickOnce 配置エラー用のカスタム ログ ファイルの場所の設定 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9e247034b22b7fef8e83235cc6666d282720a219
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63406708"
---
# <a name="how-to-set-a-custom-log-file-location-for-clickonce-deployment-errors"></a>方法: ClickOnce 配置エラー用にカスタム ログ ファイルの場所を設定する
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] すべてのデプロイのアクティベーション ログ ファイルを保持します。 これらのログ記録のインストールと初期化に関連するすべてのエラー、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]展開します。 既定では、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]各展開のアクティブ化の 1 つのログ ファイルを作成します。 これらのログ ファイルを Temporary Internet Files フォルダーに格納します。 展開のログ ファイルは、アクティベーション エラーが発生して、ユーザーがクリックしたときに、ユーザーに表示される**詳細**結果のエラー ダイアログ ボックス。

 レジストリ エディターを使用して、特定のクライアントのこの動作を変更することができます (**regedit.exe**) カスタム ログ ファイルのパスを設定します。 この場合、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 1 つのファイルにすべてのデプロイのライセンス認証の成功と失敗を記録します。

> [!CAUTION]
> レジストリ エディターを正しく使用する場合、オペレーティング システムを再インストールする必要があります深刻な問題が発生する可能性があります。 問題が発生する可能性のあることを十分に認識したうえで利用してください。

> [!NOTE]
> 切り捨てるか大きくなりすぎないようにするには、場合によっては、ログ ファイルを削除する必要があります。

 次の手順では、1 つのクライアントのカスタム ログ ファイルの場所を設定する方法について説明します。

### <a name="to-set-a-custom-log-file-location"></a>カスタム ログ ファイルの場所を設定するには

1. 開いている**Regedit.exe**します。

2. ノードに移動`HKCU\Software\Classes\Software\Microsoft\Windows\CurrentVersion\Deployment`します。

3. 文字列値を設定`LogFilePath`の完全なパスと、任意のカスタム ログの場所のファイル名にします。

     この場所は、ユーザーが書き込みアクセス権を持っているディレクトリにある必要があります。 たとえば、Windows vista では、次のフォルダー構造を作成し、設定`LogFilePath`に*C:\Users\\\<ユーザー名 > \Documents\Logs\ClickOnce\installation.log*します。

## <a name="see-also"></a>関連項目
- [ClickOnce 配置のトラブルシューティング](../deployment/troubleshooting-clickonce-deployments.md)