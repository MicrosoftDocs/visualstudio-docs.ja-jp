---
title: IActiveScriptSiteWindow::GetWindow |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptSiteWindow.GetWindow
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptSiteWindow_GetWindow
ms.assetid: 6284e38c-9dfb-4d69-903d-f243f78c0331
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7b6efa066765339375a8315695aa9c1de2f9c46b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62992058"
---
# <a name="iactivescriptsitewindowgetwindow"></a>IActiveScriptSiteWindow::GetWindow
スクリプト エンジンを表示する必要がある、ポップアップ ウィンドウの所有者として機能できるウィンドウのハンドルを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetWindow(  
    HWND *phwnd  // address of variable for window handle  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `phwnd`  
 [out]ウィンドウ ハンドルを受け取る変数のアドレス。  
  
## <a name="return-value"></a>戻り値  
 返します`S_OK`成功した場合、または`E_FAIL`場合は、エラーが発生しました。  
  
## <a name="remarks"></a>Remarks  
 このメソッドは、`IOleWindow::GetWindow`メソッド。  
  
## <a name="see-also"></a>関連項目  
 [IActiveScriptSiteWindow](../../winscript/reference/iactivescriptsitewindow.md)