---
description: 次に、Visual Studio デバッグ SDK の列挙型を示します。
title: 列挙 (Visual Studio のデバッグ) | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- enumerations [Visual Studio SDK]
- debugging [Debugging SDK], enumerations
ms.assetid: 557065bf-081f-4d57-8744-bae02b8a5a6e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 303b0ce662f56c1ab337383aaf4f4f2f09bb6ac8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105095986"
---
# <a name="enumerations-visual-studio-debugging"></a>列挙 (Visual Studio のデバッグ)
次に、[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] デバッグ SDK の列挙型を示します。

- [AD_PROCESS_ID_TYPE](../../../extensibility/debugger/reference/ad-process-id-type.md): [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) 構造体でプロセス ID を解釈する方法を指定します。

- [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md): アドレスの種類を指定します。

- [ASSEMBLYLOCRESOLUTION](../../../extensibility/debugger/reference/assemblylocresolution.md): アセンブリが配置される場所を指定します。

- [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md): デバッグ エンジン (DE) をプログラム ノードにアタッチする理由を指定します。

- [BP_COND_STYLE](../../../extensibility/debugger/reference/bp-cond-style.md): 保留中のブレークポイントとバインドされたブレークポイントのブレークポイント条件スタイルを指定します。

- [BP_ERROR_TYPE](../../../extensibility/debugger/reference/bp-error-type.md): ブレークポイントのエラーの種類を指定します。

- [BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md): ブレークポイントを設定するときに追加情報の指定に使用できるオプションのフラグを指定します。

- [BP_FLAGS90](../../../extensibility/debugger/reference/bp-flags90.md): ブレークポイントを設定するときに追加情報の指定に使用できるオプションのフラグの有効な値を列挙します。 この列挙によって [BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md) 列挙型が拡張されます。

- [BP_LOCATION_TYPE](../../../extensibility/debugger/reference/bp-location-type.md): ブレークポイント要求のブレークポイントの場所の種類を指定します。

- [BP_PASSCOUNT_STYLE](../../../extensibility/debugger/reference/bp-passcount-style.md): ブレークポイントが発生する原因となる、ブレークポイントのパス数に関連付けられた条件を指定します。

- [BP_RES_DATA_FLAGS](../../../extensibility/debugger/reference/bp-res-data-flags.md): データ ブレークポイントをエミュレートするか、ハードウェアに実装するかを指定します。

- [BP_STATE](../../../extensibility/debugger/reference/bp-state.md): バインドされたブレークポイントが存在すること、およびそれが有効になっているかどうかを明示します。

- [BP_TYPE](../../../extensibility/debugger/reference/bp-type.md): ブレークポイントがコードの場所にあるか、データの場所であるか、または別の種類のブレークポイントであるかを指定します。

- [BP_UNBOUND_REASON](../../../extensibility/debugger/reference/bp-unbound-reason.md): ブレークポイントがバインド解除された理由を示します。

- [BPERESI_FIELDS](../../../extensibility/debugger/reference/bperesi-fields.md): ブレークポイントの失敗した解決について取得する情報を指定します。

- [BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md): ブレークポイント要求について取得する情報を指定します。

- [BPREQI_FIELDS90](../../../extensibility/debugger/reference/bpreqi-fields90.md): ブレークポイント要求について取得する情報を指定する有効な値を列挙します。 この列挙によって [BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md) 列挙型が拡張されます。

- [BPRESI_FIELDS](../../../extensibility/debugger/reference/bpresi-fields.md): 正常に解決されたブレークポイントについて取得する情報を指定します。

- [CANSTOP_REASON](../../../extensibility/debugger/reference/canstop-reason.md): 実行中、特定のポイントに到達後、プログラムでは実行を停止できるか判断する目的で使用されます。

- [CONNECTION_PROTOCOL](../../../extensibility/debugger/reference/connection-protocol.md): デバッグ サーバーとデバッグ パッケージ間の通信に使用されるプロトコルを示す値。

- [CONSTRUCTOR_ENUM](../../../extensibility/debugger/reference/constructor-enum.md): さまざまな種類のコンストラクターを選択します。

- [CONTEXT_COMPARE](../../../extensibility/debugger/reference/context-compare.md): 2 つのメモリ コンテキストを比較するための条件を指定します。

- [CONTEXT_INFO_FIELDS](../../../extensibility/debugger/reference/context-info-fields.md): メモリ コンテキストについて取得する情報を指定します。

- [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md): [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) または [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) インターフェイスのさまざまな属性を記述します。

- [DEBUG_REASON](../../../extensibility/debugger/reference/debug-reason.md): デバッグのためのプロセスが起動した理由を指定します。

- [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md): デバッグ プロパティ オブジェクトについて取得する情報を指定します。

- [DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md): デバッグ参照オブジェクトについて取得する情報を指定します。

- [DISASSEMBLY_FLAGS](../../../extensibility/debugger/reference/disassembly-flags.md): 逆アセンブリのフラグを指定します。

- [DISASSEMBLY_STREAM_FIELDS](../../../extensibility/debugger/reference/disassembly-stream-fields.md): 逆アセンブリ フィールドについて取得する情報を指定します。

- [DISASSEMBLY_STREAM_SCOPE](../../../extensibility/debugger/reference/disassembly-stream-scope.md): 逆アセンブリ ストリームのスコープを指定します。

- [DisplayKind](../../../extensibility/debugger/reference/displaykind.md): [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) オブジェクトから取得してユーザーに表示する情報の種類を表す有効な値を列挙します。

- [DOCCONTEXT_COMPARE](../../../extensibility/debugger/reference/doccontext-compare.md): 2 つのドキュメント コンテキストを比較するための条件を指定します。

- [DUMPTYPE](../../../extensibility/debugger/reference/dumptype.md): ダンプするプログラムの状態の量を指定します。

- [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md): [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) オブジェクトの型を解釈する方法を指定します。

- [EncUnavailableReason](../../../extensibility/debugger/reference/encunavailablereason.md): エディット コンティニュが使用できない理由を表します。

- [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md): 式評価を制御するフラグを指定します。

- [EVALFLAGS90](../../../extensibility/debugger/reference/evalflags90.md): 式評価を制御するフラグの有効な値を列挙します。 この列挙によって [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md) 列挙型が拡張されます。

- [EVENTATTRIBUTES](../../../extensibility/debugger/reference/eventattributes.md): イベントの属性を指定します。

- [EXCEPTION_STATE](../../../extensibility/debugger/reference/exception-state.md): 例外の状態を指定します。

- [FIELD_INFO_FIELDS](../../../extensibility/debugger/reference/field-info-fields.md): [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) オブジェクトについて取得する情報を指定します。

- [FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md): [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) オブジェクトに含まれるフィールドの種類を指定します。

- [FIELD_KIND_EX](../../../extensibility/debugger/reference/field-kind-ex.md): [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) オブジェクトに格納できるその他の種類のフィールドを列挙します。 この列挙によって [FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md) 列挙型が拡張されます。

- [FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md): フィールド型の修飾子を指定します。

- [FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md): スタック フレーム オブジェクトについて取得する情報を指定します。

- [GETHOSTNAME_TYPE](../../../extensibility/debugger/reference/gethostname-type.md): ホスト名の種類を指定します。

- [GETNAME_TYPE](../../../extensibility/debugger/reference/getname-type.md): 取得するファイルの名前の種類を指定します。

- [INTERCEPT_EXCEPTION_ACTION](../../../extensibility/debugger/reference/intercept-exception-action.md): 例外をインターセプトするときに実行するアクションを指定します。

- [LAUNCH_FLAGS](../../../extensibility/debugger/reference/launch-flags.md): プログラムを起動する方法を指定します。

- [MACHINE_INFO_FIELDS](../../../extensibility/debugger/reference/machine-info-fields.md): 特定のコンピューターについて、取得する情報の種類を指定します。

- [MACHINE_INFO_FLAGS](../../../extensibility/debugger/reference/machine-info-flags.md): コンピューターを説明するために使用されます。

- [MESSAGETYPE](../../../extensibility/debugger/reference/messagetype.md): メッセージの種類と理由を指定します。

- [MODULE_FLAGS](../../../extensibility/debugger/reference/module-flags.md): モジュールを記述するために使用されます。

- [MODULE_INFO_FIELDS](../../../extensibility/debugger/reference/module-info-fields.md): デバッグ モジュール情報のフラグを指定します。

- [MODULE_INFO_FLAGS](../../../extensibility/debugger/reference/module-info-flags.md): モジュールのシンボルの状態を指定します。

- [NAME_MATCH](../../../extensibility/debugger/reference/name-match.md): 名前の照合での大文字と小文字の区別のオプションを選択します。

- [OBJECT_TYPE](../../../extensibility/debugger/reference/object-type.md): 式エバリュエーターからオブジェクトの型を指定します。

- [PARSEFLAGS](../../../extensibility/debugger/reference/parseflags.md): 式の解析方法を指定します。

- [PENDING_BP_STATE](../../../extensibility/debugger/reference/pending-bp-state.md): 保留中のブレークポイント (まだバインドされていないブレークポイント) の状態を指定します。

- [PENDING_BP_STATE_FLAGS](../../../extensibility/debugger/reference/pending-bp-state-flags.md): 保留中のブレークポイントの状態フラグを指定します。

- [PORT_SUPPLIER_DESCRIPTION_FLAGS](../../../extensibility/debugger/reference/port-supplier-description-flags.md): ポート サプライヤーに関して取得可能なメタデータを定義します。

- [PROCESS_INFO_FIELDS](../../../extensibility/debugger/reference/process-info-fields.md): プロセスについて、取得する情報の種類を指定します。

- [PROCESS_INFO_FLAGS](../../../extensibility/debugger/reference/process-info-flags.md): プロセスのプロパティを記述または指定します。

- [PROGRAM_DESTROY_FLAGS](../../../extensibility/debugger/reference/program-destroy-flags.md): プログラムの破棄フラグの有効な値を列挙します。

- [PROVIDER_FIELDS](../../../extensibility/debugger/reference/provider-fields.md): プログラム プロバイダーに関連付けられているプロパティを指定します。

- [PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md): プログラム プロバイダーから取得する必要のあるプロパティを指定します。

- [REFERENCE_COMPARE](../../../extensibility/debugger/reference/reference-compare.md): 参照の比較の種類を指定します。

- [REFERENCE_TYPE](../../../extensibility/debugger/reference/reference-type.md): 参照型を指定します。

- [SEEK_START](../../../extensibility/debugger/reference/seek-start.md): 逆アセンブリでシークを開始する位置を指定します。

- [STEPKIND](../../../extensibility/debugger/reference/stepkind.md): ステップ実行のステップの種類を指定します。

- [STEPUNIT](../../../extensibility/debugger/reference/stepunit.md): ステップ実行のステップ単位を指定します。

- [SYMBOL_SEARCH_INFO_FIELDS](../../../extensibility/debugger/reference/symbol-search-info-fields.md): 取得するシンボル情報の種類を指定します。

- [TEXT_DOC_ATTR_2](../../../extensibility/debugger/reference/text-doc-attr-2.md): ドキュメントの属性を記述します。

- [THREADPROPERTY_FIELDS](../../../extensibility/debugger/reference/threadproperty-fields.md): スレッドについて取得する情報を指定します。

- [THREADSTATE](../../../extensibility/debugger/reference/threadstate.md): スレッドの状態を指定します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h、sh.h、または ee.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [API リファレンス](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)
