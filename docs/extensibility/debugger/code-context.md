---
title: コード コンテキスト | Microsoft Docs
description: Visual Studio のデバッグにおけるコード コンテキストについて説明します。これにより、プログラムがブレークポイントで停止したときに存在するコード内の位置が記述されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: 65e4d37a-086b-426e-9394-a3534967fd59
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3e3bd252990e52f4ecaede0cc5026067b28434bc
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905723"
---
# <a name="code-context"></a>コード コンテキスト
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のデバッグにおける **コード コンテキスト**:

- デバッグ エンジン (DE) で認識されているコード内の位置を抽象化します。 現在のほとんどのランタイム アーキテクチャでは、コード コンテキストはプログラムの命令ストリームのアドレスと考えることができます。 コードを命令で表すことができない非従来型言語の場合は、他の方法でコード コンテキストを表すことができます。

- デバッグ中のプログラムの実行ストリームにおける現在の位置を記述します。

- プログラムがブレークポイントで停止したときにのみ存在します。

- ドキュメント コンテキストが関連付けられています。

- [IDebugCodeContext2](../../extensibility/debugger/reference/idebugcodecontext2.md) インターフェイスによって実装されます。

## <a name="see-also"></a>関連項目
- [ドキュメント コンテキスト](../../extensibility/debugger/document-context.md)
- [デバッガー コンテキスト](../../extensibility/debugger/debugger-contexts.md)
