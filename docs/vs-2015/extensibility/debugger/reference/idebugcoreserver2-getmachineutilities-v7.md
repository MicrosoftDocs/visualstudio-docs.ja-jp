---
title: IDebugCoreServer2::GetMachineUtilities_V7 |Microsoft Docs
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- IDebugCoreServer2::GetMachineUtilities_V7
helpviewer_keywords:
- IDebugCoreServer2::GetMachineUtilities_V7
ms.assetid: 64c1f08f-853b-4498-9810-29791581ef2f
caps.latest.revision: 18
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 217118d96fbcf50f267570bcd1c26abd5d8128c3
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2018
ms.locfileid: "47536462"
---
# <a name="idebugcoreserver2getmachineutilitiesv7"></a>IDebugCoreServer2::GetMachineUtilities_V7
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このトピックの最新バージョンをご覧[IDebugCoreServer2::GetMachineUtilities_V7](https://docs.microsoft.com/visualstudio/extensibility/debugger/reference/idebugcoreserver2-getmachineutilities-v7)します。  
  
このメソッドは、サーバーのマシン ユーティリティを取得します。  
  
> [!NOTE]
>  このメソッドは廃止されています。 使用しないでください ([!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]は常に返します`E_NOTIMPL`このメソッドが呼び出された場合)。 これは歴史的な理由から保持されます。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetMachineUtilities_V7(  
   IDebugMDMUtil2_V7** ppUtil  
);  
```  
  
```csharp  
int GetMachineUtilities_V7(  
   out IDebugMDMUtil2_V7 ppUtil  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ppUtil`  
 [out]返します、`IDebugMDMUtil2_V7`マシン ユーティリティの情報を表すインターフェイスです。  
  
## <a name="return-value"></a>戻り値  
 常に返します`E_NOTIMPL`メソッドが実装されていないことを示します。  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 常に返します`E_NOTIMPL`場合、このメソッドが呼び出されます。  
  
## <a name="see-also"></a>関連項目  
 [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)

