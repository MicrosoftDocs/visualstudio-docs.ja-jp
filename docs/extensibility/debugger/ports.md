---
title: ポート | Microsoft Docs
description: この記事では、Visual Studio のデバッガー アーキテクチャにおけるポートの定義と役割について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- ports
- debugging [Debugging SDK], ports
ms.assetid: 1d7f3aa7-7eff-4cab-bc53-0a566b1a9363
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e53b2b804433f7e9450f34dac5b21e45710cd71c
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900773"
---
# <a name="ports"></a>Port
デバッガー アーキテクチャでは、"*ポート*" は次のようなものです。

- サーバー上で実行されている一連のプロセスのコンテナー。 たとえば、ポートは、Windows CE ベースのデバイスへのシリアル ケーブル接続や、非 DCOM コンピューターへのネットワーク接続を表す場合があります。 ローカル ポートと呼ばれる 1 つの特殊なポートには、ローカル コンピューター上で実行されているすべてのプロセスが含まれます。

- 名前または識別子によって自分自身を識別できます。

- ポートで実行されているすべてのプロセスを列挙し、これらのプロセスを起動および終了することができます。

- [IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md) 引数を [AddPort](../../extensibility/debugger/reference/idebugportsupplier2-addport.md) に渡して作成される [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md) インターフェイスによって表されます。

  [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] は、すべての Windows ベースのプロセス (ネイティブとマネージドの両方) を処理する既定のポートを提供します。 Windows ベースでない外部デバイスとの接続用には、カスタム ポートを設定する必要があります。 このようなカスタム ポートを指定するには、カスタム ポート サプライヤーも設定する必要があります。

## <a name="see-also"></a>関連項目
- [サーバー](../../extensibility/debugger/servers-visual-studio-sdk.md)
- [処理](../../extensibility/debugger/processes.md)
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)
- [IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md)
- [AddPort](../../extensibility/debugger/reference/idebugportsupplier2-addport.md)
