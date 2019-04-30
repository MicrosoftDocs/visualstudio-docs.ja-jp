---
title: アクティブ スクリプトの定数、列挙型、およびエラー コード |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: aab24471-5817-45c0-be07-ffe4648923ed
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 090b494e904fbef1c0d3d8b380f7a184a6042788
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62953999"
---
# <a name="active-script-constants-enumerations-and-error-codes"></a>アクティブ スクリプトの定数、列挙型、およびエラー コード
このセクションでは、列挙型および Windows スクリプト エンジンで使用されるエラー コードについて説明します。  
  
## <a name="constants"></a>定数  
  
|定数|説明|  
|--------------|-----------------|  
|[SCRIPTTHREADID 定数](../../winscript/reference/scriptthreadid-constants.md)|スレッドの種類を指定します。|  
  
## <a name="properties"></a>プロパティ  
  
|プロパティ|説明|  
|--------------|-----------------|  
|[SCRIPTPROP_HOSTKEEPALIVE プロパティ](../../winscript/reference/scriptprop-hostkeepalive-property.md)|スクリプト エンジンを未解決の参照がある場合は、完全に機能保持するかどうかを指定するために使用します。|  
  
## <a name="enumerations"></a>列挙  
  
|列挙|説明|  
|-----------------|-----------------|  
|[SCRIPTGCTYPE 列挙型](../../winscript/reference/scriptgctype-enumeration.md)|実行するガベージ コレクションの型。|  
|[SCRIPTLANGUAGEVERSION 列挙型](../../winscript/reference/scriptlanguageversion-enumeration.md)|使用可能なバージョンのスクリプトを指定します。|  
|[SCRIPTSTATE 列挙型](../../winscript/reference/scriptstate-enumeration.md)|スクリプト エンジンの状態を指定します。|  
|||  
|[SCRIPTTHREADSTATE 列挙型](../../winscript/reference/scriptthreadstate-enumeration.md)|スクリプト エンジンでは、スレッドの状態を指定します。|  
|[SCRIPTTRACEINFO 列挙型](../../winscript/reference/scripttraceinfo-enumeration.md)|トレースしているスクリプト イベントを表します。 使用される、 [iactivescriptsitetraceinfo::sendscripttraceinfo メソッド](../../winscript/reference/iactivescriptsitetraceinfo-sendscripttraceinfo-method.md)します。|  
|[SCRIPTUICHANDLING 列挙型](../../winscript/reference/scriptuichandling-enumeration.md)|UI コントロールの処理方法を表します。|  
|[SCRIPTUICITEM 列挙型](../../winscript/reference/scriptuicitem-enumeration.md)|UI 項目の種類を表します。 使用される、 [iactivescriptsiteuicontrol::getuibehavior メソッド](../../winscript/reference/iactivescriptsiteuicontrol-getuibehavior-method.md)します。|  
  
## <a name="error-codes"></a>エラー コード  
  
|エラー コード|説明|  
|----------------|-----------------|  
|[SCRIPT_E_PROPAGATE エラー コード](../../winscript/reference/script-e-propagate-error-code.md)|スクリプト エラーは、別のスレッドで可能性のある呼び出し元に反映中です。|  
|[SCRIPT_E_RECORDED エラー コード](../../winscript/reference/script-e-recorded-error-code.md)|エラーは、スクリプト エンジンとホスト間で渡されました。|  
|[SCRIPT_E_REPORTED エラー コード](../../winscript/reference/script-e-reported-error-code.md)|スクリプト エンジンには、ホストにハンドルされない例外が報告されました。|  
  
## <a name="see-also"></a>関連項目  
 [アクティブ スクリプト インターフェイス](../../winscript/reference/active-script-interfaces.md)