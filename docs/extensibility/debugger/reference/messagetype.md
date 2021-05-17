---
description: メッセージの種類と理由を指定します。
title: MESSAGETYPE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MESSAGETYPE
helpviewer_keywords:
- MESSAGETYPE enumeration
ms.assetid: 800cc77d-3c27-4763-a9df-552a9384bd49
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b85933896dfff38c2d346fd18144710e2e6fc127
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091527"
---
# <a name="messagetype"></a>MESSAGETYPE
メッセージの種類と理由を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_MESSAGETYPE { 
   MT_OUTPUTSTRING      = 0x0000001,
   MT_MESSAGEBOX        = 0x00000002,
   MT_TYPE_MASK         = 0x000000FF,
   MT_REASON_EXCEPTION  = 0x00000100,
   MT_REASON_TRACEPOINT = 0x00000200,
   MT_REASON_MASK       = 0x0000FF00
};
typedef DWORD MESSAGETYPE;
```

```csharp
public enum enum_MESSAGETYPE { 
   MT_OUTPUTSTRING      = 0x0000001,
   MT_MESSAGEBOX        = 0x00000002,
   MT_TYPE_MASK         = 0x000000FF,
   MT_REASON_EXCEPTION  = 0x00000100,
   MT_REASON_TRACEPOINT = 0x00000200,
   MT_REASON_MASK       = 0x0000FF00
};
```

## <a name="fields"></a>フィールド
 `MT_OUTPUTSTRING`\
 メッセージを出力ウィンドウに送信することを示します。 これは `MT_MESSAGEBOX` とは相互に排他的です。

 `MT_MESSAGEBOX`\
 メッセージがメッセージ ボックスに表示されることを示します。 これは `MT_OUTPUTSTRING` とは相互に排他的です。

 `MT_TYPE_MASK`\
 メッセージの送信先を分離するマスク値。

 `MT_REASON_EXCEPTION`\
 メッセージ ボックスが例外の結果として表示されていることを示します。 これは `MT_REASON_TRACEPOINT` とは相互に排他的です。

 `MT_REASON_TRACEPOINT`\
 メッセージ ボックスがトレースポイントをヒットした結果として表示されていることを示します。 これは `MT_REASON_EXCEPTION` と相互に排他的です。

 `MT_REASON_MASK`\
 表示されるメッセージの理由を分離するマスク値。

## <a name="remarks"></a>解説
 これらの値は、[GetMessage](../../../extensibility/debugger/reference/idebugmessageevent2-getmessage.md) および [GetErrorMessage](../../../extensibility/debugger/reference/idebugerrorevent2-geterrormessage.md) メソッドから返されます。

 理由値の 1 つを、ビットごとの `OR` を使用して出力先の値の 1 つと組み合わせることができます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetMessage](../../../extensibility/debugger/reference/idebugmessageevent2-getmessage.md)
- [GetErrorMessage](../../../extensibility/debugger/reference/idebugerrorevent2-geterrormessage.md)
