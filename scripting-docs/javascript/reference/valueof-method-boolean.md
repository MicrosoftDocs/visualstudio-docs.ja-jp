---
title: valueOf メソッド (Boolean) |Microsoft ドキュメント
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-client-threshold
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-javascript
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: ac6ad343-7663-406a-a2b7-4cc5025ca3d6
caps.latest.revision: 2
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c36eda63fb38886df4d8bffec7cfdbb6c6d05eb8
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/27/2017
ms.locfileid: "24640242"
---
# <a name="valueof-method-boolean"></a>valueOf メソッド (Boolean)
指定したブール型のプリミティブ値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
boolean.valueOf()  
```  
  
## <a name="return-value"></a>戻り値  
 ブール型のプリミティブ値 (true または false)。  
  
## <a name="remarks"></a>コメント  
 次のコードでは、このメソッドを使用する方法を示します。  
  
```JavaScript  
var bool = new Boolean("true");  
var s = bool.valueOf();  
document.write(s);  
  
// Output: true  
  
```  
  
## <a name="requirements"></a>要件  
 [!INCLUDE[jsv2](../../javascript/reference/includes/jsv2-md.md)]