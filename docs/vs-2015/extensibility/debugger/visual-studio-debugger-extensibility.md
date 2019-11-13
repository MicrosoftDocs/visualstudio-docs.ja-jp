---
title: Visual Studio デバッガーの機能拡張 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Visual Studio], Debugging SDK
- Debugging SDK
ms.assetid: c088b6a2-c3ad-446b-830d-9c6f41b2934b
caps.latest.revision: 33
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0b8d37954bf238b2ed1323bf021fded94ec0c584
ms.sourcegitcommit: 3a19319e2599bd193fb2ca32020ca53942974bfd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73983667"
---
# <a name="visual-studio-debugger-extensibility"></a>Visual Studio デバッガーの拡張性
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Visual Studio には、完全にインタラクティブなソースコードデバッガーが含まれており、プログラムのバグを追跡するための強力で使いやすいツールを提供します。 デバッガーでは、、 C#、C/C++、および JavaScript の Visual Basic が完全にサポートされています。 ただし、[!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)]では、 [Microsoft ダウンロードセンター](https://www.microsoft.com/download/details.aspx?id=21835)から入手できますが、他のプログラミング言語は、同じ豊富な機能を備えたデバッガーでサポートされています。  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] デバッガーは、デバッグコンポーネントに共通のフロントエンド (つまりユーザーインターフェイス) であり、デバッグ対象の言語に固有のものです。 新しい言語では、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] デバッガーによってサポートされる必要があるのは、デバッグエンジン (DE) などの必要なバックエンドコンポーネントを作成することだけです。 ここで、[!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] が登場します。  
  
 [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] には、新しい DE を作成するために必要なすべての [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 要素への完全な参照が含まれています。 また、作業を開始するためのサンプルとチュートリアルも用意されています。  
  
 デバッグをサポートする言語プロジェクトシステムのエンドツーエンドのサンプルについては、 [IronPython サンプル](https://msdn.microsoft.com/4c41695c-12c1-4670-b43b-d8d84c9e4089)を参照してください。  
  
 次のセクションでは、[!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)]を使用してデバッガーを拡張する方法について説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [はじめに](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] のデバッグプランと SDK のインストール方法について説明します。  
  
 [カスタム デバッグ エンジンの作成](../../extensibility/debugger/creating-a-custom-debug-engine.md)  
 De をデタッチするためのプログラムの準備から、カスタムの DE プロセスについて説明します。  
  
 [CLR 式エバリュエーターの書き込み](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)  
 式エバリュエーターを記述する必要があるかどうかについて説明します。  
  
 [デバッグ エンジンの実装方法の選択](../../extensibility/debugger/choosing-a-debug-engine-implementation-strategy.md)  
 DE を実装する方法について説明します。  
  
 [参照](../../extensibility/debugger/reference/reference-visual-studio-debugging-apis.md)  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] デバッグ API について説明します。  
  
 [サンプル](../../extensibility/debugger/visual-studio-debugging-samples.md)  
 共通言語ランタイムの式エバリュエーターサンプルとデバッグエンジンサンプルへのリンクが含まれています。
