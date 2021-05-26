---
title: 従来の言語サービスのコマンドのインターセプト | Microsoft Docs
description: Visual Studio でコマンド フィルターを使用して、従来の言語サービスのコマンドをインターセプトし、言語固有の動作を追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, intercepting language service
- language services, intercepting commands
ms.assetid: eea69f03-349c-44bb-bd4f-4925c0dc3e55
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8d7af9ff4a8f04382cff4999b8c57549f3da3db7
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074679"
---
# <a name="intercepting-legacy-language-service-commands"></a>従来の言語サービスのコマンドの受信
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、テキスト ビューで処理されるような言語サービスのインターセプト コマンドを使用できます。 これは、テキスト ビューでは管理されない言語固有の動作の場合に便利です。 これらのコマンドは、言語サービスからテキスト ビューに 1 つ以上のコマンド フィルターを追加することでインターセプトできます。

## <a name="getting-and-routing-the-command"></a>コマンドの取得とルーティング
 コマンド フィルターは、特定の文字シーケンスまたはキー コマンドを監視する <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> オブジェクトです。 複数のコマンド フィルターを 1 つのテキスト ビューに関連付けることができます。 各テキスト ビューでは、コマンド フィルターのチェーンが保持されます。 新しいコマンド フィルターを作成したら、適切なテキスト ビューのチェーンにフィルターを追加します。

 コマンド フィルターをチェーンに追加するには、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> で <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> メソッドを呼び出します。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> を呼び出すと、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] は、コマンド フィルターで処理されないコマンドを渡すことができる別のコマンド フィルターを返します。

 コマンド処理には、次のオプションがあります。

- コマンドを処理してから、チェーン内の次のコマンド フィルターにコマンドを渡します。

- コマンドを処理し、次のコマンド フィルターにコマンドを渡しません。

- コマンドを処理しませんが、コマンドを次のコマンド フィルターに渡します。

- コマンドを無視します。 現在のフィルターでは処理せず、次のフィルターに渡しません。

  言語サービスで処理する必要があるコマンドの詳細については、[言語サービスのフィルターの重要なコマンド](../../extensibility/internals/important-commands-for-language-service-filters.md)に関するページを参照してください。
