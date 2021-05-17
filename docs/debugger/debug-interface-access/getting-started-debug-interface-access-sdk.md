---
description: Debug Interface Access (DIA) SDK には、説明ドキュメントと、DIA API の使用方法を示すサンプルが用意されています。
title: はじめに (Debug Interface Access SDK) | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- .dbg files
- DBG files
ms.assetid: cb3d040a-2846-40d7-bdbc-8a5beb5dd2f6
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 82c206a823b39eda744fcd6be8a1085f6c6a0c45
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634539"
---
# <a name="getting-started-debug-interface-access-sdk"></a>はじめに (Debug Interface Access SDK)
Debug Interface Access (DIA) SDK には、説明ドキュメントと、DIA API の使用方法を示すサンプルが用意されています。 DIA SDK のインターフェイスとメソッドを使用すると、.pdb ファイルと .dbg ファイルを開いてその内容からシンボル、値、属性、アドレス、その他のデバッグ情報を検索するカスタム アプリケーションを開発できます。 この SDK では、C++ アプリケーションで見つかったシンボルに関連付けられたプロパティの参照テーブルも提供されます。

 DIA SDK の最適な使用のためには、次のことに精通している必要があります。

- C++ プログラミング言語

- COM プログラミング

- サンプルをコンパイルするための Visual Studio 統合開発環境 (IDE)

  DIA SDK は通常、Visual Studio と共にインストールされ、その既定の場所は *[ドライブ]* \Program Files\Microsoft Visual Studio 9.0\DIA SDK です。 インストールの一部として、DIA SDK を実装する msdia90.dll が自動的に登録されるため、プログラムに `dia2.h` を追加し、`diaguids.lib` にリンクするだけで使用できます。

  ヘッダー: include\dia2.h

  ライブラリ: lib\diaguids.lib

  DLL: bin\msdia80.dll

  IDL: idl\dia2.idl

## <a name="in-this-section"></a>このセクションの内容

[概要](../../debugger/debug-interface-access/overview-debug-interface-access-sdk.md)

DIA の基本的なアーキテクチャを確認します。

[.Pdb ファイルの照会](../../debugger/debug-interface-access/querying-the-dot-pdb-file.md)

DIA API を使用して .pdb ファイルを照会する方法について詳しく説明します。

## <a name="see-also"></a>関連項目

- [Debug Interface Access SDK](../../debugger/debug-interface-access/debug-interface-access-sdk.md)
