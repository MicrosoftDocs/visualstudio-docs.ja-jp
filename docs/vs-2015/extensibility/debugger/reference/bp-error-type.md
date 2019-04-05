---
title: BP_ERROR_TYPE |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- BP_ERROR_TYPE
helpviewer_keywords:
- BP_ERROR_TYPE enumeration
ms.assetid: c483eaab-db29-46de-bfdb-5c2a9a9cfb68
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2317fafe410cacfca1c77b669a54669ea6e2224a
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58973631"
---
# <a name="bperrortype"></a>BP_ERROR_TYPE
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

ブレークポイントのエラーの種類を指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
enum enum_BP_ERROR_TYPE {   
   BPET_NONE            = 0x00000000,  
   BPET_TYPE_WARNING    = 0x00000001,  
   BPET_TYPE_ERROR      = 0x00000002,  
   BPET_SEV_HIGH        = 0x0F000000,  
   BPET_SEV_GENERAL     = 0x07000000,  
   BPET_SEV_LOW         = 0x01000000,  
   BPET_TYPE_MASK       = 0x0000ffff,  
   BPET_SEV_MASK        = 0xffff0000,  
   BPET_GENERAL_WARNING = BPET_SEV_GENERAL | BPET_TYPE_WARNING,  
   BPET_GENERAL_ERROR   = BPET_SEV_GENERAL | BPET_TYPE_ERROR,  
   BPET_ALL             = 0xffffffff  
};  
typedef DWORD BP_ERROR_TYPE;  
```  
  
```csharp  
public enum enum_BP_ERROR_TYPE {   
   BPET_NONE            = 0x00000000,  
   BPET_TYPE_WARNING    = 0x00000001,  
   BPET_TYPE_ERROR      = 0x00000002,  
   BPET_SEV_HIGH        = 0x0F000000,  
   BPET_SEV_GENERAL     = 0x07000000,  
   BPET_SEV_LOW         = 0x01000000,  
   BPET_TYPE_MASK       = 0x0000ffff,  
   BPET_SEV_MASK        = 0xffff0000,  
   BPET_GENERAL_WARNING = BPET_SEV_GENERAL | BPET_TYPE_WARNING,  
   BPET_GENERAL_ERROR   = BPET_SEV_GENERAL | BPET_TYPE_ERROR,  
   BPET_ALL             = 0xffffffff  
};  
```  
  
## <a name="members"></a>メンバー  
 BPET_NONE  
 ブレークポイントのエラーがないを指定します。  
  
 BPET_TYPE_WARNING  
 警告スタイルのブレークポイントのエラーを指定します。  
  
 BPET_TYPE_ERROR  
 ブレークポイント エラー エラー スタイルを指定します。  
  
 BPET_SEV_HIGH  
 重要度の高いブレークポイントのエラーを指定します。  
  
 BPET_SEV_GENERAL  
 中規模、重大度レベルのブレークポイントのエラーを指定します。  
  
 BPET_SEV_LOW  
 ブレークポイントの重大度の低いエラーを指定します。  
  
 BPET_TYPE_MASK  
 マスク スタイルのブレークポイントのエラーを指定します。  
  
 BPET_SEV_MASK  
 重大度マスクのスタイルのブレークポイントのエラーを指定します。  
  
 BPET_GENERAL_WARNING  
 一般的な型の警告ブレークポイントのエラーを指定します。  
  
 BPET_GENERAL_ERROR  
 [全般]-エラー スタイルのブレークポイントのエラーを指定します。  
  
 BPET_ALL  
 すべてのブレークポイントのエラーの種類を指定します。  
  
## <a name="remarks"></a>Remarks  
 これらの値は、演算と組み合わせることがあります`OR`に使用されると、`dwType`のメンバー、 [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)構造体。 パラメーターとして渡される、 [EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)メソッド。  
  
 ブレークポイント エラーの種類は、型の重大度レベルで構成されます。 つまり、ブレークポイントのエラーの種類は、型だけではありません (たとえば、 `BPET_TYPE_ERROR`、) または重大度レベル (など`BPET_SEV_GENERAL`) を単独で。 `BPET_GENERAL_WARNING` `BPET_GENERAL_ERROR`警告およびエラーの一般的なブレークポイントの定義済みの値を指定します。  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: msdbg.h  
  
 名前空間: Microsoft.VisualStudio.Debugger.Interop  
  
 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>関連項目  
 [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)   
 [EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)
