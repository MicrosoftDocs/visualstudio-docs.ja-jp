---
title: ブレークポイント (Visual Studio SDK) | Microsoft Docs
description: 保留中、バインド、エラーの 3 種類のブレークポイントについて説明します。 この記事では、型を実装するために使用されるインターフェイスの一覧を示します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- breakpoints
ms.assetid: acfcabed-9f2f-436c-ad18-7ca2f45d631b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b834d9b80d8abca12ea9230d3b451fb4e251859e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055207"
---
# <a name="breakpoints-visual-studio-sdk"></a>ブレークポイント (Visual Studio SDK)
ブレークポイントには、保留中、バインド、エラーの 3 種類があります。

 **保留中のブレークポイント:**

- 1 つ以上のプログラムの 1 つ以上のコード コンテキストにブレークポイントをバインドするために必要なすべての情報を含む抽象化です。 デバッグ エンジンでは、デバッグ中のプログラムによってコードが読み込まれるたびに、すべての保留中のブレークポイントをチェックし、バインドできるかどうかを確認します。

   保留中のブレークポイント自体は、コードにバインドされるのではなく、それによって生成されるすべてのバインドされたブレークポイントを収集します (含むとも言います)。

- [IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) インターフェイスによって表されます。

  **バインドされたブレークポイント:**

- 単一のコード コンテキストに関連付けられた (バインドされた) ブレークポイントの抽象化です。 個々のバインドされたブレークポイントは、保留中のブレークポイントに応答して生成されます。 ただし、保留中のブレークポイントによって複数のバインドされたブレークポイントが生成されることがあります。

   コードがアンロードされたときに、バインドされたブレークポイントをバインド解除して破棄できます。

- [IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md) インターフェイスによって表されます。

  **エラー ブレークポイント:**

- 保留中のブレークポイントをコード コンテキストにバインドしようとしたときのエラーを記述するための抽象化です。 エラー ブレークポイントでは、位置とブレークポイント式自体のいずれかのエラーが記述されます。 詳細については、「[ブレークポイントのバインド](../../extensibility/debugger/binding-breakpoints.md)」を参照してください。

   ブレークポイント エラーは、エラーと警告のいずれかです。

- [IDebugErrorBreakpoint2](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md) インターフェイスによって表されます。

## <a name="see-also"></a>関連項目
- [Programs](../../extensibility/debugger/programs.md)
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [コード コンテキスト](../../extensibility/debugger/code-context.md)
- [IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md)
- [IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [IDebugErrorBreakpoint2](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)
