---
description: スタック フレームに関連付けられている物理アドレスの範囲の、コンピューターに依存する表現を取得します。
title: IDebugStackFrame2::GetPhysicalStackRange | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2::GetPhysicalStackRange
helpviewer_keywords:
- IDebugStackFrame2::GetPhysicalStackRange
ms.assetid: 2f6992e2-ac1c-433f-83b7-a7f83a4ce63d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7612267a428986ac67a02934f8cbdec38dcb736a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053335"
---
# <a name="idebugstackframe2getphysicalstackrange"></a>IDebugStackFrame2::GetPhysicalStackRange
スタック フレームに関連付けられている物理アドレスの範囲の、コンピューターに依存する表現を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetPhysicalStackRange ( 
   UINT64* paddrMin,
   UINT64* paddrMax
);
```

```csharp
int GetPhysicalStackRange ( 
   out ulong paddrMin,
   out ulong paddrMax
);
```

## <a name="parameters"></a>パラメーター
`paddrMin`\
[出力] このスタック フレームに関連付けられている最小の物理アドレスを返します。

`paddrMax`\
[出力] このスタック フレームに関連付けられている最大の物理アドレスを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドから返される情報は、スタック フレームを並べ替えるためにセッション デバッグ マネージャー (SDM) によって使用されます。

 呼び出し履歴が下位方向に成長することを前提としています。つまり、新しいスタック フレームは、より下位のメモリ アドレスに追加されます。 この前提に合致する物理スタックの範囲が実行時アーキテクチャで提供される必要があります。

## <a name="see-also"></a>関連項目
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
