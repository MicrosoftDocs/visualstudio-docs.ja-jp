---
description: この保留中のブレークポイントをコードの場所にバインドできるかどうかを判断します。
title: IDebugPendingBreakpoint2::CanBind | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPendingBreakpoint2::CanBind
helpviewer_keywords:
- IDebugPendingBreakpoint2::CanBind method
- CanBind method
ms.assetid: 84a2b189-ccf1-467e-8fab-0c0da68f0b91
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2ffc2638d6f0a538279b400eacd4155a56054bd7
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087796"
---
# <a name="idebugpendingbreakpoint2canbind"></a>IDebugPendingBreakpoint2::CanBind
この保留中のブレークポイントをコードの場所にバインドできるかどうかを判断します。

## <a name="syntax"></a>構文

```cpp
HRESULT CanBind ( 
   IEnumDebugErrorBreakpoints2** ppErrorEnum
);
```

```csharp
int CanBind ( 
   out IEnumDebugErrorBreakpoints2 ppErrorEnum
);
```

## <a name="parameters"></a>パラメーター
`ppErrorEnum`\
[出力] エラーが発生した可能性がある場合は、[IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md) オブジェクトの一覧を含む [IEnumDebugErrorBreakpoints2](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK.` を返します。ブレークポイントがバインドできない場合は、`S_FALSE` を返します。この場合、`ppErrorEnum` パラメーターによってエラーが返されます。 それ以外の場合はエラー コードを返します。 ブレークポイントが削除されている場合は、`E_BP_DELETED` を返します。

## <a name="remarks"></a>解説
 このメソッドは、この保留中のブレークポイントがバインドされた場合に何が起きるのかを判断するために呼び出されます。 保留中のブレークポイントを実際にバインドするには、[Bind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md) メソッドを呼び出します。

## <a name="example"></a>例
 次の例は、[IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) インターフェイスを公開するシンプルな `CPendingBreakpoint` オブジェクトにこのメソッドを実装する方法を示しています。

```cpp
HRESULT CPendingBreakpoint::CanBind(IEnumDebugErrorBreakpoints2** ppErrorEnum)
{
   HRESULT hr;
   HRESULT hrT;

   // Check for a valid pointer to an error breakpoint enumerator
   // interface; otherwise, return hr = E_INVALIDARG.
   if (ppErrorEnum)
   {
      // Verify that the pending breakpoint has not been deleted. If
      // deleted, then return hr = E_BP_DELETED.
      if (m_state.state != PBPS_DELETED)
      {
         // Verify that the breakpoint is a file/line breakpoint.
         if (IsFlagSet(m_pBPRequest->m_bpRequestInfo.dwFields, BPREQI_BPLOCATION) &&
             m_pBPRequest->m_bpRequestInfo.bpLocation.bpLocationType == BPLT_CODE_FILE_LINE)
         {
            hr = S_OK;
         }
         // If the breakpoint type is not a file/line breakpoint, then the
         // result should be an error breakpoint.
         else
         {
            // If the error breakpoint member variable does not have
            // allocated memory.
            if (!m_pErrorBP)
            {
               // Create, AddRef, and initialize a CErrorBreakpoint object.
               if (CComObject<CErrorBreakpoint>::CreateInstance(&m_pErrorBP) == S_OK)
               {
                  m_pErrorBP->AddRef();
                  m_pErrorBP->Initialize(this);
               }
            }

            // Create a new enumerator of error breakpoints.
             CComObject<CEnumDebugErrorBreakpoints>* pErrorEnum;
            if (CComObject<CEnumDebugErrorBreakpoints>::CreateInstance(&pErrorEnum) == S_OK)
            {
               // Get the IDebugErrorBreakpoint2 information for the
               // CErrorBreakpoint object.
               CComPtr<IDebugErrorBreakpoint2> spErrorBP;
               hrT = m_pErrorBP->QueryInterface(&spErrorBP);
               assert(hrT == S_OK);
               if (hrT == S_OK)
               {
                  // Initialize the new enumerator of error breakpoints
                  // with the IDebugErrorBreakpoint2 information.
                  IDebugErrorBreakpoint2* rgpErrorBP[] = { spErrorBP.p };
                  hrT = pErrorEnum->Init(rgpErrorBP, &(rgpErrorBP[1]), NULL, AtlFlagCopy);
                  if (hrT == S_OK)
                  {
                     // Verify that the passed IEnumDebugErrorBreakpoints2
                     // interface can be successful queried by the
                     // created CEnumDebugErrorBreakpoints object.
                     hrT = pErrorEnum->QueryInterface(ppErrorEnum);
                     assert(hrT == S_OK);
                  }
               }

               // Otherwise, delete the CEnumDebugErrorBreakpoints object.
               if (FAILED(hrT))
               {
                  delete pErrorEnum;
               }
            }

            hr = S_FALSE;
         }
      }
      else
      {
         hr = E_BP_DELETED;
      }
   }
   else
   {
      hr = E_INVALIDARG;
   }

   return hr;
}
```

## <a name="see-also"></a>関連項目
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [IEnumDebugErrorBreakpoints2](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md)
- [IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)
- [Bind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)
