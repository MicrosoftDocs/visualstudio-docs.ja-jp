---
title: DOCCONTEXT_COMPARE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- DOCCONTEXT_COMPARE
helpviewer_keywords:
- DOCCONTEXT_COMPARE enumeration
ms.assetid: ed947c34-b07e-4b69-8381-b6e7cb842862
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5805f34528225849afb51ce6a854ef5028acb3a5
ms.sourcegitcommit: 7153e2fc717d32e0e9c8a9b8c406dc4053c9fd53
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2019
ms.locfileid: "56413034"
---
# <a name="doccontextcompare"></a>DOCCONTEXT_COMPARE
2 つのドキュメント コンテキストを比較するための条件を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_DOCCONTEXT_COMPARE {
    DOCCONTEXT_EQUAL         = 0x0001,
    DOCCONTEXT_LESS_THAN     = 0x0002,
    DOCCONTEXT_GREATER_THAN  = 0x0003,
    DOCCONTEXT_SAME_DOCUMENT = 0x0004
};
typedef DWORD DOCCONTEXT_COMPARE;
```

```csharp
enum enum_DOCCONTEXT_COMPARE {
    DOCCONTEXT_EQUAL         = 0x0001,
    DOCCONTEXT_LESS_THAN     = 0x0002,
    DOCCONTEXT_GREATER_THAN  = 0x0003,
    DOCCONTEXT_SAME_DOCUMENT = 0x0004
};
```

## <a name="members"></a>メンバー
DOCCONTEXT_EQUAL  
ターゲット ドキュメントのコンテキストに相当するリスト内の最初のドキュメント コンテキストを検索します。

DOCCONTEXT_LESS_THAN  
ターゲット ドキュメントのコンテキストよりも小さいリスト内の最初のドキュメント コンテキストを検索します。

DOCCONTEXT_GREATER_THAN  
ターゲット ドキュメントのコンテキストよりも大きいリスト内の最初のドキュメント コンテキストを検索します。

DOCCONTEXT_SAME_DOCUMENT  
ターゲット ドキュメント コンテキストと同じドキュメント内にある一覧で最初のドキュメント コンテキストを検索します。

## <a name="remarks"></a>Remarks
引数として渡される、[比較](../../../extensibility/debugger/reference/idebugdocumentcontext2-compare.md)メソッド。

これらの値は、リストの最初のドキュメント コンテキストを検索するための比較条件の指定に使用されます。 ドキュメントのコンテキストがを介してに対して自身を比較するドキュメント コンテキストの一覧を指定された、`IDebugDocumentContext2::Compare`メソッド。 比較演算子の一覧で最初のドキュメント コンテキスト`true`が返されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
[列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)  
[Compare](../../../extensibility/debugger/reference/idebugdocumentcontext2-compare.md)
