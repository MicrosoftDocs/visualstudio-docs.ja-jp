---
description: 取得するファイルの名前の種類を指定します。
title: GETNAME_TYPE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- GETNAME_TYPE
helpviewer_keywords:
- GETNAME_TYPE enumeration
ms.assetid: 2f9f1679-e9e8-4c9c-ac90-aa07bfe69914
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a65c29a1925c8d0c1de97f87707f191713c2bb03
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054596"
---
# <a name="getname_type"></a>GETNAME_TYPE
取得するファイルの名前の種類を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_GETNAME_TYPE {
    GN_NAME         = 0,
    GN_FILENAME     = 1,
    GN_BASENAME     = 2,
    GN_MONIKERNAME  = 3,
    GN_URL          = 4,
    GN_TITLE        = 5,
    GN_STARTPAGEURL = 6
};
typedef DWORD GETNAME_TYPE;
```

```csharp
public enum enum_GETNAME_TYPE {
    GN_NAME         = 0,
    GN_FILENAME     = 1,
    GN_BASENAME     = 2,
    GN_MONIKERNAME  = 3,
    GN_URL          = 4,
    GN_TITLE        = 5,
    GN_STARTPAGEURL = 6
};
```

## <a name="fields"></a>フィールド
`GN_NAME`\
ドキュメントまたはコンテキストのフレンドリ名を指定します。

`GN_FILENAME`\
ドキュメントまたはコンテキストの完全なパスを指定します。

`GN_BASENAME`\
ドキュメントまたはコンテキストの完全なパスの代わりにベース ファイル名を指定します。

`GN_MONIKERNAME`\
モニカーの形式で、ドキュメントまたはコンテキストの一意な名前を指定します。

`GN_URL`\
ドキュメントまたはコンテキストの URL 名を指定します。

`GN_TITLE`\
ドキュメントのタイトルを指定します (存在する場合)。

`GN_STARTPAGEURL`\
プロセスの開始ページの URL を取得します。

## <a name="remarks"></a>解説
これらの値は、返される名前の種類を指定するために、[GetName](../../../extensibility/debugger/reference/idebugdocument2-getname.md)、[GetName](../../../extensibility/debugger/reference/idebugdocumentcontext2-getname.md)、[GetName](../../../extensibility/debugger/reference/idebugprocess2-getname.md) メソッドにパラメーターとして渡されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetName](../../../extensibility/debugger/reference/idebugdocument2-getname.md)
- [GetName](../../../extensibility/debugger/reference/idebugdocumentcontext2-getname.md)
- [GetName](../../../extensibility/debugger/reference/idebugprocess2-getname.md)
