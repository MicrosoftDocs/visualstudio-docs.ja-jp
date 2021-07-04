---
description: この関数を使用すると、特定のコマンドの詳細設定オプションの入力をユーザーに求めることができます。
title: SccGetCommandOptions 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccGetCommandOptions
helpviewer_keywords:
- SccGetCommandOptions function
ms.assetid: bbe4aa4e-b4b0-403e-b7a0-5dd6eb24e5a9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7972d874668649b8bb86adc15008880c5fc4152e
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903932"
---
# <a name="sccgetcommandoptions-function"></a>SccGetCommandOptions 関数
この関数を使用すると、特定のコマンドの詳細設定オプションの入力をユーザーに求めることができます。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccGetCommandOptions(
   LPVOID pvContext,
   HWND hWnd,
   enum SCCCOMMAND iCommand,
   LPCMDOPTS* ppvOptions
);
```

### <a name="parameters"></a>パラメーター
 pvContext

[入力] ソース管理プラグインのコンテキスト構造体。

 hWnd

[入力] ソース管理プラグインが、提供するすべてのダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 iCommand

[入力] 詳細設定オプションが要求されるコマンド (使用できる値については、[コマンド コード](../extensibility/command-code-enumerator.md)に関するページを参照してください)。

 ppvOptions

[入力] 省略可能な構造体 (`NULL`にすることもできます)。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値が返されることが予期されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|正常終了しました。|
|SCC_I_ADV_SUPPORT|こりソース管理プラグインは、コマンドの詳細設定オプションをサポートしています。|
|SCC_I_OPERATIONCANCELED|ユーザーは、ソース管理プラグインの **[オプション]** ダイアログ ボックスを取り消しました。|
|SCC_E_OPTNOTSUPPORTED|ソース管理プラグインは、この操作をサポートしていません。|
|SCC_E_ISCHECKEDOUT|現在チェックアウトされているファイルに対してこの操作を実行することはできません。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセス中に問題が発生しました。ネットワークまたは競合の問題が原因になっている可能性があります。 再試行することをお勧めします。|
|SCC_E_NONSPECIFICERROR|不特定のエラーです。|

## <a name="remarks"></a>解説
 IDE により、最初に `ppvOptions`=`NULL` を使用してこの関数が呼び出され、指定されたコマンドの詳細設定オプション機能をソース管理プラグインがサポートしているかどうかが判断されます。 プラグインがそのコマンドの機能をサポートしている場合、ユーザーが詳細設定オプション (通常、ダイアログ ボックスの **[詳細設定]** ボタンとして実装されます) を要求し、`NULL` ポインターを指す `ppvOptions` の非 NULL ポインターを指定すると、IDE からこの関数が再度呼び出されます。 プラグインにより、ユーザーが指定した詳細設定オプションは非公開の構造体に格納され、その構造体へのポインターが `ppvOptions` に返されます。 次に、この構造体は、`SccGetCommandOptions` 関数への後続の呼び出しを含め、それを認識する必要がある他のすべてのソース管理プラグイン API 関数に渡されます。

 たとえば、次の状況を明確にするために役立つことがあります。

 ユーザーが **Get** コマンドを選択すると、IDE には **[Get]\(取得\)** ダイアログ ボックスが表示されます。 IDE から、`iCommand` が `SCC_COMMAND_GET` に設定され、`ppvOptions` が `NULL` に設定された `SccGetCommandOptions` 関数が呼び出されます。 これは、ソース管理プラグインによって、"このコマンドに詳細設定オプションはありますか?" という質問として解釈されます。 プラグインから `SCC_I_ADV_SUPPORT` が返されると、IDE により、 **[Get]\(取得\)** ダイアログ ボックスに **[詳細設定]** ボタンが表示されます。

 ユーザーが初めて **[詳細設定]** ボタンをクリックすると、IDE により、`SccGetCommandOptions` 関数が再度呼び出されます。今回は、`NULL` ポインターを指す非 `NULL``ppvOptions` が使用されます。 プラグインには、独自の **[Get Options]\(オプションの取得\)** ダイアログ ボックスが表示され、ユーザーに情報の入力が求められ、その情報は独自の構造体に格納され、`ppvOptions` でその構造体へのポインターが返されます。

 ユーザーが同じダイアログ ボックスでもう一度 **[詳細設定]** をクリックすると、IDE によって `ppvOptions` は変更されず、`SccGetCommandOptions` 関数が再度呼び出され、構造体がプラグインに返されます。 これにより、プラグインにより、ユーザーが以前に設定した値へとダイアログ ボックスを再初期化できます。 プラグインにより、所定の位置にある構造体が変更されてから返されます。

 最後に、ユーザーが IDE の **[Get]\(取得\)** ダイアログ ボックスで **[OK]** をクリックすると、IDE から [SccGet](../extensibility/sccget-function.md) が呼び出され、`ppvOptions` で返された詳細設定オプションを含む構造体が渡されます。

> [!NOTE]
> コマンド `SCC_COMMAND_OPTIONS` は、IDE により **[オプション]** ダイアログ ボックスが表示されるときに使用されます。これで、ユーザーは統合の動作を制御する環境設定を設定できるようになります。 ソース管理プラグインに独自の環境設定ダイアログ ボックスが用意されている場合は、IDE の環境設定ダイアログ ボックスの **[詳細設定]** ボタンから表示できます。 このプラグインは、この情報の取得と保持するだけの役割を担い、IDE からそれを使用したり変更したりすることはありません。

## <a name="see-also"></a>こちらもご覧ください
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [コマンド コード](../extensibility/command-code-enumerator.md)
