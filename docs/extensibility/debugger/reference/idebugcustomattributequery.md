---
description: メソッドまたは型でカスタム属性に対するクエリを表します。
title: IDebugCustomAttributeQuery | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugCustomAttributeQuery interface
ms.assetid: b804b619-70eb-4c38-80d9-c8b32b65ed3e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: cd93ea2ab13dd6ab138241b526f0818e24274318
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054271"
---
# <a name="idebugcustomattributequery"></a>IDebugCustomAttributeQuery
メソッドまたは型でカスタム属性に対するクエリを表します。

## <a name="syntax"></a>構文

```
IDebugCustomAttributeQuery : IUnknown
```

## <a name="methods"></a>メソッド
 このインターフェイスでは、次のメソッドが実装されます。

|メソッド|説明|
|------------|-----------------|
|[GetCustomAttributeByName](../../../extensibility/debugger/reference/idebugcustomattributequery-getcustomattributebyname.md)|指定された名前でカスタム属性を取得します。|
|[IsCustomAttributeDefined](../../../extensibility/debugger/reference/idebugcustomattributequery-iscustomattributedefined.md)|指定されたカスタム属性が定義されているかどうかを判断します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Sh.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
