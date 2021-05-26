---
description: シンボル インスタンスのプロパティを記述します。
title: IDiaSymbol | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol interface
ms.assetid: 01ad328a-736c-4933-a9f8-c2ded19ddd8c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f0d48d0a3ed09ea98c9bb299b921409b711b695a
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635212"
---
# <a name="idiasymbol"></a>IDiaSymbol
シンボル インスタンスのプロパティを記述します。

## <a name="syntax"></a>構文

```
IDiaSymbol : IUnknown
```

## <a name="methods-in-alphabetical-order"></a>メソッド (アルファベット順)
次の表に、`IDiaSymbol` のメソッドを示します。

> [!NOTE]
> シンボルは、シンボルの型に応じて、これらのメソッドの一部でのみ意味のあるデータを返します。 メソッドから `S_OK` が返された場合、そのメソッドは意味のあるデータを返しています。

|メソッド|説明|
|------------|-----------------|
|[IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)|シンボルのすべての子を取得します。|
|[IDiaSymbol::findChildrenEx](../../debugger/debug-interface-access/idiasymbol-findchildrenex.md)|シンボルの子を取得します。 このメソッドは、[IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md) の拡張バージョンです。|
|[IDiaSymbol::findChildrenExByAddr](../../debugger/debug-interface-access/idiasymbol-findchildrenexbyaddr.md)|指定されたアドレスにあるシンボルの有効な子を取得します。|
|[IDiaSymbol::findChildrenExByRVA](../../debugger/debug-interface-access/idiasymbol-findchildrenexbyrva.md)|指定された相対仮想アドレス (RVA) にあるシンボルの有効な子を取得します。|
|[IDiaSymbol::findChildrenExByVA](../../debugger/debug-interface-access/idiasymbol-findchildrenexbyva.md)|指定された仮想アドレスにあるシンボルの有効な子を取得します。|
|[IDiaSymbol::findInlineFramesByAddr](../../debugger/debug-interface-access/idiasymbol-findinlineframesbyaddr.md)|指定されたアドレス上のすべてのインライン フレームをクライアントが反復処理できるようにする列挙型を取得します。|
|[IDiaSymbol::findInlineFramesByRVA](../../debugger/debug-interface-access/idiasymbol-findinlineframesbyrva.md)|指定された相対仮想アドレス (RVA) 上のすべてのインライン フレームをクライアントが反復処理できるようにする列挙型を取得します。|
|[IDiaSymbol::findInlineFramesByVA](../../debugger/debug-interface-access/idiasymbol-findinlineframesbyva.md)|指定された仮想アドレス (VA) 上のすべてのインライン フレームをクライアントが反復処理できるようにする列挙型を取得します。|
|[IDiaSymbol::findInlineeLines](../../debugger/debug-interface-access/idiasymbol-findinlineelines.md)|このシンボルに直接または間接的にインライン化されているすべての関数の行番号情報をクライアントが反復処理できるようにする列挙型を取得します。|
|[IDiaSymbol::findInlineeLinesByAddr](../../debugger/debug-interface-access/idiasymbol-findinlineelinesbyaddr.md)|指定されたアドレス範囲内でこのシンボルに直接または間接的にインライン化されているすべての関数の行番号情報をクライアントが反復処理できるようにする列挙型を取得します。|
|[IDiaSymbol::findInlineeLinesByRVA](../../debugger/debug-interface-access/idiasymbol-findinlineelinesbyrva.md)|指定された相対仮想アドレス (RVA) 内でこのシンボルに直接または間接的にインライン化されているすべての関数の行番号情報をクライアントが反復処理できるようにする列挙型を取得します。|
|[IDiaSymbol::findInlineeLinesByVA](../../debugger/debug-interface-access/idiasymbol-findinlineelinesbyva.md)|指定された仮想アドレス (VA) 内でこのシンボルに直接または間接的にインライン化されているすべての関数の行番号情報をクライアントが反復処理できるようにする列挙型を取得します。|
|[IDiaSymbol::findSymbolsByRVAForAcceleratorPointerTag](../../debugger/debug-interface-access/idiasymbol-findsymbolsbyrvaforacceleratorpointertag.md)|対応するタグ値を指定すると、このメソッドは、指定された相対仮想アドレスにあるこのスタブ関数に含まれているシンボルの列挙型を返します。|
|[IDiaSymbol::findSymbolsForAcceleratorPointerTag](../../debugger/debug-interface-access/idiasymbol-findsymbolsforacceleratorpointertag.md)|C++ AMP スタブ関数内のアクセラレータ ポインター タグの数を返します。|
|[IDiaSymbol::get_acceleratorPointerTags](../../debugger/debug-interface-access/idiasymbol-get-acceleratorpointertags.md)|C++ AMP アクセラレータ スタブ関数に対応するすべてのアクセラレータ ポインター タグ値を返します。|
|[IDiaSymbol::get_access](../../debugger/debug-interface-access/idiasymbol-get-access.md)|クラス メンバーのアクセス修飾子を取得します。|
|[IDiaSymbol::get_addressOffset](../../debugger/debug-interface-access/idiasymbol-get-addressoffset.md)|アドレスの場所のオフセット部分を取得します。|
|[IDiaSymbol::get_addressSection](../../debugger/debug-interface-access/idiasymbol-get-addresssection.md)|アドレスの場所のセクション部分を取得します。|
|[IDiaSymbol::get_addressTaken](../../debugger/debug-interface-access/idiasymbol-get-addresstaken.md)|別のシンボルがこのアドレスを参照しているかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_age](../../debugger/debug-interface-access/idiasymbol-get-age.md)|プログラム データベースの経過期間値を取得します。|
|[IDiaSymbol::get_arrayIndexType](../../debugger/debug-interface-access/idiasymbol-get-arrayindextype.md)|配列インデックスの型のシンボル識別子を取得します。|
|[IDiaSymbol::get_arrayIndexTypeId](../../debugger/debug-interface-access/idiasymbol-get-arrayindextypeid.md)|シンボルの配列インデックスの型識別子を取得します。|
|[IDiaSymbol::get_backEndMajor](../../debugger/debug-interface-access/idiasymbol-get-backendmajor.md)|バックエンド メジャー バージョン番号を取得します。|
|[IDiaSymbol::get_backEndMinor](../../debugger/debug-interface-access/idiasymbol-get-backendminor.md)|バックエンド マイナー バージョン番号を取得します。|
|[IDiaSymbol::get_backEndBuild](../../debugger/debug-interface-access/idiasymbol-get-backendbuild.md)|バックエンド ビルド番号を取得します。|
|[IDiaSymbol::get_baseDataOffset](../../debugger/debug-interface-access/idiasymbol-get-basedataoffset.md)|基本データ オフセットを取得します。|
|[IDiaSymbol::get_baseDataSlot](../../debugger/debug-interface-access/idiasymbol-get-basedataslot.md)|基本データ スロットを取得します。|
|[IDiaSymbol::get_baseSymbol](../../debugger/debug-interface-access/idiasymbol-get-basesymbol.md)|ポインターの基になるシンボルを取得します。|
|[IDiaSymbol::get_baseSymbolId](../../debugger/debug-interface-access/idiasymbol-get-basesymbolid.md)|ポインターの基になるシンボル ID を取得します。|
|[IDiaSymbol::get_baseType](../../debugger/debug-interface-access/idiasymbol-get-basetype.md)|単純型の型タグを取得します。|
|[IDiaSymbol::get_bitPosition](../../debugger/debug-interface-access/idiasymbol-get-bitposition.md)|場所のビット位置を取得します。|
|[IDiaSymbol::get_builtInKind](../../debugger/debug-interface-access/idiasymbol-get-builtinkind.md)|HLSL 型の組み込みの種類を取得します。|
|[IDiaSymbol::get_callingConvention](../../debugger/debug-interface-access/idiasymbol-get-callingconvention.md)|メソッドの呼び出し規則のインジケーターを返します。|
|[IDiaSymbol::get_classParent](../../debugger/debug-interface-access/idiasymbol-get-classparent.md)|シンボルのクラスの親への参照を取得します。|
|[IDiaSymbol::get_classParentId](../../debugger/debug-interface-access/idiasymbol-get-classparentid.md)|シンボルのクラスの親識別子を取得します。|
|[IDiaSymbol::get_code](../../debugger/debug-interface-access/idiasymbol-get-code.md)|シンボルがコード アドレスを参照しているかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_compilerGenerated](../../debugger/debug-interface-access/idiasymbol-get-compilergenerated.md)|シンボルがコンパイラで生成されたかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_compilerName](../../debugger/debug-interface-access/idiasymbol-get-compilername.md)|[コンパイル単位](../../debugger/debug-interface-access/compiland.md)の作成に使用されるコンパイラの名前を取得します。|
|[IDiaSymbol::get_constructor](../../debugger/debug-interface-access/idiasymbol-get-constructor.md)|ユーザー定義データ型にコンストラクターがあるかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_container](../../debugger/debug-interface-access/idiasymbol-get-container.md)|このシンボルの含んでいるシンボルを取得します。|
|[IDiaSymbol::get_constType](../../debugger/debug-interface-access/idiasymbol-get-consttype.md)|ユーザー定義データ型が定数であるかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_count](../../debugger/debug-interface-access/idiasymbol-get-count.md)|リストまたは配列内の項目の数を取得します。|
|[IDiaSymbol::get_countLiveRanges](../../debugger/debug-interface-access/idiasymbol-get-countliveranges.md)|ローカル シンボルに関連付けられている有効なアドレス範囲の数を取得します。|
|[IDiaSymbol::get_customCallingConvention](../../debugger/debug-interface-access/idiasymbol-get-customcallingconvention.md)|関数でカスタム呼び出し規則を使用しているかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_dataBytes](../../debugger/debug-interface-access/idiasymbol-get-databytes.md)|OEM シンボルのデータ バイト数を取得します。|
|[IDiaSymbol::get_dataKind](../../debugger/debug-interface-access/idiasymbol-get-datakind.md)|データ シンボルの変数の分類を取得します。|
|[IDiaSymbol::get_editAndContinueEnabled](../../debugger/debug-interface-access/idiasymbol-get-editandcontinueenabled.md)|コンパイルされたプログラムまたはユニットのエディット コンティニュ機能を記述するフラグを取得します。|
|[IDiaSymbol::get_farReturn](../../debugger/debug-interface-access/idiasymbol-get-farreturn.md)|関数で far return を使用しているかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_frontEndMajor](../../debugger/debug-interface-access/idiasymbol-get-frontendmajor.md)|フロントエンド メジャー バージョン番号を取得します。|
|[IDiaSymbol::get_frontEndMinor](../../debugger/debug-interface-access/idiasymbol-get-frontendminor.md)|フロントエンド マイナー バージョン番号を取得します。|
|[IDiaSymbol::get_frontEndBuild](../../debugger/debug-interface-access/idiasymbol-get-frontendbuild.md)|フロントエンド ビルド番号を取得します。|
|[IDiaSymbol::get_function](../../debugger/debug-interface-access/idiasymbol-get-function.md)|パブリック シンボルが関数を参照しているかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_guid](../../debugger/debug-interface-access/idiasymbol-get-guid.md)|シンボルの GUID を取得します。|
|[IDiaSymbol::get_hasAlloca](../../debugger/debug-interface-access/idiasymbol-get-hasalloca.md)|関数に `alloca` の呼び出しが含まれているかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_hasAssignmentOperator](../../debugger/debug-interface-access/idiasymbol-get-hasassignmentoperator.md)|ユーザー定義データ型に代入演算子が定義されているかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_hasCastOperator](../../debugger/debug-interface-access/idiasymbol-get-hascastoperator.md)|ユーザー定義データ型にキャスト演算子が定義されているかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_hasDebugInfo](../../debugger/debug-interface-access/idiasymbol-get-hasdebuginfo.md)|コンパイル単位にデバッグ情報が含まれているかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_hasEH](../../debugger/debug-interface-access/idiasymbol-get-haseh.md)|関数に C++ スタイルの例外ハンドラーがあるかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_hasEHa](../../debugger/debug-interface-access/idiasymbol-get-haseha.md)|関数に非同期例外ハンドラーがあるかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_hasInlAsm](../../debugger/debug-interface-access/idiasymbol-get-hasinlasm.md)|関数にインライン アセンブリがあるかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_hasLongJump](../../debugger/debug-interface-access/idiasymbol-get-haslongjump.md)|関数に longjmp コマンド (C スタイルの例外処理の一部) が含まれているかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_hasManagedCode](../../debugger/debug-interface-access/idiasymbol-get-hasmanagedcode.md)|モジュールにマネージド コードが含まれているかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_hasNestedTypes](../../debugger/debug-interface-access/idiasymbol-get-hasnestedtypes.md)|ユーザー定義データ型に入れ子にされた型定義があるかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_hasSecurityChecks](../../debugger/debug-interface-access/idiasymbol-get-hassecuritychecks.md)|関数またはコンパイル単位に、([/GS (バッファー セキュリティ チェック)](/cpp/build/reference/gs-buffer-security-check) コンパイラ スイッチを使用して) セキュリティ チェックがコンパイルされているかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_hasSEH](../../debugger/debug-interface-access/idiasymbol-get-hasseh.md)|関数に Win32 スタイルの構造化例外処理があるかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_hasSetJump](../../debugger/debug-interface-access/idiasymbol-get-hassetjump.md)|関数に setjmp コマンドが含まれているかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_indirectVirtualBaseClass](../../debugger/debug-interface-access/idiasymbol-get-indirectvirtualbaseclass.md)|ユーザー定義データ型が間接仮想基底クラスであるかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_InlSpec](../../debugger/debug-interface-access/idiasymbol-get-inlspec.md)|関数がインライン属性でマークされているかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_interruptReturn](../../debugger/debug-interface-access/idiasymbol-get-interruptreturn.md)|関数に割り込み命令からの戻りがあるかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_intro](../../debugger/debug-interface-access/idiasymbol-get-intro.md)|関数が基底クラスの仮想関数であるかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_isAcceleratorGroupSharedLocal](../../debugger/debug-interface-access/idiasymbol-get-isacceleratorgroupsharedlocal.md)|シンボルが C++ AMP アクセラレータ用にコンパイルされたコード内のグループ共有ローカル変数に対応しているかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_isAcceleratorPointerTagLiveRange](../../debugger/debug-interface-access/idiasymbol-get-isacceleratorpointertagliverange.md)|シンボルが C++ AMP アクセラレータ用にコンパイルされたコードに含まれるポインター変数のタグ コンポーネントの "*定義範囲シンボル*" に対応しているかどうかを示すフラグを取得します。 定義範囲シンボルは、アドレス範囲の変数の場所です。|
|[IDiaSymbol::get_isAcceleratorStubFunction](../../debugger/debug-interface-access/idiasymbol-get-isacceleratorstubfunction.md)|シンボルが、`parallel_for_each` 呼び出しに対応するアクセラレータ用にコンパイルされたシェーダーの最上位関数シンボルに対応しているかどうかを示します。|
|[IDiaSymbol::get_isAggregated](../../debugger/debug-interface-access/idiasymbol-get-isaggregated.md)|データが多数のシンボルの集計の一部であるかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_isCTypes](../../debugger/debug-interface-access/idiasymbol-get-isctypes.md)|シンボル ファイルに C 型が含まれているかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_isCVTCIL](../../debugger/debug-interface-access/idiasymbol-get-iscvtcil.md)|モジュールが共通中間言語 (CIL) からネイティブ コードに変換されたかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_isDataAligned](../../debugger/debug-interface-access/idiasymbol-get-isdataaligned.md)|ユーザー定義データ型の要素が特定の境界に整列されているかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_isHLSLData](../../debugger/debug-interface-access/idiasymbol-get-ishlsldata.md)|このシンボルがハイレベル シェーディング ランゲージ (HLSL) データを表しているかどうかを示します。|
|[IDiaSymbol::get_isHotpatchable](../../debugger/debug-interface-access/idiasymbol-get-ishotpatchable.md)|モジュールが [/hotpatch (ホットパッチ可能なイメージの作成)](/cpp/build/reference/hotpatch-create-hotpatchable-image) コンパイラ スイッチを使用してコンパイルされたかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_isLTCG](../../debugger/debug-interface-access/idiasymbol-get-isltcg.md)|マネージド コンパイル単位がリンカーの LTCG にリンクされているかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_isMatrixRowMajor](../../debugger/debug-interface-access/idiasymbol-get-ismatrixrowmajor.md)|マトリックスが行優先であるかどうかを示します。|
|[IDiaSymbol::get_isMSILNetmodule](../../debugger/debug-interface-access/idiasymbol-get-ismsilnetmodule.md)|マネージド コンパイル単位が (メタデータのみを含む) .netmodule であるかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_isMultipleInheritance](../../debugger/debug-interface-access/idiasymbol-get-ismultipleinheritance.md)|`this` ポインターが、多重継承を使用するデータ メンバーを指しているかどうかを示します。|
|[IDiaSymbol::get_isNaked](../../debugger/debug-interface-access/idiasymbol-get-isnaked.md)|関数に [naked](/cpp/cpp/naked-cpp) 属性があるかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_isOptimizedAway](../../debugger/debug-interface-access/idiasymbol-get-isoptimizedaway.md)|この変数を最適化により削除するかどうかを示します。|
|[IDiaSymbol::get_isPointerBasedOnSymbolValue](../../debugger/debug-interface-access/idiasymbol-get-ispointerbasedonsymbolvalue.md)|`this` ポインターがシンボル値に基づいているかどうかを示します。|
|[IDiaSymbol::get_isPointerToDataMember](../../debugger/debug-interface-access/idiasymbol-get-ispointertodatamember.md)|このシンボルがデータ メンバーへのポインターであるかどうかを示します。|
|[IDiaSymbol::get_isPointerToMemberFunction](../../debugger/debug-interface-access/idiasymbol-get-ispointertomemberfunction.md)|このシンボルがメンバー関数へのポインターであるかどうかを示します。|
|[IDiaSymbol::get_isReturnValue](../../debugger/debug-interface-access/idiasymbol-get-isreturnvalue.md)|変数に戻り値を格納するかどうかを示します。|
|[IDiaSymbol::get_isSdl](../../debugger/debug-interface-access/idiasymbol-get-issdl.md)|モジュールが /SDL オプションを使用してコンパイルされているかどうかを示します。|
|[IDiaSymbol::get_isSingleInheritance](../../debugger/debug-interface-access/idiasymbol-get-issingleinheritance.md)|`this` ポインターが、単一継承を使用するデータ メンバーを指しているかどうかを示します。|
|[IDiaSymbol::get_isSplitted](../../debugger/debug-interface-access/idiasymbol-get-issplitted.md)|データが個々のシンボルの集計に分割されているかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_isStatic](../../debugger/debug-interface-access/idiasymbol-get-isstatic.md)|関数またはサンク レイヤーが静的であるかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_isStripped](../../debugger/debug-interface-access/idiasymbol-get-isstripped.md)|プライベート シンボルがシンボル ファイルから削除されているかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_isVirtualInheritance](../../debugger/debug-interface-access/idiasymbol-get-isvirtualinheritance.md)|`this` ポインターが、仮想継承を使用するデータ メンバーを指しているかどうかを示します。|
|[IDiaSymbol::get_language](../../debugger/debug-interface-access/idiasymbol-get-language.md)|ソースの言語を取得します。|
|[IDiaSymbol::get_length](../../debugger/debug-interface-access/idiasymbol-get-length.md)|このシンボルによって表されるオブジェクトで使用されるメモリのバイト数を取得します。|
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|シンボルの構文上の親への参照を取得します。|
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|シンボルの構文上の親識別子を取得します。|
|[IDiaSymbol::get_libraryName](../../debugger/debug-interface-access/idiasymbol-get-libraryname.md)|オブジェクトの読み込み元のライブラリまたはオブジェクト ファイルのファイル名を取得します。|
|[IDiaSymbol::get_liveRangeLength](../../debugger/debug-interface-access/idiasymbol-get-liverangelength.md)|ローカル シンボルが有効なアドレス範囲の長さを返します。|
|[IDiaSymbol::get_liveRangeStartAddressSection](../../debugger/debug-interface-access/idiasymbol-get-liverangestartaddresssection.md)|ローカル シンボルが有効な開始アドレス範囲のセクション部分を返します。|
|[IDiaSymbol::get_liveRangeStartAddressOffset](../../debugger/debug-interface-access/idiasymbol-get-liverangestartaddressoffset.md)|ローカル シンボルが有効な開始アドレス範囲のオフセット部分を返します。|
|[IDiaSymbol::get_liveRangeStartRelativeVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-liverangestartrelativevirtualaddress.md)|ローカル シンボルが有効なアドレス範囲の先頭を返します。|
|[IDiaSymbol::get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)|データ シンボルの場所の種類を取得します。|
|[IDiaSymbol::get_lowerBound](../../debugger/debug-interface-access/idiasymbol-get-lowerbound.md)|FORTRAN 配列次元の下限を取得します。|
|[IDiaSymbol::get_lowerBoundId](../../debugger/debug-interface-access/idiasymbol-get-lowerboundid.md)|FORTRAN 配列次元の下限のシンボル識別子を取得します。|
|[IDiaSymbol::get_machineType](../../debugger/debug-interface-access/idiasymbol-get-machinetype.md)|ターゲット CPU の種類を取得します。|
|[IDiaSymbol::get_managed](../../debugger/debug-interface-access/idiasymbol-get-managed.md)|シンボルがマネージド コードを参照しているかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_memorySpaceKind](../../debugger/debug-interface-access/idiasymbol-get-memoryspacekind.md)|メモリ領域の種類を取得します。|
|[IDiaSymbol::get_msil](../../debugger/debug-interface-access/idiasymbol-get-msil.md)|シンボルが Microsoft Intermediate Language (MSIL) コードを参照しているかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_name](../../debugger/debug-interface-access/idiasymbol-get-name.md)|シンボルの名前を取得します。|
|[IDiaSymbol::get_nested](../../debugger/debug-interface-access/idiasymbol-get-nested.md)|ユーザー定義データ型が入れ子になっているかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_noInline](../../debugger/debug-interface-access/idiasymbol-get-noinline.md)|関数が [noinline](/cpp/cpp/noinline) 属性でマークされているかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_noReturn](../../debugger/debug-interface-access/idiasymbol-get-noreturn.md)|関数が [noreturn](/cpp/cpp/noreturn) 属性で宣言されているかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_noStackOrdering](../../debugger/debug-interface-access/idiasymbol-get-nostackordering.md)|スタック バッファー チェックの一環としてスタックの順序付けを実行できなかったかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_notReached](../../debugger/debug-interface-access/idiasymbol-get-notreached.md)|関数またはラベルに到達することがないかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_numberOfAcceleratorPointerTags](../../debugger/debug-interface-access/idiasymbol-get-numberofacceleratorpointertags.md)|C++ AMP スタブ関数内のアクセラレータ ポインター タグの数を返します。|
|[IDiaSymbol::get_numberOfModifiers](../../debugger/debug-interface-access/idiasymbol-get-numberofmodifiers.md)|元の型に適用されている修飾子の数を取得します。|
|[IDiaSymbol::get_numberOfRegisterIndices](../../debugger/debug-interface-access/idiasymbol-get-numberofregisterindices.md)|レジスタ インデックスの数を取得します。|
|[IDiaSymbol::get_numberOfRows](../../debugger/debug-interface-access/idiasymbol-get-numberofrows.md)|マトリックス内の行の数を取得します。|
|[IDiaSymbol::get_numberOfColumns](../../debugger/debug-interface-access/idiasymbol-get-numberofcolumns.md)|マトリックス内の列の数を取得します。|
|[IDiaSymbol::get_objectFileName](../../debugger/debug-interface-access/idiasymbol-get-objectfilename.md)|オブジェクト ファイル名を取得します。|
|[IDiaSymbol::get_objectPointerType](../../debugger/debug-interface-access/idiasymbol-get-objectpointertype.md)|クラス メソッドのオブジェクト ポインターの型を取得します。|
|[IDiaSymbol::get_oemId](../../debugger/debug-interface-access/idiasymbol-get-oemid.md)|シンボルの `oemId` 値を取得します。|
|[IDiaSymbol::get_oemSymbolId](../../debugger/debug-interface-access/idiasymbol-get-oemsymbolid.md)|シンボルの `oemSymbolId` 値を取得します。|
|[IDiaSymbol::get_offset](../../debugger/debug-interface-access/idiasymbol-get-offset.md)|シンボルの場所のオフセットを取得します。|
|[IDiaSymbol::get_optimizedCodeDebugInfo](../../debugger/debug-interface-access/idiasymbol-get-optimizedcodedebuginfo.md)|関数またはラベルに、最適化されたコードとデバッグ情報が含まれているかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_overloadedOperator](../../debugger/debug-interface-access/idiasymbol-get-overloadedoperator.md)|ユーザー定義データ型にオーバーロードされた演算子があるかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_packed](../../debugger/debug-interface-access/idiasymbol-get-packed.md)|ユーザー定義データ型がパックされているかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_platform](../../debugger/debug-interface-access/idiasymbol-get-platform.md)|プログラムまたはコンパイル単位がコンパイルされたプラットフォームの種類を取得します。|
|[IDiaSymbol::get_pure](../../debugger/debug-interface-access/idiasymbol-get-pure.md)|関数が純粋仮想であるかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_rank](../../debugger/debug-interface-access/idiasymbol-get-rank.md)|FORTRAN 多次元配列のランクを取得します。|
|[IDiaSymbol::get_reference](../../debugger/debug-interface-access/idiasymbol-get-reference.md)|ポインターの型が参照であるかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_registerId](../../debugger/debug-interface-access/idiasymbol-get-registerid.md)|場所のレジスタ指定子を取得します。|
|[IDiaSymbol::get_registerType](../../debugger/debug-interface-access/idiasymbol-get-registertype.md)|レジスタの種類を取得します。|
|[IDiaSymbol::get_relativeVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-relativevirtualaddress.md)|場所の相対仮想アドレス (RVA) を取得します。|
|[IDiaSymbol::get_restrictedType](../../debugger/debug-interface-access/idiasymbol-get-restrictedtype.md)|`this` ポインターに制限ありのフラグが設定されているかどうかを示します。|
|[IDiaSymbol::get_samplerSlot](../../debugger/debug-interface-access/idiasymbol-get-samplerslot.md)|サンプラー スロットを取得します。|
|[IDiaSymbol::get_scoped](../../debugger/debug-interface-access/idiasymbol-get-scoped.md)|ユーザー定義データ型が非グローバル構文スコープに出現するかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_signature](../../debugger/debug-interface-access/idiasymbol-get-signature.md)|シンボルのシグネチャ値を取得します。|
|[IDiaSymbol::get_sizeInUdt](../../debugger/debug-interface-access/idiasymbol-get-sizeinudt.md)|ユーザー定義型のメンバーのサイズを取得します。|
|[IDiaSymbol::get_slot](../../debugger/debug-interface-access/idiasymbol-get-slot.md)|位置のスロット番号を取得します。|
|[IDiaSymbol::get_sourceFileName](../../debugger/debug-interface-access/idiasymbol-get-sourcefilename.md)|ソース ファイルのファイル名を取得します。|
|[IDiaSymbol::getSrcLineOnTypeDefn](../../debugger/debug-interface-access/idiasymbol-getsrclineontypedefn.md)|指定されたユーザー定義型が定義されている場所を示すソース ファイルと行番号を取得します。|
|[IDiaSymbol::get_stride](../../debugger/debug-interface-access/idiasymbol-get-stride.md)|行列またはストライド配列のストライドを取得します。|
|[IDiaSymbol::get_subType](../../debugger/debug-interface-access/idiasymbol-get-subtype.md)|サブタイプを取得します。|
|[IDiaSymbol::get_subTypeId](../../debugger/debug-interface-access/idiasymbol-get-subtypeid.md)|サブタイプ ID を取得します。|
|[IDiaSymbol::get_symbolsFileName](../../debugger/debug-interface-access/idiasymbol-get-symbolsfilename.md)|シンボルの読み込み元のファイルの名前を取得します。|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|一意のシンボル識別子を取得します。|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|シンボルの型の分類子を取得します。|
|[IDiaSymbol::get_targetOffset](../../debugger/debug-interface-access/idiasymbol-get-targetoffset.md)|サンク ターゲットのオフセット セクションを取得します。|
|[IDiaSymbol::get_targetRelativeVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-targetrelativevirtualaddress.md)|サンク ターゲットの相対仮想アドレス (RVA) を取得します。|
|[IDiaSymbol::get_targetSection](../../debugger/debug-interface-access/idiasymbol-get-targetsection.md)|サンク ターゲットのアドレス セクションを取得します。|
|[IDiaSymbol::get_targetVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-targetvirtualaddress.md)|サンク ターゲットの仮想アドレス (VA) を取得します。|
|[IDiaSymbol::get_textureSlot](../../debugger/debug-interface-access/idiasymbol-get-textureslot.md)|テクスチャ スロットを取得します。|
|[IDiaSymbol::get_thisAdjust](../../debugger/debug-interface-access/idiasymbol-get-thisadjust.md)|メソッドの論理 `this` adjustor を取得します。|
|[IDiaSymbol::get_thunkOrdinal](../../debugger/debug-interface-access/idiasymbol-get-thunkordinal.md)|関数のサンクの種類を取得します。|
|[IDiaSymbol::get_timeStamp](../../debugger/debug-interface-access/idiasymbol-get-timestamp.md)|基になる実行可能ファイルのタイムスタンプを取得します。|
|[IDiaSymbol::get_token](../../debugger/debug-interface-access/idiasymbol-get-token.md)|マネージド関数または変数のメタデータ トークンを取得します。|
|[IDiaSymbol::get_type](../../debugger/debug-interface-access/idiasymbol-get-type.md)|関数シグネチャへの参照を取得します。|
|[IDiaSymbol::get_typeId](../../debugger/debug-interface-access/idiasymbol-get-typeid.md)|シンボルの型識別子を取得します。|
|[IDiaSymbol::get_types](../../debugger/debug-interface-access/idiasymbol-get-types.md)|このシンボルについて、コンパイラ固有の型の値の配列を取得します。|
|[IDiaSymbol::get_typeIds](../../debugger/debug-interface-access/idiasymbol-get-typeids.md)|このシンボルについて、コンパイラ固有の型識別子の値の配列を取得します。|
|[IDiaSymbol::get_uavSlot](../../debugger/debug-interface-access/idiasymbol-get-uavslot.md)|uav スロットを取得します。|
|[IDiaSymbol::get_udtKind](../../debugger/debug-interface-access/idiasymbol-get-udtkind.md)|さまざまなユーザー定義型 (UDT) を取得します。|
|[IDiaSymbol::get_unalignedType](../../debugger/debug-interface-access/idiasymbol-get-unalignedtype.md)|ユーザー定義データ型が整列されていないかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_undecoratedName](../../debugger/debug-interface-access/idiasymbol-get-undecoratedname.md)|C++ の装飾 (リンケージ) 名の非装飾名を取得します。|
|[IDiaSymbol::get_undecoratedNameEx](../../debugger/debug-interface-access/idiasymbol-get-undecoratednameex.md)|拡張フィールドの値に基づいて非装飾名を取得する、`get_undecoratedName` メソッドの拡張機能。|
|[IDiaSymbol::get_unmodifiedTypeId](../../debugger/debug-interface-access/idiasymbol-get-unmodifiedtypeid.md)|元の (変更されていない) 型の ID を取得します。|
|[IDiaSymbol::get_upperBound](../../debugger/debug-interface-access/idiasymbol-get-upperbound.md)|FORTRAN 配列次元の上限を取得します。|
|[IDiaSymbol::get_upperBoundId](../../debugger/debug-interface-access/idiasymbol-get-upperboundid.md)|FORTRAN 配列次元の上限のシンボル識別子を取得します。|
|[IDiaSymbol::get_value](../../debugger/debug-interface-access/idiasymbol-get-value.md)|定数の値を取得します。|
|[IDiaSymbol::get_virtual](../../debugger/debug-interface-access/idiasymbol-get-virtual.md)|関数が仮想であるかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_virtualAddress](../../debugger/debug-interface-access/idiasymbol-get-virtualaddress.md)|場所の仮想アドレス (VA) を取得します。|
|[IDiaSymbol::get_virtualBaseClass](../../debugger/debug-interface-access/idiasymbol-get-virtualbaseclass.md)|ユーザー定義データ型が仮想基底クラスであるかどうかを示すフラグを取得します。|
|[IDiaSymbol::get_virtualBaseDispIndex](../../debugger/debug-interface-access/idiasymbol-get-virtualbasedispindex.md)|仮想ベースの変位テーブルのインデックスを取得します。|
|[IDiaSymbol::get_virtualBaseOffset](../../debugger/debug-interface-access/idiasymbol-get-virtualbaseoffset.md)|仮想関数の仮想関数テーブル内のオフセットを取得します。|
|[IDiaSymbol::get_virtualBasePointerOffset](../../debugger/debug-interface-access/idiasymbol-get-virtualbasepointeroffset.md)|仮想ベース ポインターのオフセットを取得します。|
|[IDiaSymbol::get_virtualBaseTableType](../../debugger/debug-interface-access/idiasymbol-get-virtualbasetabletype.md)|仮想ベース テーブル ポインターの型を取得します。|
|[IDiaSymbol::get_virtualTableShape](../../debugger/debug-interface-access/idiasymbol-get-virtualtableshape.md)|ユーザー定義型の仮想テーブルの型のシンボル インターフェイスを取得します。|
|[IDiaSymbol::get_virtualTableShapeId](../../debugger/debug-interface-access/idiasymbol-get-virtualtableshapeid.md)|シンボルの仮想テーブル図形識別子を取得します。|
|[IDiaSymbol::get_volatileType](../../debugger/debug-interface-access/idiasymbol-get-volatiletype.md)|ユーザー定義データ型が揮発性かどうかを示すフラグを取得します。|

## <a name="remarks"></a>解説

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
このインターフェイスを取得するには、次のいずれかのメソッドを呼び出します。

- [IDiaEnumSymbols::Item](../../debugger/debug-interface-access/idiaenumsymbols-item.md)

- [IDiaEnumSymbols::Next](../../debugger/debug-interface-access/idiaenumsymbols-next.md)

- [IDiaEnumSymbolsByAddr::Next](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr-next.md)

- [IDiaEnumSymbolsByAddr::Prev](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr-prev.md)

- [IDiaEnumSymbolsByAddr::symbolByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr-symbolbyaddr.md)

- [IDiaEnumSymbolsByAddr::symbolByRVA](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr-symbolbyrva.md)

- [IDiaEnumSymbolsByAddr::symbolByVA](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr-symbolbyva.md)

- [IDiaSession::findSymbolByAddr](../../debugger/debug-interface-access/idiasession-findsymbolbyaddr.md)

- [IDiaSession::findSymbolByRVA](../../debugger/debug-interface-access/idiasession-findsymbolbyrva.md)

- [IDiaSession::findSymbolByRVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyrvaex.md)

- [IDiaSession::findSymbolByVA](../../debugger/debug-interface-access/idiasession-findsymbolbyva.md)

- [IDiaSession::findSymbolByVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyvaex.md)

- [IDiaSession::findSymbolByToken](../../debugger/debug-interface-access/idiasession-findsymbolbytoken.md)

- [IDiaSession::symbolById](../../debugger/debug-interface-access/idiasession-symbolbyid.md)

- [IDiaStackWalkHelper::symbolForVA](../../debugger/debug-interface-access/idiastackwalkhelper-symbolforva.md)

- [IDiaSymbol::get_types](../../debugger/debug-interface-access/idiasymbol-get-types.md)

## <a name="example"></a>例
この例は、指定された相対仮想アドレスにある関数のローカル変数を表示する方法を示しています。 また、さまざまな型のシンボルが相互にどのように関連しているのかも示しています。

> [!NOTE]
> `CDiaBSTR` は、`BSTR` をラップし、インスタンス化がスコープ外になったときに文字列の解放を自動的に処理するクラスです。

```C++
void DumpLocalVars( DWORD rva, IDiaSession *pSession )
{
    CComPtr< IDiaSymbol > pBlock;
    if ( FAILED( psession->findSymbolByRVA( rva, SymTagBlock, &pBlock ) ) )
    {
        Fatal( "Failed to find symbols by RVA" );
    }
    CComPtr< IDiaSymbol > pscope;
    for ( ; pBlock != NULL; )
    {
        CComPtr< IDiaEnumSymbols > pEnum;
        // local data search
        if ( FAILED( pBlock->findChildren( SymTagNull, NULL, nsNone, &pEnum ) ) )
        {
            Fatal( "Local scope findChildren failed" );
        }
        CComPtr< IDiaSymbol > pSymbol;
        DWORD tag;
        DWORD celt;
        while ( pEnum != NULL &&
                SUCCEEDED( pEnum->Next( 1, &pSymbol, &celt ) ) &&
                celt == 1)
        {
            pSymbol->get_symTag( &tag );
            if ( tag == SymTagData )
            {
                CDiaBSTR name;
                DWORD    kind;
                pSymbol->get_name( &name );
                pSymbol->get_dataKind( &kind );
                if ( name != NULL )
                    wprintf_s( L"\t%s (%s)\n", name, szDataKinds[ kind ] );
            }
            else if ( tag == SymTagAnnotation )
            {
                CComPtr< IDiaEnumSymbols > pValues;
                // local data search
                wprintf_s( L"\tAnnotation:\n" );
                if ( FAILED( pSymbol->findChildren( SymTagNull, NULL, nsNone, &pValues ) ) )
                    Fatal( "Annotation findChildren failed" );
                pSymbol = NULL;
                while ( pValues != NULL &&
                        SUCCEEDED( pValues->Next( 1, &pSymbol, &celt ) ) &&
                        celt == 1 )
                {
                    CComVariant value;
                    if ( pSymbol->get_value( &value ) != S_OK )
                        Fatal( "No value for annotation data." );
                    wprintf_s( L"\t\t%ws\n", value.bstrVal );
                    pSymbol = NULL;
                }
            }
            pSymbol = NULL;
        }
        pBlock->get_symTag( &tag );
        if ( tag == SymTagFunction )    // stop when at function scope
            break;
        // move to lexical parent
        CComPtr< IDiaSymbol > pParent;
        if ( SUCCEEDED( pBlock->get_lexicalParent( &pParent ) )
            && pParent != NULL ) {
            pBlock = pParent;
        }
        else
        {
            Fatal( "Finding lexical parent failed." );
        }
    };
}
```

## <a name="requirements"></a>必要条件
`Header:` Dia2.h

ライブラリ: diaguids.lib

DLL: msdia80.dll

## <a name="see-also"></a>関連項目
- [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaEnumSymbolsByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [シンボル型のクラス階層](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)
- [シンボルとシンボル タグ](../../debugger/debug-interface-access/symbols-and-symbol-tags.md)
- [コンパイル単位](../../debugger/debug-interface-access/compiland.md)
