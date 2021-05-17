---
title: CompilandDetails | Microsoft Docs
description: Visual Studio Debug Interface Access SDK で CompilandDetails シンボル型 (SymTagCompilandDetails) に関する参照情報を見つけます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- CompilandDetails symbol
ms.assetid: ddc7d794-c622-4c63-b2a6-72f8b2d0022a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: e217294eeec332a7b629ae39715b6973f7ebb2a9
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "108634218"
---
# <a name="compilanddetails"></a>CompilandDetails
コンパイル単位情報は、`SymTagCompiland` タグ (低い詳細度) と `SymTagCompilandDetails` タグ (高い詳細度) を持つシンボルに分割されます。 `SymTagCompilandDetails` は、`SymTagCompiland` シンボルでは使用できないコンパイル単位に関する豊富な情報を提供します。

## <a name="properties"></a>プロパティ
 次の表に、このシンボルの種類に対して有効なプロパティを示します。

|プロパティ|データ型|説明|
|--------------|---------------|-----------------|
|[IDiaSymbol::get_backEndBuild](../../debugger/debug-interface-access/idiasymbol-get-backendbuild.md)|`DWORD`|コンパイラのバックエンド ビルド番号。|
|[IDiaSymbol::get_backEndMajor](../../debugger/debug-interface-access/idiasymbol-get-backendmajor.md)|`DWORD`|コンパイラのバックエンド メジャー バージョン番号。|
|[IDiaSymbol::get_backEndMinor](../../debugger/debug-interface-access/idiasymbol-get-backendminor.md)|`DWORD`|コンパイラのバックエンド マイナー バージョン番号。|
|[IDiaSymbol::get_compilerName](../../debugger/debug-interface-access/idiasymbol-get-compilername.md)|`BSTR`|このコンパイル単位を生成したコンパイラの名前 (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_editAndContinueEnabled](../../debugger/debug-interface-access/idiasymbol-get-editandcontinueenabled.md)|`BOOL`|コンパイル時にエディット コンティニュが有効になっていた場合は `TRUE`。|
|[IDiaSymbol::get_frontEndBuild](../../debugger/debug-interface-access/idiasymbol-get-frontendbuild.md)|`DWORD`|コンパイラのフロントエンド ビルド番号。|
|[IDiaSymbol::get_frontEndMajor](../../debugger/debug-interface-access/idiasymbol-get-frontendmajor.md)|`DWORD`|コンパイラのフロントエンド メジャー バージョン番号。|
|[IDiaSymbol::get_frontEndMinor](../../debugger/debug-interface-access/idiasymbol-get-frontendminor.md)|`DWORD`|コンパイラのフロントエンド マイナー バージョン番号。|
|[IDiaSymbol::get_hasDebugInfo](../../debugger/debug-interface-access/idiasymbol-get-hasdebuginfo.md)|`BOOL`|このコンパイル単位にデバッグ情報が含まれている場合は `TRUE` (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_hasManagedCode](../../debugger/debug-interface-access/idiasymbol-get-hasmanagedcode.md)|`BOOL`|このコンパイル単位にマネージド コードが含まれている場合は `TRUE` (DIA SDK v8.0 以降のみ)。|
|[IDiaSymbol::get_hasSecurityChecks](../../debugger/debug-interface-access/idiasymbol-get-hassecuritychecks.md)|`BOOL`|コンパイル単位が [/GS (バッファーのセキュリティ チェック)](/cpp/build/reference/gs-buffer-security-check) コンパイラ スイッチを使用してコンパイルされた場合は `TRUE` (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_isCVTCIL](../../debugger/debug-interface-access/idiasymbol-get-iscvtcil.md)|`BOOL`|コンパイル単位が共通中間言語 (CIL) コードからネイティブ コードに変換された場合は `TRUE`。|
|[IDiaSymbol::get_isDataAligned](../../debugger/debug-interface-access/idiasymbol-get-isdataaligned.md)|`BOOL`|ユーザー定義型 (UDT) が指定したメモリ境界に配置されている場合は `TRUE` (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_isHotpatchable](../../debugger/debug-interface-access/idiasymbol-get-ishotpatchable.md)|`BOOL`|コンパイル単位が [/hotpatch (ホットパッチ可能なイメージの作成)](/cpp/build/reference/hotpatch-create-hotpatchable-image) コンパイラ スイッチを使用してコンパイルされた場合は `TRUE` (DIA SDK v8.0 以降のみ)。|
|[IDiaSymbol::get_isLTCG](../../debugger/debug-interface-access/idiasymbol-get-isltcg.md)|`BOOL`|コンパイル単位が [/LTCG (リンク時のコード生成)](/cpp/build/reference/ltcg-link-time-code-generation) コンパイラ スイッチを使用してコンパイルされた場合は `TRUE` (DIA SDK V8.0 以降のみ)。|
|[IDiaSymbol::get_isMSILNetmodule](../../debugger/debug-interface-access/idiasymbol-get-ismsilnetmodule.md)|`BOOL`|コンパイル単位が Microsoft Intermediate Language (MSIL) モジュールの場合は TRUE (DIA SDK v8.0 以降のみ)。|
|[IDiaSymbol::get_language](../../debugger/debug-interface-access/idiasymbol-get-language.md)|`DWORD`|ソース コード言語。|
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|コンパイル単位のシンボル。|
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|構文上の親シンボルの ID。|
|[IDiaSymbol::get_platform](../../debugger/debug-interface-access/idiasymbol-get-platform.md)|`DWORD`|コンパイル単位がコンパイルされたプラットフォーム ([CV_CPU_TYPE_e 列挙型](../../debugger/debug-interface-access/cv-cpu-type-e.md)の値の 1 つ)。|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|シンボルのインデックス ID。|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|`SymTagCompilandDetails` ([SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)の値の 1 つ) を返します。|

## <a name="remarks"></a>解説
 多くの場合、コンパイラは 2 パス コンパイラと呼ばれる形式です。コンパイラのバージョンによっては、各パスが個別のプログラムによって処理される場合があります。 これらはそれぞれフロントエンドとバックエンドのコンパイラと呼ばれます。そのため、バックエンドとフロントエンドのバージョン番号についてシンボル プロパティを使用します。

## <a name="see-also"></a>関連項目
- [コンパイル単位](../../debugger/debug-interface-access/compiland.md)
- [シンボル型の構文階層](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)