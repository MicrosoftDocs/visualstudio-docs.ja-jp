---
title: LocationType |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- LocationType enumeration
ms.assetid: d3e1eedc-bfd3-4c91-881b-d69565138d0f
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 28bcaa626797313f6ea68a17da33ef9ea192a856
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68154206"
---
# <a name="locationtype"></a>LocationType
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

シンボルの場所の情報の種類を示します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
enum LocationType {   
   LocIsNull,  
   LocIsStatic,  
   LocIsTLS,  
   LocIsRegRel,  
   LocIsThisRel,  
   LocIsEnregistered,  
   LocIsBitField,  
   LocIsSlot,  
   LocIsIlRel,  
   LocInMetaData,  
   LocIsConstant,  
   LocTypeMax  
};  
```  
  
## <a name="elements"></a>Elements  
 `LocIsNull`  
 場所の情報は、ご利用いただけません。  
  
 `LocIsStatic`  
 場所は静的です。  
  
 `LocIsTLS`  
 場所は、スレッド ローカル ストレージにです。  
  
 `LocIsRegRel`  
 場所は、レジスタの相対です。  
  
 `LocIsThisRel`  
 場所は`this`-相対します。  
  
 `LocIsEnregistered`  
 場所は、レジスタでです。  
  
 `LocIsBitField`  
 場所は、ビット フィールドでです。  
  
 `LocIsSlot`  
 場所は、Microsoft Intermediate Language (MSIL) のスロットです。  
  
 `LocIsIlRel`  
 場所は、MSIL 相対パスです。  
  
 `LocInMetaData`  
 メタデータ内の場所は。  
  
 `LocIsConstant`  
 場所は、定数値でです。  
  
 `LocTypeMax`  
 この列挙体の場所の種類の数。  
  
## <a name="remarks"></a>Remarks  
 使用できるプロパティ、 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)インターフェイスは、イメージ ファイル内のシンボルの場所によって異なります。 詳細については、次を参照してください。[シンボルの場所](../../debugger/debug-interface-access/symbol-locations.md)します。  
  
 この列挙体の値が呼び出しによって返される、 [idiasymbol::get_locationtype](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)メソッド。  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: cvconst.h  
  
## <a name="see-also"></a>関連項目  
 [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [IDiaSymbol::get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)   
 [シンボルの場所](../../debugger/debug-interface-access/symbol-locations.md)
