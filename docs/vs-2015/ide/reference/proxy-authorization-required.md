---
title: プロキシ認証が要求される | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: troubleshooting
ms.assetid: c2d24ae1-9902-460e-b72a-0299eed9ee82
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 7456e60b42b18ad706b951ee58ca5c33f05cabc1
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665717"
---
# <a name="proxy-authorization-required"></a>プロキシ認証が要求される
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

プロキシ**認証が必要な**エラーは、通常、ユーザーがプロキシサーバー経由で Visual Studio online リソースに接続し、プロキシサーバーが呼び出しをブロックしている場合に発生します。

このエラーを修正するには、次の手順のうち1つ以上を試してください。

- Visual Studio を再起動します。 プロキシ認証のダイアログ ボックスが表示されます。 ダイアログ ボックスに資格情報を入力します。

- 上記の手順で問題が解決しない場合、考えられる原因は、プロキシ サーバーが http://go.microsoft.com のアドレスに対しては資格情報を要求せず、*.visualStudio.com のアドレスに対しては資格情報を要求することです。 これらのサーバーについては、次の Url を許可一覧に追加して、Visual Studio でのすべてのサインインシナリオのブロックを解除する必要があります。

  - *.windows.net

  - *.microsoftonline.com

  - *.visualstudio.com

  - *.microsoftonline.com

  - *.live.com

- @No__t_0 アドレスを許可一覧から削除して、Visual Studio の再起動時にプロキシ認証ダイアログが http://go.microsoft.com アドレスとサーバーエンドポイントの両方に表示されるようにすることができます。

- プロキシで既定の資格情報を使用する場合は、次の手順を実行します。

   1. devenv.exe.config (devenv.exe の構成ファイル) を次の場所から探します。 **%ProgramFiles%\Microsoft Visual Studio 14.0\Common7\IDE** (または **%ProgramFiles(x86)%\Microsoft Visual Studio 14.0\Common7\IDE**)

   2. 構成ファイル内で、 `<system.net>` ブロックを探し、次のコードを追加します。

      ```xml
      <defaultProxy enabled="true" useDefaultCredentials="true">
          <proxy bypassonlocal="True" proxyaddress=" HYPERLINK "http://<yourproxy:port#" http://<yourproxy:port#>"/>
      </defaultProxy>
      ```

      @No__t_0 にネットワークの正しいプロキシアドレスを挿入します。

- [このブログの投稿](http://blogs.msdn.com/b/rido/archive/2010/05/06/how-to-connect-to-tfs-through-authenticated-web-proxy.aspx)に記載されている手順に従って、プロキシを使用するためのコードを追加します。
