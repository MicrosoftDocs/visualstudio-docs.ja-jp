---
title: Init |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: c55ddec8-9101-4673-979b-4109caca9146
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ea9f8a24d342668b3574c3798a32c58c124aca7b
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58975256"
---
# <a name="init"></a>Init
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

グラフィックス情報をアクティブにキャプチャしてグラフィックス ログ ファイルに記録するように、グラフィックス診断のアプリ内コンポーネントを準備します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
void Init(  
  std::function<void (int len, wchar_t * pszBuffer)> vsgLogGetter  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `vsgLogGetter`  
 パラメーターとして、`wchar_t` で構成されるバッファーの長さとそのバッファーへのポインターを受け取り、`void` を返す、呼び出し可能なエンティティ (関数、関数ポインター、ラムダ、関数オブジェクトなど)。 呼び出されると、呼び出し可能なエンティティは、グラフィックス情報を記録するために使用されるファイル名を決定し、返される前に指定されたバッファーにファイル名を書き込みます。  
  
## <a name="remarks"></a>Remarks  
 コンストラクターの `Init` パラメーターを `VsgDbg` に指定することで、`bDefaultInit` クラスのインスタンスが構築されると `true` 関数が自動的に呼び出されます。それ以外の場合は、グラフィックス情報をアクティブにキャプチャして記録する前に、`Init` を明示的に呼び出す必要があります。  
  
 `UnInit` を呼び出してアクティブなグラフィックス ログ ファイルを終了して閉じ、`Init` を再度呼び出して、グラフィックス情報をさらにキャプチャして新しいグラフィック ログ ファイルに記録することができます。 この操作を何度でも繰り返して、同じ `VsgDbg` インスタンスを使用して複数の独立したグラフィックス ログ ファイルを作成することができます。  
  
## <a name="see-also"></a>関連項目  
 [UnInit](../debugger/init.md)
