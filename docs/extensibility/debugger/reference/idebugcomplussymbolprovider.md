---
description: マネージド コードに固有のメソッドを持つ COM+ シンボル プロバイダーを表します。
title: IDebugComPlusSymbolProvider | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugComPlusSymbolProvider interface
ms.assetid: 5b98e908-fd15-49a6-9010-933c9b948085
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 13541766cdcd6cdd3a0a49673703d6abea82a5c7
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094173"
---
# <a name="idebugcomplussymbolprovider"></a>IDebugComPlusSymbolProvider
マネージド コードに固有のメソッドを持つ COM+ シンボル プロバイダーを表します。

## <a name="syntax"></a>構文

```
IDebugComPlusSymbolProvider : IDebugSymbolProvider
```

## <a name="notes-for-implementers"></a>実装側の注意
 式エバリュエーター (EE) に役立つインターフェイスと、デバッグ エンジン (DE) で使用することが意図されたインターフェイスの境界はありませんが、次のメソッドは、DE 開発者のみが対象となる可能性があります: AreSymbolsLoaded、GetAddressesInModuleFromPosition、GetEntryPoint、GetFunctionLineOffset、GetLocalVariableLayout、IsFunctionStale、LoadSymbols、LoadSymbolsFromStream、ReplaceSymbols、UnloadSymbols、および UpdateSymbols。

## <a name="methods"></a>メソッド
 このインターフェイスは、[IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md) インターフェイスのメソッドに加えて、次のメソッドを実装します。

|メソッド|説明|
|------------|-----------------|
|[AreSymbolsLoaded](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-aresymbolsloaded.md)|アプリケーション ドメイン識別子を指定して、指定したモジュールのデバッグ シンボルを読み込むかどうかを決定します。|
|[CreateTypeFromPrimitive](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-createtypefromprimitive.md)|指定したプリミティブ型から型を作成します。|
|[GetAddressesInModuleFromPosition](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getaddressesinmodulefromposition.md)|指定したモジュール内のドキュメントの位置をデバッグ アドレスの配列にマップします。|
|[GetArrayTypeFromAddress](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getarraytypefromaddress.md)|デバッグ アドレスを指定して、指定した配列に関する型情報を取得します。|
|[GetAssemblyName](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getassemblyname.md)|モジュールとアプリケーション ドメインを指定して、アセンブリの名前を取得します。|
|[GetAttributedClassesForLanguage](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getattributedclassesforlanguage.md)|指定されたプログラミング言語で実装されている、指定された属性を持つクラスを取得します。|
|[GetAttributedClassesinModule](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getattributedclassesinmodule.md)|指定されたモジュールの指定した属性を持つクラスを取得します。|
|[GetEntryPoint](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getentrypoint.md)|アプリケーション エントリ ポイントを取得します。|
|[GetFunctionLineOffset](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getfunctionlineoffset.md)|指定された行オフセットを表す関数内のアドレスを取得します。|
|[GetLocalVariablelayout](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getlocalvariablelayout.md)|一連のメソッドのローカル変数のレイアウトを取得します。|
|[GetNameFromToken](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getnamefromtoken.md)|メタデータ オブジェクトを指定して、指定したトークンに関連付けられている名前を返します。|
|[GetSymAttribute](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getsymattribute.md)|指定したモジュールの指定された親属性を持つデバッグ シンボルを取得します。|
|[GetSymUnmanagedReader](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getsymunmanagedreader.md)|アンマネージド コードによって使用されるシンボル リーダーを取得します。|
|[GetTypeFromAddress](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-gettypefromaddress.md)|デバッグ アドレスを指定してシンボル型を取得します。|
|[IsFunctionDeleted](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-isfunctiondeleted.md)|指定したデバッグ アドレスにある関数が削除されるかどうかを判断します。|
|[IsFunctionStale](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-isfunctionstale.md)|指定したデバッグ アドレスにある関数が古くなったと見なされるかどうかを判断します。|
|[IsHiddenCode](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-ishiddencode.md)|指定したデバッガー アドレスにあるコードが非表示かどうかを判断します。|
|[LoadSymbols](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-loadsymbols.md)|指定したデバッグ シンボルをメモリに読み込みます。|
|[LoadSymbolsFromStream](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-loadsymbolsfromstream.md)|データ ストリームを指定してデバッグ シンボルを読み込みます。|
|[ReplaceSymbols](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-replacesymbols.md)|現在のデバッグ シンボルを、指定したデータ ストリーム内のものに置き換えます。|
|[UnloadSymbols](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-unloadsymbols.md)|指定したモジュールのデバッグ シンボルをメモリからアンロードします。|
|[UpdateSymbols](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-updatesymbols.md)|メモリ内のデバッグ シンボルを、指定したデータ ストリームのもので更新します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Sh.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
