---
description: この関数では、ソース管理システムに新しいファイルが追加されます。
title: SccAdd 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccAdd
helpviewer_keywords:
- SccAdd function
ms.assetid: 545268f3-8e83-446a-a398-1a9db9e866e8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7c577bd865a7534a5c4e13253e921ef188e7f0ac
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085690"
---
# <a name="sccadd-function"></a>SccAdd 関数
この関数では、ソース管理システムに新しいファイルが追加されます。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccAdd(
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPCSTR*   lpFileNames,
   LPCSTR    lpComment,
   LONG*     pfOptions,
   LPCMDOPTS pvOptions
);
```

### <a name="parameters"></a>パラメーター
 pvContext

[入力] ソース管理プラグインのコンテキスト構造体。

 hWnd

[入力] 提供するすべてのダイアログ ボックスの親としてソース管理プラグインで使用できる IDE ウィンドウへのハンドル。

 nFiles

[入力] `lpFileNames` 配列に指定されている、現在のプロジェクトに追加されるように選択されたファイルの数。

 lpFileNames

[入力] 追加するファイルの完全修飾ローカル名の配列。

 lpComment

[入力] 追加されるすべてのファイルに適用されるコメント。

 pfOptions

[入力] ファイルごとに提供されるコマンド フラグの配列。

 pvOptions

[入力] ソース管理プラグイン固有のオプション。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値が返されることが予期されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|追加操作が正常に完了しました。|
|SCC_E_FILEALREADYEXISTS|選択したファイルは既にソース管理されています。|
|SCC_E_TYPENOTSUPPORTED|ファイルの種類 (バイナリなど) が、ソース管理システムでサポートされていません。|
|SCC_E_OPNOTSUPPORTED|ソース管理システムでは、この操作をサポートしていません。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセス中に問題が発生しました。ネットワークまたは競合の問題が原因になっている可能性があります。 再試行することをお勧めします。|
|SCC_E_NOTAUTHORIZED|ユーザーには、この操作の実行が許可されていません。|
|SCC_E_NONSPECIFICERROR|不特定のエラーです。追加は実行されません。|
|SCC_I_OPERATIONCANCELED|操作は完了前にキャンセルされました。|
|SCC_I_RELOADFILE|ファイルまたはプロジェクトを再度読み込む必要があります。|
|SCC_E_FILENOTEXIST|ローカル ファイルが見つかりませんでした。|

## <a name="remarks"></a>解説
 通常の `fOptions` は、ここでは配列 `pfOptions` で置き換えられ、ファイルごとに 1 つの `LONG` オプションが指定されます。 これは、ファイルの種類がファイルによって異なる場合があるためです。

> [!NOTE]
> 同じファイルに対して `SCC_FILETYPE_TEXT` オプションと `SCC_FILETYPE_BINARY` オプションの両方を指定することは無効ですが、どちらも指定しないことは有効です。 どちらも設定しないのは `SCC_FILETYPE_AUTO` を設定することと同じです。この場合、ソース管理プラグインによってファイルの種類が自動検出されます。

 `pfOptions` 配列で使用されるフラグの一覧を以下に示します。

|オプション|値|説明|
|------------|-----------|-------------|
|SCC_FILETYPE_AUTO|0x00|ソース管理プラグインで、ファイルの種類を検出する必要があります。|
|SCC_FILETYPE_TEXT|0x01|ASCII テキスト ファイルを示します。|
|SCC_FILETYPE_BINARY|0x02|ASCII テキスト以外のファイルの種類を示します。|
|SCC_ADD_STORELATEST|0x04|ファイルの最新のコピーのみを格納し、デルタは格納しません。|
|SCC_FILETYPE_TEXT_ANSI|0x08|ファイルを ANSI テキストとして扱います。|
|SCC_FILETYPE_UTF8|0x10|ファイルを UTF8 形式の Unicode テキストとして扱います。|
|SCC_FILETYPE_UTF16LE|0x20|ファイルを UTF16 リトル エンディアン形式の Unicode テキストとして扱います。|
|SCC_FILETYPE_UTF16BE|0x40|ファイルを UTF16 ビッグ エンディアン形式の Unicode テキストとして扱います。|

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
