---
description: この関数では、ソース管理プラグインを初期化し、統合開発環境 (IDE) に機能と制限を提供します。
title: SccInitialize 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccInitialize
helpviewer_keywords:
- SccInitialize function
ms.assetid: 5bc0d28b-2c68-4d43-9e51-541506a8f76e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 633e8909febd758df455a9375f735a93e3407c77
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902528"
---
# <a name="sccinitialize-function"></a>SccInitialize 関数
この関数では、ソース管理プラグインを初期化し、統合開発環境 (IDE) に機能と制限を提供します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccInitialize (
   LPVOID* ppvContext,
   HWND    hWnd,
   LPCSTR  lpCallerName,
   LPSTR   lpSccName,
   LPLONG  lpSccCaps,
   LPSTR   lpAuxPathLabel,
   LPLONG  pnCheckoutCommentLen,
   LPLONG  pnCommentLen
);
```

#### <a name="parameters"></a>パラメーター
 `ppvContext`

[入力] ソース管理プラグインでは、そのコンテキスト構造体へのポインターをここに格納できます。

 `hWnd`

[入力] ソース管理プラグインが、提供するすべてのダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 `lpCallerName`

[入力] ソース管理プラグインを呼び出しているプログラムの名前。

 `lpSccName`

[入力、出力] ソース管理プラグインが独自の名前を格納するバッファー (`SCC_NAME_LEN` 文字以下)。

 `lpSccCaps`

[出力] ソース管理プラグインの機能フラグを返します。

 `lpAuxPathLabel`

[入力、出力] ソース管理プラグインが、[SccOpenProject](../extensibility/sccopenproject-function.md) と [SccGetProjPath](../extensibility/sccgetprojpath-function.md) によって返される `lpAuxProjPath` パラメーターの説明の文字列を格納するバッファー (`SCC_AUXLABEL_LEN` 文字以下)。

 `pnCheckoutCommentLen`

[出力] チェックアウト コメントの許容される最大の長さを返します。

 `pnCommentLen`

[出力] その他のコメントの許容される最大の長さを返します。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値が返されることが予期されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|ソース管理の初期化に成功しました。|
|SCC_E_INITIALIZEFAILED|システムを初期化できませんでした。|
|SCC_E_NOTAUTHORIZED|ユーザーは指定された操作の実行が許可されていません。|
|SCC_E_NONSPECFICERROR|不特定のエラー。ソース管理システムは初期化されませんでした。|

## <a name="remarks"></a>解説
 IDE では、ソース管理プラグインを最初に読み込むときに、この関数を呼び出します。 これにより、IDE では、呼び出し元の名前などの特定の情報をプラグインに渡すことができます。 また、IDE には、コメントの許容される最大の長さやプラグインの機能などの特定の情報が返されます。

 `ppvContext` は `NULL` ポインターを指します。 ソース管理プラグインでは、独自に使用する構造体を割り当て、その構造体へのポインターを `ppvContext` に格納できます。 IDE では、このポインターを他のすべての VSSCI API 関数に渡すため、プラグインは、グローバル ストレージに頼ることなくコンテキスト情報を取得したり、プラグインの複数のインスタンスをサポートしたりすることができます。 この構造体は、[SccUninitialize](../extensibility/sccuninitialize-function.md) が呼び出されたときに割り当て解除する必要があります。

 `lpCallerName` および `lpSccName` パラメーターを使用すると、IDE とソース管理プラグインは名前を交換できます。 これらの名前は、単に複数のインスタンスを区別するために使用することも、実際にメニューやダイアログ ボックスに表示することもできます。

 `lpAuxPathLabel` パラメーターは、補助プロジェクト パスを識別するためのコメントとして使用される文字列であり、ソリューション ファイルに格納され、[SccOpenProject](../extensibility/sccopenproject-function.md) の呼び出しでソース管理プラグインに渡されます。 [!INCLUDE[vsvss](../extensibility/includes/vsvss_md.md)] では、文字列 "SourceSafe プロジェクト:" を使用します。その他のソース管理プラグインでは、この特定の文字列の使用を避ける必要があります。

 `lpSccCaps` パラメーターは、ソース管理プラグインに、そのプラグインの機能を示すビットフラグを格納する場所を提供します。 (機能ビットフラグの完全な一覧については、「[機能フラグ](../extensibility/capability-flags.md)」を参照)。 たとえば、プラグインが、呼び出し元によって提供されたコールバック関数に結果を書き込むことを計画している場合、そのプラグインは機能ビット SCC_CAP_TEXTOUT を設定します。 これにより、IDE は、バージョン管理の結果のためのウィンドウを作成するように通知されます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccUninitialize](../extensibility/sccuninitialize-function.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)
- [機能フラグ](../extensibility/capability-flags.md)
