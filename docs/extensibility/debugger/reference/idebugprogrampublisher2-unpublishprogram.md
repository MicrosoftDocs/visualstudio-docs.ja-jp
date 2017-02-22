---
title: "IDebugProgramPublisher2::UnpublishProgram | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "vs-ide-sdk"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "IDebugProgramPublisher2::UnpublishProgram"
helpviewer_keywords: 
  - "IDebugProgramPublisher2::UnpublishProgram"
ms.assetid: 627e7d38-b2ac-4873-9a40-37ff7f47cd1d
caps.latest.revision: 9
caps.handback.revision: 9
ms.author: "gregvanl"
manager: "ghogen"
---
# IDebugProgramPublisher2::UnpublishProgram
[!INCLUDE[vs2017banner](../../../code-quality/includes/vs2017banner.md)]

デバッグするプログラムの利用不可になります。  
  
## 構文  
  
```cpp  
HRESULT UnpublishProgram(  
   IUnknown* pDebuggeeInterface  
);  
```  
  
```c#  
int UnpublishProgram(  
   object pDebuggeeInterface  
);  
```  
  
#### パラメーター  
 `pDebuggeeInterface`  
 \[入力\] プログラムに `IUnknown` のインターフェイス。  これは [PublishProgram](../Topic/IDebugProgramPublisher2::PublishProgram.md) のメソッドに指定された値と同じで削除するプログラムを識別します \(つまりクッキーとして使用されます\)。  
  
## 戻り値  
 正常に終了した場合戻り `S_OK`; それ以外の場合はエラー コード。  
  
## 解説  
 デバッグ エンジンとセッションにプログラムで使用できるようにするにはマネージャーを使用して [PublishProgram](../Topic/IDebugProgramPublisher2::PublishProgram.md) のメソッドをデバッグします。  
  
## 参照  
 [IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)   
 [PublishProgram](../Topic/IDebugProgramPublisher2::PublishProgram.md)