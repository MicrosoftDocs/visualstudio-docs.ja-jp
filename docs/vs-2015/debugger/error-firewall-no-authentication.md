---
title: エラー :認証がファイアウォール設定されていません |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.error.firewall.noauth
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: dda1acb8-bed7-4bc8-9991-9cdc49c2ac1e
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3ad413f3e958fa6dc8edd22ef4be1428b6941bd6
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58977547"
---
# <a name="error-firewall-no-authentication"></a>エラー :ファイアウォールの認証が設定されていません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

リモート コンピューターのインターネット接続ファイアウォールが、リモート デバッグを許可するように設定されていません。 `No Authentication` を使用してリモート デバッグを実行するには、例外リストに msvsmon.exe を追加する必要があります。 また、IPSEC ポートを開く必要がある場合もあります。  
  
> [!NOTE]
>  リモート デバッガーでは Windows ファイアウォールの自動構成が可能です。 サード パーティのソフトウェア ファイアウォールやハードウェア ファイアウォールなど、Windows ファイアウォール以外のファイアウォールを使用する場合は、リモート デバッグを許可するようにファイアウォールを手動で構成する必要があります。 そのためには、msvsmon.exe がリッスンしている TCP/IP ポートのトラフィックを許可します。 既定では、これらのポートは 4018 と 4019 です。4018 はすべてのオペレーティング システムで使用され、4019 は Windows x64 でのみ使用されます。該当するポートで x86 プロセスのデバッグを許可します。  
  
 詳細については、次を参照してください。[設定 Up the Remote Tools のデバイスで](http://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c)します。
