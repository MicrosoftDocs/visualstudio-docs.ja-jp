---
description: この関数では、ファイルまたはプロジェクトのソース管理プロパティが表示されます。
title: SccProperties 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccProperties
helpviewer_keywords:
- SccProperties function
ms.assetid: 1bed38c9-73d2-4474-9717-f9dc26a89cbe
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: cd50353ab29c05e5e5db2dc2b3f363af46ca8aa7
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904192"
---
# <a name="sccproperties-function"></a>SccProperties 関数
この関数では、ファイルまたはプロジェクトのソース管理プロパティが表示されます。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccProperties (
   LPVOID pvContext,
   HWND   hWnd,
   LPCSTR lpFileName
);
```

#### <a name="parameters"></a>パラメーター
 pvContext

[入力] ソース管理プラグインのコンテキスト構造体。

 hWnd

[入力] ソース管理プラグインが、提供するすべてのダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 lpFileName

[入力] ファイルまたはプロジェクトの完全修飾パス名。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値が返されることが予期されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|プロパティが正常に表示されました。|
|SCC_I_RELOADFILE|バージョン管理システムによってファイルのプロパティが変更されたため、IDE によってこのファイルを再読み込みする必要があります。|
|SCC_E_PROJNOTOPEN|指定したプロジェクトがソース管理で開かれていません。|
|SCC_E_NOTAUTHORIZED|このファイルまたはプロジェクトのプロパティを表示する権限がユーザーにありません。|
|SCC_E_FILENOTCONTROLLED|指定したファイルまたはプロジェクトは、ソースが管理されていません。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|不明なエラーまたは一般的なエラーが発生しました。|

## <a name="remarks"></a>解説
 ソース管理プラグインによって、プロパティが専用のダイアログ ボックスに表示されます。

 プロパティはソース管理プラグインによって定義され、プラグインごとに異なる場合があります。 ファイルのソース管理プロパティのユーザーによる変更がプラグインで許可されると、`SCC_I_RELOAD` が返され、このファイルまたはプロジェクトを再読み込みする必要があることが IDE に通知されます。

## <a name="see-also"></a>こちらもご覧ください
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
