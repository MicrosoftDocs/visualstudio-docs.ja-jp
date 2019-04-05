---
title: ブレークポイント (Visual Studio SDK) |Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- breakpoints
ms.assetid: acfcabed-9f2f-436c-ad18-7ca2f45d631b
caps.latest.revision: 11
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 4223f694c55025c0fc3e4d0afe8fca530940520b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2018
ms.locfileid: "51764746"
---
# <a name="breakpoints-visual-studio-sdk"></a>ブレークポイント (Visual Studio SDK)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ブレークポイントの 3 種類があります。 保留中、バインド、およびエラー。  
  
 **保留中のブレークポイント A:**  
  
- 1 つまたは複数のプログラム内の 1 つまたは複数のコード コンテキストにブレークポイントをバインドするために必要なすべての情報を格納する抽象化。 毎回、原因を読み込むコードをデバッグ対象のプログラム デバッグ エンジンを確認します保留中のすべてのブレークポイントをバインドできるかどうかを参照してください。  
  
   自体保留中のブレークポイントことはありませんコードにバインドしますではなく収集し、言いますを生成するすべてのバインドされたブレークポイントを含みます。  
  
- によって表される、 [IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)インターフェイス。  
  
  **バインドされたブレークポイント。**  
  
- ブレークポイントの抽象化に関連付けられているか 1 つのコード コンテキストに制限されます。 バインドされた各ブレークポイントは保留中のブレークポイントへの応答で生成されます。 ただし、保留中のブレークポイントは、複数のバインドされたブレークポイントが生成ことができます。  
  
   コードが読み込まれると、バインドされたブレークポイントはバインドされていないし、破棄されます。  
  
- によって表される、 [IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md)インターフェイス。  
  
  **エラー ブレークポイントの場合:**  
  
- コードのコンテキストに保留中のブレークポイントをバインドするときにエラーを説明するための抽象型です。 エラー、ブレークポイントでは、またはブレークポイント式自体の場所で、いずれかのエラーについて説明します。 詳細については、[ブレークポイントのバインド](../../extensibility/debugger/binding-breakpoints.md)を参照してください。  
  
   ブレークポイントのエラーは、エラーまたは警告のいずれかにできます。  
  
- によって表される、 [IDebugErrorBreakpoint2](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)インターフェイス。  
  
## <a name="see-also"></a>関連項目  
 [プログラム](../../extensibility/debugger/programs.md)   
 [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)   
 [コード コンテキスト](../../extensibility/debugger/code-context.md)   
 [IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md)   
 [IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)   
 [IDebugErrorBreakpoint2](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)

