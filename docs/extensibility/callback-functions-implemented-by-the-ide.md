---
title: IDE によって実装されたコールバック関数 | Microsoft Docs
description: プラグインが、IDE に情報を渡すためにソース管理操作中の適切なタイミングで呼び出すことができるコールバック関数について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, callback functions
- callback functions, source control plug-ins
ms.assetid: 4a8833f0-6ac0-4ea7-9400-8275aa991468
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7e2e361551fbe03b7f0ef41b19c5d4136aa50472
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105068103"
---
# <a name="callback-functions-implemented-by-the-ide"></a>IDE によって実装されたコールバック関数
統合開発環境 (IDE) との統合をできるだけシームレスに確立し、統合されたエンドユーザー エクスペリエンスを提供するために、ソース管理プラグインでは、IDE によって実装されたコールバック関数を使用できます。 プラグインでは、IDE に情報を渡すためにソース管理操作中の適切なタイミングでこれらの関数を呼び出すことができます。それにより、IDE では、これらの情報をそのネイティブ UI に埋め込み要素として表示できます。 このシナリオでは、プラグインが独自の UI を使用している場合に比べて、ユーザー エクスペリエンスが断片化されることは少なくなります。

 必要なヘッダー ファイルは *scc.h* です。 その既定の場所は *\Program Files\VSIP 8.0\EnvSDK\common\inc\\* です。 また、 *\Program Files\VSIP 8.0\MSSCCI\\* 内のソース管理プラグインのサンプルが含まれている VSIP フォルダーにも存在します。

## <a name="in-this-section"></a>このセクションの内容
- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md) IDE 経由でソース管理プラグインからのメッセージを表示するために [SccOpenProject](../extensibility/sccopenproject-function.md) によって使用されるコールバック関数について説明します。

- [POPLISTFUNC](../extensibility/poplistfunc.md) IDE にソース管理プラグインでしか使用できない情報 (バージョン管理下にあるファイルの完全な一覧など) への完全なアクセス権がない場合に [SccPopulateList](../extensibility/sccpopulatelist-function.md) によって使用されるコールバック関数について説明します。

- [QUERYCHANGESFUNC](../extensibility/querychangesfunc.md) [SccQueryChanges](../extensibility/sccquerychanges-function.md) 操作で使用されるコールバック関数について説明します。

- [POPDIRLISTFUNC](../extensibility/popdirlistfunc.md) [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md) 操作で使用されるコールバック関数について説明します。

- [OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md) ソース管理プラグインで名前の変更を IDE に戻すことができるようにする [SccSetOption](../extensibility/sccsetoption-function.md) の呼び出しによって設定されるコールバック関数について説明します。

## <a name="related-sections"></a>関連項目
- [SccOpenProject](../extensibility/sccopenproject-function.md) プロジェクトを開きます。

- [SccPopulateList](../extensibility/sccpopulatelist-function.md) ファイルの一覧でそれらの現在の状態を調べます。 さらに、ファイルが `nCommand` の条件に一致しない場合は、`pfnPopulate` 関数を使用して呼び出し元に通知します。

- [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md) ソース管理下にある 1 つまたは複数のプロジェクト内のディレクトリとファイルの一覧を調べます。 見つかった各ディレクトリおよびファイル名は、コールバック関数に渡されます。

- [SccQueryChanges](../extensibility/sccquerychanges-function.md) ファイルの一覧に対して行われた名前の変更を調べます。 各ファイル名は、その変更の状態と共にコールバック関数に渡されます。

- [SccSetOption](../extensibility/sccsetoption-function.md) さまざまなオプションを設定します。 各オプションは `SCC_OPT_xxx` で始まり、独自の定義された一連の値が含まれています。

- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md) ソース管理プラグイン SDK の参照セクションの内容について説明します。
