---
title: ドキュメント コンテキスト | Microsoft Docs
description: Visual Studio のデバッグにおけるドキュメント コンテキストについて説明します。これは、コード コンテキストのソース ファイル内の位置またはソース ドキュメント内の位置を表します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: 8e8b5702-5c16-4988-953d-69dd807d8b84
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 34c69e11c57574c07a8ecb40480842834a8ee53f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097241"
---
# <a name="document-context"></a>ドキュメント コンテキスト
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のデバッグにおける *ドキュメント コンテキスト* は:

- ソース ファイル内の位置を表します。 ソース ファイルが存在しない可能性がある言語の場合、ドキュメント コンテキストによって、通常、実行時環境によって生成されるドキュメント内の位置を識別します。 たとえば、スクリプト エンジンによって、スクリプトからドキュメントが生成される場合があります。 詳細については、「[ドキュメントの位置](../../extensibility/debugger/document-position.md)」を参照してください。

- コード コンテキストに対応するソース ドキュメント内の位置を記述します。 シンボル ハンドラーによって、コンパイラまたはインタープリターによって生成された情報を使用して、コード コンテキストがドキュメント コンテキストにマップされます。

- [IDebugDocumentContext2](../../extensibility/debugger/reference/idebugdocumentcontext2.md) インターフェイスによって実装されます。

## <a name="see-also"></a>関連項目
- [コード コンテキスト](../../extensibility/debugger/code-context.md)
- [シンボル プロバイダー](../../extensibility/debugger/symbol-provider.md)
- [シンボル プロバイダーのインターフェイス](../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [デバッガー コンテキスト](../../extensibility/debugger/debugger-contexts.md)
