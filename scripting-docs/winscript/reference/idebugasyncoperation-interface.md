---
title: "IDebugAsyncOperation インターフェイス |Microsoft ドキュメント"
ms.custom: 
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- IDebugAsyncOperation interface
ms.assetid: ebb2ea75-1443-4d8a-812d-171a166f5f9d
caps.latest.revision: 
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 157ed1248535855fcb53ca2eb6f49427fea94149
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/27/2017
---
# <a name="idebugasyncoperation-interface"></a>IDebugAsyncOperation インターフェイス
プロセスをデバッグ マネージャーを実装して、`IDebugAsyncOperation`インターフェイスです。 言語エンジンを呼び出して、`IDebugApplication::CreateAsyncDebugOperation`このインターフェイスへの参照を取得します。 言語エンジンを使用できる、`IDebugAsyncOperation`同期デバッグ操作に非同期アクセスを提供するインターフェイスです。  
  
 継承されたメソッドだけでなく`IUnknown`、`IDebugAsyncOperation`インターフェイスは、次のメソッドを公開します。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[IDebugAsyncOperation::GetSyncDebugOperation](../../winscript/reference/idebugasyncoperation-getsyncdebugoperation.md)|このオブジェクトに関連付けられている同期デバッグ操作を返します。|  
|[IDebugAsyncOperation::Start](../../winscript/reference/idebugasyncoperation-start.md)|非同期操作を開始するがします。|  
|[IDebugAsyncOperation::Abort](../../winscript/reference/idebugasyncoperation-abort.md)|操作をキャンセルします。|  
|[IDebugAsyncOperation::QueryIsComplete](../../winscript/reference/idebugasyncoperation-queryiscomplete.md)|デバッグ操作が完了したかどうかを判断します。|  
|[IDebugAsyncOperation::GetResult](../../winscript/reference/idebugasyncoperation-getresult.md)|同期のデバッグ操作から返されたオブジェクト パラメーターと戻り値を提供します。|