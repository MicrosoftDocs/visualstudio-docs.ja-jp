---
title: IDebugGenericParamField |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugGenericParamField interface
ms.assetid: ba24f499-5ba7-4c67-83e6-923229b52327
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ab5cb19475ae92ab1e89bdce5c833e0f18a2cccb
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56720708"
---
# <a name="idebuggenericparamfield"></a>IDebugGenericParamField
マネージ コードのジェネリック型のパラメーターを表します。

## <a name="syntax"></a>構文

```
IDebugGenericParamField : IDebugField
```

## <a name="notes-for-implementers"></a>実装についてのメモ
 ジェネリックのサポートに使用されます。

## <a name="methods"></a>メソッド
 メソッドだけでなく、 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)インターフェイスでは、このインターフェイスは、次のメソッドを実装します。

|メソッド|説明|
|------------|-----------------|
|[ConstraintCount](../../../extensibility/debugger/reference/idebuggenericparamfield-constraintcount.md)|このジェネリック パラメーターに関連付けられている制約の数を返します。|
|[GetConstraints](../../../extensibility/debugger/reference/idebuggenericparamfield-getconstraints.md)|このジェネリック パラメーターに関連付けられている制約を取得します。|
|[GetFlags](../../../extensibility/debugger/reference/idebuggenericparamfield-getflags.md)|このジェネリック パラメーターのフラグを取得します。|
|[GetIndex](../../../extensibility/debugger/reference/idebuggenericparamfield-getindex.md)|このジェネリック パラメーターのインデックスを取得します。|
|[GetNameOfFormalParam](../../../extensibility/debugger/reference/idebuggenericparamfield-getnameofformalparam.md)|このジェネリック パラメーターの名前を取得します。|
|[GetOwner](../../../extensibility/debugger/reference/idebuggenericparamfield-getowner.md)|このジェネリック パラメーターの型またはメソッドの所有者を取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー:Sh.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll