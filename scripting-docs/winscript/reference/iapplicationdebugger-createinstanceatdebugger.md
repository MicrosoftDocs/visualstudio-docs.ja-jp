---
title: IApplicationDebugger::CreateInstanceAtDebugger |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IApplicationDebugger.CreateInstanceAtDebugger
apilocation:
- scrobj.dll
helpviewer_keywords:
- IApplicationDebugger::CreateInstanceAtDebugger
ms.assetid: 6763afac-c86a-4e88-9580-77108fb242fb
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 601f20c530ec5e275139d1e70d3df58fa88cd715
ms.sourcegitcommit: d3a485d47c6ba01b0fc9878cbbb7fe88755b29af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58147632"
---
# <a name="iapplicationdebuggercreateinstanceatdebugger"></a>IApplicationDebugger::CreateInstanceAtDebugger
コードによってデバッガー プロセス内のオブジェクトの作成を許可されているプロセス外の - デバッガーにします。  
  
> [!IMPORTANT]
>  信頼できないコードを信頼されたデバッガー スレッドで任意のオブジェクトを作成できるため、このメソッドを実装しない必要があります。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT CreateInstanceAtDebugger(  
   REFCLSID    rclsid,  
   IUnknown*   pUnkOuter,  
   DWORD       dwClsContext,  
   REFIID      riid,  
   IUnknown**  ppvObject  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `rclsid`  
 [in]クラスを作成するオブジェクトの識別子 (CLSID)。  
  
 `pUnkOuter`  
 [in]場合`NULL`集計の一部として、オブジェクトが作成されていません。 それ以外の場合、`pUnkOuter`集計オブジェクトへのポインターは、`IUnknown`インターフェイス (制御`IUnknown`)。  
  
 `dwClsContext`  
 [in]実行可能コードを実行するためのコンテキスト。 値が列挙体から取得されます`CLSCTX`します。  
  
 `riid`  
 [in]オブジェクトと通信するために使用するインターフェイスの識別子です。  
  
 `ppvObject`  
 [out]要求されたインターフェイス ポインターを受け取るポインター変数のアドレス`riid`します。 成功時に、*`ppvObject`要求されたインターフェイス ポインターが含まれています。 障害時に、 \* `ppvObject`が含まれています`NULL`します。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|[値]|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>Remarks  
 このメソッドからデリゲートを`CoCreateInstance`します。  
  
 メソッドは現在実装されていません。  
  
## <a name="see-also"></a>関連項目  
 [IApplicationDebugger インターフェイス](../../winscript/reference/iapplicationdebugger-interface.md)