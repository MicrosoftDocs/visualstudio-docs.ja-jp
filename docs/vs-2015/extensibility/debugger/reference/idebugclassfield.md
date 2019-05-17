---
title: IDebugClassField |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugClassField
helpviewer_keywords:
- IDebugClassField interface
ms.assetid: 49358cbc-8973-4862-9dcc-79b1248e6712
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2bd5dfaea68abae6730a97efdff088ca6e7c7a00
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65696989"
---
# <a name="idebugclassfield"></a>IDebugClassField
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、型としてクラスを表します。  
  
## <a name="syntax"></a>構文  
  
```  
IDebugClassField : IDebugContainerField  
```  
  
## <a name="notes-for-implementers"></a>実装についてのメモ  
 シンボル プロバイダーを実装する同一のオブジェクトにこのインターフェイスを実装する、 [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)インターフェイス。 このインターフェイスは、クラス型を表す特殊化です。  
  
## <a name="notes-for-callers"></a>呼び出し元のノート  
 インターフェイスの数がこのインターフェイスを含むを返すことができるメソッドを持つ[IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)、 [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)、および[IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)します。 また、使用する[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)からこのインターフェイスを取得する、 [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)インターフェイスの場合、 [GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)メソッドは、フラグを返します`FIELD_TYPE_CLASS`します。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 メソッドだけでなく、 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)と[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)インターフェイスでは、このインターフェイスは、次を実装します。  
  
|メソッド|説明|  
|------------|-----------------|  
|[EnumBaseClasses](../../../extensibility/debugger/reference/idebugclassfield-enumbaseclasses.md)|このクラスの基底クラスの列挙子を作成します。|  
|[DoesInterfaceExist](../../../extensibility/debugger/reference/idebugclassfield-doesinterfaceexist.md)|特定のインターフェイスは、クラスで定義されているかどうかを決定します。|  
|[EnumNestedClasses](../../../extensibility/debugger/reference/idebugclassfield-enumnestedclasses.md)|このクラスの入れ子になったクラスの列挙子を作成します。|  
|[GetEnclosingClass](../../../extensibility/debugger/reference/idebugclassfield-getenclosingclass.md)|このクラスの外側のクラスを取得します。|  
|[EnumInterfacesImplemented](../../../extensibility/debugger/reference/idebugclassfield-enuminterfacesimplemented.md)|このクラスによって実装されるインターフェイスの列挙子を作成します。|  
|[EnumConstructors](../../../extensibility/debugger/reference/idebugclassfield-enumconstructors.md)|このクラスのコンス トラクターの列挙子を作成します。|  
|[GetDefaultIndexer](../../../extensibility/debugger/reference/idebugclassfield-getdefaultindexer.md)|既定のインデクサーの名前を取得します。|  
|[EnumNestedEnums](../../../extensibility/debugger/reference/idebugclassfield-enumnestedenums.md)|このクラスの入れ子になった列挙子の列挙子を作成します。|  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: sh.h  
  
 名前空間: Microsoft.VisualStudio.Debugger.Interop  
  
 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>関連項目  
 [シンボルプロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)   
 [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
