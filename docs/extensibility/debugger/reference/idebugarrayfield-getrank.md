---
title: IDebugArrayField::GetRank |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayField::GetRank
helpviewer_keywords:
- IDebugArrayField::GetRank method
ms.assetid: 2364b876-5be1-4bab-9b8f-3b6121da35c6
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1c091c7696867f369262a81259105dcf23fbe4c9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62877740"
---
# <a name="idebugarrayfieldgetrank"></a>IDebugArrayField::GetRank
ランクの配列の次元数を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetRank( 
   DWORD* pdwRank
);
```

```csharp
int GetRank(
   out uint pdwRank
);
```

#### <a name="parameters"></a>パラメーター
 `pdwRank`

 [out]順位を返します。

## <a name="return-value"></a>戻り値
 成功した場合、S_OK を返します。それ以外の場合、エラー コードを返します。

## <a name="remarks"></a>Remarks
 配列のランクは、ディメンションの数に対応します。 C++ および C# の場合、多次元配列、配列の配列で実際には、1 次元の配列だけを考慮するそのためことができます (および`GetRank`メソッドは常に 1 を返します)。 [!INCLUDE[vbprvb](../../../code-quality/includes/vbprvb_md.md)]、その一方で、多次元配列は異なる方法で処理およびそのような配列のランクには、ディメンションの数が反映されます (および`GetRank`メソッドは常にディメンションの数を返します)。

## <a name="see-also"></a>関連項目
- [IDebugArrayField](../../../extensibility/debugger/reference/idebugarrayfield.md)