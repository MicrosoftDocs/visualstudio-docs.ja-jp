---
description: デバッグ セッションを終了するときに、デバッグ エンジンによって、Visual Studio UI の既定の動作をオーバーライドできるようにします。
title: IDebugProgramDestroyEventFlags2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProgramDestroyEventFlags2 interface
ms.assetid: d384ff71-dc71-40b9-a871-801f8b6a3418
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6cb54b3a88255f9102f617298ff23c3e117d3cdd
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084234"
---
# <a name="idebugprogramdestroyeventflags2"></a>IDebugProgramDestroyEventFlags2
デバッグ セッションを終了するときに、デバッグ エンジンによって、[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] UI の既定の動作をオーバーライドできるようにします。

## <a name="syntax"></a>構文

```
IDebugProgramDestroyEventFlags2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスは、デバッグ エンジンによって実装されます。 これは、プロセスの有効期間にわたって複数のプログラムを作成して破棄する可能性のあるホストに便利です。

## <a name="methods"></a>メソッド
 次の表に、`IDebugProgramDestroyEventFlags2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[GetFlags](../../../extensibility/debugger/reference/idebugprogramdestroyeventflags2-getflags.md)|プログラムの破棄フラグを取得します。|

## <a name="remarks"></a>解説
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] UI の既定の動作では、すべてのプログラムがプログラム破棄イベントを送信した後にデザイン モードに戻ります。 このインターフェイスを使用すると、デバッグ エンジンでその動作を変更できます。

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
