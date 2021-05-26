---
description: この関数は、現在の状態の完全修飾ディレクトリの一覧を調べます。
title: SccDirQueryInfo 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccDirQueryInfo
helpviewer_keywords:
- SccDirQueryInfo function
ms.assetid: 459e2d99-573d-47c4-b834-6d82c5e14162
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 81087d4f4da3435fb7bc80ec4a965394c7d6c7f3
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060329"
---
# <a name="sccdirqueryinfo-function"></a>SccDirQueryInfo 関数
この関数は、現在の状態の完全修飾ディレクトリの一覧を調べます。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccDirQueryInfo(
LPVOID  pContext,
LONG    nDirs,
LPCSTR* lpDirNames,
LPLONG  lpStatus
);
```

### <a name="parameters"></a>パラメーター
 pContext

[入力] ソース管理プラグインのコンテキスト構造体。

 nDirs

[入力] クエリ対象として選択されたディレクトリの数。

 lpDirNames

[入力] クエリ対象のディレクトリの完全修飾パスの配列。

 lpStatus

[入力、出力] ステータス フラグを返すソース管理プラグインの配列構造体 (詳細については、[ディレクトリ状態コード](../extensibility/directory-status-code-enumerator.md)に関するページを参照してください)。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値を返すことが想定されます。

|値|説明|
|-----------|-----------------|
|SCC_OK|クエリに成功しました。|
|SCC_E_OPNOTSUPPORTED|ソース コード管理システムでは、この操作はサポートされていません。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセス中に問題が発生しました。ネットワークまたは競合の問題である可能性があります。 再試行することをお勧めします。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|不特定のエラーです。|

## <a name="remarks"></a>解説
 関数により、返される配列に `SCC_DIRSTATUS` ファミリのビットのビットマスク ([ディレクトリ状態コード](../extensibility/directory-status-code-enumerator.md)に関するページを参照) が入力されます。これは、所与のディレクトリごとに 1 つのエントリです。 状態配列は、呼び出し元によって割り当てられます。

 IDE では、ディレクトリの名前を変更する前に、この関数を使用して、ディレクトリがソース管理下にあるかどうかを、対応するプロジェクトがあるかどうかをクエリすることによって確認します。 ディレクトリがソース管理下にない場合、IDE からユーザーに適切な警告を提供できます。

> [!NOTE]
> ソース管理プラグインで 1 つ以上の状態値を実装しないことが選択された場合は、実装されていないビットを 0 に設定する必要があります。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [ディレクトリの状態コード](../extensibility/directory-status-code-enumerator.md)
