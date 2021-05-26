---
title: POPLISTFUNC | Microsoft Docs
description: ファイルまたはディレクトリのリストを更新するためにソース管理プラグインによって使用される POPLISTFUNC コールバック関数について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- POPDIRLISTFUNC
helpviewer_keywords:
- POPLISTFUNC callback function
ms.assetid: b2199fd5-d707-4628-92dd-e2a01e2f507a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: aec322d73e49d4aae91956bd8df015a01c922a10
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090240"
---
# <a name="poplistfunc"></a>POPLISTFUNC
このコールバックは、IDE によって [SccPopulateList](../extensibility/sccpopulatelist-function.md) に提供され、ソース管理プラグインでファイルまたはディレクトリのリストを更新するために使用されます (`SccPopulateList` 関数にも提供されています)。

 ユーザーが IDE で **Get** コマンドを選択すると、IDE には、ユーザーが取得できるすべてのファイルのリスト ボックスが表示されます。 残念ながら、IDE では、ユーザーが取得する可能性のあるすべてのファイルの正確なリストを認識していません。このリストはプラグインのみに含まれています。 他のユーザーがソース コード管理プロジェクトにファイルを追加している場合、これらのファイルはリストに表示されますが、IDE では認識されません。 IDE によって、ユーザーが取得できると思われるファイルのリストが作成されます。 このリストをユーザーに表示する前に、[SccPopulateList](../extensibility/sccpopulatelist-function.md)`,` を呼び出して、ソース管理プラグインによってリストでファイルを追加および削除できるようにします。

## <a name="signature"></a>署名
 ソース管理プラグインでは、IDE によって実装された関数を次のプロトタイプで呼び出すことによって、リストを変更します。

```cpp
typedef BOOL (*POPLISTFUNC) (
   LPVOID pvCallerData,
   BOOL fAddRemove,
   LONG nStatus,
   LPSTR lpFileName
);
```

## <a name="parameters"></a>パラメーター
 pvCallerData 呼び出し元 (IDE) によって [SccPopulateList](../extensibility/sccpopulatelist-function.md) に渡される `pvCallerData` パラメーター。 ソース管理プラグインでは、このパラメーターの内容について何も想定していません。

 fAddRemove `TRUE` の場合は、`lpFileName` が、ファイル リストに追加する必要があるファイルです。 `FALSE` の場合は、`lpFileName` が、ファイル リストから削除する必要があるファイルです。

 nStatus 状態 `lpFileName` (`SCC_STATUS` ビットの組み合わせ。詳細については、「[ファイルの状態コード](../extensibility/file-status-code-enumerator.md)」を参照してください)。

 lpFileName リストで追加または削除するファイル名の完全なディレクトリ パス。

## <a name="return-value"></a>戻り値

|値|説明|
|-----------|-----------------|
|`TRUE`|プラグインでは、この関数の呼び出しを続行できます。|
|`FALSE`|IDE 側で問題が発生しました (メモリ不足の状況など)。 プラグインで操作を停止する必要があります。|

## <a name="remarks"></a>解説
 ソース管理プラグインによってファイル リストで追加または削除しようとしているファイルごとに、この関数を呼び出して `lpFileName` を渡します。 `fAddRemove` フラグは、リストに追加する新しいファイルまたは削除する前のファイルを示します。 `nStatus` パラメーターは、ファイルの状態を示します。 SCC プラグインでファイルの追加と削除を完了すると、[SccPopulateList](../extensibility/sccpopulatelist-function.md) 呼び出しから戻ります。

> [!NOTE]
> Visual Studio では `SCC_CAP_POPULATELIST` 機能ビットが必要です。

## <a name="see-also"></a>関連項目
- [IDE で実装されるコールバック関数](../extensibility/callback-functions-implemented-by-the-ide.md)
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
- [SccPopulateList](../extensibility/sccpopulatelist-function.md)
- [ファイルの状態コード](../extensibility/file-status-code-enumerator.md)
