---
description: この関数では、ソース管理プラグインが、指定された各ファイルに対する MSSCCPRJ.SCC ファイルの作成をサポートしているかどうかを判定します。
title: SccWillCreateSccFile 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccWillCreateSccFile
helpviewer_keywords:
- SccWillCreateSccFile function
ms.assetid: 0d7542f0-4351-41b3-b24c-960ab99c05a1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9f9e6df29b9f44d852c7c84488a3febf590fcc0e
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900448"
---
# <a name="sccwillcreatesccfile-function"></a>SccWillCreateSccFile 関数
この関数では、ソース管理プラグインが、指定された各ファイルに対する MSSCCPRJ.SCC ファイルの作成をサポートしているかどうかを判定します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccWillCreateSccFile(
   LPVOID  pContext,
   LONG    nFiles,
   LPCSTR* lpFileNames,
   LPBOOL  pbSccFiles
);
```

#### <a name="parameters"></a>パラメーター
 pContext

[入力] ソース管理プラグインのコンテキスト ポインター。

 nFiles

[入力] `lpFileNames` 配列に含まれているファイル名の数であると同時に、`pbSccFiles` 配列の長さでもあります。

 lpFileNames

[入力] チェックする完全修飾ファイル名の配列 (配列は呼び出し元で割り当てる必要がある)。

 pbSccFiles

[入力、出力] 結果を格納するための配列。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値が返されることが予期されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|正常終了しました。|
|SCC_E_INVALIDFILEPATH|配列内のいずれかのパスが無効です。|
|SCC_E_NONSPECIFICERROR|不特定のエラーです。|

## <a name="remarks"></a>解説
 この関数は、ソース管理プラグインが、指定された各ファイルに対する MSSCCPRJ.SCC ファイルのサポートを提供しているかどうかを判定するためのファイルの一覧を使用して呼び出されます (MSSCCPRJ.SCC ファイルの詳細については、「[MSSCCPRJ.SCC ファイル](../extensibility/mssccprj-scc-file.md)」を参照)。 ソース管理プラグインでは、初期化中に `SCC_CAP_SCCFILE` を宣言することによって、MSSCCPRJ.SCC ファイルを作成する機能があるかどうかを宣言できます。 プラグインでは、指定されたファイルのうちのどれに MSSCCPRJ.SCC のサポートがあるかを示すために、`pbSccFiles` 配列内のファイルごとに `TRUE` または `FALSE` を返します。 プラグインがこの関数から成功コードを返した場合は、戻り配列内の値が使用されます。 失敗した場合、この配列は無視されます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [MSSCCPRJ.SCC File](../extensibility/mssccprj-scc-file.md)
