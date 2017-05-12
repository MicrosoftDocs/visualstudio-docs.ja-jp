---
title: "IDebugDocumentText::GetDocumentAttributes | Microsoft Docs"
ms.custom: ""
ms.date: "01/18/2017"
ms.prod: "windows-script-interfaces"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
apiname: IDebugDocumentText.GetDocumentAttributes
apilocation: pdm.dll
helpviewer_keywords: 
  - "IDebugDocumentText::GetDocumentAttributes"
ms.assetid: 8c544ca1-8db4-4bca-973e-09315d9a0ee5
caps.latest.revision: 8
author: "mikejo5000"
ms.author: "mikejo"
manager: "ghogen"
caps.handback.revision: 8
---
# IDebugDocumentText::GetDocumentAttributes
ドキュメントの属性を返します。  
  
## 構文  
  
```  
HRESULT GetDocumentAttributes(  
   TEXT_DOC_ATTR*  ptextdocattr  
);  
```  
  
#### パラメーター  
 `ptextdocattr`  
 \[入力\]ドキュメントのテキスト属性。  
  
## 戻り値  
 このメソッドは `HRESULT` を返します。  指定できる値は、に含まれていますが、次の表に、これらはありません。  
  
|値|説明|  
|-------|--------|  
|`S_OK`|メソッドが成功しました。|  
  
## 解説  
 このメソッドは、文書の属性を返します。  
  
## 参照  
 [IDebugDocumentText インターフェイス](../../winscript/reference/idebugdocumenttext-interface.md)   
 [TEXT\_DOC\_ATTR 定数](../../winscript/reference/text-doc-attr-constants.md)