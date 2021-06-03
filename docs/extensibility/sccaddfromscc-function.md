---
description: この関数では、ソース管理システムに既に存在するファイルをユーザーが参照し、そのファイルを現在のプロジェクトの一部として含めることができます。
title: SccAddFromScc 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccAddFromScc
helpviewer_keywords:
- SccAddFromScc function
ms.assetid: 902e764d-200e-46e1-8c42-4da7b037f9a0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: be67fd18c6cac7217da0d79aaef766e942e15fb9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085677"
---
# <a name="sccaddfromscc-function"></a>SccAddFromScc 関数
この関数では、ソース管理システムに既に存在するファイルをユーザーが参照し、そのファイルを現在のプロジェクトの一部として含めることができます。 たとえば、この関数では、ファイルをコピーすることなく、共通のヘッダー ファイルを現在のプロジェクトに取得できます。 返されるファイルの配列 `lplpFileNames` には、ユーザーが IDE プロジェクトに追加するファイルのリストが含まれています。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccAddFromScc (
   LPVOID   pvContext,
   HWND     hWnd,
   LPLONG   lpnFiles,
   LPCSTR** lplpFileNames
);
```

### <a name="parameters"></a>パラメーター
 pvContext

[入力] ソース管理プラグインのコンテキスト構造体。

 hWnd

[入力] 提供するすべてのダイアログ ボックスの親としてソース管理プラグインで使用できる IDE ウィンドウへのハンドル。

 lpnFiles

[入力、出力] 追加されるファイルの数のバッファー。 (`lplpFileNames` によって指されているメモリが解放される場合は `NULL` です。 詳細については、「解説」を参照してください。)

 lplpFileNames

[入力、出力] ディレクトリ パスのない、すべてのファイル名へのポインターの配列。 この配列は、ソース管理プラグインによって割り当ておよび解放が行われます。 `lpnFiles` = 1 で、`lplpFileNames` が `NULL` ではない場合、`lplpFileNames` によって指されている配列の最初の名前には追加先のフォルダーが含まれています。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値が返されることが予期されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|ファイルが正常に検出され、プロジェクトに追加されました。|
|SCC_I_OPERATIONCANCELED|操作が取り消されました。追加は行われません。|
|SCC_I_RELOADFILE|ファイルまたはプロジェクトを再度読み込む必要があります。|

## <a name="remarks"></a>解説
 IDE によってこの関数が呼び出されます。 ソース管理プラグインでローカルの出力先フォルダーの指定がサポートされる場合、IDE では `lpnFiles` = 1 を渡し、ローカル フォルダー名を `lplpFileNames` に渡します。

 `SccAddFromScc` 関数への呼び出しが戻ると、プラグインによって `lpnFiles` と `lplpFileNames` に値が割り当てられ、必要に応じてファイル名配列のメモリが割り当てられます (この割り当てによって `lplpFileNames` のポインターが置き換えられることに注意してください)。 ソース管理プラグインは、すべてのファイルをユーザーのディレクトリまたは指定された追加先フォルダーに配置する役割を担います。 その後、IDE によって、IDE プロジェクトにファイルが追加されます。

 最後に、IDE によってこの関数の 2 回目の呼び出しが行われます (`lpnFiles` に `NULL` が渡されます)。 これは、`lplpFileNames``.` のファイル名配列に割り当てられたメモリを解放するために、ソース管理プラグインによって特別なシグナルとして解釈されます

 `lplpFileNames` は `char ***` ポインターです。 ソース管理プラグインによって、ファイル名へのポインターの配列へのポインターが配置されるため、この API の標準的な方法でリストが渡されます。

> [!NOTE]
> VSSCI API の初期バージョンでは、追加されたファイルのターゲットプロジェクトを示す方法が提供されていませんでした。 これに対応するために、`lplpFIleNames` パラメーターのセマンティクスが拡張され、出力パラメーターではなく入力/出力パラメーターにされました。 1 つのファイルのみが指定された場合 (つまり、`lpnFiles` = 1 によって指されている値)、`lplpFileNames` の最初の要素にはターゲット フォルダーが含まれています。 これらの新しいセマンティクスを使用するために、IDE では `nOption` パラメーターを `SCC_OPT_SHARESUBPROJ` に設定して `SccSetOption` 関数を呼び出します。 ソース管理プラグインでこのセマンティクスがサポートされない場合は、`SCC_E_OPTNOTSUPPORTED` が返されます。 これにより、**ソース管理からの追加** 機能の使用が無効になります。 プラグインで **ソース管理からの追加** 機能 (`SCC_CAP_ADDFROMSCC`) がサポートされる場合は、新しいセマンティクスをサポートし、`SCC_I_SHARESUBPROJOK` が返される必要があります。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccSetOption](../extensibility/sccsetoption-function.md)
