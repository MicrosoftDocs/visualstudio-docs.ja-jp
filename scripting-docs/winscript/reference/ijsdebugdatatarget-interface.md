---
title: IJsDebugDataTarget インターフェイス |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: a9b784d6-958f-4d55-b3f6-c2d6b260a16b
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3cbb4b0b54fb9a3821d3033ef0e65fd0bafbc246
ms.sourcegitcommit: d3a485d47c6ba01b0fc9878cbbb7fe88755b29af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58159286"
---
# <a name="ijsdebugdatatarget-interface"></a>IJsDebugDataTarget インターフェイス
デバッガーによって実装されており、対象のデバッガー プロセスの状態にアクセスして変更する機能を提供します。  
  
## <a name="syntax"></a>構文  
  
```cpp
IJsDebugDataTarget : public IUnknown;  
```  
  
## <a name="members"></a>メンバー  
  
### <a name="public-methods"></a>パブリック メソッド  
  
|名前|説明|  
|----------|-----------------|  
|[IJsDebugDataTarget::AllocateVirtualMemory メソッド](../../winscript/reference/ijsdebugdatatarget-allocatevirtualmemory-method.md)|ターゲット プロセスの仮想アドレス空間内のメモリ領域を予約/コミットします。|  
|[IJsDebugDataTarget::CreateStackFrameEnumerator メソッド](../../winscript/reference/ijsdebugdatatarget-createstackframeenumerator-method.md)|スタック フレームの列挙子を作成します。|  
|[IJsDebugDataTarget::FreeVirtualMemory メソッド](../../winscript/reference/ijsdebugdatatarget-freevirtualmemory-method.md)|ターゲット プロセスの仮想アドレス空間内のメモリ領域を解放/デコミットします。|  
|[IJsDebugDataTarget::GetThreadContext メソッド](../../winscript/reference/ijsdebugdatatarget-getthreadcontext-method.md)|指定したスレッドのコンテキストを取得します。|  
|[IJsDebugDataTarget::GetTlsValue メソッド](../../winscript/reference/ijsdebugdatatarget-gettlsvalue-method.md)|スレッドがデバッグ中の場合は、スレッド ローカル ストレージ (TLS) スロット内の値を、指定したインデックスに基づいて取得します。|  
|[IJsDebugDataTarget::ReadBSTR メソッド](../../winscript/reference/ijsdebugdatatarget-readbstr-method.md)|デバッグ対象から BSTR を読み取ります。|  
|[IJsDebugDataTarget::ReadMemory メソッド](../../winscript/reference/ijsdebugdatatarget-readmemory-method.md)|ターゲット プロセスのメモリを読み取ります。|  
|[IJsDebugDataTarget::ReadNullTerminatedString メソッド](../../winscript/reference/ijsdebugdatatarget-readnullterminatedstring-method.md)|指定した数の文字をターゲットから読み取ります。|  
|[IJsDebugDataTarget::WriteMemory メソッド](../../winscript/reference/ijsdebugdatatarget-writememory-method.md)|ターゲット プロセスのメモリを読み取ります。|  
  
## <a name="requirements"></a>必要条件  
 **ヘッダー:** jscript9diag.h です  
  
## <a name="see-also"></a>関連項目  
 [Windows スクリプト インターフェイスのリファレンス](../../winscript/reference/windows-script-interfaces-reference.md)