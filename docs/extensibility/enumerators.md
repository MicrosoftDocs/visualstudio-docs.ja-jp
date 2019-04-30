---
title: 列挙子 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, enumerators
ms.assetid: a60030c5-e1d1-47e1-84bb-cbfe838ab479
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 37f469ecc0ae097592a128b30a6a6f189d58d94b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62863955"
---
# <a name="enumerators"></a>列挙子
このセクションでは、ソース管理プラグインが認識する必要がありますソース コントロールのプラグイン API で列挙子のデータ型を示します。

## <a name="in-this-section"></a>このセクションの内容
- [コマンド コード](../extensibility/command-code-enumerator.md)のオプションを列挙、 [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)と[SccPopulateList](../extensibility/sccpopulatelist-function.md)関数。

- [メッセージ](../extensibility/message-enumerator.md)印刷のコールバックを使用するフラグの列挙[LPTEXTOUTPROC](../extensibility/lptextoutproc.md)します。

- [状態コードをファイル](../extensibility/file-status-code-enumerator.md)という名前のソース管理下にあるファイルの状態を示す定数値が含まれます。

- [ディレクトリの状態コード](../extensibility/directory-status-code-enumerator.md)という名前のソース管理下のディレクトリの状態を示す定数値が含まれます。

## <a name="related-sections"></a>関連項目
- [ソース管理プラグインを作成する](../extensibility/internals/creating-a-source-control-plug-in.md)ソース管理プラグインの SDK を定義し、含まれているリソースを説明します。

- [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)指定されたコマンドの詳細設定オプションのユーザーに求めます。

- [SccPopulateList](../extensibility/sccpopulatelist-function.md)その現在の状態のファイルの一覧を検査します。 また、使用して、`pfnPopulate`ファイルでの条件が一致しない場合に、呼び出し元に通知するため、`nCommand`します。

- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)によって使用されるコールバック関数について説明します[SccOpenProject](../extensibility/sccopenproject-function.md) ide プラグインのソース管理からのメッセージを表示します。

- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)ソース管理プラグイン API のすべての要素の完全な一覧を提供します。