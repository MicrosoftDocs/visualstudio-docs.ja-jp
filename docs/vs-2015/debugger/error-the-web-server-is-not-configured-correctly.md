---
title: エラー :Web サーバーが正しく構成されていない |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.remote.projnotconfigured
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugger, Web application errors
ms.assetid: 875ba87f-c372-4126-8fe3-e33931cf26c0
caps.latest.revision: 25
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 643be465aab889b1f31e8fa75dba68261444bc31
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60061009"
---
# <a name="error-the-web-server-is-not-configured-correctly"></a>エラー :Web サーバーは正しく構成されていません。
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このエラーでは以下の原因が考えられます。  
  
- デバッグしようとした .NET Web アプリケーションは、別のコンピューターにコピーされたか、手動で名前が変更されたか、または別の場所に移動されています。  
  
- インターネット インフォメーション サービス (IIS) の接続が確立していません IIS への Web サイトの配置に関する詳細については、「 [Web サイトの作成](http://www.iis.net/learn/get-started/getting-started-with-iis/create-a-web-site)」を参照してください。  
  
- ASP.NET アプリケーションをデバッグしようとしている場合、IIS 8 以降を実行しているリモート コンピューターに配置する手順については、「 [IIS への発行](https://docs.asp.net/en/latest/publishing/iis.html) 」を参照してください。また、IIS 7.5 を実行しているリモート コンピューターに配置する手順については、「 [Remote Debugging ASP.NET on a Remote IIS 7.5 Computer](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md) 」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [Web アプリケーションのデバッグ: エラーとトラブルシューティング](../debugger/debugging-web-applications-errors-and-troubleshooting.md)
