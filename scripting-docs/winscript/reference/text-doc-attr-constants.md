---
title: TEXT_DOC_ATTR 定数 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- TEXT_DOC_ATTR
apilocation:
- scrobj.dll
helpviewer_keywords:
- TEXT_DOC_ATTR constants
ms.assetid: fd9c53a4-8f73-4c6a-abe5-6b831ecd5b1e
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d22b178d85d304f19e52727ef2c67d77f16da1b3
ms.sourcegitcommit: d3a485d47c6ba01b0fc9878cbbb7fe88755b29af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58147385"
---
# <a name="textdocattr-constants"></a>TEXT_DOC_ATTR 定数
ドキュメントの属性を記述します。  
  
## <a name="syntax"></a>構文  
  
```cpp
typedef DWORD TEXT_DOC_ATTR;  
```  
  
## <a name="constants"></a>定数  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|TEXT_DOC_ATTR_READONLY|0x00000001|ドキュメントとは、読み取り専用です。|  
|TEXT_DOC_ATTR_TYPE_PRIMARY|0x00000002|ドキュメントは、このドキュメントのツリーのプライマリ ファイルです。|  
|TEXT_DOC_ATTR_TYPE_WORKER|0x00000004|ドキュメントは、作業者です。|  
|TEXT_DOC_ATTR_TYPE_SCRIPT|0x00000008|ドキュメントは、スクリプト ファイルです。|  
  
## <a name="see-also"></a>関連項目  
 [アクティブ スクリプト デバッガーの定数、列挙型、および構造体](../../winscript/reference/active-script-debugger-constants-enumerations-and-structures.md)