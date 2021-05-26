---
description: この関数は、ソース管理システム内のファイルの名前を変更します。
title: SccRename 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccRename
helpviewer_keywords:
- SccRename function
ms.assetid: b467ade6-a1db-4c0b-b60f-7850ec4f79eb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d9d42e796f1ec2176e9de79ca392aab070581324
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073834"
---
# <a name="sccrename-function"></a>SccRename 関数
この関数は、ソース管理システム内のファイルの名前を変更します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccRename(
   LPVOID pvContext,
   HWND   hWnd,
   LPCSTR lpFileName,
   LPCSTR lpNewName
);
```

#### <a name="parameters"></a>パラメーター
 pvContext

[入力] ソース管理プラグインのコンテキスト構造体。

 hWnd

[入力] ソース管理プラグインが、提供するすべてのダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 lpFileName

[入力] 名前が変更されるファイルの完全修飾ファイル名。

 lpNewName

[入力] 完全修飾の新しい名前。 ディレクトリ パスが異なる場合、ファイルはあるサブディレクトリから別のサブディレクトリに移動されています。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値を返すことが想定されます。

|値|説明|
|-----------|-----------------|
|SCC_OK|名前の変更操作は正常に完了しました。|
|SCC_E_PROJNOTOPEN|プロジェクトがソース管理下で開かれていません。|
|SCC_E_FILENOTCONTROLLED|ファイルはソース管理されていません。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセス中に問題が発生しました。ネットワークまたは競合の問題である可能性があります。|
|SCC_E_NOTAUTHORIZED|ユーザーにはこの操作を完了する権限がありません。|
|SCC_E_COULDNOTCREATEPROJECT|名前の変更プロセスの一部としてプロジェクトを作成できませんでした。|
|SCC_E_OPNOTPERFORMED|操作が実行されませんでした。|
|SCC_E_NONSPECIFICERROR|指定されていないエラーまたは一般的なエラーが発生しました。|

## <a name="remarks"></a>解説
 この関数を使用すると、ファイルの名前を変更したり、ソース管理システム内のある場所から別の場所にファイルを移動したりすることができます。 ソース管理プラグインでディスク上のファイルへアクセスしようとしないでください。 ローカル ファイルの名前を変更するのは IDE の役割です。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
