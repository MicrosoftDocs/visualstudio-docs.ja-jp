---
description: この関数によって、特定のソース管理コマンドのファイルの一覧が更新され、指定したすべてのファイルについてソース管理の状態が提供されます。
title: SccPopulateList 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccPopulateList
helpviewer_keywords:
- SccPopulateList function
ms.assetid: 7416e781-c571-4a7f-8af3-a089ce8be662
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b386c576b48e14b6118f62d451c42ac20f048b45
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902346"
---
# <a name="sccpopulatelist-function"></a>SccPopulateList 関数
この関数によって、特定のソース管理コマンドのファイルの一覧が更新され、指定したすべてのファイルについてソース管理の状態が提供されます。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccPopulateList (
   LPVOID          pvContext,
   enum SCCCOMMAND nCommand,
   LONG            nFiles,
   LPCSTR*         lpFileNames,
   POPLISTFUNC     pfnPopulate,
   LPVOID          pvCallerData,
   LPLONG          lpStatus,
   LONG            fOptions
);
```

#### <a name="parameters"></a>パラメーター
 pvContext

[入力] ソース管理プラグインのコンテキスト構造体。

 nCommand

[入力] `lpFileNames` 配列のすべてのファイルに適用されるソース管理コマンド (使用可能なコマンドの一覧については、[コマンド コード](../extensibility/command-code-enumerator.md)に関するページを参照してください)。

 nFiles

[入力] `lpFileNames` 配列に含まれているファイルの数。

 lpFileNames

[入力] IDE に認識されているファイル名の配列。

 pfnPopulate

[入力] ファイルの追加や削除のために呼び出す IDE コールバック関数 (詳細については、「[POPLISTFUNC](../extensibility/poplistfunc.md)」を参照してください)。

 pvCallerData

[入力] 変更なしでコールバック関数に渡される値。

 lpStatus

[入力、出力] ソース管理プラグインが各ファイルの状態フラグを返すための配列。

 fOptions

[入力] コマンド フラグ (詳細については、「[特定のコマンドで使用されるビットフラグ](../extensibility/bitflags-used-by-specific-commands.md)」の「PopulateList フラグ」セクションを参照してください)。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値が返されることが予期されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|正常終了しました。|
|SCC_E_NONSPECIFICERROR|不特定のエラーです。|

## <a name="remarks"></a>解説
 この関数では、ファイルの一覧について現在の状態を調べます。 `nCommand` の条件に一致しないファイルがあると、`pfnPopulate` コールバック関数を使用して呼び出し元に通知します。 たとえば、コマンドが `SCC_COMMAND_CHECKIN` で、一覧内の 1 ファイルがチェックアウトされていない場合、コールバックを使用して呼び出し元に通知されます。 場合によっては、ソース管理プラグインによって、コマンドに含められる他のファイルが検出され、それらが追加されることがあります。 たとえば、これによって、Visual Basic ユーザーが、自身または自分のプロジェクトで使用されているが Visual Basic プロジェクト ファイルに表示されない .bmp ファイルをチェックアウトできるようになります。 ユーザーが IDE で **Get** コマンドを選択します。 IDE には、ユーザーが取得できると想定されるすべてのファイルの一覧が表示されますが、一覧が表示される前に `SccPopulateList` 関数が呼び出されて、表示される一覧が最新の状態であると保証されます。

## <a name="example"></a>例
 IDE によって、ユーザーが取得できると思われるファイルの一覧が作成されます。 この一覧が表示される前に `SccPopulateList` 関数が呼び出され、一覧に対するファイルの追加や削除をソース管理プラグインが行えるようになります。 プラグインは、指定のコールバック関数を呼び出して一覧を変更します (詳細については、「[POPLISTFUNC](../extensibility/poplistfunc.md)」を参照してください)。

 プラグインは続けて `pfnPopulate` 関数を呼び出し、これによってファイルの追加や削除が行われ、完了すると、`SccPopulateList` 関数が返されます。 これで、IDE によって一覧が表示されます。 `lpStatus` 配列は、IDE によって渡された最初の一覧のすべてのファイルを表します。 プラグインは、コールバック関数を使用するだけでなく、これらすべてのファイルの状態を設定します。

> [!NOTE]
> ソース管理プラグインには、この関数からすぐに制御を戻すだけのオプションが必ずあります (一覧はそのままになります)。 プラグインがこの関数を実装する場合は、最初に [SccInitialize](../extensibility/sccinitialize-function.md) を呼び出すときに `SCC_CAP_POPULATELIST` 機能ビット フラグを設定してこれを指定することができます。 既定では、プラグインは、渡されるすべての項目がファイルであると常に想定します。 ただし、IDE によって `SCC_PL_DIR` フラグが `fOptions` パラメーターに設定されると、渡されるすべての項目がディレクトリであると見なされます。 プラグインは、ディレクトリに属するすべてのファイルを追加する必要があります。 IDE によって、ファイルとディレクトリが混在して渡されることはありません。

## <a name="see-also"></a>こちらもご覧ください
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
- [POPLISTFUNC](../extensibility/poplistfunc.md)
- [特定のコマンドで使用されるビットフラグ](../extensibility/bitflags-used-by-specific-commands.md)
- [コマンド コード](../extensibility/command-code-enumerator.md)
