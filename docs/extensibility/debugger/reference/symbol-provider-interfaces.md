---
title: シンボルプロバイダーのインターフェイス |Microsoft Docs
description: この記事では、中断モード中に呼び出し履歴内の変数を評価する Visual Studio SDK のシンボル処理インターフェイスの説明にリンクしています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- interfaces, symbol handler
- symbol handler, interfaces
- symbol handler, evaluating variables
ms.assetid: 4201f10e-c9f7-4b38-bb45-40fe0082d5bf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7be44c623f93d9ecc4f9f5d4488c462ed8a9969d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061434"
---
# <a name="symbol-provider-interfaces"></a>シンボル プロバイダーのインターフェイス
次に、[!INCLUDE[vsipsdk](../../../extensibility/includes/vsipsdk_md.md)] のシンボル処理インターフェイスを示します。

## <a name="discussion"></a>ディスカッション
 これらのインターフェイスは、中断モード中に呼び出し履歴の変数を評価するために使用されます。 これらは、共通言語ランタイム シンボル プロバイダー (SP) に対してのみ実装されます。

|インターフェイス|実装先|説明|
|---------------|--------------------|-----------------|
|[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)|SP|項目のアドレスを表します。|
|[IDebugAddress2](../../../extensibility/debugger/reference/idebugaddress2.md)|SP|項目のアドレスを表し、プロセス ID にアクセスできるようにします。|
|[IDebugArrayField](../../../extensibility/debugger/reference/idebugarrayfield.md)|SP|配列シンボルまたは配列型を表します。|
|[IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)|SP|クラス シンボルまたはクラス型を表します。|
|[IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)|SP|マネージド コードに固有のメソッドを持つ COM+ シンボル プロバイダーを表します。|
|[IDebugComPlusSymbolProvider2](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2.md)|SP|マネージド コードに固有のメソッドを持つ COM+ シンボル プロバイダーを表し、**IDebugComPlusSymbolProvider** を拡張します。|
|[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)|SP|他のシンボルまたは型のコンテナーであるシンボルまたは型を表します。|
|[IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)|SP|シンボルにアタッチできるカスタム属性を表します。|
|[IDebugCustomAttributeQuery](../../../extensibility/debugger/reference/idebugcustomattributequery.md)|SP|メソッドまたは型でカスタム属性に対するクエリを表します。|
|[IDebugCustomAttributeQuery2](../../../extensibility/debugger/reference/idebugcustomattributequery2.md)|SP|シンボルのカスタム属性にアクセスできるようにします。|
|[IDebugDynamicField](../../../extensibility/debugger/reference/idebugdynamicfield.md)|SP|実行時に決定できる任意の型に応じた基本インターフェイス。|
|[IDebugDynamicFieldCOMPlus](../../../extensibility/debugger/reference/idebugdynamicfieldcomplus.md)|SP|[IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md) オブジェクトの動的フィールドを表します。|
|[IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)|SP|列挙型を表します。|
|[IDebugExtendedField](../../../extensibility/debugger/reference/idebugextendedfield.md)|SP|マネージド コード ジェネリックをサポートするために使用できるフィールドの型を拡張します。|
|[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)|SP|すべてのフィールドの基本クラスです。シンボルまたは型の説明を表します。|
|[IDebugGenericFieldDefinition](../../../extensibility/debugger/reference/idebuggenericfielddefinition.md)|SP|マネージド コード ジェネリック型のフィールドの定義を表します。|
|[IDebugGenericFieldInstance](../../../extensibility/debugger/reference/idebuggenericfieldinstance.md)|SP|マネージド コード ジェネリック型のフィールドのインスタンスを表します。|
|[IDebugGenericParamField](../../../extensibility/debugger/reference/idebuggenericparamfield.md)|SP|マネージド コード ジェネリック型のパラメーターを表します。|
|[IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)|SP|メソッドを表します。|
|[IDebugModOpt](../../../extensibility/debugger/reference/idebugmodopt.md)|SP|デバッグの省略可能な修飾子を表します。|
|[IDebugPointerField](../../../extensibility/debugger/reference/idebugpointerfield.md)|SP|ポインターを表します。|
|[IDebugPrimitiveTypeField](../../../extensibility/debugger/reference/idebugprimitivetypefield.md)|SP|[IDebugField](../../../extensibility/debugger/reference/idebugfield.md) インターフェイスからのプリミティブ型の列挙値を表します。|
|[IDebugPropertyField](../../../extensibility/debugger/reference/idebugpropertyfield.md)|SP|取得または設定できるマネージド コード クラスのプロパティを表します。|
|[IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)|SP|シンボルと型を提供するシンボル プロバイダーを表します。|
|[IDebugSymbolProviderDirect](../../../extensibility/debugger/reference/idebugsymbolproviderdirect.md)|SP|メタデータおよびコア シンボル インターフェイスに直接アクセスできるシンボル プロバイダーを表します。|
|[IDebugTypeFieldBuilder](../../../extensibility/debugger/reference/idebugtypefieldbuilder.md)|SP|型を表すフィールドを作成する機能を表します。|
|[IDebugTypeFieldBuilder2](../../../extensibility/debugger/reference/idebugtypefieldbuilder2.md)|SP|**IDebugTypeFieldBuilder** を拡張して、配列型を作成できるようにします。|
|[IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)|SP|[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) オブジェクトのコレクションを表します。|
|[IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)|SP|[IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md) オブジェクトのコレクションを表します。|
|[IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)|SP|[IDebugField](../../../extensibility/debugger/reference/idebugfield.md) オブジェクトのコレクションを表します。|

## <a name="see-also"></a>関連項目
- [API リファレンス](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)
