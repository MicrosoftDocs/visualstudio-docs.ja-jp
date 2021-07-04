---
title: Visual Studio を修復します
titleSuffix: ''
description: Visual Studio 2017 のインストールを修復する方法について説明します
ms.date: 10/12/2020
ms.custom: vs-acquisition
ms.topic: how-to
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 55ebb7c44b44a14154cc54f54885455821f9ee68
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386788"
---
# <a name="repair-visual-studio"></a>Visual Studio を修復します

Visual Studio のインストールが損傷したり、破損したりすることがあります。 修復は、更新プログラムを含め、すべてのインストール操作のインストール時の問題を解決するのに役立ちます。

## <a name="when-to-use-repair"></a>修復を使用する場面
* インストール ペイロードの問題が発生している場合。 これは、ディスクへのファイルの書き込みに失敗し、破損したファイルを削除することで修正できない場合に発生する可能性があります。 修復によって、必要なファイルを再取得できます。 
* クライアント側のダウンロードで問題が発生している場合。 接続またはプロキシの問題を解決したことを前提として、修復が役に立つ場合があります。 
* Visual Studio の更新で問題が発生している場合。 修復では、多くの一般的な更新プログラムの問題が修正されます。 

> [!TIP] 
> Windows インストーラーなど、基になる Windows サービスの問題によってインストールの問題が発生した場合は、修復によって同じ問題が発生する可能性があります。 システムの問題には、破損した Windows インストーラーや不安定なインターネット接続などがあります。 システムの問題を確認するには、インストール操作から生成されたエラー レポートを使用します。

> [!NOTE] 
> Visual Studio を修復すると、ユーザー設定がリセットされ、既にあるアセンブリが再インストールされます。 製品の問題が発生している場合は、修復によって問題が解決されない可能性があるため、[Visual Studio フィードバック チケット](https://aka.ms/feedback/suggest?space=8)を作成します。

## <a name="how-to-repair"></a>修復方法
::: moniker range="vs-2017"

1. コンピューター上の **Visual Studio インストーラー** を見つけます。

     たとえば、Windows 10 Anniversary Update 以降を実行しているコンピューター上では、 **[スタート]** を選択し、**Visual Studio インストーラー** としてリスト表示される **V** の文字までスクロールします。

   > [!NOTE]
   > 一部のコンピューターでは、Visual Studio インストーラーが **Microsoft Visual Studio インストーラー** として **"M"** の項に表示される場合があります。
   >
   > Visual Studio インストーラーは `C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe` にもあります。

1. インストーラーを開き、 **[その他]** を選択した後、 **[修復]** を選択します。

    ![Visual Studio インストーラーから Visual Studio を修復する](media/repair-visual-studio.png "Visual Studio インストーラーから Visual Studio を修復する")

   > [!NOTE]
   > Visual Studio を修復すると、環境がリセットされます。 昇格なしでインストールした、ユーザーごとの拡張機能などのローカル カスタマイズや、ユーザー設定、およびプロファイルが削除されます。 テーマ、色、キー バインドなど、同期された設定が復元されます。
   >

   > [!TIP]
   > **[修復]** オプションは、インストールされている Visual Studio のインスタンスに対してのみ表示されます。 **[修復]** オプションが表示されない場合は、Visual Studio インストーラーに "インストール済み" ではなく "使用可能" と表示されているバージョンで **[その他]** を選択した可能性があります。

::: moniker-end

::: moniker range=">=vs-2019"

1. コンピューター上の **Visual Studio インストーラー** を見つけます。

     Windows の [スタート] メニューで "installer" を検索できます。

     ![Visual Studio インストーラー](media/vs-2019/visual-studio-installer.png "Visual Studio インストーラーを検索する")

     > [!NOTE]
     > また、Visual Studio インストーラーは次の場所にもあります。
     >
     > `C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe`

    続行する前に、インストーラーの更新が必要な場合があります。 その場合は、画面の指示に従います。

1. インストーラーで、インストールした Visual Studio のエディションを探します。 次に、 **[その他]** を選択した後、 **[修復]** を選択します。

     ![Visual Studio 2019 を修復する](media/vs-2019/vs-installer-repair.png "Visual Studio 2019 を修復する")

   > [!NOTE]
   > Visual Studio を修復すると、環境がリセットされます。 昇格なしでインストールした、ユーザーごとの拡張機能などのローカル カスタマイズや、ユーザー設定、およびプロファイルが削除されます。 テーマ、色、キー バインドなど、同期された設定が復元されます。
   >

   > [!TIP]
   > **[修復]** オプションは、インストールされている Visual Studio のインスタンスに対してのみ表示されます。 **[修復]** オプションが表示されない場合は、Visual Studio インストーラーに "インストール済み" ではなく "使用可能" と表示されているバージョンで **[その他]** を選択した可能性があります。

::: moniker-end

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目

* [Visual Studio のインストール](install-visual-studio.md)
* [Visual Studio の更新](update-visual-studio.md)
* [Visual Studio のアンインストール](uninstall-visual-studio.md)
* [Visual Studio のインストールとアップグレードの問題のトラブルシューティング](troubleshooting-installation-issues.md)
