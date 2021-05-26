---
title: .NET コンパイラ プラットフォーム (&quot;Roslyn&quot;) の拡張機能 | Microsoft Docs
description: ツールや開発者が、プログラムに関してコンパイラで保持されている豊富な情報を共有できるようにする、.NET コンパイラ プラットフォームについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 564201b3-1e18-4b88-b615-42c2f57f3fe8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: af9be2c4a57763b4521f3564e95c760e5bdd566d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091163"
---
# <a name="net-compiler-platform-quotroslynquot-extensibility"></a>.NET コンパイラ プラットフォーム (&quot;Roslyn&quot;) の拡張機能
.NET コンパイラ プラットフォーム ("Roslyn") の中核となる任務は、C# および Visual Basic コンパイラを開き、プログラムに関してコンパイラで保持されている豊富な情報をツールや開発者が共有できるようにすることです。 コード分析ツールではコードの品質を向上させ、コード ジェネレーターはアプリケーションの構築に役立ちます。 ツールがスマートになったので、ツールでは、コンパイラのみで保持されているコードの深い知識にアクセスする必要性が高まっています。 Roslyn コンパイラでは、(ソース コード入力とオブジェクト コード出力の) あいまいな変換の代わりに、自分のツールとアプリケーション内でコードに関連するタスクに使用できる API が提供されます。

 これの一番いいところは、Roslyn コンパイラ、API、サンプル、チュートリアル、これらの API の上に構築された実際のツールはすべて、[github.com/dotnet/roslyn](https://github.com/dotnet/Roslyn) では完全にオープン ソースである点です。 詳細を確認して、Roslyn の使用を開始するには、OSS サイトにアクセスしてください。 エンド ユーザーとして使用できる最新の C# および Visual Basic の機能を入手するためのリンクと、Roslyn API を活用したツール ビルダーとして開始するためのリンクが記載されています。

## <a name="see-also"></a>関連項目
- [Roslyn アナライザーの概要](../extensibility/getting-started-with-roslyn-analyzers.md)
