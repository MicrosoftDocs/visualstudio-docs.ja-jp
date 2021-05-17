---
title: IDebugProperty3 | Microsoft Docs
description: このインターフェイスでは、プロパティに関連付けられた任意の長い文字列を取得し、プロパティに一意の ID を関連付けて、プロパティのカスタム ビューアーの一覧を取得し、結果として発生したエラーを報告する機能でプロパティの値を設定するためのサポートを提供します。
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty3
helpviewer_keywords:
- IDebugProperty3 interface
ms.assetid: 8f9be68d-4490-4eca-8f6b-8a10ed77e226
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 933810ac5b1e0ba34edf7cfe8d4303180c862fe2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105083909"
---
# <a name="idebugproperty3"></a>IDebugProperty3
このインターフェイスでは、次のものに対するサポートを提供します。

- プロパティに関連付けられた任意の長い文字列を取得します。

- 一意の ID をプロパティに関連付けます。

- プロパティのカスタム ビューアーの一覧を取得します。

- 結果として発生したエラーを報告する機能でプロパティの値を設定します

## <a name="syntax"></a>構文

```
IDebugProperty3 : IDebugProperty2
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグ エンジン (DE) では、長い文字列、プロパティ ID、カスタム ビューアーをサポートするために、[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) を実装する同じオブジェクトにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 `IDebugProperty2` インターフェイスを取得するには、このインターフェイスの [QueryInterface](/cpp/atl/queryinterface) を呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 `IDebugProperty3` インターフェイスでは、`IDebugProperty2` から継承されたメソッドに加えて次のメソッドが公開されます。

|メソッド|説明|
|------------|-----------------|
|[GetStringCharLength](../../../extensibility/debugger/reference/idebugproperty3-getstringcharlength.md)|プロパティに関連付けられている文字列の長さを返します。|
|[GetStringChars](../../../extensibility/debugger/reference/idebugproperty3-getstringchars.md)|ユーザーが指定したバッファー内の文字列を返します。|
|[CreateObjectID](../../../extensibility/debugger/reference/idebugproperty3-createobjectid.md)|このプロパティの一意の ID を作成します。|
|[DestroyObjectID](../../../extensibility/debugger/reference/idebugproperty3-destroyobjectid.md)|このプロパティの一意の ID を破棄します。|
|[GetCustomViewerCount](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)|このプロパティを表示できるカスタム ビューアーの数を返します。|
|[GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)|このプロパティを表示できるカスタム ビューアーの一覧を返します。|
|[SetValueAsStringWithError](../../../extensibility/debugger/reference/idebugproperty3-setvalueasstringwitherror.md)|このプロパティの値を設定し、何らかの問題が発生した場合にエラー メッセージを返します。|

## <a name="remarks"></a>解説
- [SetValueAsStringWithError](../../../extensibility/debugger/reference/idebugproperty3-setvalueasstringwitherror.md) は、セッション デバッグ マネージャー (SDM) でプロパティの値を設定するために推奨される方法です。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugCustomViewer](../../../extensibility/debugger/reference/idebugcustomviewer.md)
