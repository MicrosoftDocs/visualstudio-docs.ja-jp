---
title: IDebugEngine2::CreatePendingBreakpoint |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugEngine2::CreatePendingBreakpoint
helpviewer_keywords:
- IDebugEngine2::CreatePendingBreakpoint
ms.assetid: 92e85b90-a931-48d9-89a7-a6edcb83ae5a
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 84c36d08c7ad907006eb9f41d2f6e2c9cd77e7bf
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68196045"
---
# <a name="idebugengine2creatependingbreakpoint"></a>IDebugEngine2::CreatePendingBreakpoint
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

デバッグ エンジン (DE) には、保留中のブレークポイントを作成します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT CreatePendingBreakpoint(   
   IDebugBreakpointRequest2*  pBPRequest,  
   IDebugPendingBreakpoint2** ppPendingBP  
);  
```  
  
```csharp  
int CreatePendingBreakpoint(   
   IDebugBreakpointRequest2     pBPRequest,  
   out IDebugPendingBreakpoint2 ppPendingBP  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pBPRequest`  
 [in][IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)を作成する保留中のブレークポイントを表すオブジェクト。  
  
 `ppPendingBP`  
 [out]返します、 [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)保留中のブレークポイントを表すオブジェクト。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。 通常返す`E_FAIL`場合、`pBPRequest`パラメーターがの場合は、DE でサポートされている任意の言語と一致しません、`pBPRequest`パラメーターが無効か不完全です。  
  
## <a name="remarks"></a>Remarks  
 保留中のブレークポイントは、本質的にコードにブレークポイントをバインドするために必要なすべての情報のコレクションです。 このメソッドから返された保留中のブレークポイントがまでコードにバインドされていない、[バインド](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)メソッドが呼び出されます。  
  
 各保留中のブレークポイントのユーザー セット、セッション デバッグ マネージャー (SDM) このメソッドを呼び出します接続されている各 DE でします。 ブレークポイントがその DE で実行されているプログラムに対して有効であることを確認する DE の責任です。  
  
 ユーザーは、コードの行にブレークポイントを設定、ときに、DE はこのコードに対応するドキュメント内の最も近い行にブレークポイントをバインドする無料です。 これにより、ユーザーが、複数行ステートメントの最初の行にブレークポイントを設定するが、(すべてのコードはデバッグ情報の属性) の最後の行にバインドしています。  
  
## <a name="example"></a>例  
 次の例は、単純なは、このメソッドを実装する方法を示しています。`CProgram`オブジェクト。 既定の実装、`IDebugEngine2::CreatePendingBreakpoint`メソッドは、各プログラムのこの実装にすべての呼び出しを転送します。  
  
```  
HRESULT CProgram::CreatePendingBreakpoint(IDebugBreakpointRequest2* pBPRequest, IDebugPendingBreakpoint2** ppPendingBP)     
{    
  
   // Create and initialize the CPendingBreakpoint object.  
   CComObject<CPendingBreakpoint> *pPending;    
   CComObject<CPendingBreakpoint>::CreateInstance(&pPending);    
   pPending->Initialize(pBPRequest, m_pInterp, m_pCallback, m_pEngine);    
   return pPending->QueryInterface(ppPendingBP);    
}    
```  
  
## <a name="see-also"></a>関連項目  
 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)   
 [バインド](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)   
 [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)   
 [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
