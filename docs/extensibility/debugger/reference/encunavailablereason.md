---
description: エディット コンティニュが使用できない理由を表します。
title: EncUnavailableReason | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- EncUnavailableReason
helpviewer_keywords:
- EncUnavailableReason enumeration
ms.assetid: c10aa4c0-d7e0-4de1-b8ff-7e050985eb12
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e63ad7994d485bb39f8ec789d8906cd7d5946840
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105095989"
---
# <a name="encunavailablereason"></a>EncUnavailableReason
`This is for internal use only!` **エディット コンティニュ** が使用できない理由を表します。

## <a name="syntax"></a>構文

```cpp
enum tagEncUnavailableReason {
    ENCUN_NONE,
    ENCUN_INTEROP,
    ENCUN_SQLCLR,
    ENCUN_MINIDUMP,
    ENCUN_EMBEDDED,
    ENCUN_ATTACH,
    ENCUN_WIN64
};
typedef enum tagEncUnavailableReason EncUnavailableReason;
```

```csharp
public enum EncUnavailableReason {
    ENCUN_NONE,
    ENCUN_INTEROP,
    ENCUN_SQLCLR,
    ENCUN_MINIDUMP,
    ENCUN_EMBEDDED,
    ENCUN_ATTACH,
    ENCUN_WIN64
};
```

## <a name="fields"></a>フィールド
`ENCUN_NONE`\
エディット コンティニュを使用できない明確な理由はありません。

`ENCUN_INTEROP`\
エディット コンティニュは、相互運用呼び出し時に使用できません。

`ENCUN_SQLCLR`\
エディット コンティニュは、共通言語ランタイム (CLR) を使用する SQL プロシージャ呼び出し時に使用できません。

`ENCUN_MINIDUMP`\
エディット コンティニュは、ミニダンプの処理中に使用できません。

`ENCUN_EMBEDDED`\
エディット コンティニュは、埋め込みコードの処理時に使用できません。

`ENCUN_ATTACH`\
セッションがデバッガーにアタッチされていて、デバッガーによって起動されていないため、エディット コンティニュは使用できません。

`ENCUN_WIN64`\
エディット コンティニュは、64 ビットの Windows コードの処理中は使用できません。

## <a name="remarks"></a>解説
この列挙は、[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] による内部使用専用です。 カスタム ポート サプライヤーによって実装された [GetENCAvailableState](../../../extensibility/debugger/reference/idebugprocess3-getencavailablestate.md) および [DisableENC](../../../extensibility/debugger/reference/idebugprocess3-disableenc.md) では、常に `E_NOTIMPL` を返す必要があります。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.idl

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)

- [DisableENC](../../../extensibility/debugger/reference/idebugprocess3-disableenc.md)

- [GetENCAvailableState](../../../extensibility/debugger/reference/idebugprocess3-getencavailablestate.md)
