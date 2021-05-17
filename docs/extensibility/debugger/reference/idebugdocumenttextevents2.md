---
description: このインターフェイスは、デバッグ エンジンによって提供されるソース ドキュメントに対する変更について、Visual Studio に通知するために使用されます。
title: IDebugDocumentTextEvents2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentTextEvents2
helpviewer_keywords:
- IDebugDocumentTextEvents2 interface
ms.assetid: a10cbb6b-11a8-4056-b42a-2ecebf0e690d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: edf7cd483b39fb1fb5dc182a08bbbca8295b2359
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094095"
---
# <a name="idebugdocumenttextevents2"></a>IDebugDocumentTextEvents2
このインターフェイスは、デバッグ エンジンによって提供されるソース ドキュメントに対する変更について、Visual Studio に通知するために使用されます。

## <a name="syntax"></a>構文

```
IDebugDocumentTextEvents2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE は、ソース コードに対する変更をサポートするために、このインターフェイスを実装します。 通常、このインターフェイスは [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md) インターフェイスを実装するのと同じオブジェクトに実装されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] は、<xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint.Advise%2A> メソッドの呼び出しによって、このインターフェイスを取得します。 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint> インターフェイスは、<xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer.EnumConnectionPoints%2A> メソッドの呼び出しから取得されます。 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer> インターフェイスは、[IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md) インターフェイスの [QueryInterface](/cpp/atl/queryinterface) メソッドを呼び出すことによって取得されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugDocumentTextEvents2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[onDestroy](../../../extensibility/debugger/reference/idebugdocumenttextevents2-ondestroy.md)|ドキュメント全体が破棄されたことを示します。|
|[onInsertText](../../../extensibility/debugger/reference/idebugdocumenttextevents2-oninserttext.md)|テキストがドキュメントに挿入されたことをデバッグ パッケージに通知します。|
|[onRemoveText](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onremovetext.md)|ドキュメントからテキストが削除されたことをデバッグ パッケージに通知します。|
|[onReplaceText](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onreplacetext.md)|ドキュメント内でテキストが置換されていることをデバッグ パッケージに通知します。|
|[onUpdateTextAttributes](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onupdatetextattributes.md)|ドキュメントでテキスト属性が更新されたことをデバッグ パッケージに通知します。|
|[onUpdateDocumentAttributes](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onupdatedocumentattributes.md)|ドキュメントの属性が更新されたことを、イベントの受信側に通知します。|

## <a name="remarks"></a>解説
 `IDebugDocumentTextEvent2` インターフェイスを活用できるのは、独自のドキュメントを提供するデバッグ エンジンのみです。 この例として、スクリプト デバッグ エンジンが挙げられます。 スクリプトを解釈するプロセスでは、どのディスク ファイルにも存在せず、DE のみが認識する、新しいソース コードを生成できます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)
- [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)
