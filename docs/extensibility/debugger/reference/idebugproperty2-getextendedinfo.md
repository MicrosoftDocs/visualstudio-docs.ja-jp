---
description: プロパティの拡張情報を取得します。
title: IDebugProperty2::GetExtendedInfo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetExtendedInfo
helpviewer_keywords:
- IDebugProperty2::GetExtendedInfo
ms.assetid: 0c9c0b2b-7540-4424-adb5-fce7aa37a026
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ad540166ff769aaa894ad4142843553951217234
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065035"
---
# <a name="idebugproperty2getextendedinfo"></a>IDebugProperty2::GetExtendedInfo
プロパティの拡張情報を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetExtendedInfo ( 
   REFGUID* guidExtendedInfo,
   VARIANT* pExtendedInfo
);
```

```csharp
int GetExtendedInfo ( 
   ref Guid guidExtendedInfo,
   out object pExtendedInfo
);
```

## <a name="parameters"></a>パラメーター
`guidExtendedInfo`\
[入力] 取得する拡張情報の種類を決定する GUID。 詳細については、「解説」を参照してください。

`pExtendedInfo`\
[出力] 拡張プロパティ情報を取得するために使用できる `VARIANT` (C++) またはオブジェクト (C#) を返します。 たとえば、このパラメーターは `IUnknown` インターフェイスを返す場合があり、このインターフェイスをクエリして [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md) インターフェイスを取得できます。 詳細については、「解説」を参照してください。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。 取得する拡張情報がない場合は、`S_GETEXTENDEDINFO_NO_EXTENDEDINFO` を返します。

## <a name="remarks"></a>解説
 このメソッドの存在目的は、[GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) メソッドを呼び出して取得するのに適していない情報を取得することです。

 次の GUID は通常、このメソッドによって認識されます (どのアセンブリでも名前を使用できないため、C# の場合は GUID 値が指定されます)。 内部使用のために追加の GUID を作成できます。

|名前|GUID|説明|
|----------|----------|-----------------|
|guidDocument|{3f98de84-fee9-11d0-b47f-00a0244a1dd2}|ドキュメントへの `IUnknown` インターフェイスを返します。 通常、[IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md) インターフェイスは、この `IUnknown` インターフェイスから取得できます。|
|guidCodeContext|{e2fc65e-56ce-11d1-b528-00aax004a8797}|ドキュメント コンテキストへの `IUnknown` インターフェイスを返します。 通常、[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) インターフェイスは、この `IUnknown` インターフェイスから取得できます。|
|guidCustomViewerSupported|{d9c9da31-ffbe-4eeb-9186-23121e3c088c}|通常は式エバリュエーターによって実装される、カスタム ビューアーの CLSID を含む文字列を返します。|
|guidExtendedInfoSlot|{6df235ad-82c6-4292-9c97-7389770bc42f}|このプロパティがマネージド コードのローカル アドレスを表す場合、目的のスロット番号を表す 32 ビットの数値を返します。|
|guidExtendedInfoSignature|{b5fb6d46-f805-417f-96a3-8ba737073ffd}|プロパティ オブジェクトに関連付けられている変数の署名を含む文字列を返します。|

## <a name="see-also"></a>関連項目
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
