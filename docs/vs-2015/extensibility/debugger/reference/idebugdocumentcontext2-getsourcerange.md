---
title: IDebugDocumentContext2::GetSourceRange |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2::GetSourceRange
helpviewer_keywords:
- IDebugDocumentContext2::GetSourceRange
ms.assetid: 5903c75e-5390-4d13-9314-1ee276255313
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: bcec6af2b8e7b1acfdc9c3cf38cb18654be78c53
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58977145"
---
# <a name="idebugdocumentcontext2getsourcerange"></a>IDebugDocumentContext2::GetSourceRange
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このドキュメントのコンテキストのソース コードの範囲を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetSourceRange(   
   TEXT_POSITION* pBegPosition,  
   TEXT_POSITION* pEndPosition  
);  
```  
  
```csharp  
int GetSourceRange(   
   TEXT_POSITION[] pBegPosition,  
   TEXT_POSITION[] pEndPosition  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pBegPosition`  
 [入力、出力]A [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)構造体の開始位置が入力されます。 この情報が必要でない場合は、この引数を null 値を設定します。  
  
 `pEndPosition`  
 [入力、出力]A [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)構造体の終了位置が入力されます。 この情報が必要でない場合は、この引数を null 値を設定します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。  
  
## <a name="remarks"></a>Remarks  
 ソース範囲は、コードの原因である前のステートメントの直後に現在のステートメントのバックアップからのソース コードの全体の範囲です。 ソース範囲は、逆アセンブル ウィンドウでコードのコメントを含むソース ステートメントを混在させる場合の通常使用されます。  
  
 このドキュメントのコンテキスト内に含まれるコード ステートメントだけの範囲を取得する、 [GetStatementRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md)メソッド。  
  
## <a name="see-also"></a>関連項目  
 [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)   
 [GetStatementRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md)   
 [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
