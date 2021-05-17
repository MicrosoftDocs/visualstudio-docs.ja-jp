---
description: このプロパティ型のビューアーのインスタンスを作成するために、そのビューアーに関する情報を取得します。
title: IPropertyProxyEESide::GetManagedViewerCreationData | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyEESide::GetManagedViewerCreationData
helpviewer_keywords:
- IPropertyProxyEESide::GetManagedViewerCreationData
ms.assetid: c4eb4d60-8816-4d52-bc8d-dffd4f066499
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fc0ab85a3000db2090e9679b0ae065b9280f20cf
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105082505"
---
# <a name="ipropertyproxyeesidegetmanagedviewercreationdata"></a>IPropertyProxyEESide::GetManagedViewerCreationData
このプロパティ型のビューアーのインスタンスを作成するために、そのビューアーに関する情報を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetManagedViewerCreationData(
   BSTR*                  assemName,
   IEEDataStorage**       assemBytes,
   IEEDataStorage**       assemPdb,
   BSTR*                  className,
   ASSEMBLYLOCRESOLUTION* alr,
   BOOL*                  replacementOk
);
```

```csharp
int GetManagedViewerCreationData(
   out string                     assemName,
   out IEEDataStorage             assemBytes,
   out IEEDataStorage             assemPdb,
   out string                     className,
   out enum_ASSEMBLYLOCRESOLUTION alr,
   out int                        replacementOk
);
```

## <a name="parameters"></a>パラメーター
`assemName`\
[出力] このオブジェクトを保持しているアセンブリの名前を返します。

`assemBytes`\
[出力] このオブジェクトのアセンブリ バイトを格納している [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md) オブジェクトを返します (バイトを使用できない場合、これは null 値です)。

`assemPdb`\
[出力] このオブジェクトのシンボル ストア情報を格納している `IEEDataStorage` オブジェクトを返します (シンボル ストアを使用できない場合、これは null 値です)。

`className`\
[出力] このオブジェクトを格納しているクラス名を返します。

`alr`\
[出力] アセンブリの場所を示す値を [ASSEMBLYLOCRESOLUTION](../../../extensibility/debugger/reference/assemblylocresolution.md) 列挙型から返します。

`replacementOk`\
[出力] このオブジェクトの値を変更できる場合は、0 以外 (`TRUE`) を返します。オブジェクトが読み取り専用の場合は、0 (`FALSE`) を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドは、マネージド ビューアーのインスタンスを作成するために型ビジュアライザーによって使用されます。

## <a name="see-also"></a>関連項目
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [ASSEMBLYLOCRESOLUTION](../../../extensibility/debugger/reference/assemblylocresolution.md)
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
