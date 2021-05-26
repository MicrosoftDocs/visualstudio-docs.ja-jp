---
title: Visual Studio 2017 の機能拡張の破壊的変更
description: Visual Studio 2017 の機能拡張モデルに加えられた破壊的変更の技術的な詳細と、これらに対応するためにユーザーが実行できる内容について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 11/09/2016
ms.topic: conceptual
ms.assetid: 54d5af60-0b44-4ae1-aa57-45aa03f89f3d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c07d48eb63c727701c3b6fcde9d405f9c96abec1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105068194"
---
# <a name="changes-in-visual-studio-2017-extensibility"></a>Visual Studio 2017 の機能拡張の変更

Visual Studio 2017 は、ユーザー システムへの Visual Studio の影響を軽減しながら、インストールされているワークロードや機能に関するユーザーの選択肢を広げる、[より高速で、かつ軽量の Visual Studio インストール エクスペリエンス](https://devblogs.microsoft.com/visualstudio/faster-leaner-visual-studio-installer)を提供します。 これらの機能強化をサポートするために、Microsoft は機能拡張モデルに、いくつかの破壊的変更を含む変更を加えました。 この記事では、これらの変更の技術的な詳細と、これらに対応するために実行できる内容について説明します。

> [!NOTE]
> 一部の情報は特定の時点の実装に関する詳細であるため、後で変更されることがあります。

## <a name="changes-affecting-vsix-format-and-installation"></a>VSIX 形式とインストールに影響を与える変更

Visual Studio 2017 では、軽量のインストール エクスペリエンスをサポートするために VSIX v3 (バージョン 3) 形式が導入されました。

VSIX 形式の変更には、次のものが含まれます。

* セットアップの前提条件の宣言。 Visual Studio の軽量で、かつ高速なインストールという公約を実現するために、インストーラーでは、ユーザーにより多くの構成オプションを提供するようになっています。 その結果、拡張機能に必要な機能やコンポーネントが確実にインストールされるようにするために、拡張機能ではそれらの依存関係を宣言する必要があります。

  * Visual Studio 2017 インストーラーは、拡張機能のインストールの一部として、ユーザーに必要なコンポーネントを取得してインストールすることを自動的に提案します。
  * ユーザーは、新しい VSIX v3 形式を使用してビルドされていない拡張機能をインストールしようとしている場合も警告されます。それらが、マニフェストでバージョン 15.0 がターゲットであるとマークされている場合でも同じです。

* VSIX 形式に関して拡張された機能。 サイドバイサイド インストールもサポートしている Visual Studio の[影響の少ないインストール](https://devblogs.microsoft.com/visualstudio/anatomy-of-a-low-impact-visual-studio-install)を実現するために、ほとんどの構成データがシステム レジストリに保存されることはなくなっており、Visual Studio 固有のアセンブリは GAC から移動されました。 また、VSIX 形式と VSIX インストール エンジンの機能も強化されているため、MSI や EXE の代わりにこれを使用して、一部のインストールの種類の拡張機能をインストールできるようになりました。

新機能には、次のものが含まれます。

* 指定された Visual Studio インスタンスへの登録。
* [拡張機能フォルダー](set-install-root.md)外でのインストール。
* プロセッサ アーキテクチャの検出。
* 言語で区別された言語パックへの依存。
* [NGEN のサポート](ngen-support.md)を含むインストール。

## <a name="build-an-extension-for-visual-studio-2017"></a>Visual Studio 2017 の拡張機能を構築する

Visual Studio 2017 では、新しい VSIX v3 マニフェスト形式を作成するためのデザイナー ツールを使用できます。 これらのデザイナー ツールの使用、または VSIX v3 拡張機能を開発するためにプロジェクトやマニフェストを手動で更新する方法の詳細については、付属のドキュメント「[方法: 機能拡張プロジェクトを Visual Studio 2017 に移行する](how-to-migrate-extensibility-projects-to-visual-studio-2017.md)」を参照してください。

## <a name="change-visual-studio-user-data-path"></a>変更: Visual Studio のユーザー データ パス

以前は、Visual Studio の各メジャー リリースのインストールは各コンピューターに 1 つしか存在できませんでした。 Visual Studio 2017 のサイドバイサイド インストールをサポートするために、ユーザーのコンピューターには Visual Studio の複数のユーザー データ パスが存在できます。

Visual Studio プロセスの内部で実行されるコードを、Visual Studio 設定マネージャーを使用するように更新する必要があります。 Visual Studio プロセスの外部で実行されるコードでは、[このガイダンスに従って](locating-visual-studio.md)、特定の Visual Studio インストールのユーザー パスを見つけることができます。

## <a name="change-global-assembly-cache-gac"></a>変更: グローバル アセンブリ キャッシュ (GAC)

ほとんどの Visual Studio コア アセンブリは GAC にインストールされなくなりました。 Visual Studio プロセス内で実行されるコードが引き続き、必要なアセンブリを実行時に検索できるように、次の変更が加えられました。

> [!NOTE]
> 下の [INSTALLDIR] は、Visual Studio のインストール ルート ディレクトリを示しています。 *VSIXInstaller.exe* ではこれを自動的に設定しますが、カスタムの展開コードを記述するには、[Visual Studio の検索](locating-visual-studio.md)に関するページを参照してください。

* GAC のみにインストールされていたアセンブリ:

  これらのアセンブリは、<em>[INSTALLDIR]\Common7\IDE\*、*[INSTALLDIR]\Common7\IDE\PublicAssemblies</em>、または *[INSTALLDIR]\Common7\IDE\PrivateAssemblies* の下にインストールされるようになりました。 これらのフォルダーは、Visual Studio プロセスのプローブ パスの一部です。

* プローブ以外のパスと GAC にインストールされていたアセンブリ:

  * GAC 内のコピーがセットアップから削除されました。
  * アセンブリのコード ベース エントリを指定するために、 *.pkgdef* ファイルが追加されました。

    次に例を示します。

    ```
    [$RootKey$\RuntimeConfiguration\dependentAssembly\codeBase\{UniqueGUID}]
    "name"="AssemblyName" "codeBase"="$PackageFolder$\AssemblyName.dll"
    "publicKeyToken"="Public Key Token"
    "culture"="neutral"
    "version"=15.0.0.0
    ```

    実行時に、Visual Studio の pkgdef サブシステムが、これらのエントリを [`<codeBase>`](/dotnet/framework/configure-apps/file-schema/runtime/codebase-element) 要素として Visual Studio プロセスのランタイム構成ファイル ( *[VSAPPDATA]\devenv.exe.config* の下) にマージします。 これにより、プローブ パス経由の検索が回避されるため、これが Visual Studio プロセスでアセンブリを検索できるようにするための推奨される方法です。

### <a name="reacting-to-this-breaking-change"></a>この破壊的変更への対応

* 拡張機能が Visual Studio プロセスの内部で実行される場合:

  * コードで Visual Studio コア アセンブリを検索できます。
  * 必要に応じて、 *.pkgdef* ファイルを使用してアセンブリのパスを指定することを検討してください。

* 拡張機能が Visual Studio プロセスの外部で実行される場合:

  構成ファイルまたはアセンブリ リゾルバーを使用して、<em>[INSTALLDIR]\Common7\IDE\*、*[INSTALLDIR]\Common7\IDE\PublicAssemblies</em>、または *[INSTALLDIR]\Common7\IDE\PrivateAssemblies* の下で Visual Studio コア アセンブリを探すことを検討してください。

## <a name="change-reduce-registry-impact"></a>変更: レジストリへの影響を軽減する

### <a name="global-com-registration"></a>グローバル COM 登録

* 以前、Visual Studio では、ネイティブな COM 登録をサポートするために、多数のレジストリ キーを HKEY_CLASSES_ROOT および HKEY_LOCAL_MACHINE ハイブにインストールしていました。 この影響を軽減するために、Visual Studio では現在、[COM コンポーネントの登録を必要としないアクティベーション](/previous-versions/dotnet/articles/ms973913(v=msdn.10))を使用します。
* その結果、%ProgramFiles(x86)%\Common Files\Microsoft Shared\MSEnv の下にあるほとんどの TLB/OLB/DLL ファイルが、Visual Studio によって既定ではインストールされなくなりました。 これらのファイルは現在、Visual Studio ホスト プロセスによって使用される対応する登録を必要としない COM マニフェストと共に、[INSTALLDIR] の下にインストールされます。
* その結果、Visual Studio COM インターフェイスのグローバル COM 登録に依存する外部コードでは、これらの登録が見つからなくなります。 Visual Studio プロセスの内部で実行されるコードでは違いは確認されません。

### <a name="visual-studio-registry"></a>Visual Studio レジストリ

* 以前、Visual Studio では、多数のレジストリ キーをシステムの **HKEY_LOCAL_MACHINE** および **HKEY_CURRENT_USER** ハイブの Visual Studio 固有のキーの下にインストールしていました。

  * **HKLM\Software\Microsoft\VisualStudio\{Version}** : MSI インストーラーとコンピューターごとの拡張機能によって作成されたレジストリ キー。
  * **HKCU\Software\Microsoft\VisualStudio\{Version}** : ユーザー固有の設定を格納するために Visual Studio によって作成されたレジストリ キー。
  * **HKCU\Software\Microsoft\VisualStudio\{Version}_Config**: 上記の Visual Studio HKLM キーのコピーに加えて、拡張機能によって *.pkgdef* ファイルからマージされたレジストリ キー。

* レジストリへの影響を軽減するために、Visual Studio では現在 [RegLoadAppKey](/windows/desktop/api/winreg/nf-winreg-regloadappkeya) 関数を使用して、レジストリ キーを *[VSAPPDATA]\privateregistry.bin* の下にあるプライベート バイナリ ファイルに格納します。 システム レジストリに残されている Visual Studio 固有のキーはごく少数です。
* Visual Studio プロセスの内部で実行される既存のコードには影響を与えません。 Visual Studio では、HKCU Visual Studio 固有のキーの下でのすべてのレジストリ操作をプライベート レジストリにリダイレクトします。 その他のレジストリの場所に対する読み取りと書き込みでは、引き続きシステム レジストリを使用します。
* 外部コードでは、Visual Studio レジストリ エントリをこのファイルから読み込んで読み取る必要があります。

### <a name="react-to-this-breaking-change"></a>この破壊的変更に対応する

* 外部コードは、COM コンポーネントの登録を必要としないアクティベーションも使用するように変換する必要があります。
* 外部コンポーネントでは、[このガイダンスに従って](https://devblogs.microsoft.com/setup/changes-to-visual-studio-15-setup)、Visual Studio の場所を見つけることができます。
* 外部コンポーネントでは、Visual Studio レジストリ キーに対する直接の読み取りまたは書き込みの代わりに、[外部の設定マネージャー](/dotnet/api/microsoft.visualstudio.settings.externalsettingsmanager)を使用することをお勧めします。
* 拡張機能で使用しているコンポーネントに、登録のための別の手法が実装されているかどうかを確認します。 たとえば、デバッガー拡張機能では、新しい [msvsmon JSON ファイル COM 登録](migrate-debugger-COM-registration.md)を利用できる可能性があります。