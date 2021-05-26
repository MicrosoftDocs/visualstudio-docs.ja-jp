---
title: サポートされている Roslyn パッケージのバージョン マッピング
description: この記事では、さまざまなバージョンの Visual Studio でサポートされている .NET コンパイラ プラットフォーム (Roslyn) パッケージのバージョンについて説明します。
ms.custom: SEO-VS-2020
ms.date: 04/29/2019
ms.topic: reference
helpviewer_keywords:
- roslyn package versions
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8fd9e62de70dd5bff81b5fdaee05822c7171981e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060511"
---
# <a name="net-compiler-platform-package-version-reference"></a>.NET コンパイラ プラットフォーム パッケージ バージョン リファレンス

次の表では、さまざまなバージョンの Visual Studio でサポートされている [.NET コンパイラ プラットフォーム (Roslyn) パッケージ](https://www.nuget.org/packages/Microsoft.Net.Compilers/)のバージョンについて説明します。

たとえば、カスタム アナライザーが Visual Studio 2017 のすべてのバージョンで動作するようにするには、バージョン 2.0 の Microsoft.Net.Compilers をターゲットにする必要があります。

| Roslyn パッケージ バージョン | サポートされている Visual Studio の最小バージョン |
| - | - |
| 3.x | Visual Studio 2019 |
| 2.10.0 | Visual Studio 2017 バージョン 15.9 |
| 2.9.0 | Visual Studio 2017 バージョン 15.8 |
| 2.8.2 | Visual Studio 2017 バージョン 15.7 |
| 2.7.0 | Visual Studio 2017 バージョン 15.6 |
| 2.6.1 | Visual Studio 2017 バージョン 15.5 |
| 2.4.0 | Visual Studio 2017 バージョン 15.4 |
| 2.3.2 | Visual Studio 2017 バージョン 15.3 |
| 2.2.0 | Visual Studio 2017 バージョン 15.2 |
| 2.1.0 | Visual Studio 2017 バージョン 15.1 |
| 2.0.0 | Visual Studio 2017 RTM |
| 1.3.2 | Visual Studio 2015 更新プログラム 3 |
| 1.2.2 | Visual Studio 2015 更新プログラム 2 |
| 1.1.1 | Visual Studio 2015 更新プログラム 1 |
| 1.0.1 | Visual Studio 2015 RTM |

> [!TIP]
> サポートされている Visual Studio の最小バージョンが Visual Studio 2017 バージョンである Roslyn パッケージの場合、後から公開されているため Visual Studio 2019 のすべてのバージョンはすべてサポートされています。

## <a name="see-also"></a>関連項目

- [.NET Compiler Platform SDK](/dotnet/csharp/roslyn-sdk/)
- [Roslyn アナライザーの概要](getting-started-with-roslyn-analyzers.md)
