---
title: ヘルプ コンテンツ マネージャーのオーバーライド
description: Visual Studio IDE のヘルプ ビューアーとヘルプ関連機能の既定の動作を変更する、ヘルプ コンテンツ マネージャーのオーバーライドについて説明します。
ms.date: 11/01/2017
ms.topic: conceptual
ms.assetid: 95fe6396-276b-4ee5-b03d-faacec42765f
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f9c9a950156f29bda68a134af2eb299b3431445f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99944291"
---
# <a name="help-content-manager-overrides"></a>ヘルプ コンテンツ マネージャーのオーバーライド

Visual Studio IDE のヘルプ ビューアーとヘルプ関連の機能の既定の動作を変更できます。 一部のオプションは、さまざまなレジストリ キー値を設定する [.pkgdef](https://devblogs.microsoft.com/visualstudio/whats-a-pkgdef-and-why/) ファイルを作成することで指定されます。 他のオプションはレジストリで直接設定されます。

## <a name="how-to-control-help-viewer-behavior-by-using-a-pkgdef-file"></a>.pkgdef ファイルを使用してヘルプ ビューアーの動作を制御する方法

1. 最初の行に `[$RootKey$\Help]` として *.pkgdef* ファイルを作成します。

2. 次の表で説明するレジストリ キー値のいずれかまたはすべてを別の行に追加します。例: `"UseOnlineHelp"=dword:00000001`

3. ファイルを *%ProgramFiles(x86)%\Microsoft Visual Studio\2017\\<エディション\>\Common7\IDE\CommonExtensions* にコピーします。

4. 開発者コマンド プロンプトで `devenv /updateconfiguration` を実行します。

### <a name="registry-key-values"></a>レジストリ キー値

|レジストリ キー値|種類|データ|説明|
|------------------|----|----|-----------|
|NewContentAndUpdateService|string|\<http URL for service endpoint\>|一意のサービス エンドポイントを定義する|
|UseOnlineHelp|dword|ローカルのヘルプを指定するには `0`、オンライン ヘルプを指定するには `1`|オンライン ヘルプまたはオフライン ヘルプの既定を定義する|
|OnlineBaseUrl|string|\<http URL for service endpoint\>|一意の F1 エンドポイントを定義する|
|OnlineHelpPreferenceDisabled|dword|オンライン ヘルプの設定オプションを有効にするには `0`、無効にするには `1`|オンライン ヘルプの設定オプションを無効にする|
|DisableManageContent|dword|ヘルプ ビューアーの **[コンテンツの管理]** タブを有効にするには`0`、無効にするには `1`|**[コンテンツの管理]** タブを無効にする|
|DisableFirstRunHelpSelection|dword|Visual Studio を初めて起動する際に構成されるヘルプ機能を有効にするには `0`、無効にするには `1`|Visual Studio を初めて起動する際にコンテンツのインストールを無効にする|

### <a name="example-pkgdef-file-contents"></a>.pkgdef ファイルの内容の例

```pkgdef
[$RootKey$\Help]
"NewContentAndUpdateService"="https://some.service.endpoint"
"UseOnlineHelp"=dword:00000001
"OnlineBaseUrl"="https://some.service.endpoint"
"OnlineHelpPreferenceDisabled"=dword:00000000
"DisableManageContent"=dword:00000000
"DisableFirstRunHelpSelection"=dword:00000001
```

## <a name="use-registry-editor-to-change-help-viewer-behavior"></a>レジストリ エディターを使用してヘルプ ビューアーの動作を変更する

レジストリ エディターでレジストリ キー値を設定することで、次の 2 つの動作を制御できます。

|タスク|レジストリ キー|値|データ|
|----------|-----|------|----|
|Override BITS ジョブの優先順位をオーバーライドする|HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node (64-bit コンピューターの場合)\Microsoft\Help\v2.3|BITSPriority|**foreground**、**high**、**normal**、または **low**|
|ネットワーク共有上のローカル コンテンツ ストアを指定する|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Help\ v2.3\Catalogs\VisualStudio15|LocationPath|"*ContentStoreNetworkShare*"|

## <a name="see-also"></a>関連項目

- [ヘルプ ビューアーの管理者ガイド](../help-viewer/administrator-guide.md)
- [ヘルプ コンテンツ マネージャーのコマンド ライン引数](../help-viewer/command-line-arguments.md)
- [Microsoft ヘルプ ビューアー](../help-viewer/overview.md)