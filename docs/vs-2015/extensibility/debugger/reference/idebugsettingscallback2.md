---
title: IDebugSettingsCallback2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugSettingsCallback2 interface
ms.assetid: 7e525d0b-7d7a-4d1c-8b78-e1398fa922f2
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c3e962c00d6c9230cab765ed56e7607cbfd91765
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58976464"
---
# <a name="idebugsettingscallback2"></a>IDebugSettingsCallback2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

デバッグを有効にメトリックの設定を読み取るエンジン リモートです。  
  
## <a name="syntax"></a>構文  
  
```  
IDebugSettingsCallback2D : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装についてのメモ  
 このインターフェイスは、セッション デバッグ マネージャーのイベント コールバックによって実装され、デバッグ エンジンによって消費されるは。 これは、される可能性がありますもローカル Dbgmetric [d] .lib の代わりにします。  
  
## <a name="methods"></a>メソッド  
 次の表は、メソッドの`IDebugSettingsCallback2`します。  
  
|メソッド|説明|  
|------------|-----------------|  
|[EnumEEs](../../../extensibility/debugger/reference/idebugsettingscallback2-enumees.md)|言語とベンダーの識別子を指定された使用可能な式エバリュエーターを列挙します。|  
|[GetEELocalObject](../../../extensibility/debugger/reference/idebugsettingscallback2-geteelocalobject.md)|メトリックが指定された、式エバリュエーターのローカル オブジェクトを取得します。|  
|[GetEEMetricDword](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricdword.md)|式エバリュエーターの指定したメトリックに対応する値を取得します。|  
|[GetEEMetricFile](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricfile.md)|式エバリュエーター メトリック ファイルが指定された名前またはメトリックを取得します。|  
|[GetEEMetricGuid](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricguid.md)|指定した名前、式エバリュエーター メトリックの一意の識別子を取得します。|  
|[GetEEMetricString](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricstring.md)|指定した名前、式エバリュエーターのメトリックの値の文字列を取得します。|  
|[GetMetricDword](../../../extensibility/debugger/reference/idebugsettingscallback2-getmetricdword.md)|指定した名前のメトリックの値を取得します。|  
|[GetMetricGuid](../../../extensibility/debugger/reference/idebugsettingscallback2-getmetricguid.md)|指定した名前のメトリックの一意の識別子を取得します。|  
|[GetMetricString](../../../extensibility/debugger/reference/idebugsettingscallback2-getmetricstring.md)|指定した名前のメトリックの値の文字列を取得します。|  
  
## <a name="requirements"></a>必要条件  
 ヘッダー:Msdbg.h  
  
 名前空間: Microsoft.VisualStudio.Debugger.Interop  
  
 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="example"></a>例  
 次の例では、受け取る関数、 **IDebugSettingsCallback2**オブジェクトをパラメーターとして。  
  
```cpp#  
HRESULT GetDebugSettingsCallback (IDebugSettingsCallback2 **ppCallback)  
{  
    HRESULT hRes = E_FAIL;  
  
    if ( ppCallback )  
   {  
        if ( EVAL(m_pdec) )  
            hRes = m_pdec->QueryInterface(IID_IDebugSettingsCallback2, (void **)ppCallback);  
        else  
            hRes = E_FAIL;  
    }  
    else  
        hRes = E_INVALIDARG;  
  
    return ( hRes );  
}  
```
