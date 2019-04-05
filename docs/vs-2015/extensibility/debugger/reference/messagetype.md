---
title: MESSAGETYPE |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- MESSAGETYPE
helpviewer_keywords:
- MESSAGETYPE enumeration
ms.assetid: 800cc77d-3c27-4763-a9df-552a9384bd49
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c17564c992f4c8855d8a96165975a5d0e132755c
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58974860"
---
# <a name="messagetype"></a>MESSAGETYPE
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

メッセージの種類と理由を指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
enum enum_MESSAGETYPE {   
   MT_OUTPUTSTRING      = 0x0000001,  
   MT_MESSAGEBOX        = 0x00000002,  
   MT_TYPE_MASK         = 0x000000FF,  
   MT_REASON_EXCEPTION  = 0x00000100,  
   MT_REASON_TRACEPOINT = 0x00000200,  
   MT_REASON_MASK       = 0x0000FF00  
};  
typedef DWORD MESSAGETYPE;  
```  
  
```csharp  
public enum enum_MESSAGETYPE {   
   MT_OUTPUTSTRING      = 0x0000001,  
   MT_MESSAGEBOX        = 0x00000002,  
   MT_TYPE_MASK         = 0x000000FF,  
   MT_REASON_EXCEPTION  = 0x00000100,  
   MT_REASON_TRACEPOINT = 0x00000200,  
   MT_REASON_MASK       = 0x0000FF00  
};  
```  
  
## <a name="members"></a>メンバー  
 MT_OUTPUTSTRING  
 出力ウィンドウにメッセージを送信する必要があることを示します。 これはから相互に排他的な`MT_MESSAGEBOX`します。  
  
 MT_MESSAGEBOX  
 メッセージがメッセージ ボックスに表示することを示します。 これはから相互に排他的な`MT_OUTPUTSTRING`します。  
  
 MT_TYPE_MASK  
 メッセージの送信先を分離するマスク値。  
  
 MT_REASON_EXCEPTION  
 例外の結果として、メッセージ ボックスが表示されていることを示します。 これはから相互に排他的な`MT_REASON_TRACEPOINT`します。  
  
 MT_REASON_TRACEPOINT  
 トレース ポイントに達した結果として、メッセージ ボックスが表示されていることを示します。 これは、相互に排他的`MT_REASON_EXCEPTION`します。  
  
 MT_REASON_MASK  
 表示されているメッセージの原因を分離するマスク値。  
  
## <a name="remarks"></a>Remarks  
 これらの値から返される、 [GetMessage](../../../extensibility/debugger/reference/idebugmessageevent2-getmessage.md)と[GetErrorMessage](../../../extensibility/debugger/reference/idebugerrorevent2-geterrormessage.md)メソッド。  
  
 理由の値のいずれかの演算を使用して出力先の値のいずれかと組み合わせることができます`OR`します。  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: msdbg.h  
  
 名前空間: Microsoft.VisualStudio.Debugger.Interop  
  
 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>関連項目  
 [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [GetMessage](../../../extensibility/debugger/reference/idebugmessageevent2-getmessage.md)   
 [GetErrorMessage](../../../extensibility/debugger/reference/idebugerrorevent2-geterrormessage.md)
