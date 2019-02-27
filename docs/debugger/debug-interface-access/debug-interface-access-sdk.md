---
title: Debug Interface Access SDK |Microsoft Docs
ms.date: 07/24/2018
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- debugging [DIA SDK]
- debugger [DIA SDK]
- DIA SDK
ms.assetid: 4c0abe53-11d3-4b7a-bdc7-b054f85aaf40
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 915f594a984af41da167e0fd3d58beb2f6ddd978
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56608085"
---
# <a name="debug-interface-access-sdk"></a>Debug Interface Access SDK

Microsoft デバッグ インターフェイス アクセス ソフトウェア開発キット (DIA SDK) は、Microsoft ポスト コンパイラ ツールによって生成されたプログラム データベース (.pdb) ファイルに格納されている情報のデバッグへのアクセスを提供します。 ポスト コンパイラ ツールによって生成される .pdb ファイルの形式が定数のリビジョンを受けて、ために、形式を公開する実用的ではありません。 DIA API を使用すると、検索し、.pdb ファイルに格納されているデバッグ情報を参照するアプリケーションを開発できます。 このようなアプリケーションはスタック トレース バック情報を報告やパフォーマンス データを分析などのことができます。

## <a name="in-this-section"></a>このセクションの内容

[はじめに](../../debugger/debug-interface-access/getting-started-debug-interface-access-sdk.md)

機能 DIA SDK の概要が示され、および必須のヘッダーとライブラリ ファイル DIA SDK がインストールされているを指定します。

[.Pdb ファイルの照会](../../debugger/debug-interface-access/querying-the-dot-pdb-file.md)

DIA API を使用して、.pdb ファイルを照会する方法について説明します。

[シンボルとシンボル タグ](../../debugger/debug-interface-access/symbols-and-symbol-tags.md)

DIA API でシンボルとシンボル タグの使用方法について説明します。

[参照](../../debugger/debug-interface-access/debug-interface-access-sdk-reference.md)

インターフェイス、メソッド、列挙型、および DIA API の構造が含まれています。

[Dia2dump サンプル](../../debugger/debug-interface-access/dia2dump-sample.md)

DIA API を使用して検索し、デバッグ情報を参照する方法を示しています。
