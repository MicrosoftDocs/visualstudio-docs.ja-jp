---
title: IManagedAddin::Load
description: 管理対象の VSTO アドインが読み込まれるときに呼び出されます。
ms.date: 02/02/2017
ms.topic: interface
dev_langs:
- VB
- CSharp
helpviewer_keywords: ''
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: fc89ba13e9fc0f62b264cdb926e1a8392c0b41bd
ms.sourcegitcommit: 8590cf6b3351e82827fd21159beefef0c02bf162
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2021
ms.locfileid: "102469763"
---
# <a name="imanagedaddinload"></a>IManagedAddin::Load
  管理対象の VSTO アドインが読み込まれるときに呼び出されます。

## <a name="syntax"></a>構文

```csharp
HRESULT Load([in] BSTR bstrManifestURL,
             [in] IDispatch *pdispApplication);
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------------|-----------------|
|*bstrManifestURL*|VSTO アドインのマニフェストの完全なパス。|
|*pdispApplication*|VSTO アドインを読み込むホスト アプリケーションを表す IDispatch のポインター。|

## <a name="return-value"></a>戻り値
 メソッドが正常に完了したかどうかを示す HRESULT 値。

## <a name="remarks"></a>解説
 マニフェストは、VSTO アドインの読み込みに使用される情報を提供するファイル (通常は XML ファイル) です。 たとえば、マニフェストには、VSTO アドイン アセンブリの場所や、VSTO アドインが読み込まれるときにインスタンス化するエントリ ポイント クラスを指定できます。

 *bstrManifestURL* パラメーターには、VSTO アドインの **HKEY_CURRENT_USER\Software\Microsoft\Office\\ _\<application name>_ \Addins\\ _\<add-in ID>_** レジストリ キーの `Manifest` エントリの値が格納されます。 詳細については、「[IManagedAddin インターフェイス](../vsto/imanagedaddin-interface.md)」を参照してください。

 読み込まれる VSTO アドインのアプリケーション ドメインやセキュリティ ポリシーの構成などのタスクを実行するように、 [IManagedAddIn::Load](../vsto/imanagedaddin-load.md) メソッドを実装します。

## <a name="see-also"></a>関連項目
- [IManagedAddin インターフェイス](../vsto/imanagedaddin-interface.md)
- [IManagedAddin::Unload](../vsto/imanagedaddin-unload.md)
