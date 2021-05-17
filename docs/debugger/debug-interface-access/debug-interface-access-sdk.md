---
description: Microsoft Debug Interface Access ソフトウェア開発キット (DIA SDK) は、Microsoft ポストコンパイラ ツールで生成されたプログラム データベース (.pdb) ファイルに保存されているデバッグ情報へのアクセスを提供します。
title: Debug Interface Access SDK | Microsoft Docs
ms.date: 07/24/2018
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- debugging [DIA SDK]
- debugger [DIA SDK]
- DIA SDK
ms.assetid: 4c0abe53-11d3-4b7a-bdc7-b054f85aaf40
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: fbb7c9025094249715f1d69a8d58d8725d294107
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634532"
---
# <a name="debug-interface-access-sdk"></a>Debug Interface Access SDK

Microsoft Debug Interface Access ソフトウェア開発キット (DIA SDK) は、Microsoft ポストコンパイラ ツールで生成されたプログラム データベース (.pdb) ファイルに保存されているデバッグ情報へのアクセスを提供します。 ポストコンパイラ ツールによって生成される .pdb ファイルの形式は常に改訂されているため、形式を公開することは実用的ではありません。 DIA API を使用すると、.pdb ファイルに格納されているデバッグ情報を検索および参照するアプリケーションを開発できます。 このようなアプリケーションでは、スタックのトレースバック情報の報告や、パフォーマンス データの分析などを行うことができます。

## <a name="in-this-section"></a>このセクションの内容

[はじめに](../../debugger/debug-interface-access/getting-started-debug-interface-access-sdk.md)

DIA SDK 機能の概要について説明し、DIA SDK がインストールされる場所、および必要なヘッダー ファイルとライブラリ ファイルを示します。

[.Pdb ファイルの照会](../../debugger/debug-interface-access/querying-the-dot-pdb-file.md)

DIA API を使用して .pdb ファイルを照会する方法について説明します。

[シンボルとシンボル タグ](../../debugger/debug-interface-access/symbols-and-symbol-tags.md)

DIA API でのシンボルおよびシンボル タグの使用方法について説明します。

[参照](../../debugger/debug-interface-access/debug-interface-access-sdk-reference.md)

DIA API のインターフェイス、メソッド、列挙型、および構造体が含まれています。

[Dia2dump サンプル](../../debugger/debug-interface-access/dia2dump-sample.md)

DIA API を使用してデバッグ情報を検索および参照する方法について説明します。
