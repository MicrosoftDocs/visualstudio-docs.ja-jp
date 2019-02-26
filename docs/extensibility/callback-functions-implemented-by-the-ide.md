---
title: IDE によって実装されるコールバック関数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, callback functions
- callback functions, source control plug-ins
ms.assetid: 4a8833f0-6ac0-4ea7-9400-8275aa991468
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fc3b4423b54975c773de743b093f882f1fd9c42c
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56697560"
---
# <a name="callback-functions-implemented-by-the-ide"></a>IDE によって実装されるコールバック関数
統合することとして可能な限りと統合されたエクスペリエンスを提供するシームレスな統合開発環境 (IDE) ソース管理プラグイン使用できます、IDE によって実装されるコールバック関数。 プラグインできるこれらの関数、IDE に情報を渡すのソース管理操作中に適切なタイミングでIDE は、ネイティブ UI に埋め込まれた要素としてこの情報を表示できます。 ユーザーは、場合、プラグインの使用、独自の UI よりもこのシナリオで断片化の経験を持ちます。

 必要なヘッダー ファイルは*scc.h*します。 既定の場所は *\Program Files\VSIP 8.0\EnvSDK\common\inc\\* します。 ソース管理プラグイン サンプルの VSIP フォルダーにも *\Program Files\VSIP 8.0\MSSCCI\\* します。

## <a name="in-this-section"></a>このセクションの内容
- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)によって使用されるコールバック関数について説明します[SccOpenProject](../extensibility/sccopenproject-function.md) ide プラグインのソース管理からのメッセージを表示します。

- [POPLISTFUNC](../extensibility/poplistfunc.md)によって使用されるコールバック関数について説明します[SccPopulateList](../extensibility/sccpopulatelist-function.md) IDE でソース管理プラグインの完全な一覧でのみ使用可能な情報への完全なアクセスがない場合バージョン管理下にあるファイル。

- [QUERYCHANGESFUNC](../extensibility/querychangesfunc.md)によって使用されるコールバック関数について説明します、 [SccQueryChanges](../extensibility/sccquerychanges-function.md)操作。

- [POPDIRLISTFUNC](../extensibility/popdirlistfunc.md)によって使用されるコールバック関数について説明します、 [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)操作。

- [OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md)コールバック関数を呼び出して設定について説明します、 [SccSetOption](../extensibility/sccsetoption-function.md)ソース管理プラグイン名の変更がバックアップには、IDE と通信するようにします。

## <a name="related-sections"></a>関連項目
- [SccOpenProject](../extensibility/sccopenproject-function.md)プロジェクトを開きます。

- [SccPopulateList](../extensibility/sccpopulatelist-function.md)その現在の状態のファイルの一覧を検査します。 また、使用して、`pfnPopulate`ファイルでの条件が一致しない場合に、呼び出し元に通知するため、`nCommand`します。

- [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)ディレクトリおよびファイルをプロジェクトまたはソース管理下にあるプロジェクトの一覧を検査します。 各ディレクトリとファイル名が見つかりましたが、コールバック関数に渡されます。

- [SccQueryChanges](../extensibility/sccquerychanges-function.md)ファイルの一覧に加えられた名前の変更を調べます。 各ファイル名は、その状態の変更とコールバック関数に渡されます。

- [SccSetOption](../extensibility/sccsetoption-function.md)さまざまなオプションを設定します。 各オプションが始まる`SCC_OPT_xxx`あり、独自の値の定義済みセット。

- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)ソース管理プラグインの SDK のリファレンス セクションの内容について説明します。