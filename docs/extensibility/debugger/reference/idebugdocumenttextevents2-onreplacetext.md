---
title: "IDebugDocumentTextEvents2::onReplaceText | Microsoft Docs"
ms.custom: ""
ms.date: "11/04/2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "vs-ide-sdk"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "IDebugDocumentTextEvents2::OnReplaceText"
helpviewer_keywords: 
  - "IDebugDocumentTextEvents2::onReplaceText"
ms.assetid: cb39f025-66d8-4dc0-bef6-1bdc8e07db92
caps.latest.revision: 10
ms.author: "gregvanl"
manager: "ghogen"
caps.handback.revision: 10
---
# IDebugDocumentTextEvents2::onReplaceText
[!INCLUDE[vs2017banner](../../../code-quality/includes/vs2017banner.md)]

テキストが文書に置き換えられたデバッグのパッケージに通知します。  
  
## 構文  
  
```cpp#  
HRESULT onReplaceText(   
   TEXT_POSITION pos,  
   DWORD         dwNumToReplace  
);  
```  
  
```c#  
int onReplaceText(   
   enum_TEXT_POSITION pos,  
   uint               dwNumToReplace  
);  
```  
  
#### パラメーター  
 `pos`  
 \[入力\] [TEXT\_POSITION](../../../extensibility/debugger/reference/text-position.md) はテキストの位置に置き換えられたかを示します。  
  
 `dwNumToReplace`  
 \[入力\] 置換テキストの文字数を指定します。  
  
## 戻り値  
 正常に終了した場合戻り `S_OK`; それ以外の場合はエラー コード。  
  
## 参照  
 [IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md)   
 [TEXT\_POSITION](../../../extensibility/debugger/reference/text-position.md)