---
title: IDebugAlias |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugAlias
helpviewer_keywords:
- IDebugAlias interface
ms.assetid: 3cc4c9a4-7805-4239-b00e-eb4a024f3c55
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6c05b6987804681176abdde0e8c94a7463a9163c
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63442315"
---
# <a name="idebugalias"></a>IDebugAlias
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

> [!IMPORTANT]
> Visual Studio 2015 での式エバリュエーターの実装には、この方法は非推奨とされます。 CLR 式エバリュエーターの実装方法の詳細についてを参照してください[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)と[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)します。  
  
 変数の数値のエイリアスを表します。 エイリアスは、単に別の変数名です。  
  
## <a name="syntax"></a>構文  
  
```  
IDebugAlias : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装についてのメモ  
 式エバリュエーター (EE) は、変数の数値の別名をサポートするには、このインターフェイスを実装します。  
  
## <a name="notes-for-callers"></a>呼び出し元のノート  
 [CreateAlias](../../../extensibility/debugger/reference/idebugobject2-createalias.md)特定のオブジェクトの別名を作成します。 別名を検索するには、使用[FindAlias](../../../extensibility/debugger/reference/idebugbinder3-findalias.md)または[GetAllAliases](../../../extensibility/debugger/reference/idebugbinder3-getallaliases.md)します。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次のメソッドが定義されている、`IDebugAlias`インターフェイス。  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetObject](../../../extensibility/debugger/reference/idebugalias-getobject.md)|このエイリアスが参照するオブジェクトを取得します。|  
|[GetName](../../../extensibility/debugger/reference/idebugalias-getname.md)|エイリアス名を取得します。|  
|[GetICorDebugValue](../../../extensibility/debugger/reference/idebugalias-geticordebugvalue.md)|取得、`ICorDebugValue`へのアクセスを提供するインターフェイスのマネージ コードについてはこのオブジェクト (マネージ コードのみ)。|  
|[Dispose](../../../extensibility/debugger/reference/idebugalias-dispose.md)|このエイリアスとして使用されていないをマークします。|  
  
## <a name="remarks"></a>Remarks  
 エイリアスは、後に、1001 #、# 文字の文字列形式の 10 進数です。  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: ee.h  
  
 名前空間: Microsoft.VisualStudio.Debugger.Interop  
  
 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>関連項目  
 [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)   
 [CreateAlias](../../../extensibility/debugger/reference/idebugobject2-createalias.md)   
 [FindAlias](../../../extensibility/debugger/reference/idebugbinder3-findalias.md)   
 [GetAllAliases](../../../extensibility/debugger/reference/idebugbinder3-getallaliases.md)
