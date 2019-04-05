---
title: IDebugManagedObject |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugManagedObject
helpviewer_keywords:
- IDebugManagedObject interface
ms.assetid: 3ae09d34-112c-4285-80ee-9f7f8dc414d7
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c098f7ada916ad5d1d611d04af9223f147299f0b
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58973355"
---
# <a name="idebugmanagedobject"></a>IDebugManagedObject
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

> [!IMPORTANT]
>  Visual Studio 2015 での式エバリュエーターの実装には、この方法は非推奨とされます。 CLR 式エバリュエーターの実装方法の詳細についてを参照してください[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)と[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)します。  
  
 このインターフェイスは、式エバリュエーターを値クラスのインスタンスでプロパティまたはメソッドを呼び出すには、(EE) を使用できます (たとえば、 `System.Decimal`) を呼び出さずに、その値を設定して[評価](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md)デバッグ中のプログラムで。  
  
## <a name="syntax"></a>構文  
  
```  
IDebugManagedObject : IDebugObject  
```  
  
## <a name="notes-for-implementers"></a>実装についてのメモ  
 式エバリュエーターでは、変数などのマネージ コード オブジェクトを表すには、このインターフェイスを実装します。  
  
## <a name="notes-for-callers"></a>呼び出し元のノート  
 このインターフェイスを取得する呼び出し[GetManagedDebugObject](../../../extensibility/debugger/reference/idebugobject-getmanageddebugobject.md)上、 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)を表す値クラスのインスタンス。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 継承されたメソッドだけでなく[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)、`IDebugManagedObject`インターフェイスは、次のメソッドを公開します。  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject-getmanagedobject.md)|マネージ コード オブジェクトを表すし、適切なマネージ コードのインターフェイスを取得できるインターフェイスを返します。|  
|[SetFromManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject-setfrommanagedobject.md)|このオブジェクトの値を指定したマネージ コード オブジェクトの値に設定します。|  
  
## <a name="remarks"></a>Remarks  
 式エバリュエーターでは、解析ツリーで、マネージ コード オブジェクトを格納するのにこのインターフェイスを使用します。  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: ee.h  
  
 名前空間: Microsoft.VisualStudio.Debugger.Interop  
  
 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>関連項目  
 [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)   
 [Evaluate](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md)
