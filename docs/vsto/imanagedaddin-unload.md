---
title: IManagedAddin::Unload
description: 管理対象の VSTO アドインがアンロードされる直前に呼び出されます。
ms.date: 02/02/2017
ms.topic: interface
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Unload method
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: e45fd9e6385388b9c6bc32098cf59799618d511b
ms.sourcegitcommit: 8590cf6b3351e82827fd21159beefef0c02bf162
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2021
ms.locfileid: "102469711"
---
# <a name="imanagedaddinunload"></a>IManagedAddin::Unload
  管理対象の VSTO アドインがアンロードされる直前に呼び出されます。

## <a name="syntax"></a>構文

```csharp
HRESULT Unload();
```

## <a name="return-value"></a>戻り値
 メソッドが正常に完了したかどうかを示す HRESULT 値。

## <a name="remarks"></a>解説
 このメソッドは、Microsoft Office の現在のバージョンでは呼び出されません。 このメソッドは将来使用するために予約されています。

## <a name="see-also"></a>関連項目
- [IManagedAddin インターフェイス](../vsto/imanagedaddin-interface.md)
- [IManagedAddin::Load](../vsto/imanagedaddin-load.md)
