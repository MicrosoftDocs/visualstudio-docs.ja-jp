---
title: エンタープライズ展開に既定値を設定する
description: Visual Studio のエンタープライズ展開で使用するドメイン ポリシーとその他の構成操作について説明します。
ms.date: 04/13/2021
ms.custom: seodec18
ms.topic: conceptual
f1_keywords:
- gpo
- policy
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 9B7B4608-7A3F-4FF4-BDCE-42D9F7CE6DBA
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: cc88e6ffe91b111626fa76057742233527bf203f
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112306905"
---
# <a name="set-defaults-for-enterprise-deployments-of-visual-studio"></a>Visual Studio のエンタープライズ展開に既定値を設定する

Visual Studio の展開に影響するレジストリ ポリシーを設定することができます。 これらのポリシーはコンピューターに対してグローバルであり、次の場合に影響があります。

- 他のバージョンまたはインスタンスと共有されているパッケージがいくつかインストールされている場合
- パッケージのキャッシュ場所とキャッシュされているかどうか
- 管理者の更新プログラムを適用する方法

これらのポリシーのいくつかを[コマンド ライン オプション](use-command-line-parameters-to-install-visual-studio.md)を使用して設定してコンピューターのレジストリ値を設定できるだけでなく、グループ ポリシーを使用して組織全体にこれらを配布することもできます。

## <a name="registry-keys"></a>レジストリ キー

一部の場所にエンタープライズの既定を設定して、グループ ポリシーまたは直接レジストリから、それらを管理できます。 Visual Studio は順番にエンタープライズ ポリシーが設定されているかを確認し、以下の順番でポリシー値が検出された時点で、残りのキーは無視されます。

1. `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\VisualStudio\Setup`
2. `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\Setup`
3. `HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\VisualStudio\Setup` (64 ビット オペレーティング システム)

いくつかのレジストリ値は、未設定の場合、最初に使われたときに自動的に設定されます。 これにより、以後のインストールでも同じ値が使われるようになります。 これらの値は、2 番目のレジストリ キーである `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\Setup` に格納されます。

以下のレジストリ値を設定できます。

::: moniker range="vs-2017"

| **名前**                      | **Type**                    | **[Default]**                                         | **説明**                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|-------------------------------|-----------------------------|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `CachePath`                   | `REG_SZ` または `REG_EXPAND_SZ` | %ProgramData%\Microsoft\VisualStudio\Packages       | パッケージ マニフェストと、ペイロード (省略可能) が格納されるディレクトリ。 詳細については、「[パッケージ キャッシュの無効化または移動](disable-or-move-the-package-cache.md)」ページを参照してください。                                                                                                                                                                                                                                                                                        |
| `KeepDownloadedPayloads`      | `REG_DWORD`                 | 1                                                   | パッケージのペイロードはインストール後も保持されます。 この値はいつでも変更できます。 ポリシーを無効にすると、修復または変更するインスタンスでキャッシュされたパッケージのペイロードがすべて削除されます。 詳細については、「[パッケージ キャッシュの無効化または移動](disable-or-move-the-package-cache.md)」ページを参照してください。                                                                                                                                                                             |
| `SharedInstallationPath`      | `REG_SZ` または `REG_EXPAND_SZ` | %ProgramFiles(x86)%\Microsoft Visual Studio\Shared  | Visual Studio の異なるバージョンのインスタンスで共有されているパッケージがいくつかインストールされているディレクトリ。 値はいつでも変更できますが、変更が反映されるのは以後のインストールのみです。 元の場所に既にインストールされている製品は移動しないでください。移動すると、正しく機能しない場合があります。                                                                                                                                                                                  |
| `BackgroundDownloadDisabled`  | `REG_DWORD`                 | 0                                                   | インストールされているすべての Visual Studio 製品に対して、更新プログラムが自動的にダウンロードされないようにします。 この値はいつでも変更できます。                                                                                                                                                                                                                                                                                                                                             |
| `AdministratorUpdatesEnabled` | `REG_DWORD`                 | 0                                                   | 管理者向け更新プログラムをクライアント コンピューターに適用することを許可します。 この値が指定されていないか、0 に設定されている場合、管理者向け更新プログラムはブロックされます。 この値は管理用です。 詳細については、[管理者向け更新プログラムを有効にする](enabling-administrator-updates.md)方法に関するページを参照してください。                                                                                                                                                                                      |
| `AdministratorUpdatesOptOut`  | `REG_DWORD`                 | 0                                                   | ユーザーが Visual Studio の管理者向け更新プログラムの受け取りを希望していないことを示します。 このレジストリ値がない、または値 0 が設定されている場合は、Visual Studio ユーザーが Visual Studio の管理者向け更新プログラムの受け取りを希望していることを意味します。 これは開発者ユーザー向けです (クライアント コンピューター上に管理者権限がある場合)。 詳細については、[管理者向け更新プログラムを適用する](../install/applying-administrator-updates.md#understanding-configuration-options)方法に関するページを参照してください。 |
| `UpdateConfigurationFile`     | `REG_SZ` または `REG_EXPAND_SZ` | %ProgramData%\Microsoft\VisualStudio\updates.config | 管理者向け更新プログラムを構成するためのファイル パス。 詳細については、「[管理者向け更新プログラムを構成する方法](../install/applying-administrator-updates.md#methods-for-configuring-an-administrator-update)」を参照してください。                                                                                                                                                                                                                                             |

::: moniker-end

::: moniker range="vs-2019"

| **名前**                         | **Type**                    | **[Default]**                                         | **説明**                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|----------------------------------|-----------------------------|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `CachePath`                      | `REG_SZ` または `REG_EXPAND_SZ` | %ProgramData%\Microsoft\VisualStudio\Packages       | パッケージ マニフェストと、ペイロード (省略可能) が格納されるディレクトリ。 詳細については、「[パッケージ キャッシュの無効化または移動](disable-or-move-the-package-cache.md)」ページを参照してください。                                                                                                                                                                                                                                                                                        |
| `KeepDownloadedPayloads`         | `REG_DWORD`                 | 1                                                   | パッケージのペイロードはインストール後も保持されます。 この値はいつでも変更できます。 ポリシーを無効にすると、修復または変更するインスタンスでキャッシュされたパッケージのペイロードがすべて削除されます。 詳細については、「[パッケージ キャッシュの無効化または移動](disable-or-move-the-package-cache.md)」ページを参照してください。                                                                                                                                                                             |
| `SharedInstallationPath`         | `REG_SZ` または `REG_EXPAND_SZ` | %ProgramFiles(x86)%\Microsoft Visual Studio\Shared  | Visual Studio の異なるバージョンのインスタンスで共有されているパッケージがいくつかインストールされているディレクトリ。 値はいつでも変更できますが、変更が反映されるのは以後のインストールのみです。 元の場所に既にインストールされている製品は移動しないでください。移動すると、正しく機能しない場合があります。                                                                                                                                                                                  |
| `BackgroundDownloadDisabled`     | `REG_DWORD`                 | 0                                                   | インストールされているすべての Visual Studio 製品に対して、更新プログラムが自動的にダウンロードされないようにします。 この値はいつでも変更できます。                                                                                                                                                                                                                                                                                                                                             |
| `AdministratorUpdatesEnabled`    | `REG_DWORD`                 | 0                                                   | 管理者向け更新プログラムをクライアント コンピューターに適用することを許可します。 この値が指定されていないか、0 に設定されている場合、管理者向け更新プログラムはブロックされます。 この値は管理用です。 詳細については、[管理者向け更新プログラムを有効にする](enabling-administrator-updates.md)方法に関するページを参照してください。                                                                                                                                                                                      |
| `AdministratorUpdatesOptOut`     | `REG_DWORD`                 | 0                                                   | ユーザーが Visual Studio の管理者向け更新プログラムの受け取りを希望していないことを示します。 このレジストリ値がない、または値 0 が設定されている場合は、Visual Studio ユーザーが Visual Studio の管理者向け更新プログラムの受け取りを希望していることを意味します。 これは開発者ユーザー向けです (クライアント コンピューター上に管理者権限がある場合)。 詳細については、[管理者向け更新プログラムを適用する](../install/applying-administrator-updates.md#understanding-configuration-options)方法に関するページを参照してください。 |
| `UpdateConfigurationFile`        | `REG_SZ` または `REG_EXPAND_SZ` | %ProgramData%\Microsoft\VisualStudio\updates.config | 管理者向け更新プログラムを構成するためのファイル パス。 詳細については、「[管理者向け更新プログラムを構成する方法](../install/applying-administrator-updates.md#methods-for-configuring-an-administrator-update)」を参照してください。                                                                                                                                                                                                                                             |
| `BaselineStickinessVersions2019` | `REG_SZ` または `REG_EXPAND_SZ` | `16.7.0`                                            | クライアントが使用すべきサービス ベースラインのマイナー バージョン。 詳細については、[管理者向け更新プログラムを適用する](../install/applying-administrator-updates.md#understanding-configuration-options)方法に関するページを参照してください。                                                                                                                                                                                                                                                    |

::: moniker-end

::: moniker range=">=vs-2022"

| **名前**                         | **Type**                    | **[Default]**                                         | **説明**                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|----------------------------------|-----------------------------|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `CachePath`                      | `REG_SZ` または `REG_EXPAND_SZ` | %ProgramData%\Microsoft\VisualStudio\Packages       | パッケージ マニフェストと、ペイロード (省略可能) が格納されるディレクトリ。 詳細については、「[パッケージ キャッシュの無効化または移動](disable-or-move-the-package-cache.md)」ページを参照してください。                                                                                                                                                                                                                                                                                        |
| `KeepDownloadedPayloads`         | `REG_DWORD`                 | 1                                                   | パッケージのペイロードはインストール後も保持されます。 この値はいつでも変更できます。 ポリシーを無効にすると、修復または変更するインスタンスでキャッシュされたパッケージのペイロードがすべて削除されます。 詳細については、「[パッケージ キャッシュの無効化または移動](disable-or-move-the-package-cache.md)」ページを参照してください。                                                                                                                                                                             |
| `SharedInstallationPath`         | `REG_SZ` または `REG_EXPAND_SZ` | %ProgramFiles%\Microsoft Visual Studio\Shared       | Visual Studio の異なるバージョンのインスタンスで共有されているパッケージがいくつかインストールされているディレクトリ。 値はいつでも変更できますが、変更が反映されるのは以後のインストールのみです。 元の場所に既にインストールされている製品は移動しないでください。移動すると、正しく機能しない場合があります。                                                                                                                                                                                  |
| `BackgroundDownloadDisabled`     | `REG_DWORD`                 | 0                                                   | インストールされているすべての Visual Studio 製品に対して、更新プログラムが自動的にダウンロードされないようにします。 この値はいつでも変更できます。                                                                                                                                                                                                                                                                                                                                             |
| `AdministratorUpdatesEnabled`    | `REG_DWORD`                 | 0                                                   | 管理者向け更新プログラムをクライアント コンピューターに適用することを許可します。 この値が指定されていないか、0 に設定されている場合、管理者向け更新プログラムはブロックされます。 この値は管理用です。 詳細については、[管理者向け更新プログラムを有効にする](enabling-administrator-updates.md)方法に関するページを参照してください。                                                                                                                                                                                      |
| `AdministratorUpdatesOptOut`     | `REG_DWORD`                 | 0                                                   | ユーザーが Visual Studio の管理者向け更新プログラムの受け取りを希望していないことを示します。 このレジストリ値がない、または値 0 が設定されている場合は、Visual Studio ユーザーが Visual Studio の管理者向け更新プログラムの受け取りを希望していることを意味します。 これは開発者ユーザー向けです (クライアント コンピューター上に管理者権限がある場合)。 詳細については、[管理者向け更新プログラムを適用する](../install/applying-administrator-updates.md#understanding-configuration-options)方法に関するページを参照してください。 |
| `UpdateConfigurationFile`        | `REG_SZ` または `REG_EXPAND_SZ` | %ProgramData%\Microsoft\VisualStudio\updates.config | 管理者向け更新プログラムを構成するためのファイル パス。 詳細については、「[管理者向け更新プログラムを構成する方法](../install/applying-administrator-updates.md#methods-for-configuring-an-administrator-update)」を参照してください。                                                                                                                                                                                                                                             |
| `BaselineStickinessVersions2019` | `REG_SZ` または `REG_EXPAND_SZ` | `16.7.0`                                            | クライアントが使用すべきサービス ベースラインのマイナー バージョン。 詳細については、[管理者向け更新プログラムを適用する](../install/applying-administrator-updates.md#understanding-configuration-options)方法に関するページを参照してください。                                                                                                                                                                                                                                                    |

::: moniker-end

> [!IMPORTANT]
> インストール後に `CachePath` のレジストリ ポリシーを変更する場合は、既存のパッケージ キャッシュを新しい場所に移動して、`SYSTEM` および `Administrators` にフル コントロールが、`Everyone` に読み取りアクセスが可能になるようにセキュリティを保護する必要があります。
> 既存のキャッシュの移動やセキュリティの保護に失敗すると、今後のインストールで問題が発生する場合があります。

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目

- [Visual Studio のインストール](install-visual-studio.md)
- [Visual Studio 管理者ガイド](visual-studio-administrator-guide.md)
- [管理者の更新を適用する](applying-administrator-updates.md)
- [パッケージ キャッシュの無効化または移動](disable-or-move-the-package-cache.md)
- [コマンド ライン パラメーターを使用して Visual Studio をインストールする](use-command-line-parameters-to-install-visual-studio.md)
