---
title: リモート デバッガーのダウンロード
description: リモート デバッガーのダウンロード リンク
services: ''
author: mikejo5000
ms.service: ''
ms.topic: include
ms.date: 05/23/2018
ms.author: mikejo
ms.custom: include file
ms.openlocfilehash: 600f34377e5901148149bb6e94c2277b37a435af
ms.sourcegitcommit: 36f5ffd6ae3215fe31837f4366158bf0d871f7a9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59291792"
---
リモート デバイスまたは、デバッグするサーバーではなく、Visual Studio のコンピューターにダウンロードして、次の表にあるリンクから、リモート ツールの正しいバージョンをインストールします。

- 最新 remote tools for Visual Studio のバージョンをダウンロードします。 リモート ツールの最新のバージョンは Visual Studio の以前のバージョンと互換性のあるが、以降の Visual Studio バージョンと互換性のないリモート ツールの以前のバージョン。
- それらをインストールしているコンピューターと同じアーキテクチャを使用して、リモート ツールをダウンロードします。 たとえば、64 ビットのオペレーティング システムを実行しているリモート コンピューター上の 32 ビット アプリケーションをデバッグする場合は、64 ビットのリモート ツールをインストールします。

::: moniker range=">=vs-2019"

|Version|リンク|メモ|
|-|-|-|
|Visual Studio 2019 RC|[リモート ツール](https://visualstudio.microsoft.com/downloads/?q=remote+tools#remote-tools-for-visual-studio-2019)|すべての Visual Studio 2019 バージョンと互換性があります。 (X 86、x64、または ARM64 など)、デバイスのオペレーティング システムに一致するバージョンをダウンロードします。 Windows Server で、次を参照してください。[ファイルのダウンロードのブロックを解除](../../debugger/remote-debugging-unblock-file-download.md)については、リモート ツールをダウンロードします。|
|Visual Studio 2017 (最新バージョン)|[リモート ツール](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202017)|すべての Visual Studio 2017 バージョンと互換性があります。 (X 86、x64、または ARM64 など)、デバイスのオペレーティング システムに一致するバージョンをダウンロードします。 Windows Server で、次を参照してください。[ファイルのダウンロードのブロックを解除](../../debugger/remote-debugging-unblock-file-download.md)については、リモート ツールをダウンロードします。|
|Visual Studio 2015|[リモート ツール](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202015)|Visual Studio 2015 用リモート ツール My.VisualStudio.com から利用できます。 メッセージが表示されたら、結合、無料[Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/)プログラム、または、Visual Studio のサブスクリプション ID でサインイン Windows Server で、次を参照してください。[ファイルのダウンロードのブロックを解除](../../debugger/remote-debugging-unblock-file-download.md)については、リモート ツールをダウンロードします。|
|Visual Studio 2013|[リモート ツール](/previous-versions/visualstudio/visual-studio-2013/bt727f1t(v=vs.120)#installing-the-remote-tools)|Visual Studio 2013 のドキュメント内のページをダウンロードします。|
|Visual Studio 2012|[リモート ツール](/previous-versions/visualstudio/visual-studio-2012/bt727f1t(v=vs.110)#installing-the-remote-tools)|Visual Studio 2012 のドキュメント内のページをダウンロードします。|

::: moniker-end

::: moniker range="vs-2017"

|Version|リンク|メモ|
|-|-|-|
|Visual Studio 2017 (最新バージョン)|[リモート ツール](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202017)|すべての Visual Studio 2017 バージョンと互換性があります。 (X 86、x64、または ARM64 など)、デバイスのオペレーティング システムに一致するバージョンをダウンロードします。 Windows Server で、次を参照してください。[ファイルのダウンロードのブロックを解除](../../debugger/remote-debugging-unblock-file-download.md)については、リモート ツールをダウンロードします。|
|Visual Studio 2015|[リモート ツール](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202015)|Visual Studio 2015 用リモート ツール My.VisualStudio.com から利用できます。 メッセージが表示されたら、結合、無料[Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/)プログラム、または、Visual Studio のサブスクリプション ID でサインイン Windows Server で、次を参照してください。[ファイルのダウンロードのブロックを解除](../../debugger/remote-debugging-unblock-file-download.md)については、リモート ツールをダウンロードします。|
|Visual Studio 2013|[リモート ツール](/previous-versions/visualstudio/visual-studio-2013/bt727f1t(v=vs.120)#installing-the-remote-tools)|Visual Studio 2013 のドキュメント内のページをダウンロードします。|
|Visual Studio 2012|[リモート ツール](/previous-versions/visualstudio/visual-studio-2012/bt727f1t(v=vs.110)#installing-the-remote-tools)|Visual Studio 2012 のドキュメント内のページをダウンロードします。|

::: moniker-end

リモート デバッガーを実行するにはコピーすることによって*msvsmon.exe*リモート ツールをインストールするのではなく、リモートのコンピューターにします。 ただし、リモート デバッガー構成ウィザード (*rdbgwiz.exe*) はリモート ツールをインストールする場合にのみ使用できます。 リモート デバッガーをサービスとして実行する場合、構成ウィザードを使用する必要があります。 詳細については、次を参照してください。 [(省略可能) 構成サービスとしてリモート デバッガー](../../debugger/remote-debugging.md#bkmk_configureService)します。

>[!NOTE]
>- ARM デバイスで Windows 10 アプリをデバッグするには、リモート ツールの最新バージョンで使用可能な ARM64 を使用します。
>- Windows RT デバイスで Windows 10 アプリをデバッグするには、リモート ツールのダウンロード、Visual Studio 2015 でのみ使用できる ARM を使用します。
