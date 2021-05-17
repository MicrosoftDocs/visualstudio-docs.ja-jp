---
title: デバッグ用の SDK ヘルパー | Microsoft Docs
description: デバッグ エンジン、式エバリュエーター、シンボル プロバイダーを C++ で実装するためのグローバル ヘルパー関数である関数および宣言について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- dbgmetric.lib
- registry, Debugging SDK
- Debugging SDK, registry locations
- dbgmetric.h
- metrics [Debugging SDK]
ms.assetid: 80a52e93-4a04-4ab2-8adc-a7847c2dc20b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4f5a34513130ea112393ffbb4935093bcea6e797
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061538"
---
# <a name="sdk-helpers-for-debugging"></a>デバッグ用の SDK ヘルパー
これらの関数および宣言は、デバッグ エンジン、式エバリュエーター、シンボル プロバイダーを C++ で実装するためのグローバル ヘルパー関数です。

> [!NOTE]
> 現時点では、これらの関数と宣言のマネージド バージョンはありません。

## <a name="overview"></a>概要
 デバッグ エンジン、式エバリュエーター、およびシンボル プロバイダーを Visual Studio で使用するためには、それらを登録する必要があります。 これを行うには、レジストリ サブキーとエントリを設定します。これは "メトリックの設定" とも呼ばれます。 次のグローバル関数は、これらのメトリックを更新するプロセスを容易にするように設計されています。 これらの関数によって更新される各レジストリ サブキーのレイアウトを確認するには、レジストリの場所に関するセクションを参照してください。

## <a name="general-metric-functions"></a>汎用メトリック関数
 これらは、デバッグ エンジンで使用されている一般的な関数です。 式エバリュエーターおよびシンボル プロバイダー用の特殊な関数については、後で詳しく説明します。

### <a name="getmetric-method"></a>GetMetric メソッド
 レジストリからメトリック値を読み取ります。

```cpp
HRESULT GetMetric(
   LPCWSTR pszMachine,
   LPCWSTR pszType,
   REFGUID guidSection,
   LPCWSTR pszMetric,
   DWORD * pdwValue,
   LPCWSTR pszAltRoot
);
```

|パラメーター|説明|
|---------------|-----------------|
|pszMachine|[in] 書き込まれるレジスタを持つ可能性のあるリモート コンピューターの名前 (`NULL` はローカル コンピューター)。|
|pszType|[in] メトリックの種類の 1 つ。|
|guidSection|[in] 特定のエンジン、エバリュエーター、例外などの GUID。これにより、特定の要素のメトリック タイプの下にサブセクションが指定されます。|
|pszMetric|[in] 取得されるメトリック。 これは、特定の値の名前に対応します。|
|pdwValue|[in] メトリックからの値の格納場所です。 DWORD (この例)、BSTR、GUID、または GUID の配列を返すことのできる数種類の GetMetric があります。|
|pszAltRoot|[in] 使用する代替レジストリ ルート。 既定値を使用するように `NULL` を設定します。|

### <a name="setmetric-method"></a>SetMetric メソッド
 指定されたメトリック値をレジストリで設定します。

```cpp
HRESULT SetMetric(
         LPCWSTR pszType,
         REFGUID guidSection,
         LPCWSTR pszMetric,
   const DWORD   dwValue,
         bool    fUserSpecific,
         LPCWSTR pszAltRoot
);
```

|パラメーター|説明|
|---------------|-----------------|
|pszType|[in] メトリックの種類の 1 つ。|
|guidSection|[in] 特定のエンジン、エバリュエーター、例外などの GUID。これにより、特定の要素のメトリック タイプの下にサブセクションが指定されます。|
|pszMetric|[in] 取得されるメトリック。 これは、特定の値の名前に対応します。|
|dwValue|[in] メトリックの値の格納場所。 DWORD (この例)、BSTR、GUID、または GUID の配列を格納できる数種類の SetMetric があります。|
|fUserSpecific|[in] メトリックがユーザー固有である場合、ローカル コンピューター ハイブではなくユーザーのハイブに書き込まれる必要がある場合は TRUE。|
|pszAltRoot|[in] 使用する代替レジストリ ルート。 既定値を使用するように `NULL` を設定します。|

### <a name="removemetric-method"></a>RemoveMetric メソッド
 指定されたメトリック値をレジストリから削除します。

```cpp
HRESULT RemoveMetric(
   LPCWSTR pszType,
   REFGUID guidSection,
   LPCWSTR pszMetric,
   LPCWSTR pszAltRoot
);
```

|パラメーター|説明|
|---------------|-----------------|
|pszType|[in] メトリックの種類の 1 つ。|
|guidSection|[in] 特定のエンジン、エバリュエーター、例外などの GUID。これにより、特定の要素のメトリック タイプの下にサブセクションが指定されます。|
|pszMetric|[in] 削除するメトリック。 これは、特定の値の名前に対応します。|
|pszAltRoot|[in] 使用する代替レジストリ ルート。 既定値を使用するように `NULL` を設定します。|

### <a name="enummetricsections-method"></a>EnumMetricSections Method
 レジストリ内のさまざまなメトリック セクションを列挙します。

```cpp
HRESULT EnumMetricSections(
   LPCWSTR pszMachine,
   LPCWSTR pszType,
   GUID *  rgguidSections,
   DWORD * pdwSize,
   LPCWSTR pszAltRoot
);
```

|パラメーター|説明|
|---------------|-----------------|
|pszMachine|[in] 書き込まれるレジスタを持つ可能性のあるリモート コンピューターの名前 (`NULL` はローカル コンピューター)。|
|pszType|[in] メトリックの種類の 1 つ。|
|rgguidSections|[in、out] 入力される GUID の事前に割り当てられた配列。|
|pdwSize|[in] `rgguidSections` 配列に格納できる GUID の最大数。|
|pszAltRoot|[in] 使用する代替レジストリ ルート。 既定値を使用するように `NULL` を設定します。|

## <a name="expression-evaluator-functions"></a>式エバリュエーター関数

|機能|説明|
|--------------|-----------------|
|GetEEMetric|レジストリからメトリック値を読み取ります。|
|SetEEMetric|指定されたメトリック値をレジストリで設定します。|
|RemoveEEMetric|指定されたメトリック値をレジストリから削除します。|
|GetEEMetricFile|指定したメトリックからファイル名を取得して読み込み、ファイルの内容を文字列として返します。|

## <a name="exception-functions"></a>例外関数

|機能|説明|
|--------------|-----------------|
|GetExceptionMetric|レジストリからメトリック値を読み取ります。|
|SetExceptionMetric|指定されたメトリック値をレジストリで設定します。|
|RemoveExceptionMetric|指定されたメトリック値をレジストリから削除します。|
|RemoveAllExceptionMetrics|すべての例外メトリックをレジストリから削除します。|

## <a name="symbol-provider-functions"></a>シンボル プロバイダー関数

|機能|説明|
|--------------|-----------------|
|GetSPMetric|レジストリからメトリック値を読み取ります。|
|SetSPMetric|指定されたメトリック値をレジストリで設定します。|
|RemoveSPMetric|指定されたメトリック値をレジストリから削除します。|

## <a name="enumeration-functions"></a>列挙関数

|機能|説明|
|--------------|-----------------|
|EnumMetricSections|指定したメトリックの種類に該当するすべてのメトリックを列挙します。|
|EnumDebugEngine|登録されているデバッグ エンジンを列挙します。|
|EnumEEs|登録されている式エバリュエーターを列挙します。|
|EnumExceptionMetrics|すべての例外メトリックを列挙します。|

## <a name="metric-definitions"></a>メトリック定義
 定義済みのメトリック名には、これらの定義を使用できます。 名前は、さまざまなレジストリ キーおよび値の名前に対応し、たとえば `extern LPCWSTR metrictypeEngine` のようなワイド文字列としてすべてが定義されます。

|定義済みのメトリックの種類|説明: 基本キーの対象|
|-----------------------------|---------------------------------------|
|metrictypeEngine|すべてのデバッグ エンジンのメトリック。|
|metrictypePortSupplier|すべてのポート サプライヤー メトリック。|
|metrictypeException|すべての例外メトリック。|
|metricttypeEEExtension|すべての式エバリュエーター拡張機能。|

|デバッグ エンジンのプロパティ|説明|
|-----------------------------|-----------------|
|metricAddressBP|アドレスのブレークポイントのサポートを示すには、0 以外に設定します。|
|metricAlwaysLoadLocal|常にデバッグ エンジンをローカルに読み込むには、0 以外に設定します。|
|metricLoadInDebuggeeSession|不使用|
|metricLoadedByDebuggee|デバッグ エンジンが常にデバッグ中のプログラムを使用して読み込まれることを示すには、0 以外に設定します。|
|metricAttach|既存のプログラムへの添付ファイルのサポートを示すには、0 以外に設定します。|
|metricCallStackBP|呼び出し履歴ブレークポイントのサポートを示すには、0 以外に設定します。|
|metricConditionalBP|条件付きブレークポイントのサポートを示すには、0 以外に設定します。|
|metricDataBP|データの変更でのブレークポイントの設定のサポートを示すには、0 以外に設定します。|
|metricDisassembly|逆アセンブリの一覧の作成のサポートを示すには、0 以外に設定します。|
|metricDumpWriting|ダンプ書き込み (出力デバイスへのメモリのダンプ) のサポートを示すには、0 以外に設定します。|
|metricENC|エディット コンティニュのサポートを示すには、0 以外に設定します。 **注:** カスタム デバッグ エンジンでは、これを設定しないようにするか、常に 0 に設定する必要があります。|
|metricExceptions|例外のサポートを示すには、0 以外に設定します。|
|metricFunctionBP|名前付きブレークポイント (特定の関数名が呼び出されたときに中断するブレークポイント) のサポートを示すには、0 以外に設定します。|
|metricHitCountBP|"ヒット ポイント" ブレークポイント (特定の回数に達した後にのみトリガーされるブレークポイント) の設定のサポートを示すには、0 以外の値に設定します。|
|metricJITDebug|Just-In-Time デバッグ (実行中のプロセスで例外が発生したときにデバッガーが起動されます) のサポートを示すには、0 以外の値に設定します。|
|metricMemory|不使用|
|metricPortSupplier|ポート サプライヤーが実装されている場合は、これをその CLSID に設定します。|
|metricRegisters|不使用|
|metricSetNextStatement|次のステートメント (これは中間ステートメントの実行をスキップします) を設定するためのサポートを示すには、0 以外に設定します。|
|metricSuspendThread|スレッド実行を中断するためのサポートを示すには、0 以外に設定します。|
|metricWarnIfNoSymbols|記号がない場合にユーザーに通知する必要があることを示すには、0 以外に設定します。|
|metricProgramProvider|プログラム プロバイダーの CLSID にこれを設定します。|
|metricAlwaysLoadProgramProviderLocal|プログラム プロバイダーを常にローカルで読み込む必要があることを示すには、これを 0 以外に設定します。|
|metricEngineCanWatchProcess|プログラム プロバイダーではなくプロセス イベントをデバッグ エンジンが監視することを示すには、これを 0 以外に設定します。|
|metricRemoteDebugging|リモート デバッグのサポートを示すには、これを 0 以外に設定します。|
|metricEncUseNativeBuilder|エディット コンティニュ マネージャーがデバッグ エンジンの encbuild.dll を使用してエディット コンティニュ用にビルドする必要があることを示すには、これを 0 以外に設定します。 **注:** カスタム デバッグ エンジンでは、これを設定しないようにするか、常に 0 に設定する必要があります。|
|metricLoadUnderWOW64|64 ビット プロセスをデバッグするときに、WOW でデバッグ対象プロセスにデバッグ エンジンを読み込む必要があることを示すには、これを 0 以外に設定します。それ以外の場合は、(WOW64 で実行されている) Visual Studio プロセスにデバッグ エンジンが読み込まれます。|
|metricLoadProgramProviderUnderWOW64|WOW で 64 ビット プロセスをデバッグするときに、プログラム プロバイダーをデバッグ対象プロセスに読み込む必要があることを示すには、これを 0 以外に設定します。それ以外の場合は、Visual Studio プロセスに読み込まれます。|
|metricStopOnExceptionCrossingManagedBoundary|マネージド/アンマネージド コードの境界を越えて、ハンドルされない例外がスローされた場合にプロセスを停止する必要があることを示すには、これを 0 以外に設定します。|
|metricAutoSelectPriority|デバッグ エンジンの自動選択の優先度を設定します (値が大きいほど優先順位が高くなります)。|
|metricAutoSelectIncompatibleList|自動選択で無視されるデバッグ エンジンの GUID を指定するエントリを含むレジストリ キー。 これらのエントリは、文字列として表現された GUID を持つ数値 (0、1、2 など) です。|
|metricIncompatibleList|このデバッグ エンジンと互換性のないデバッグ エンジンの GUID を指定するエントリを含むレジストリ キー。|
|metricDisableJITOptimization|デバッグ中に Just-In-Time 最適化 (マネージド コードの場合) を無効にするには、これを 0 以外に設定します。|

|式エバリュエーターのプロパティ|説明|
|-------------------------------------|-----------------|
|metricEngine|これは、指定された式エバリュエーターをサポートするデバッグ エンジンの数を保持します。|
|metricPreloadModules|プログラムに対して式エバリュエーターを起動したときにモジュールをプリロードするには、これを 0 以外に設定します。|
|metricThisObjectName|これを "this" オブジェクト名に設定します。|

|式エバリュエーター拡張機能のプロパティ|説明|
| - |-----------------|
|metricExtensionDll|この拡張機能をサポートする dll の名前。|
|metricExtensionRegistersSupported|サポートされているレジスタの一覧。|
|metricExtensionRegistersEntryPoint|レジスタにアクセスするためのエントリ ポイント。|
|metricExtensionTypesSupported|サポートされている種類の一覧。|
|metricExtensionTypesEntryPoint|種類にアクセスするためのエントリ ポイント。|

|ポート サプライヤーのプロパティ|説明|
|------------------------------|-----------------|
|metricPortPickerCLSID|ポート ピッカー (ユーザーがポートを選択し、デバッグに使用するポートを追加するために使用できるダイアログ ボックス) の CLSID。|
|metricDisallowUserEnteredPorts|ユーザーが入力したポートをポート サプライヤーに追加できない場合は 0 以外の値 (これにより、ポートピッカー ダイアログ ボックスが基本的に読み取り専用になります)。|
|metricPidBase|プロセス ID を割り当てるときにポート サプライヤーによって使用される基本プロセス ID。|

|定義済み SP ストアの種類|説明|
|-------------------------------|-----------------|
|storetypeFile|シンボルは個別のファイルに格納されます。|
|storetypeMetadata|シンボルは、メタデータとしてアセンブリに格納されます。|

|その他のプロパティ|説明|
|------------------------------|-----------------|
|metricShowNonUserCode|非ユーザー コードを表示するには、これを 0 以外に設定します。|
|metricJustMyCodeStepping|ユーザー コードでのみステップ実行を行えることを示すには、これを 0 以外に設定します。|
|metricCLSID|特定のメトリックの種類であるオブジェクトの CLSID。|
|metricName|特定のメトリックの種類であるオブジェクトのわかりやすい名前。|
|metricLanguage|言語名。|

## <a name="registry-locations"></a>レジストリの場所
 メトリックは、特に `VisualStudio` サブキーで、レジストリから読み取られ、レジストリに書き込まれます。

> [!NOTE]
> ほとんどの場合、メトリックは HKEY_LOCAL_MACHINE キーに書き込まれます。 ただし、場合によっては、HKEY_CURRENT_USER が書き込み先のキーになります。 Dbgmetric.lib は、両方のキーを処理します。 メトリックを取得すると、最初に HKEY_CURRENT_USER が検索され、次に HKEY_LOCAL_MACHINE が検索されます。 メトリックを設定するときに、使用する最上位のキーをパラメーターで指定します。

 *[registry key]* \

 `Software`\

 `Microsoft`\

 `VisualStudio`\

 *[version root]* \

 *[metric root]* \

 *[metric type]* \

 *[metric] = [metric value]*

 *[metric] = [metric value]*

 *[metric] = [metric value]*

|プレースホルダー|説明|
|-----------------|-----------------|
|*[registry key]*|`HKEY_CURRENT_USER` または `HKEY_LOCAL_MACHINE`。|
|*[version root]*|Visual Studio のバージョン (たとえば、`7.0`、`7.1`、`8.0`)。 ただし、このルートは、 **/rootsuffix** スイッチを使用して **devenv.exe** に変更することもできます。 VSIP の場合、この修飾子は通常は **Exp** であるため、バージョンのルートはたとえば 8.0Exp になります。|
|*[metric root]*|これは、dbgmetric.lib のデバッグ バージョンが使用されているかどうかによって、`AD7Metrics` か `AD7Metrics(Debug)` のいずれかになります。 **注:**  dbgmetric.lib が使用されているかどうかにかかわらず、レジストリに反映する必要があるデバッグ バージョンとリリース バージョンが異なる場合は、この名前付け規則に従う必要があります。|
|*[metric type]*|`Engine`、`ExpressionEvaluator`、`SymbolProvider` など、書き込まれるメトリックの種類。これらはすべて、dbgmetric.h 内で `metricTypeXXXX` として定義されます。ここで `XXXX` は特定の種類の名前です。|
|*[metric]*|メトリックを設定するために値が割り当てられるエントリの名前。 メトリックの実際の編成は、メトリックの種類によって異なります。|
|*[metric value]*|メトリックに割り当てられた値。 値が持つ必要がある型 (文字列、数値など) は、メトリックによって異なります。|

> [!NOTE]
> すべての GUID は、`{GUID}` の形式で格納されます。 たとえば、「 `{123D150B-FA18-461C-B218-45B3E4589F9B}` 」のように入力します。

### <a name="debug-engines"></a>デバッグ エンジン
 次に、レジストリ内のデバッグ エンジンのメトリックの編成を示します。 `Engine` はデバッグ エンジンのメトリックの種類の名前であり、上記のレジストリ サブツリーの *[metric type]* に対応します。

 `Engine`\

 *[engine guid]* \

 `CLSID` =  *[class guid]*

 *[metric] = [metric value]*

 *[metric] = [metric value]*

 *[metric] = [metric value]*

 `PortSupplier`\

 `0` =  *[port supplier guid]*

 `1` =  *[port supplier guid]*

|プレースホルダー|説明|
|-----------------|-----------------|
|*[engine guid]*|デバッグ エンジンの GUID。|
|*[class guid]*|このデバッグ エンジンを実装するクラスの GUID。|
|*[port supplier guid]*|存在する場合は、ポート サプライヤーの GUID。 多くのデバッグ エンジンでは既定のポート サプライヤーが使用されるため、独自のサプライヤーは指定しません。 この場合は、サブキー `PortSupplier` は存在しません。|

### <a name="port-suppliers"></a>ポート サプライヤー
 次に、レジストリ内のポート サプライヤーのメトリックの編成を示します。 `PortSupplier` は、ポート サプライヤーのメトリックの種類の名前であり、 *[metric type]* に対応します。

 `PortSupplier`\

 *[port supplier guid]* \

 `CLSID` =  *[class guid]*

 *[metric] = [metric value]*

 *[metric] = [metric value]*

|プレースホルダー|説明|
|-----------------|-----------------|
|*[port supplier guid]*|ポート サプライヤーの GUID|
|*[class guid]*|このポート サプライヤーを実装するクラスの GUID|

### <a name="symbol-providers"></a>シンボル プロバイダー
 次に、レジストリ内のシンボル サプライヤーのメトリックの編成を示します。 `SymbolProvider` は、シンボル プロバイダーのメトリックの種類の名前であり、 *[metric type]* に対応します。

 `SymbolProvider`\

 *[symbol provider guid]* \

 `file`\

 `CLSID` =  *[class guid]*

 *[metric] = [metric value]*

 *[metric] = [metric value]*

 `metadata`\

 `CLSID` =  *[class guid]*

 *[metric] = [metric value]*

 *[metric] = [metric value]*

|プレースホルダー|説明|
|-----------------|-----------------|
|*[symbol provider guid]*|シンボル プロバイダーの GUID|
|*[class guid]*|このシンボル プロバイダーを実装するクラスの GUID|

### <a name="expression-evaluators"></a>式エバリュエーター
 次に、レジストリ内の式エバリュエーター メトリックの編成を示します。 `ExpressionEvaluator` は、式エバリュエーターのメトリックの種類の名前であり、 *[metric type]* に対応します。

> [!NOTE]
> 式エバリュエーターのすべてのメトリックの変更は、適切な式エバリュエーターのメトリック関数で処理されることを前提としているため、`ExpressionEvaluator` のメトリックの種類は dbgmetric.h で定義されていません (`ExpressionEvaluator` サブキーのレイアウトはやや複雑であるため、詳細は dbgmetric.lib 内で非表示になっています)。

 `ExpressionEvaluator`\

 *[language guid]* \

 *[vendor guid]* \

 `CLSID` =  *[class guid]*

 *[metric] = [metric value]*

 *[metric] = [metric value]*

 `Engine`\

 `0` =  *[debug engine guid]*

 `1` =  *[debug engine guid]*

|プレースホルダー|説明|
|-----------------|-----------------|
|*[language guid]*|言語の GUID|
|*[vendor guid]*|ベンダーの GUID|
|*[class guid]*|この式エバリュエーターを実装するクラスの GUID|
|*[debug engine guid]*|この式エバリュエーターが動作するデバッグ エンジンの GUID|

### <a name="expression-evaluator-extensions"></a>式エバリュエーター拡張機能
 次に、レジストリ内の式エバリュエーター拡張機能メトリックの編成を示します。 `EEExtensions` は、式エバリュエーター拡張機能のメトリックの種類の名前であり、 *[metric type]* に対応します。

 `EEExtensions`\

 *[extension guid]* \

 *[metric] = [metric value]*

 *[metric] = [metric value]*

|プレースホルダー|説明|
|-----------------|-----------------|
|*[extension guid]*|式エバリュエーター拡張機能の GUID|

### <a name="exceptions"></a>例外
 次に、レジストリ内の例外メトリックの編成を示します。 `Exception` は、例外のメトリックの種類の名前であり、 *[metric type]* に対応します。

 `Exception`\

 *[debug engine guid]* \

 *[exception types]* \

 *[exception]* \

 *[metric] = [metric value]*

 *[metric] = [metric value]*

 *[exception]* \

 *[metric] = [metric value]*

 *[metric] = [metric value]*

|プレースホルダー|説明|
|-----------------|-----------------|
|*[debug engine guid]*|例外をサポートするデバッグ エンジンの GUID。|
|*[exception types]*|処理できる例外のクラスを識別するサブキーの一般的なタイトル。 一般的な名前は、**C++ 例外**、**Win32 例外**、**共通言語ランタイム例外**、**ネイティブ ランタイム チェック** です。 これらの名前は、ユーザーに対して特定のクラスの例外を識別するためにも使用されます。|
|*[exception]*|例外の名前。たとえば、 **_com_error** や **Control-Break** です。 これらの名前は、ユーザーに対して特定の例外を識別するためにも使用されます。|

## <a name="requirements"></a>必要条件
 これらのファイルは、[!INCLUDE[vs_dev10_ext](../../../extensibility/debugger/reference/includes/vs_dev10_ext_md.md)] SDK のインストール ディレクトリ (既定では *[drive]* \Program Files\Microsoft Visual Studio 2010 SDK\\) にあります。

 ヘッダー: includes\dbgmetric.h

 ライブラリ: libs\ad2de.lib、libs\dbgmetric.lib

## <a name="see-also"></a>関連項目
- [API リファレンス](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)
