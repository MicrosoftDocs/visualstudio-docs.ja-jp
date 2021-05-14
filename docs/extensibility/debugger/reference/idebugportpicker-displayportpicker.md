---
description: 指定されたダイアログ ボックスを表示し、ユーザーがポートを選択できるようにします。
title: IDebugPortPicker::DisplayPortPicker | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- DisplayPortPicker
- IDebugPortPicker::DisplayPortPicker
ms.assetid: 08511ef5-be64-4069-b169-a569cc94bc64
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a49c1379d2bb3946f75eddd9d80bdccdb370d3ab
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105072313"
---
# <a name="idebugportpickerdisplayportpicker"></a>IDebugPortPicker::DisplayPortPicker
指定されたダイアログ ボックスを表示し、ユーザーがポートを選択できるようにします。

## <a name="syntax"></a>構文

```cpp
HRESULT DisplayPortPicker(
   HWND hwndParentDialog,
   BSTR* pbstrPortId
);
```

```csharp
public int DisplayPortPicker(
   int hwndParentDialog,
   out string pbstrPortId
);
```

## <a name="parameters"></a>パラメーター
`hwndParentDialog`\
[入力] 親ダイアログ ボックスのハンドル。

`pbstrPortId`\
[出力] ポート識別子文字列。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。 戻り値が `S_FALSE` の場合 (または戻り値が `S_OK` で、`BSTR` が`NULL` に設定されている場合)、ユーザーが **[キャンセル]** をクリックしたことを示します。

## <a name="see-also"></a>関連項目
- [IDebugPortPicker](../../../extensibility/debugger/reference/idebugportpicker.md)
