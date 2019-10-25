---
title: 'Scc: ファイル関数 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccWillCreateSccFile
helpviewer_keywords:
- SccWillCreateSccFile function
ms.assetid: 0d7542f0-4351-41b3-b24c-960ab99c05a1
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2ac7657258b79b2e53bee8138bc5b2728f618eac
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72720118"
---
# <a name="sccwillcreatesccfile-function"></a>SccWillCreateSccFile 関数
この関数は、ソース管理プラグインが MSSCCPRJ.SCC の作成をサポートしているかどうかを判断します。指定された各ファイルの SCC ファイル。

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

からソース管理プラグインのコンテキストポインター。

 nFiles

から@No__t_0 配列に含まれるファイル名の数および `pbSccFiles` 配列の長さ。

 lpFileNames 名

から確認する完全修飾ファイル名の配列 (配列は呼び出し元によって割り当てられる必要があります)。

 pbSccFiles

[入力、出力]結果を格納する配列。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|成功。|
|SCC_E_INVALIDFILEPATH|配列内のパスの1つが無効です。|
|SCC_E_NONSPECIFICERROR|不特定のエラーです。|

## <a name="remarks"></a>Remarks
 この関数は、ソース管理プラグインが MSSCCPRJ.SCC でサポートを提供するかどうかを判断するために、ファイルのリストを使用して呼び出されます。指定された各ファイルの SCC ファイル (MSSCCPRJ.SCC の詳細については、「」を参照してください)。SCC ファイル、「Mssccprj.scc」を参照してください[。SCC ファイル](../extensibility/mssccprj-scc-file.md))。 ソース管理プラグインでは、MSSCCPRJ.SCC を作成する機能があるかどうかを宣言できます。初期化中に `SCC_CAP_SCCFILE` を宣言することによる SCC ファイル。 このプラグインは `pbSccFiles` 配列内のファイルごとに `TRUE` または `FALSE` を返し、指定されたファイルのどれが MSSCCPRJ.SCC しているかを示します。SCC サポート。 プラグインが関数から成功コードを返す場合、返される配列の値は受け入れられます。 失敗した場合、配列は無視されます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [MSSCCPRJ.SCC File](../extensibility/mssccprj-scc-file.md)