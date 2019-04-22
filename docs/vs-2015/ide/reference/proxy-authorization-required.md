---
title: プロキシ認証が要求される | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
ms.assetid: c2d24ae1-9902-460e-b72a-0299eed9ee82
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: b0c197a15962d12e101e0d3ab164d706375620d9
ms.sourcegitcommit: 53aa5a413717a1b62ca56a5983b6a50f7f0663b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59648248"
---
# <a name="proxy-authorization-required"></a>プロキシ認証が要求される
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

このエラーは通常、ユーザーがプロキシ サーバーを経由して Visual Studio オンラインに接続し、そのプロキシ サーバーが呼び出しをブロックしたときに発生します。 Visual Studio オンラインは、IDE へのユーザーのサインイン状態を維持するために使用されます。  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
-   Visual Studio を再起動します。 プロキシ認証のダイアログ ボックスが表示されます。 ダイアログ ボックスに資格情報を入力します。  
  
-   上記の手順で問題が解決しない場合、考えられる原因は、プロキシ サーバーが http://go.microsoft.com のアドレスに対しては資格情報を要求せず、*.visualStudio.com のアドレスに対しては資格情報を要求することです。 これらのサーバーの場合、次のリストをホワイトリストに設定し、Visual Studio におけるあらゆるサインイン シナリオのブロックを解除する必要があります。  
  
    -   *.windows.net  
  
    -   *.microsoftonline.com  
  
    -   *.visualstudio.com  
  
    -   *.microsoftonline.com  
  
    -   *.live.com  
  
-   それ以外の場合を削除することができます、 http://go.microsoft.comアドレスをホワイト リストから、プロキシ認証ダイアログ ボックスが両方に表示されるように、 http://go.microsoft.comアドレスと Visual Studio を再起動すると、サーバー エンドポイント。  
  
-   OR  
  
-   プロキシで既定の資格情報を使用する場合は、次の手順を実行します。  
  
    1.  devenv.exe.config (devenv.exe の構成ファイル) を次の場所から探します。 **%ProgramFiles%\Microsoft Visual Studio 14.0\Common7\IDE** (または **%ProgramFiles(x86)%\Microsoft Visual Studio 14.0\Common7\IDE**)  
  
    2.  構成ファイル内で、 `<system.net>` ブロックを探し、次のコードを追加します。  
  
        ```xml  
        <defaultProxy enabled="true" useDefaultCredentials="true">  
            <proxy bypassonlocal="True" proxyaddress=" HYPERLINK "http://<yourproxy:port#" http://<yourproxy:port#>"/>  
        </defaultProxy>  
  
        ```  
  
         `proxyaddress="<http://<yourproxy:port#>`には、使用しているネットワークの正しいプロキシ アドレスを挿入する必要があります。  
  
-   OR  
  
-   [このポスト](http://blogs.msdn.com/b/rido/archive/2010/05/06/how-to-connect-to-tfs-through-authenticated-web-proxy.aspx) の指示に従ってプロキシの使用を許可するコードを追加することもできます。
