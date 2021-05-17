---
title: 複数のプロジェクト接続全体への設定の適用
description: ソース管理プラグインを使用してバッチ操作を実行することで、複数のプロジェクト接続全体に設定を適用する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, application of settings
ms.assetid: 2116d3d0-c46c-4d0a-b482-08a178584f46
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 71b4a3de89653ab63f57171bcb52ee32ddfcf07d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105078995"
---
# <a name="application-of-settings-across-multiple-project-connections"></a>複数のプロジェクト接続全体への設定の適用
ソース管理プラグイン API バージョン 1.2 を使用して構築されたソース管理プラグインでは、バッチ操作を使用して、複数のプロジェクトまたは複数の接続コンテキストの全体に同じソース管理操作を実行できます。 バッチを使用すると、ユーザー エクスペリエンスから、プロジェクトごとの冗長なダイアログ ボックスを削除できます。

 ソース管理プラグイン API バージョン 1.1 を使用して構築されたソース管理プラグインで複数の接続に属する複数の項目 (別々のファイル共有コンピューター上にある 2 つの Web プロジェクトなど) をユーザーが選択してチェックアウトする場合、ユーザーに同じダイアログ ボックスが繰り返し表示されます。 このシナリオは、ユーザーがダイアログ ボックスの **[すべてに適用]** チェック ボックスをクリックした場合にも発生します。これは、IDE によって各接続コンテキストの状態がリセットされるためです。

## <a name="new-capability-flag"></a>新しい機能フラグ
 `SccBeginBatch` 関数により、バッチ操作が進行中であることを示す `SCC_CAP_BATCH` フラグが設定されます。

## <a name="new-functions"></a>新しい関数
次の新しい関数では、バッチ操作をサポートしています。

- [SccBeginBatch](../../extensibility/sccbeginbatch-function.md)

- [SccEndBatch](../../extensibility/sccendbatch-function.md)

`SCCBeginBatch` 関数によって、ソース管理操作のグループが開始されます。 `SccEndBatch` 関数によって、グループが閉じます。 グループを入れ子にすることはできません。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API バージョン 1.2 の新機能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
