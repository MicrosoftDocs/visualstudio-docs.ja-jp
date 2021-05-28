---
description: カスタム ビューアーまたは型ビジュアライザーを識別する構造体。
title: DEBUG_CUSTOM_VIEWER | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUG_CUSTOM_VIEWER
helpviewer_keywords:
- DEBUG_CUSTOM_VIEWER structure
ms.assetid: 8e0ef3f0-0107-48e8-a037-6e52b4c4ed9d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 76c02956acd9277f203c67bede7369d6bb7a603a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096279"
---
# <a name="debug_custom_viewer"></a>DEBUG_CUSTOM_VIEWER
カスタム ビューアーまたは型ビジュアライザーを識別する構造体。

## <a name="syntax"></a>構文

```cpp
typedef struct tagDEBUG_CUSTOM_VIEWER {
    DWORD dwID;
    BSTR  bstrMenuName;
    BSTR  bstrDescription;
    GUID  guidLang;
    GUID  guidVendor;
    BSTR  bstrMetric;
} DEBUG_CUSTOM_VIEWER;
```

```csharp
public struct DEBUG_CUSTOM_VIEWER {
    public uint   dwID;
    public string bstrMenuName;
    public string bstrDescription;
    public Guid   guidLang;
    public Guid   guidVendor;
    public string bstrMetric;
};
```

## <a name="members"></a>メンバー
`dwID`\
1 つの `GUID`で実装された複数のビューアーまたはビジュアライザーを区別する ID。

`bstrMenuName`\
ドロップダウン メニューに表示されるテキスト。

`bstrDescription`\
カスタム ビューアーまたは型ビジュアライザーの説明 (使用されていない場合は null 値を指定する必要があります)。

`guidLang`\
提供する式エバリュエーターの言語。

`guidVendor`\
提供する式エバリュエーターのベンダー。

`bstrMetric`\
カスタム ビューアーまたは型ビジュアライザーの `CLSID` を格納するメトリック。

## <a name="remarks"></a>解説
この構造体の一覧は、[GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md) メソッド (および拡張機能により、[GetCustomViewerList](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md) メソッド) を呼び出すことによって返されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)
- [GetCustomViewerList](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)
