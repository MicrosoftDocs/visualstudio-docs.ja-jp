---
description: Microsoft デバッグ情報にアクセスするには、DIA SDK を使用します。
title: 概要 (Debug Interface Access SDK) | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- user-defined types
- .dbg files
- modules
- interfaces [DIA SDK]
- DBG files
- procedures [DIA SDK]
- executable files
- COM objects, in DIA SDK
- compilands
- executable images
ms.assetid: 720b4479-a8bc-4fec-860e-80c1a0780405
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c505216cd38b5321f291515794fc07ff58e8d698
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634562"
---
# <a name="overview-debug-interface-access-sdk"></a>概要 (Debug Interface Access SDK)
Microsoft デバッグ情報にアクセスするには、DIA SDK を使用します。 DIA SDK には COM ベースの API セットが用意されています。これを使用すると、Microsoft でデバッグ情報の形式が変更されても、そのたびにコードを書き直す必要がなくなります。 DIA SDK では、[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] バージョン 5.0 以降で生成された .pdb ファイルと .dbg ファイルにある以前のバージョンのデバッグ情報を一部読み取ることもできます。

 特に明記されていない限り、DIA SDK 内のインターフェイスはそれぞれ異なる COM オブジェクトを表します。 追加のインターフェイス (つまり、追加のオブジェクト) は、既存のインターフェイス ポインターで `QueryInterface` を呼び出すのではなく、明示的なクエリ ([IDiaDataSource::openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md) や [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md) など) によって作成されます。

## <a name="see-also"></a>関連項目
- [IDiaDataSource::openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md)
- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)
