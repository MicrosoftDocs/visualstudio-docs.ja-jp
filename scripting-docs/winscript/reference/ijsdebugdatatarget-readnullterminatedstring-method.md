---
title: Ijsdebugdatatarget::readnullterminatedstring メソッド |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IJsDebugDataTarget.ReadNullTerminatedString
apilocation:
- jscript9diag.dll
ms.assetid: 64683b39-6fc2-40c4-82ae-2a6f58d392d5
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a681dcedf873f0cb96f47b14278f47271cd43ec8
ms.sourcegitcommit: 116e9614867e0b3c627ce9001012a4c39435a42b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/08/2019
ms.locfileid: "54093328"
---
# <a name="ijsdebugdatatargetreadnullterminatedstring-method"></a>IJsDebugDataTarget::ReadNullTerminatedString メソッド
指定した数の文字をターゲットから読み取ります。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT ReadNullTerminatedString(  
   UINT64 address,  
   UINT16 characterSize,  
   UINT32 maxCharacters,  
   BSTR *pString  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `address`  
 [入力] 読み取り元のアドレス。  
  
 `characterSize`  
 [入力] 文字列の各文字のサイズ。  
  
 `maxCharacters`  
 [in]読み取る文字の最大数。 maxCharacters は妥当な必要があります。 128 MB を超えるメモリを要求するような値を指定すると、エラーが発生します。  文字列が maxCharacters の文字数を超えた場合、結果の文字列でその超えた部分は切り捨てられます。  
  
 `pString`  
 [出力] ターゲットから読み取った BSTR。  
  
## <a name="return-value"></a>戻り値  
  
## <a name="remarks"></a>Remarks  
 切り捨てられた場合は S_FALSE を返します。  
  
## <a name="requirements"></a>必要条件  
 **ヘッダー:** jscript9diag.h です  
  
## <a name="see-also"></a>関連項目  
 [IJsDebugDataTarget インターフェイス](../../winscript/reference/ijsdebugdatatarget-interface.md)