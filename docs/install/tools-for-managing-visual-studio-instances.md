---
title: Visual Studio インスタンスの検出および管理用のツール
titleSuffix: ''
description: クライアント コンピューター上の Visual Studio のインストールを検出して管理するために使用できるツールについて説明します。
ms.date: 04/06/2021
ms.custom: seodec18
ms.topic: conceptual
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 85686707-14C0-4860-9B7A-66485D43D241
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 914449fe1db792614af1f9ed22464cb9fdb91481
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112306892"
---
# <a name="tools-for-detecting-and-managing-visual-studio-instances"></a>Visual Studio インスタンスの検出および管理用のツール

クライアント コンピューター上の Visual Studio のインストールを検出し、インストールを管理するために使用できるツールがいくつかあります。

## <a name="detecting-existing-visual-studio-instances"></a>既存の Visual Studio インスタンスの検出

次のツールとユーティリティを使用すると、クライアント コンピューターにインストールされている Visual Studio インスタンスを検出および管理するのに役立ちます。

* [**vswhere**](https://github.com/microsoft/vswhere): Visual Studio に組み込まれているか、個別のディストリビューションで使用可能な実行可能ファイルです。特定のコンピューター上のすべての Visual Studio インスタンスの場所を見つけるのに役立ちます。
* [**VSSetup.PowerShell**](https://github.com/microsoft/vssetup.powershell): セットアップ構成 API を使用して Visual Studio のインストール済みインスタンスを識別する PowerShell スクリプトです。
* [**VS-Setup-Samples**](https://github.com/microsoft/vs-setup-samples): セットアップ構成 API を使用して既存のインストールを照会する方法を示す C# と C++ のサンプルです。
* [**Windows Management Instrumentation (WMI)**](/windows/win32/wmisdk/wmi-start-page): Visual Studio のインスタンス情報は、Visual Studio のクラス MSFT_VSInstance を使用して照会できます。
* [**セットアップ構成 API**](<xref:Microsoft.VisualStudio.Setup.Configuration>) は、Visual Studio インスタンスを問い合わせるために独自のユーティリティを構築する開発者向けのインターフェイスを提供します。
* [**Microsoft Endpoint Configuration Manager ソフトウェア インベントリ**](/mem/configmgr/core/clients/manage/inventory/introduction-to-software-inventory): クライアント デバイス上の Visual Studio インスタンスに関する情報を収集するために使用できます。

## <a name="using-vswhereexe"></a>vswhere.exe の使用

`vswhere.exe` は Visual Studio 2017 以降に自動的に含まれていますが、[vswhere リリース ページ](https://github.com/Microsoft/vswhere/releases)からダウンロードすることもできます。 ツールのヘルプ情報を取得する場合は `vswhere -?` を使用します。 たとえば、このコマンドを使用すると、製品の以前のバージョンとプレリリースを含む Visual Studio のすべてのリリースが表示され、結果が JSON 形式で出力されます。

```shell
C:\Program Files (x86)\Microsoft Visual Studio\Installer> vswhere.exe -legacy -prerelease -format json
```

## <a name="using-windows-management-instrumentation-wmi"></a>Windows Management Instrumentation (WMI) の使用

コンピューターに Visual Studio Client Detector Utility がインストールされている場合は、WMI を使用して Visual Studio インスタンス情報を照会できます。 Visual Studio Client Detector Utility は、2020 年 5 月 12 日以降にリリースされたすべての Visual Studio 2017、Visual Studio 2019、Visual Studio 2022 の更新プログラムにより既定でインストールされます。 個別にインストールする場合は、[Microsoft Update カタログ](https://catalog.update.microsoft.com/)からも入手できます。  ユーティリティを使用して Visual Studio インスタンス情報を返す方法の例については、クライアント コンピューターで管理者として PowerShell を開き、次のコマンドを入力します。

```shell
Get-CimInstance MSFT_VSInstance
```

## <a name="using-microsoft-endpoint-configuration-manager"></a>Microsoft Endpoint Configuration Manager の使用

[Microsoft Endpoint Configuration Manager ソフトウェア インベントリ](/mem/configmgr/core/clients/manage/inventory/introduction-to-software-inventory)機能を使用して、クライアント デバイス上の Visual Studio インスタンスに関する情報のクエリを実行し、収集することができます。 たとえば、次のクエリを実行すると、インストールされているすべての Visual Studio 2017 および 2019 インスタンスについて、Visual Studio がインストールされている表示名、バージョン、およびデバイス名が返されます。

```WQL
select distinct SMS_G_System_COMPUTER_SYSTEM.Name, SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName, SMS_G_System_ADD_REMOVE_PROGRAMS.Version from SMS_R_System inner join SMS_G_System_COMPUTER_SYSTEM on SMS_G_System_COMPUTER_SYSTEM.ResourceID = SMS_R_System.ResourceId inner join SMS_G_System_ADD_REMOVE_PROGRAMS on SMS_G_System_ADD_REMOVE_PROGRAMS.ResourceID = SMS_R_System.ResourceId where SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName like "Visual Studio %[a-z]% 201[7,9]" 
```

::: moniker range="vs-2017"

> [!TIP]
> Visual Studio 2017 のインストールの詳細については、[Visual Studio セットアップのアーカイブ](https://devblogs.microsoft.com/setup/tag/vs2017/)に関するブログ記事を参照してください。

::: moniker-end

## <a name="editing-the-registry-for-a-visual-studio-instance"></a>Visual Studio インスタンスのレジストリの編集

Visual Studio ではレジストリ設定はプライベートな場所に保存されているため、同じバージョンの Visual Studio の複数のインスタンスを side-by-side で同じコンピューターで使用できます。

これらのエントリはグローバル レジストリには保存されないため、レジストリ エディターを使用してレジストリ設定を変更するための特別な指示があります。

1. Visual Studio で開いているインスタンスがある場合は、閉じてください。

1. `regedit.exe`を起動します。

1. `HKEY_LOCAL_MACHINE` ノードを選択します。

1. レジストリ エディターのメイン メニューから **[ファイル]**  >  **[ハイブの読み込み...]** を選択して、**AppData\Local** フォルダーに保存されているプライベート レジストリ ファイルを選択します。 次に例を示します。

   ```shell
   %localappdata%\Microsoft\VisualStudio\<config>\privateregistry.bin
   ```

   > [!NOTE]
   > `<config>` は参照する Visual Studio のインスタンスに対応します。

分離されたハイブの名前になるハイブ名を指定するように求められます。 これを行うと、作成した分離されたハイブの下にあるレジストリを参照できるようになります。

> [!IMPORTANT]
> Visual Studio を再度開始する前に、作成した分離されたハイブをアップロードする必要があります。 これを行うには、レジストリ エディターのメイン メニューから **[ファイル]**  >  **[ハイブのアンロード]** の順に選択します。 (これを行わない場合、ファイルがロックされたままになり、Visual Studio で開始することができません。)

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目

* [Visual Studio 管理者ガイド](../install/visual-studio-administrator-guide.md)
