---
title: 構造体と共用体 | Microsoft Docs
description: この記事では、Visual Studio Debugging SDK の構造体と共用体の参照箇所にリンクしています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- structures [Visual Studio SDK]
ms.assetid: 9ff0a8f8-1ee6-4fdd-8b80-206436ff589b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 055c8972643a94bd8f13aa6e5e6bc5dde600140b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061473"
---
# <a name="structures-and-unions"></a>構造体と共用体
次に示すのは、Visual Studio Debugging SDK の構造体と共用体です。

- [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) プロセス ID を指定します。これは、システム ID または GUID のいずれかになります。

- [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md) ブレークポイントが発生する条件を記述します。

- [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md) 位置、プログラム、スレッドを含むエラー ブレークポイントの解決を記述します。

- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md) ブレークポイントの場所を記述するために使用される構造体の種類を指定します。

- [BP_LOCATION_CODE_ADDRESS](../../../extensibility/debugger/reference/bp-location-code-address.md) コード内のアドレスでのブレークポイントの位置を記述するコンポーネントを定義します。

- [BP_LOCATION_CODE_CONTEXT](../../../extensibility/debugger/reference/bp-location-code-context.md) デバッグ対象のプログラム内のアドレスに直接バインドされているブレークポイントの位置を記述します。

- [BP_LOCATION_CODE_FILE_LINE](../../../extensibility/debugger/reference/bp-location-code-file-line.md) コード ソース ファイル内の行でのブレークポイントの位置を記述します。

- [BP_LOCATION_CODE_FUNC_OFFSET](../../../extensibility/debugger/reference/bp-location-code-func-offset.md) コード内の関数でのブレークポイントのオフセット位置を記述します。

- [BP_LOCATION_CODE_STRING](../../../extensibility/debugger/reference/bp-location-code-string.md) ユーザーが IDE から入力できる文字列に基づいてコードのブレークポイントを設定するために使用されます。

- [BP_LOCATION_DATA_STRING](../../../extensibility/debugger/reference/bp-location-data-string.md) ユーザーが IDE から入力できる文字列に基づいたデータ ブレークポイントを設定するために使用されます。

- [BP_LOCATION_RESOLUTION](../../../extensibility/debugger/reference/bp-location-resolution.md) 特定の位置にあるブレークポイントの解決方法を記述します。

- [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md) 以前に合格した後に、ブレークポイントが発生する回数と条件を記述します。

- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) ブレークポイントを実装するために必要な情報が含まれています。

- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md) ブレークポイントを実装するために必要な情報が含まれています ([BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) 構造体と同じですが、ベンダーの GUID、制約、トレースポイントの情報が含まれます)。

- [BP_RESOLUTION_CODE](../../../extensibility/debugger/reference/bp-resolution-code.md) コードのブレークポイントの位置を記述します。

- [BP_RESOLUTION_DATA](../../../extensibility/debugger/reference/bp-resolution-data.md) データ ブレークポイントのバインド結果を記述します。

- [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md) コードのブレークポイントまたはデータ ブレークポイントのどちらかのバインドされたブレークポイント情報を記述します。

- [BP_RESOLUTION_LOCATION](../../../extensibility/debugger/reference/bp-resolution-location.md) ブレークポイントの解決の位置の構造体を指定します。

- [BSTR_ARRAY](../../../extensibility/debugger/reference/bstr-array.md) 文字列の配列を記述します。

- [BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md) メタデータから取得したフィールドの種類に関する情報を指定します。

- [CODE_PATH](../../../extensibility/debugger/reference/code-path.md) 関数またはメソッドの呼び出しを記述します。

- [COMPUTER_INFO](../../../extensibility/debugger/reference/computer-info.md) デバッガーが実行されているコンピューターを記述します。

- [CONST_GUID_ARRAY](../../../extensibility/debugger/reference/const-guid-array.md) GUID の一覧を記述します。

- [CONTEXT_INFO](../../../extensibility/debugger/reference/context-info.md) メモリ コンテキストまたはコード コンテキストを記述します。

- [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md) デバッグ中のプログラム内のアドレスを記述します。

- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md) さまざまな種類の多数のアドレスのいずれかを表します。

- [DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md) カスタム ビューアーまたは型ビジュアライザーを識別します。

- [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 名前、型、値を持つ階層的性質のオブジェクトを示すデバッグ プロパティを記述します。

- [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) 参照を記述します。

- [Disassemblydata](../../../extensibility/debugger/reference/disassemblydata.md) 表示のために IDE への逆アセンブリを記述します。

- [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md) デバッグ中のプログラムによってスローされた例外またはランタイム エラーを記述します。

- [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md) ローカル変数、パラメーター、またはその他のフィールドを記述します。

- [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) スタック フレームを記述します。

- [GUID_ARRAY](../../../extensibility/debugger/reference/guid-array.md) 利用できるデバッグ エンジンの一意の識別子からなる配列を記述します。

- [JMC_CODE_SPEC](../../../extensibility/debugger/reference/jmc-code-spec.md) モジュールの JustMyCode 情報を設定するために使用されます。

- [MACHINE_INFO](../../../extensibility/debugger/reference/machine-info.md) 特定のコンピューターを記述します。

- [METADATA_ADDRESS_ARRAYELEM](../../../extensibility/debugger/reference/metadata-address-arrayelem.md) 配列内の配列要素を記述します。

- [METADATA_ADDRESS_FIELD](../../../extensibility/debugger/reference/metadata-address-field.md) クラスまたは構造体のフィールドのアドレスを記述します。

- [METADATA_ADDRESS_LOCAL](../../../extensibility/debugger/reference/metadata-address-local.md) スコープ (通常は関数またはメソッド) 内のローカル変数のアドレスを記述します。

- [METADATA_ADDRESS_METHOD](../../../extensibility/debugger/reference/metadata-address-method.md) クラスのメソッドのアドレスを記述します。

- [METADATA_ADDRESS_PARAM](../../../extensibility/debugger/reference/metadata-address-param.md) メソッドまたは関数のパラメーターを記述します。

- [METADATA_ADDRESS_RETVAL](../../../extensibility/debugger/reference/metadata-address-retval.md) メソッドまたは関数からの戻り値を記述します。

- [METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md) メタデータから取得したフィールドの種類を記述します。

- [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md) 特定のモジュール (DLL、EXE、またはアセンブリ) を記述します。

- [MODULE_SYMBOL_SEARCH_INFO](../../../extensibility/debugger/reference/module-symbol-search-info.md) 検索されたシンボル検索パスに関するステータス情報を示します。

- [NATIVE_ADDRESS](../../../extensibility/debugger/reference/native-address.md) ネイティブ アドレスを記述します。

- [PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md) PDB シンボルから取得されたフィールドの種類を記述します。

- [PENDING_BP_STATE_INFO](../../../extensibility/debugger/reference/pending-bp-state-info.md) コードの場所にバインドする準備ができているブレークポイントの状態を記述します。

- [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md) プロセスを記述します。

- [PROGRAM_NODE_ARRAY](../../../extensibility/debugger/reference/program-node-array.md) プログラム ノードを表す [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) オブジェクトの一覧を記述します。

- [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md) コンピューター上で実行されているプロセスを記述します。

- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) 指定されたテキスト内の行と列の位置を記述します。

- [THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md) スレッドのプロパティを記述します。

- [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md) フィールドの種類を記述します。

- [UNMANAGED_ADDRESS_PHYSICAL](../../../extensibility/debugger/reference/unmanaged-address-physical.md) 物理アドレスを記述します。

- [UNMANAGED_ADDRESS_THIS_RELATIVE](../../../extensibility/debugger/reference/unmanaged-address-this-relative.md) `this` ポインター (Visual Basic では `Me`) に対する相対アドレスを記述します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h、sh.h、または ee.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [API リファレンス](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)
