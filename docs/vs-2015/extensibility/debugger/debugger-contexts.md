---
title: デバッガー コンテキスト |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: 79808036-b680-4e4c-9c61-4ed43aa11323
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 771a3cd8ae25173f3033b3a3229e516570f5dedc
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60116239"
---
# <a name="debugger-contexts"></a>デバッガー コンテキスト
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]デバッグ、デバッグ エンジン (DE) の動作を同時にいくつかの異なるコンテキスト内で。  
  
- コード コンテキスト、プログラムの実行のストリームの現在の場所について説明します。  
  
- ドキュメントのコンテキストまたは位置で、ソース ドキュメント内の現在位置をについて説明します。  
  
- 式の評価は行わコンテキストを記述する式の評価のコンテキスト。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [コード コンテキスト](../../extensibility/debugger/code-context.md)  
 場所コードは表現できない手順については、他の手段で、従来とは異なる言語ではなく現在の実行時のアーキテクチャでプログラムの命令ストリーム内のアドレスとして、コードのコンテキストについて説明します。  
  
 [ドキュメントの位置](../../extensibility/debugger/document-position.md)  
 Visual Studio の IDE に既知のソース ファイル内の位置の抽象化を使用してデバッグ ドキュメントの位置を定義します。  
  
 [ドキュメントのコンテキスト](../../extensibility/debugger/document-context.md)  
 説明で、Visual Studio のデバッグ ソース ファイルに関連ドキュメント コンテキストを表します。 また、シンボル ハンドラーがドキュメントのコンテキストにコードのコンテキストをマップする方法について説明します。  
  
 [式の評価のコンテキスト](../../extensibility/debugger/expression-evaluation-context.md)  
 Visual Studio で使用する式の評価コンテキストについてを説明します。 たとえば、スタック フレームに関連付けられている式の評価のコンテキストでは、ローカル変数、メソッド パラメーター、およびクラス メンバーを評価するため、コンテキストを提供します。  
  
## <a name="related-sections"></a>関連項目  
 [デバッグの概念](../../extensibility/debugger/debugger-concepts.md)  
 デバッグ アーキテクチャの主要な概念をについて説明します。  
  
 [コンポーネントのデバッグ](../../extensibility/debugger/debugger-components.md)  
 デバッグ エンジン (DE)、式エバリュエーター (EE) およびシンボル ハンドラー (SH) を含む Visual Studio のデバッグ コンポーネントの概要を示します。  
  
 [タスクのデバッグ](../../extensibility/debugger/debugging-tasks.md)  
 プログラムを起動して、式の評価などのさまざまなデバッグ タスクへのリンクが含まれています。
