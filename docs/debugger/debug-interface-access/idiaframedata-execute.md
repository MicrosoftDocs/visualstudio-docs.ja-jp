---
description: スタック アンワインドを実行し、スタック ウォーク フレーム インターフェイスに結果を返します。
title: IDiaFrameData::execute | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::execute method
ms.assetid: 7a6c7d03-1ff1-4059-bd54-5f407eeebc26
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 483854d0bea61af1bf8bd1f5338770fcc49b37be
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634919"
---
# <a name="idiaframedataexecute"></a>IDiaFrameData::execute
スタック アンワインドを実行し、スタック ウォーク フレーム インターフェイスに結果を返します。

## <a name="syntax"></a>構文

```C++
HRESULT execute ( 
   IDiaStackWalkFrame* frame
);
```

#### <a name="parameters"></a>パラメーター
 `frame`

[入力] フレーム レジスタの状態を保持する [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md) オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。 次の表に、このメソッドで返される可能性のある戻り値を示します。

|値|説明|
|-----------|-----------------|
|E_DIA_INPROLOG|プロローグ コードでスタック フレームを実行できません。|
|E_DIA_SYNTAX|フレーム プログラムで解析エラーが発生しました。|
|E_DIA_FRAME_ACCESS|レジスタまたはメモリにアクセスできません。|
|E_DIA_VALUE|値の計算エラー (0 による除算など)。|

## <a name="remarks"></a>解説
 このメソッドは、スタックをアンワインドするためにデバッグ時に呼び出されます。 [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md) オブジェクトは、レジスタの更新を受け取り、`execute` メソッドで使用されるメソッドを提供するために、クライアント アプリケーションによって実装されます。

## <a name="see-also"></a>関連項目
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
- [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)
