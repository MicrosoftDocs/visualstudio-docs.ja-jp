---
title: コード コンテキスト |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: 65e4d37a-086b-426e-9394-a3534967fd59
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d59a4c79cb21386fa6f6e7031404aeb0b435b3b9
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60088185"
---
# <a name="code-context"></a>コード コンテキスト
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 、デバッグ、**コード コンテキスト**:  
  
- デバッグ エンジン (DE) に既知としては、コード内の位置の抽象化を提供します。 ほとんどのランタイム アーキテクチャの今日では、コードのコンテキストできます見なすことがプログラムの命令ストリーム内のアドレス。 従来とは異なる言語では、コードは、命令表現いない可能性があります、その他のいくつかの方法でコードのコンテキストを表すことができます。  
  
- デバッグ中のプログラムの実行のストリームの現在の位置をについて説明します。  
  
- ブレークポイントにプログラムが停止時にのみ存在します。  
  
- 関連付けられているドキュメント コンテキストがあります。  
  
- によって実装される、 [IDebugCodeContext2](../../extensibility/debugger/reference/idebugcodecontext2.md)インターフェイス。  
  
## <a name="see-also"></a>関連項目  
 [ドキュメントのコンテキスト](../../extensibility/debugger/document-context.md)   
 [デバッガー コンテキスト](../../extensibility/debugger/debugger-contexts.md)
