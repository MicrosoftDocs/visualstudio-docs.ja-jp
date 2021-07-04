---
title: デバッガー コンテキスト | Microsoft Docs
description: Visual Studio のデバッグ エンジンがコード コンテキスト、ドキュメント コンテキストまたは位置、式評価コンテキストなどの個別のコンテキスト内でどのように動作するかについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: 79808036-b680-4e4c-9c61-4ed43aa11323
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5103561a420c3836f60a22790335522a83798966
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903672"
---
# <a name="debugger-contexts"></a>デバッガー コンテキスト
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] でのデバッグでは、デバッグ エンジン (DE) は、次のような複数の異なるコンテキスト内で同時に動作します。

- コード コンテキスト - プログラムの実行ストリーム内の現在の位置を記述します。

- ドキュメント コンテキストまたは位置 - ソース ドキュメント内の現在の位置を記述します。

- 式評価コンテキスト - 式の評価が行われるコンテキストを記述します。

## <a name="in-this-section"></a>このセクションの内容
 [コード コンテキスト](../../extensibility/debugger/code-context.md) - 今日の実行時アーキテクチャでは、プログラムの命令ストリーム内のアドレスとして扱われるコード コンテキストと、コードが命令によってではなく、他の方法で表される非従来型言語を比較します。

 [ドキュメントの位置](../../extensibility/debugger/document-position.md) - IDE で認識されているソース ファイル内の位置を抽象化して、Visual Studio のデバッグでのドキュメントの位置を定義します。

 [ドキュメント コンテキスト](../../extensibility/debugger/document-context.md) - ソース ファイルに関して、ドキュメント コンテキストが Visual Studio のデバッグで何を表すかについて説明します。 また、シンボル ハンドラーによって、コード コンテキストがドキュメント コンテキストにどのようにマップされるかについても説明します。

 [式評価コンテキスト](../../extensibility/debugger/expression-evaluation-context.md) - Visual Studio の式評価コンテキストに関する情報が提供されます。 たとえば、スタック フレームに関連付けられた式評価コンテキストでは、ローカル変数、メソッド パラメーター、クラス メンバーなどを評価するためのコンテキストが提供されます。

## <a name="related-sections"></a>関連項目
 [デバッグの概念に関するページ](../../extensibility/debugger/debugger-concepts.md) 主要なデバッグ アーキテクチャの概念について説明します。

 [デバッグのコンポーネント関するページ](../../extensibility/debugger/debugger-components.md) デバッグ エンジン (DE)、式エバリュエーター (EE)、シンボル ハンドラー (SH) などの Visual Studio デバッグ コンポーネントの概要を示します。

 [タスクをデバッグする](../../extensibility/debugger/debugging-tasks.md) プログラムの起動や式の評価といった、さまざまなデバッグ タスクへのリンクが含まれています。
