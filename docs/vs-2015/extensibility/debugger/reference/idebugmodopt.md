---
title: IDebugModOpt |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugModOpt interface
ms.assetid: ebd525e3-d140-4071-9d8c-41871de4125e
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 66f499225d2b319f3678c88894a1217d90b10135
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68162518"
---
# <a name="idebugmodopt"></a>IDebugModOpt
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

デバッグ オプションの修飾子を表します。  
  
## <a name="syntax"></a>構文  
  
```  
IDebugModOpt : IUnknown  
```  
  
## <a name="notes-for-callers"></a>呼び出し元のノート  
 取得した、 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)クラスまたはメソッドを表すオブジェクト。  
  
## <a name="methods"></a>メソッド  
 このインターフェイスは、次のメソッドを実装します。  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetModOpts](../../../extensibility/debugger/reference/idebugmodopt-getmodopts.md)|オプションの修飾子の一覧を取得します。|  
  
## <a name="requirements"></a>必要条件  
 ヘッダー:Sh.h  
  
 名前空間: Microsoft.VisualStudio.Debugger.Interop  
  
 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll
