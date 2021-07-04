---
title: ドキュメントの位置 | Microsoft Docs
description: Visual Studio デバッグでのドキュメントの位置により、IDE で認識されるソース ファイル内の位置を抽象化する方法を説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: b59d739c-7572-427f-a70d-4e5df63d02c1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 58a3ac3db62619c5d0eaa9e89e09d7d5def06ff1
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898163"
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
