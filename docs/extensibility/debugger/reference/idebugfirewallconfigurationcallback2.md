---
description: DCOM を使用して、ファイアウォールがリモート デバッグをブロックしないようにするために、デバッグ エンジンで Visual Studio UI に要求できるようにします。
title: IDebugFirewallConfigurationCallback2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugFirewallConfigurationCallback2 interface
ms.assetid: 0827361c-b97c-4851-9898-ab6d88c81811
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c67cc1ab9335cfeb197ca67937510b3137d6432c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073613"
---
# <a name="idebugfirewallconfigurationcallback2"></a>IDebugFirewallConfigurationCallback2
DCOM を使用して、ファイアウォールがリモートデバッグをブロックしないようにするために、デバッグエンジンで [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] UI に要求できるようにします。

## <a name="syntax"></a>構文

```
IDebugFirewallConfigurationCallback2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 セッション デバッグ マネージャーのポート オブジェクトによって実装されます。

## <a name="methods"></a>メソッド
 次の表は、`IDebugFirewallConfigurationCallback2` のメソッドを示しています。

|メソッド|説明|
|------------|-----------------|
|[EnsureDCOMUnblocked](../../../extensibility/debugger/reference/idebugfirewallconfigurationcallback2-ensuredcomunblocked.md)|ファイアウォールがリモート デバッグをブロックしないように要求します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
