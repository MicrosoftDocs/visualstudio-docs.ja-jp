---
title: ドキュメントの位置 | Microsoft Docs
description: Visual Studio デバッグでのドキュメントの位置により、IDE で認識されるソース ファイル内の位置を抽象化する方法を説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: b59d739c-7572-427f-a70d-4e5df63d02c1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5d14f9619059735aaecabf72adef248c69ed247e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097254"
---
# <a name="document-position"></a>ドキュメントの位置
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のデバッグにおける "*ドキュメントの位置*":

- IDE で認識されるソース ファイル内の位置を抽象化します。 現在、ほとんどの言語では、ドキュメントの位置をソース ファイル内の位置と見なすことができます。

- デバッグ エンジンに対するソース ドキュメント内の位置を記述します。

- [IDebugDocumentPosition2](../../extensibility/debugger/reference/idebugdocumentposition2.md) インターフェイスによって実装されます。

## <a name="see-also"></a>関連項目
- [コード コンテキスト](../../extensibility/debugger/code-context.md)
- [ドキュメント コンテキスト](../../extensibility/debugger/document-context.md)
- [シンボル プロバイダー](../../extensibility/debugger/symbol-provider.md)
- [シンボル プロバイダー インターフェイス](../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [デバッガー コンテキスト](../../extensibility/debugger/debugger-contexts.md)
