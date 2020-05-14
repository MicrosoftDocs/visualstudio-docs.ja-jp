---
title: を読み込むイベント 2::GetModule |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModuleLoadEvent2::GetModule
helpviewer_keywords:
- IDebugModuleLoadEvent2::GetModule
ms.assetid: c86482bb-9ce5-4e63-bbe0-969b50169424
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b90547709e5524ce005b0598b0b8d482cfecf173
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80726724"
---
# <a name="idebugmoduleloadevent2getmodule"></a>IDebugModuleLoadEvent2::GetModule
読み込みまたはアンロードされているモジュールを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetModule( 
   IDebugModule2** pModule,
   BSTR*           pbstrDebugMessage,
   BOOL*           pbLoad
);
```

```csharp
int GetModule( 
   out IDebugModule2 pModule,
   ref string        pbstrDebugMessage,
   ref int           pbLoad
);
```

## <a name="parameters"></a>パラメーター
`pModule`\
[アウト]読み込み中またはアンロード中のモジュールを表す[IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)オブジェクトを返します。

`pbstrDebugMessage`\
[イン、アウト]このイベントを説明するオプションのメッセージを返します。 このパラメーターが NULL 値の場合、メッセージは要求されません。

`pbLoad`\
[イン、アウト]モジュールが`TRUE`ロード中の場合は 0 以外`FALSE`( ) 、 モジュールがアンロード中の場合は 0 ( ) 以外の値を指定します。 このパラメーターが NULL 値の場合、状況は要求されません。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugModuleLoadEvent2](../../../extensibility/debugger/reference/idebugmoduleloadevent2.md)
- [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)
