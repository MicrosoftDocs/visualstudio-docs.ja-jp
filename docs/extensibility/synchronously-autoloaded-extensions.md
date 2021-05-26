---
title: 同期的に自動的に読み込む拡張機能
description: 拡張機能から同期的に自動読み込みされたパッケージをブロックする、Visual Studio 2019 以降の既定の動作について説明します。
ms.custom: SEO-VS-2020
ms.date: 12/11/2019
ms.topic: conceptual
ms.assetid: 822e3cf8-f723-4ff1-8467-e0fb42358a1f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 35b63f8e84e6879d09fda4c35924b5b9d1d60ccd
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056065"
---
# <a name="synchronously-autoloaded-extensions"></a>同期的に自動的に読み込む拡張機能

同期的に自動読み込みされた拡張機能は、Visual Studio のパフォーマンスに悪影響を及ぼすため、代わりに非同期の自動読み込みを使用するように変更する必要があります。 既定では、Visual Studio 2019 以降は、拡張機能から同期的に自動読み込みされたパッケージをブロックし、ユーザーに通知します。

![拡張機能の互換性に関する警告](media/extension-compatibility-warning-16-1.png.png)

次のようにすることができます。

- **[同期自動読み込みを許可する]** をクリックして、拡張機能を自動読み込みできるようにします。 Visual Studio のオプションでこの設定を変更するには、[環境]、[拡張機能] の順にクリックしてから、[拡張機能の同期自動読み込みを許可します] チェック ボックスをオンにします。 

- **[パフォーマンスを管理]** をクリックして、拡張機能とツール ウィンドウに関するパフォーマンスの問題が表示される [[パフォーマンス マネージャー] ダイアログ](#performance-manager-dialog)を開きます。

- **[現在の拡張機能に対してこのメッセージを表示しない]** をクリックして通知を無視し、インストール済みの既存の拡張機能からの通知が今後表示されないようにします。 同期的に自動読み込みする新しい拡張機能を追加すると、この通知が再び表示されるようになります。 Visual Studio のその他の機能に関する通知は引き続き表示されます。

## <a name="performance-manager-dialog"></a>[パフォーマンス マネージャー] ダイアログ

![[パフォーマンス マネージャー] ダイアログ](media/performance-manager.png)

ユーザー セッションでパッケージを同期的に読み込んだ拡張機能はすべて、 **[非推奨の API]** タブに表示されます。

* **[この問題に関する詳細]** をクリックすると、非推奨の API に関する詳細情報が収集されます。
* 移行の進行状況については、拡張機能のベンダーにお問い合わせください。

## <a name="specify-synchronous-autoload-settings-using-group-policy"></a>グループ ポリシーを使用して同期自動読み込みの設定を指定する

管理者は、グループ ポリシーで同期自動読み込みを許可するようにできます。 これを行うには、次のキーでレジストリ ベースのポリシーを設定します。

**HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\VisualStudio\SynchronousAutoload**

エントリ = **Allowed**

値 = (DWORD)
* **0** は同期自動読み込みが許可されていません
* **1** は同期自動読み込みが許可されています

## <a name="extension-authors"></a>拡張機能の作成者
拡張機能の作成者は、[AsyncPackage への移行](https://github.com/Microsoft/VSSDK-Extensibility-Samples/tree/master/AsyncPackageMigration)に関するページで、パッケージを非同期自動読み込みに移行する手順を確認できます。

## <a name="see-also"></a>関連項目
Visual Studio 2019 での同期自動読み込みの設定の詳細については、[同期自動読み込みの動作](https://devblogs.microsoft.com/visualstudio/updates-to-synchronous-autoload-of-extensions-in-visual-studio-2019/)に関するページをご覧ください。
