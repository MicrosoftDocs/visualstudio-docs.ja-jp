---
description: '[プロセスにアタッチ] ダイアログ ボックスの [トランスポート情報] セクション内のテキストを、Visual Studio UI で表示できるようにします。'
title: IDebugPortSupplierDescription2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPortSupplierDescription2 interface
ms.assetid: dd19b9d6-0703-44b3-9498-cedffa0ce5b7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: dba3cd07bb84843ff4d2531cdde63ab9e671f961
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071923"
---
# <a name="idebugportsupplierdescription2"></a>IDebugPortSupplierDescription2
**[プロセスにアタッチ]** ダイアログ ボックスの **[トランスポート情報]** セクション内のテキストを、[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] UI で表示できるようにします。

## <a name="syntax"></a>構文

```
IDebugPortSupplierDescription2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスはポート サプライヤーによって実装されます。

## <a name="methods"></a>メソッド
 次の表は、`IDebugPortSupplierDescription2` のメソッドを示しています。

|メソッド|説明|
|------------|-----------------|
|[GetDescription](../../../extensibility/debugger/reference/idebugportsupplierdescription2-getdescription.md)|ポート サプライヤーの説明と説明のメタデータを取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
