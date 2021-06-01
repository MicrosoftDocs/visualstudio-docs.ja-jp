---
title: 変更ログ (Visual Studio Tools for Unity、Windows) | Microsoft Docs
description: Visual Studio Tools for Unity、Windows の変更ログを確認します。 バージョン 1.0.0.0 から 4.7.0.0 以降にかけて行われた変更を確認します。
ms.custom: ''
ms.date: 3/1/2021
ms.technology: vs-unity-tools
ms.prod: visual-studio-dev16
ms.topic: conceptual
ms.assetid: ea490b7e-fc0d-44b1-858a-a725ce20e396
author: therealjohn
ms.author: johmil
manager: crdun
ms.workload:
- unity
ms.openlocfilehash: a03d0fc896fcbc971bc62cd9391c4f38d0aad06c
ms.sourcegitcommit: 3e1ff87fba290f9e60fb4049d011bb8661255d58
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2021
ms.locfileid: "107879383"
---
# <a name="change-log-visual-studio-tools-for-unity-windows"></a>変更ログ (Visual Studio Tools for Unity、Windows)

Visual Studio Tools for Unity の変更ログです。

## <a name="4910"></a>4.9.1.0
リリース日: 2021 年 3 月 2 日

### <a name="new-features"></a>新機能

- **評価:**

  - ルートのゲーム オブジェクトを示す `Active Scene` を [ローカル] に追加しました。

  - Unity プロジェクトで広く使用されていることから、`this.gameObject` を [ローカル] に追加しました。

  - `Children` と `Components` のグループを `GameObject` のすべてのインスタンスに追加し、すべてのオブジェクトを階層に簡単に表示できるようにしました。

  - シーン内のすべての位置を表示するために、`Scene Path` を `GameObject` のすべてのインスタンスに追加しました。

  - ソース ジェネレーターでエンティティを使用するときの `JobEntityBatch`/Lambdas のサポートを追加しました。

  - (インデックス バケットを使用して) 大きな配列を表示するためのサポートを強化しました。
  
  - 2019.4 API で不足している Unity メッセージを追加しました。

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - ENU 以外の言語のさまざまな UI の問題を修正しました。

  - [`UNT0018`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0018.md) 診断に関する安定性の問題を修正しました。
  
- **デバッグ:**

  - `Trace` メソッドを使用するときに VM が切断される問題を修正しました。

- **評価:**

  - 例外をスローする古いプロパティのフィルター処理を修正しました。

## <a name="4900"></a>4.9.0.0
リリース日: 2021 年 1 月 20 日

### <a name="new-features"></a>新機能

- **統合:**

  - `raytrace shaders`、`UXML`、および `USS` のファイルのサポートを追加しました。

  - `.vsconfig` 生成のサポートを追加しました。 Unity プロジェクトを使用するときに、Visual Studio で不足しているコンポーネントが検出され、それらをインストールするように求められるようになりました。

  - (コルーチンとして使用されているすべてのメソッドの) Unity メッセージ API を更新しました。

  - Android SDK 検出を更新しました。

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - インスタンス選択ダイアログを使用するときの、プロセスの更新を修正しました。

  - コルーチンと `AssetPostprocessor.OnAssignMaterialModel` に対して間違った警告を出す、[`UNT0006`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0006.md) 診断を修正しました。

## <a name="4820"></a>4.8.2.0
リリース日: 2020 年 11 月 10 日

### <a name="new-features"></a>新機能

- **統合:**

  - `MonoBehaviour` だけでなく `Component` を継承するすべてに適用されるように、[`UNT0010`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0010.md) 診断を改善しました。

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - CodeLens メッセージの無効化を修正しました。

## <a name="4810"></a>4.8.1.0
リリース日: 2020 年 10 月 13 日

### <a name="new-features"></a>新機能

- **評価:**

  - 呼び出しによる暗黙的な変換のサポートが追加されました。 以前は、エバリュエーターによって厳密な型チェックが適用され、`Failed to find a match for method([parameters...])` 警告メッセージが生成されていました。

- **統合:**

  - [`UNT0018`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0018.md) 診断が追加されました。 `Update`、`FixedUpdate`、`LateUpdate`、または `OnGUI` のようなパフォーマンスが重要なメッセージでは、`System.Reflection` 機能を使用しないでください。

  - [`USP0003`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0003.md) および [`USP0005`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0005.md) サプレッサーを改善し、すべての `AssetPostprocessor` 静的メソッドがサポートされるようになりました。

  - `CS8618` 用の [`USP0016`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0016.md) サプレッサーが追加されました。 `C# 8.0` によって、null 許容参照型と null 非許容参照型が導入されます。 `UnityEngine.Object` から継承する型の初期化検出はサポートされず、エラーが発生します。

  - 現在、Unity 2019.x と 2020.x+ の両方で、同じプレーヤーおよび asmdef プロジェクト生成メカニズムを使用しています。

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - コメント内のメッセージが予期せずに完了することを修正しました。

## <a name="4800"></a>4.8.0.0 
リリース日: 2020 年 9 月 14 日

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - Unity 2019.x でのプレーヤー プロジェクト生成を修正しました。

## <a name="4710"></a>4.7.1.0
リリース日: 2020 年 8 月 5 日

### <a name="new-features"></a>新機能

- **統合:**

  - 既定のテンプレートに名前空間のサポートを追加しました。
  
  - Unity メッセージ API を 2019.4 に更新しました。

  - `CA1823` 用の [`USP0013`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0013.md) サプレッサーが追加されました。 `SerializeField` または `SerializeReference` 属性を持つプライベート フィールドを未使用としてマークすることはできません (FxCop)。
  
  - `CA1822` 用の [`USP0014`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0014.md) サプレッサーが追加されました。 Unity メッセージを `static` 修飾子の候補としてフラグ設定することはできません (FxCop)。

  - `CA1801` 用の [`USP0015`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0015.md) サプレッサーが追加されました。 使用されていないパラメーターを Unity メッセージから削除することはできません (FxCop)。
  
  - [`USP0009`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0009.md) サプレッサーに MenuItem サポートを追加しました。  

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - 追加のかっこやメソッド引数と共に動作しない [`USP0001`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0001.md) および [`USP0002`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0002.md) サプレッサーを修正しました。
  
  - Unity の設定で自動更新が無効になっている場合でも資産データベースの更新が強制される問題を修正しました。

## <a name="4700"></a>4.7.0.0
リリース日: 2020 年 6 月 23 日

### <a name="new-features"></a>新機能

- **統合:**

  - Unity によってソリューションとプロジェクトが再生成されるときに、ソリューション フォルダーを保持するためのサポートを追加しました。

  - [`UNT0015`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0015.md) 診断が追加されました。 `InitializeOnLoadMethod` または `RuntimeInitializeOnLoadMethod` 属性を使用して、不適切なメソッド シグネチャを検出します。

  - [`UNT0016`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0016.md) 診断が追加されました。 文字列リテラルである最初の引数と共に `Invoke`、`InvokeRepeating`、`StartCoroutine`、または `StopCoroutine` を使用するのは、タイプ セーフではありません。

  - [`UNT0017`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0017.md) 診断が追加されました。 `SetPixels` の呼び出しは低速です。

  - シェーダー ファイルに対するブロック コメントとインデントのサポートを追加しました。

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - Unity メッセージ ウィザードでメッセージをフィルター処理するときに、選択項目がリセットされません。
  
  - Unity API ドキュメントを開くときに、常に既定のブラウザーが使用されます。
  
  - 次の規則で [`USP0004`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0004.md)、[`USP0006`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0006.md)、および [`USP0007`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0007.md) サプレッサーを修正しました: SerializeField 属性で修飾されたすべてのフィールドの `IDE0044` (読み取り専用)、`IDE0051` (未使用)、`CS0649` (未割り当て) が抑制されます。 `Unity.Object` を拡張したすべての型のパブリック フィールドの `CS0649` (未割り当て) が抑制されます。

  - [`UNT0014`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0014.md) 診断のジェネリック型パラメーターのチェックを修正しました。

- **評価:**

  - 列挙型での等価比較を修正しました。

## <a name="4610"></a>4.6.1.0
リリース日: 2020 年 5 月 19 日

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - Unity 側でメッセージング サーバーを作成できない場合に警告します。
  
  - ライトウェイト コンパイル中にアナライザーを適切に実行します。
  
  - UPE から作成された MonoBehaviour クラスがファイル名と一致しない問題を修正しました。

## <a name="4600"></a>4.6.0.0
リリース日: 2020 年 4 月 14 日

### <a name="new-features"></a>新機能

- **統合:**

  - CodeLens のサポート (Unity スクリプトとメッセージ) を追加しました。
  
  - [`UNT0012`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0012.md) 診断が追加されました。 `StartCoroutine()` でコルーチンの呼び出しが検出されてラップされます。

  - [`UNT0013`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0013.md) 診断が追加されました。 無効または重複する `SerializeField` 属性が検出され削除されます。

  - [`UNT0014`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0014.md) 診断が追加されました。 コンポーネント以外またはインターフェイス以外の型を使用して呼び出された `GetComponent()` が検出されます。
  
  - `IDE0051` 用の [`USP0009`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0009.md) サプレッサーが追加されました。 `ContextMenu` 属性を持つメソッド、または `ContextMenuItem` 属性を持つフィールドによって参照されているメソッドには未使用のフラグが設定されません。

  - `IDE0051` 用の [`USP0010`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0010.md) サプレッサーが追加されました。 `ContextMenuItem` 属性を持つフィールドに未使用のフラグが設定されません。
  
  - `IDE0044` 用の [`USP0011`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0011.md) サプレッサーが追加されました。 `ContextMenuItem` 属性を持つフィールドが読み取り専用にされません。
  
  - [`USP0004`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0004.md)、[`USP0006`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0006.md)、[`USP0007`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0007.md) は、`SerializeReference` 属性と `SerializeField` 属性の両方で動作するようになりました。
  
### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - エディターが通信できる場合にのみ、start/stop コマンドが Unity に送信されます。
  
  - 継承されたメッセージを含むように QuickInfo ドキュメントを修正しました。
  
  - `CreateInspectorGUI` メッセージのメッセージ スコープを修正しました。

  - ポリモーフィックな修飾子を持つメソッドでは、[`UNT0001`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0001.md) が報告されません。

- **評価:**

  - エイリアス化の使用の処理を修正しました。

## <a name="4510"></a>4.5.1.0

リリース日: 2020 年 3 月 16 日

### <a name="new-features"></a>新機能

- **統合:**

  - `IDE0051` 用の [`USP0008`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0008.md) サプレッサーが追加されました。 Invoke、InvokeRepeating、StartCoroutine、または StopCoroutine で使用されるプライベート メソッドを未使用としてマークすることはできません。

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - OnDrawGizmos と OnDrawGizmosSelected のドキュメントを修正しました。

- **評価:**

  - ラムダ引数の検査を修正しました。

## <a name="4501"></a>4.5.0.1

リリース日: 2020 年 2 月 19 日

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - [`UNT0006`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0006.md) の不適切なメッセージの署名に対する診断チェックを修正しました。 複数のレベルの継承を含む型を検査すると、この診断は次のメッセージで失敗します: `warning AD0001: Analyzer 'Microsoft.Unity.Analyzers.MessageSignatureAnalyzer' threw an exception of type 'System.ArgumentException' with message 'An item with the same key has already been added`。

## <a name="4500"></a>4.5.0.0

リリース日: 2020 年 1 月 22 日

### <a name="new-features"></a>新機能

- **統合:**

  - HLSL ファイルのサポートが追加されました。
  
  - `IDE0051` 用の [`USP0006`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0006.md) サプレッサーが追加されました。 `SerializeField` 属性を持つプライベート フィールドを未使用としてマークすることはできません。
  
  - `CS0649` 用の [`USP0007`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0007.md) サプレッサーが追加されました。 `SerializeField` 属性を持つフィールドを未割り当てとしてマークすることはできません。  

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - プロジェクトの生成を修正しました (`GenerateTargetFrameworkMonikerAttribute` ターゲットは常に正しく配置されていませんでした)。

## <a name="4420"></a>4.4.2.0

リリース日: 2019 年 12 月 3 日

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - 診断のユーザー定義インターフェイスを修正しました。

  - クイック ヒントの間違った形式の式を修正しました。

## <a name="4410"></a>4.4.1.0

リリース日: 2019 年 11 月 6 日

### <a name="new-features"></a>新機能

- **統合:**

  - Unity バックグラウンド プロセスのサポートを追加しました。 (デバッガーは子プロセスではなくメイン プロセスに自動接続できます)。
  
  - Unity メッセージのクイック ヒントを追加しました。関連するドキュメントが表示されます。

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - タグ比較アナライザー [`UNT0002`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0002.md) の、高度なバイナリ式および呼び出し式を修正しました。

### <a name="deprecated-features"></a>非推奨の機能

- **統合:**

  - 今後、Visual Studio Tools for Unity では Visual Studio 2017 以降のみがサポートされます。

## <a name="4400"></a>4.4.0.0

リリース日: 2019 年 10 月 15 日

### <a name="new-features"></a>新機能

- **統合:**

  - すべての Unity メッセージに対して `IDE0060` (未使用パラメーター) 用の [`USP0005`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0005.md) サプレッサーが追加されました。
  
  - `TooltipAttribute` でタグ付けされたフィールド用のクイック ヒントを追加しました。 (これは、このフィールドを使用する単純な get アクセサーに対しても機能します)。

## <a name="4330"></a>4.3.3.0

リリース日: 2019 年 9 月 23 日

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - 軽量ビルドに関するエラーおよび警告報告を修正しました。

## <a name="4320"></a>4.3.2.0

リリース日: 2019 年 9 月 16 日

### <a name="new-features"></a>新機能

- **統合:**

  - Unity に固有の新しい診断を追加することによって、Visual Studio が Unity プロジェクトをより深く理解できるようにしました。 また、Unity プロジェクトには適用されない一般的な C# 診断を抑制することで、IDE をよりスマートにしました。 たとえば、IDE では、インスペクター変数 `readonly` を変更するクイック修正は表示されません。これにより、Unity エディターで変数を変更できなくなります。
    - [`UNT0001`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0001.md):Unity メッセージは空の場合でもランタイムによって呼び出されます。それらのメッセージを宣言する場合は、不要な処理を Unity ランタイムが回避するようにしないでください。
    - [`UNT0002`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0002.md):文字列の等価性を使用したタグ比較は、組み込みの CompareTag メソッドよりも遅くなります。
    - [`UNT0003`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0003.md):型の安全性のため、GetComponent のフォームは汎用的なものを使用することが推奨されています。
    - [`UNT0004`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0004.md):更新メッセージはフレームレートに依存しているため、Time.fixedDeltaTime ではなく Time.deltaTime instead を使用する必要があります。
    - [`UNT0005`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0005.md):FixedUpdate メッセージはフレームレートに依存しないため、Time.deltaTime ではなく Time.fixedDeltaTime を使用する必要があります。
    - [`UNT0006`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0006.md):この Unity メッセージに対して無効なメソッド署名が検出されました。
    - [`UNT0007`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0007.md):Unity では、null 合体演算子と互換性のない、Unity オブジェクト用の null 比較演算子がオーバーライドされます。
    - [`UNT0008`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0008.md):Unity では、null 反映演算子と互換性のない、Unity オブジェクト用の null 比較演算子がオーバーライドされます。
    - [`UNT0009`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0009.md):InitializeOnLoad 属性をクラスに適用する場合は、静的コンストラクターを指定する必要があります。 InitializeOnLoad 属性を使用すると、エディターの起動時にそれが確実に呼び出されます。
    - [`UNT0010`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0010.md):MonoBehaviours は、AddComponent() を使用してのみ作成する必要があります。 MonoBehaviour はコンポーネントであり、GameObject にアタッチする必要があります。
    - [`UNT0011`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0011.md):ScriptableObject は CreateInstance() を使用してのみ作成する必要があります。 Unity メッセージ メソッドを処理するには、Unity エンジンによって ScriptableObject を作成する必要があります。
    - `IDE0029` の [`USP0001`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0001.md): Unity オブジェクトでは、null 合体演算子を使用しないでください。
    - `IDE0031` の [`USP0002`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0002.md): Unity オブジェクトでは null 反映演算子を使用しなきでください。
    - `IDE0051` の [`USP0003`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0003.md): Unity メッセージは Unity ランタイムによって呼び出されます。
    - `IDE0044` の [`USP0004`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0004.md): SerializeField 属性を持つフィールドを読み取り専用にしないでください。

## <a name="4310"></a>4.3.1.0

リリース日: 2019 年 9 月 4 日

### <a name="new-features"></a>新機能

- **評価:**

  - 型の表示を改善するためのサポートが追加されました。すなわち、`List'1[[System.Object, <corlib...>]]` ではなく `List<object>` になりました。

  - ポインター メンバー アクセスのサポートが追加されました。すなわち、`p->data->member` のようになりました。

  - 配列初期化子での暗黙的な変換のサポートが追加されました。すなわち、`new byte [] {1,2,3,4}` のようになりました。

## <a name="4300"></a>4.3.0.0

リリース日: 2019 年 8 月 13 日

### <a name="new-features"></a>新機能

- **デバッガー:**

  - MDS プロトコル 2.51 のサポートが追加されました。

- **統合:**

  - "Unity にアタッチ インスタンス" ウィンドウの並べ替え、検索、更新機能が改善されました。 ローカル プレーヤーの場合でも PID が表示されるようになりました (システム上でリスニング ソケットを問い合わせ、所有プロセスを取得します)。

  - asmdef ファイルのサポートが追加されました。

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - Unity プレーヤーとの通信中の誤った形式のメッセージの処理を修正しました。

- **評価:**

  - 式の名前空間の処理を修正しました。

  - IntPtr 型を使用した検査を修正しました。
  
  - 例外とともにステップ実行の問題を修正しました。

  - 擬似識別子 ($exception など) の評価を修正しました。

  - 無効なアドレスを逆参照するときにクラッシュしないようにします。  

  - アンロードされた AppDomain の問題を修正しました。

## <a name="4201"></a>4.2.0.1

リリース日: 2019 年 7 月 24 日

### <a name="new-features"></a>新機能

- **統合:**

  - Unity プロジェクト エクスプローラーからあらゆる種類のファイルを作成する新しいオプションを追加しました。
  
  - Unity プロジェクトに高速ビルドを使用する場合の診断キャッシュを改善します。

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - ファイル拡張子が既知のエディターによって処理されなかった問題を修正しました。

  - Unity プロジェクト エクスプローラーでのカスタム拡張子へのサポートを追加しました。

  - メイン ダイアログの外部での保存設定を修正しました。

  - レガシの Microsoft.VisualStudio.MPF 依存関係を削除しました。

## <a name="4110"></a>4.1.1.0

リリース日: 2019 年 5 月 24 日

### <a name="new-features"></a>新機能

- **統合:**

  - MonoBehaviour API を 2019.1 に更新しました。

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - ライトウェイト ビルドが有効な場合に、警告とエラーが出力に報告されることを修正しました。

  - ライトウェイト ビルドのパフォーマンスを修正しました。

## <a name="4100"></a>4.1.0.0

リリース日: 2019 年 5 月 21 日

### <a name="new-features"></a>新機能

- **統合:**

  - プロジェクトの再読み込みを高速化する新しいバッチ API のサポートを追加しました。

  - IntelliSense エラーと警告の使用を優先して、Unity プロジェクトのフル ビルドを無効にしました。 Indeed Unity では、Unity が内部で実行していることを表すクラス ライブラリ プロジェクトによって Visual Studio ソリューションが作成されます。 ただし、Visual Studio でのビルドの結果は、Unity によって使用されたり、選択されたりすることはありません。それらのコンパイル パイプラインが閉じているためです。 Visual Studio でのビルドによって、何もしなくてもリソースが消費されます。 フル ビルドに依存するツールまたは設定があるため、フル ビルドを必要とする場合は、この最適化を無効にできます ([ツール]/[オプション]/[Tools for Unity]/[プロジェクトのフル ビルドを無効にする])。

  - Unity プロジェクトが読み込まれると、Unity プロジェクト エクスプローラー (UPE) が自動的に表示されます。 UPE はソリューション エクスプローラーの横にドッキングされます。

  - Unity 2019.x によるプロジェクト名抽出メカニズムを更新しました。

  - UPE での Unity パッケージのサポートを追加しました。 参照されているパッケージ (`Packages` フォルダー内の manifest.json を使用して) とローカル パッケージ (`Packages` フォルダーに埋め込まれた) のみが表示されます。

- **Project Generation:**

  - ソリューション ファイルを処理するときに、外部のプロパティを保持します。

- **評価:**

  - 別名で修飾された名前 (現在のところグローバル名前空間のみ) のサポートを追加しました。 そのため、式エバリュエーターで形式 global::namespace.type を使用した型を受け付けるようになりました。

  - `pointer[index]` 形式のサポートを追加しました。これはポインター逆参照 `*(pointer+index)` 形式と同じ意味です。

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - Microsoft.VisualStudio.MPF の依存関係の問題を修正しました。

  - プロジェクトが読み込まれていない状態での UWP プレーヤーのアタッチを修正しました。

  - Visual Studio がまだ接続されていない場合の、資産データベースの自動更新を修正しました。

  - ラベルとチェック ボックスのテーマの問題を修正しました。

- **デバッガー:**

  - 静的コンストラクターによるステップ実行を修正しました。

## <a name="4005"></a>4.0.0.5

リリース日: 2019 年 2 月 27 日

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - セットアップ パッケージでの Visual Studio のバージョン検出を修正しました。

  - セットアップ パッケージから未使用のアセンブリを削除しました。

## <a name="4004"></a>4.0.0.4

リリース日: 2019 年 2 月 13 日

### <a name="new-features"></a>新機能

- **統合:**

  - インストール時に Unity プロセスを適切に検出するためのサポートを追加し、セットアップ エンジンによるファイル ロックの処理を改善できるようにしました。

  - `ScriptableObject` API を更新しました。

## <a name="4003"></a>4.0.0.3

リリース日: 2019 年 1 月 31 日

### <a name="new-features"></a>新機能

- **Project Generation:**

  - パブリック フィールドとシリアル化されたフィールドで、警告が発行されなくなりました。 `CS0649` および `IDE0051` のメッセージを作成していた Unity プロジェクトでは、これらのコンパイラの警告を自動抑制しました。

- **統合:**

  - Unity エディターとプレーヤー インスタンスを表示するユーザー エクスペリエンスを改善しました (ウィンドウのサイズが変更可能になり、均一な余白が使用され、サイズ変更グリップが表示されます)。 Unity エディターのプロセス ID 情報を追加しました。

  - `MonoBehaviour` API を更新しました。

- **評価:**

  - ローカル関数のサポートを追加しました。

  - 擬似変数のサポートを追加しました (例外とオブジェクトの識別子)。

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - モニカー画像とテーマに関連する問題を修正しました。

  - 資産データベースが自動更新されるとき、デバッグ中は出力ウィンドウにのみ書き込みます。

  - MonoBehaviour ウィザードのフィルター処理での UI の遅延を修正しました。

- **デバッガー:**

  - 古いプロトコル バージョン使用時の名前付き引数に対するカスタム属性の読み取りを修正しました。

## <a name="4002"></a>4.0.0.2

リリース日: 2019 年 1 月 23 日

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - 試験的ビルドの生成を修正しました。

  - UI スレッドの負荷を最小限に抑えるようにプロジェクト ファイルのイベント処理を修正しました。

  - テキストの一括変更での補完プロバイダーを修正しました。

- **デバッガー:**

  - アタッチされたデバッガーへのユーザー デバッグ メッセージの表示を修正しました。

## <a name="4001"></a>4.0.0.1

リリース日: 2018 年 12 月 10 日

### <a name="new-features"></a>新機能

- **評価:**

  - 式の評価には、NRefactory よりも Roslyn を使用するように置き換えました。

  - ポインターへのサポートを追加しました: 逆参照、キャスト、およびポインターの算術演算 (これには、Unity 2018.2+ および新しいランタイムの両方が必要です)。

  - (C++ の場合のように) 配列ポインター ビューのサポートを追加しました。 ポインター式を取得してから、コンマと表示する要素数を付け加えます。

  - 非同期のコンストラクトのサポートを追加しました。

- **統合:**

  - 保存時に Unity のアセット データベースを自動更新するサポートを追加しました。 これは既定で有効になっており、Visual Studio 内にスクリプトを保存するときに Unity 側での再コンパイルをトリガーします。 この機能は、[ツール]\[オプション]\[Tools for Unity]\[保存時に Unity の AssetDatabase を更新] で無効にすることができます。

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - 優先する外部エディターとして Visual Studio が選択されていない場合のブリッジ アクティブ化を修正しました。

  - 形式が正しくないかサポートされていない式での式の評価を修正しました。

## <a name="4000"></a>4.0.0.0

リリース日: 2018 年 12 月 4 日

### <a name="new-features"></a>新機能

- **統合:**

  - Visual Studio 2019 のサポートが追加されました (外部スクリプト エディターとして Visual Studio 2019 を使えるようにするには、少なくとも Unity 2018.3 が必要です)。

  - Visual Studio イメージ サービスとカタログを導入し、HDPI のスケール、ピクセル パーフェクトなイメージ、およびテーマを完全にサポートします。

### <a name="deprecated-features"></a>非推奨の機能

- **統合:**

  - 今後、Visual Studio Tools for Unity では Unity 5.2 以降のみをサポートします (Unity の組み込み Visual Studio の統合による)。

  - 今後、Visual Studio Tools for Unity では Visual Studio 2015 以降のみをサポートします。

  - 従来の言語サービス、エラー一覧、およびステータス バーを削除しました。

  - クイック Monobehaviour ウィザードを削除しました (専用の intellisense のサポートに置き換えました)。

## <a name="3903"></a>3.9.0.3

リリース日: 2018 年 11 月 28 日

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - 最初のプロジェクト内にあるスクリプトの追加または削除時の、プロジェクトの再読み込みと IntelliSense の問題が修正されました。

## <a name="3902"></a>3.9.0.2

リリース日: 2018 年 11 月 19 日

### <a name="bug-fixes"></a>バグ修正

- **デバッガー:**

  - Unity のデバッガー エンジンとの通信に使用されるライブラリでのデッドロックを修正しました。このバグによって、特に [Unity にアタッチ] を選択した場合やゲームを再起動したときに、Visual Studio または Unity がフリーズしていました。

## <a name="3901"></a>3.9.0.1

リリース日: 2018 年 11 月 15 日

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - 別のデフォルト エディターが選択されたときの Unity プラグイン アクティベーションを修正しました。

## <a name="3900"></a>3.9.0.0

リリース日: 2018 年 11 月 13 日

### <a name="bug-fixes"></a>バグ修正

- **Project Generation:**

  - Unity により修正された Unity パフォーマンス バグの回避策がロールバックされました。

## <a name="3807"></a>3.8.0.7

リリース日: 2018 年 9 月 20 日

### <a name="bug-fixes"></a>バグ修正

- **デバッガー:**

  - (以前のバージョン 3.9.0.2 からの移植) Unity のデバッガー エンジンとの通信に使用されるライブラリでのデッドロックを修正しました。このバグによって、特に [Unity にアタッチ] を選択した場合やゲームを再起動したときに、Visual Studio または Unity がフリーズしていました。

## <a name="3806"></a>3.8.0.6

リリース日: 2018 年 8 月 27 日

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - プロジェクトとソリューションの再読み込みを修正しました。

## <a name="3805"></a>3.8.0.5

リリース日: 2018 年 8 月 20 日

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - プロジェクト監視のサブスクリプション破棄を修正しました。

## <a name="3804"></a>3.8.0.4

リリース日: 2018 年 8 月 14 日

### <a name="new-features"></a>新機能

- **評価:**

  - ポインター値のサポートが追加されました。

  - ジェネリック メソッドのサポートが追加されました。

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - 複数のプロジェクトのスマート リロードが変更されました。

## <a name="3803"></a>3.8.0.3

リリース日: 2018 年 7 月 24 日

### <a name="bug-fixes"></a>バグ修正

- **Project Generation:**

  - (以前のバージョン 3.9.0.0 からの移植) Unity により修正された Unity パフォーマンス バグの回避策がロールバックされました。

## <a name="3802"></a>3.8.0.2

リリース日: 2018 年 7 月 7 日

### <a name="bug-fixes"></a>バグ修正

- **Project Generation:**

  - Unity のパフォーマンスのバグの一時的な回避策: プロジェクト生成時の MonoIslands のキャッシュ。

## <a name="3801"></a>3.8.0.1

リリース日: 2018 年 6 月 26 日

### <a name="new-features"></a>新機能

- **デバッグ:**

  - UserLog コマンドと UserBreak コマンドのサポートを追加しました。

  - Lazy 型ロード サポートを追加しました (ネットワーク ロードとデバッガー応答待機時間を最適化)。

### <a name="bug-fixes"></a>バグ修正

- **評価:**

  - 二項演算子式の評価とメソッドの検索が改善されました。

## <a name="3800"></a>3.8.0.0

リリース日: 2018 年 5 月 30 日

### <a name="new-features"></a>新機能

- **デバッグ:**

  - 非同期コンストラクトで変数を表示するためのサポートが追加されました。

  - コンパイラ コンストラクトによる警告を回避するために、ブレークポイント設定時に入れ子にされた型を処理するサポートが追加されました。

- **統合:**

  - Shader の TextMate 文法のサポートが追加されました (Shader コード配色には C++ ワークロードが不要になりました)。

### <a name="bug-fixes"></a>バグ修正

- **Project Generation:**

  - 今後、新しい Unity ランタイムを使用するときにはポータブル pdb を mdb に変換しないでください。

## <a name="3701"></a>3.7.0.1

リリース日: 2018 年 5 月 7 日

### <a name="bug-fixes"></a>バグ修正

- **インストーラー:**

  - 試験的ビルドを使うときの依存関係の問題を解決しました。

## <a name="3700"></a>3.7.0.0

リリース日: 2018 年 5 月 7 日

### <a name="new-features"></a>新機能

- **デバッグ:**

  - 調整されたデバッグのサポートが追加されました (同じ Visual Studio セッションでの複数のプレーヤー/エディターのデバッグ)。

  - Android USB プレーヤーのデバッグのサポートが追加されました。

  - UWP/IL2CPP プレーヤーのデバッグのサポートが追加されました。

- **評価:**

  - 16 進指定子のサポートが追加されました。

  - ウォッチ ウィンドウの評価エクスペリエンスが強化されました。

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - 例外設定の使用方法が修正されました。

- **Project Generation:**

  - パッケージ マネージャーのコンパイル単位が生成から除外されました。

## <a name="3605"></a>3.6.0.5

リリース日: 2018 年 3 月 13 日

### <a name="new-features"></a>新機能

- **Project Generation:**

  - Unity 2018.1 の新しいプロジェクト ジェネレーターのサポートが追加されました。

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - カスタム プロジェクトでの破損した状態の処理を修正しました。

- **デバッガー:**

  - 次のステートメントの設定を修正しました。

## <a name="3604"></a>3.6.0.4

リリース日: 2018 年 3 月 5 日

### <a name="bug-fixes"></a>バグ修正

- **Project Generation:**

  - Mono バージョンの検出を修正しました。

- **統合:**

  - 2018.1 とプラグインのアクティブ化のタイミングの問題を修正しました。

## <a name="3603"></a>3.6.0.3

リリース日: 2018 年 2 月 23 日

### <a name="new-features"></a>新機能

- **Project Generation:**

  - .NET Standard のサポートを追加しました。

### <a name="bug-fixes"></a>バグ修正

- **Project Generation:**

  - Unity ターゲット フレームワークの検出を修正しました。

- **デバッガー:**

  - ユーザーコードの外部でスローされた例外での中断を修正しました。

## <a name="3602"></a>3.6.0.2

リリース日: 2018 年 2 月 7 日

### <a name="new-features"></a>新機能

- **統合:**

  - 2017.3 の UnityMessage API サーフェスを更新しました。

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - プロジェクトの再読み込みは、外部での変更時のみ実行されます (調整による)。

## <a name="3601"></a>3.6.0.1

リリース日: 2018 年 1 月 24 日

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - pdb から mdb への自動デバッグ シンボル変換を修正済み

  - 配列のサイズを変更するときに、インスペクターに影響する EditorPrefs.GetBool への間接的な呼び出しを修正しました。

## <a name="3600"></a>3.6.0.0

リリース日: 2018 年 1 月 10 日

### <a name="new-features"></a>新機能

- **Project Generation:**

  - 2018.1 MonoIsland 参照モデルのサポートを追加しました。

- **評価:**

  - $Exception 識別子のサポートを追加しました。

- **デバッガー:**

  - 新しい Unity ランタイムを使用した DebuggerHidden/DebuggerStepThrough 属性のサポートを追加しました。

- **ウィザード:**

  - ウィザードの '最新' バージョンを導入しました。

### <a name="bug-fixes"></a>バグ修正

- **Project Generation:**

  - プレーヤー プロジェクトに対するプロジェクト guid の計算を修正しました。

- **デバッガー:**

  - 中断イベントを処理するときの競合を修正しました。

- **ウィザード:**

  - roslyn コンテキストは、メソッドの挿入前に更新されます。

## <a name="3503"></a>3.5.0.3

リリース日: 2018 年 1 月 9 日

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - pdb から mdb への自動デバッグ シンボル変換を修正済み

## <a name="3502"></a>3.5.0.2

リリース日: 2017 年 12 月 4 日

### <a name="new-features"></a>新機能

- **統合:**

  - Unity プロジェクトが、Unity からのスクリプトの追加または削除時に自動的に Visual Studio に再読み込みされるようになりました。

- **デバッガー:**

  - Unity エディターをデバッグするために Xamarin および Visual Studio for Mac で共有された Mono デバッガーを使用するオプションが追加されました。

  - ポータブル デバッグ シンボル ファイルのサポートが追加されました。

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - セットアップの依存関係の問題を修正しました。

  - Unity API のヘルプ メニューが表示されないという問題を修正しました。

- **Project Generation:**

  - IL2CPP/.NET 4.6 のバックエンドの UWP ゲームで動作している場合の player プロジェクトの生成を修正しました。

  - アセンブリのファイル名に余分な .dll 拡張子が誤って追加される問題を修正しました。

  - グローバルではなく、特定のプロジェクト API 互換性レベルの使用を修正しました。

  - 既定値が 'true' になったので、AllowAttachedDebuggingOfEditor Unity フラグを強要しません。

## <a name="3402"></a>3.4.0.2

リリース日: 2017 年 9 月 19 日

### <a name="new-features"></a>新機能

- **Project Generation:**

  - assembly.json コンパイル単位のサポートが追加されました。

  - プロジェクト フォルダーへの Unity アセンブリのコピーが停止しました。

- **デバッガー:**

  - 新しい Unity ランタイムで次のステートメントを設定するためのサポートが追加されました。

  - 新しい Unity ランタイムによる Decimal 型のサポートが追加されました。

  - 暗黙的/明示的な変換のサポートが追加されました。

### <a name="bug-fixes"></a>バグ修正

- **評価:**

  - 暗黙的なサイズによる配列の作成が修正されました。

  - コンパイラがローカルで生成した項目が修正されました。

- **Project Generation:**

  - 4\.6 API レベルの Microsoft.CSharp の参照が修正されました。

## <a name="3302"></a>3.3.0.2

リリース日: 2017 年 8 月 15 日

### <a name="bug-fixes"></a>バグ修正

- **Project Generation:**

  - Unity 5.5 と以前のバージョンの Visual Studio ソリューションの生成を修正しました。

## <a name="3300"></a>3.3.0.0

リリース日: 2017 年 8 月 14 日

### <a name="new-features"></a>新機能

- **評価:**

  - 新しい Unity ランタイムによる構造体の作成のサポートが追加されました。

  - ポインターの最低限のサポートが追加されました。

### <a name="bug-fixes"></a>バグ修正

- **評価:**

  - プリミティブに対するメソッド呼び出しが修正されました。

  - BeforeFieldInit とマークされた型によるフィールド評価が修正されました。

  - 二項演算子 (減算) でサポートされていない呼び出しが修正されました。

  - Visual Studio ウォッチへの項目の追加時の問題が修正されました。

- **Project Generation:**

  - mcs.rsp ファイルを使用したアセンブリ名の参照が修正されました。

  - API レベルの定義が修正されました。

## <a name="3200"></a>3.2.0.0

リリース日: 2017 年 5 月 10 日

### <a name="new-features"></a>新機能

- **インストーラー:**

  - MEF キャッシュの消去に関するサポートが追加されました。

### <a name="bug-fixes"></a>バグ修正

- **コード エディター:**

  - カスタム属性を使用した分類/補完が修正されました。

  - Unity メッセージの画面のちらつきが修正されました。

## <a name="3100"></a>3.1.0.0

リリース日: 2017 年 4 月 7 日

### <a name="new-features"></a>新機能

- **デバッガー:**

  - 新しい Unity ランタイムのサポートが追加されました (.NET 4.6/C# 6 と互換性あり)。

- **Project Generation:**

  - .NET 4.6 プロファイルのサポートが追加されました。

  - mcs.rsp のサポートが追加されました。

  - Unity 5.6 の使用時にはアンセーフ コンパイル スイッチが常に有効になります。

  - Windows ストア プラットフォームと il2cpp バック エンドの使用時に "Player" プロジェクトの生成のサポートが追加されました。

### <a name="bug-fixes"></a>バグ修正

- **コード エディター:**

  - オートコンプリートでメソッドを挿入した後のキャレット位置を修正しました。

- **Project Generation:**

  - アセンブリ バージョンの後処理を削除しました。

## <a name="3001"></a>3.0.0.1

リリース日: 2017 年 3 月 7 日

### <a name="this-version-includes-all-new-features-and-bug-fixes-introduced-with-28x-series"></a>このバージョンには、2.8.x シリーズで導入されたすべての新機能とバグ修正が含まれています。

## <a name="2820---30-preview-3"></a>2.8.2.0 - 3.0 プレビュー 3
リリース日: 2017 年 1 月 25 日

### <a name="bug-fixes"></a>バグ修正

- **プロジェクトの生成:**

  - 最初はバイナリ DLL として次にプロジェクト参照として 2 回参照されたプラグイン プロジェクトの固定回帰。

## <a name="2810---30-preview-2"></a>2.8.1.0 - 3.0 プレビュー 2
リリース日: 2017 年 1 月 23 日

### <a name="bug-fixes"></a>バグ修正

- **コード エディター:**

  - かっこが完了していない状態で属性宣言を開始したときのクラッシュを修正しました。

- **デバッガー:**

  - 新しい Unity コンパイラ/ランタイムでのコルーチンを使用した関数のブレークポイントを修正しました。

  - バインドできないブレークポイントの場合 (対応するソースの場所が見つからない場合) の警告を追加しました。

- **Project Generation:**

  - 特別な/ローカライズされた文字を使用した csproj 生成を修正しました。

  - ライブラリなどのアセットの外部 (Facebook SDK).での参照を修正しました

- **その他:**

  - Unity がインストールまたはアンインストールするときに実行されないようにするチェックを追加しました。

  - リモートの Unity のドキュメントをターゲットとして https に切り替えました。

## <a name="2800---30-preview"></a>2.8.0.0 - 3.0 プレビュー
リリース日: 2016 年 11 月 17 日

### <a name="new-features"></a>新機能

- **全般:**

  - Visual Studio 2017 インストーラーのサポートを追加しました。

  - Visual Studio 2017 拡張機能のサポートを追加しました。

  - ローカライズのサポートを追加しました。

- **コード エディター:**

  - C# の IntelliSense の Unity メッセージを追加しました。

  - C# のコード配色の Unity メッセージを追加しました。

- **デバッガー:**

  - `is`、`as`、直接キャスト、`default`、`new` 式のサポートを追加しました。

  - 文字列連結式のサポートを追加しました。

  - 整数値の 16 進数表示のサポートが追加されました。

  - 新しい一時変数 (ステートメント) の作成のサポートが追加されました。

  - 暗黙的なプリミティブの変換のサポートが追加されました。

  - 型が必要なときまたは見つからないときのエラー メッセージを追加しました。

- **Project Generation:**

  - プロジェクト名から CSharp のサフィックスを削除しました。

  - システム全体の msbuild ターゲット ファイルへの参照を削除しました。

- **ウィザード:**

  - Editor や EditorWindow などの非動作の型の Unity メッセージのサポートを追加しました。

  - Unity のメッセージの挿入および書式設定のために Roslyn に切り替えました。

### <a name="bug-fixes"></a>バグ修正

- **デバッガー:**

  - ジェネリック型を評価するときに Unity がクラッシュするバグを修正しました。

  - Null 許容型の処理を修正しました。

  - 列挙値の処理を修正しました。

  - 入れ子になったメンバーの種類の処理を修正しました。

  - コレクション インデクサーのアクセスを修正しました。

  - 新しい C# コンパイラでの反復子フレームのデバッグのサポートを追加しました。

- **Project Generation:**

  - Unity Web Player を対象としたコンパイルを妨げるバグを修正しました。

  - Web エンコードされたファイル名のスクリプトをコンパイルするときにコンパイルを妨げるバグを修正しました。

## <a name="2300"></a>2.3.0.0

リリース日: 2016 年 7 月 14 日

### <a name="new-features"></a>新機能

- **全般:**

  - Visual Studio のエラー一覧で Unity コンソール ログを無効にするオプションを追加しました。

  - 生成されたプロジェクトのプロパティを変更できるオプションを追加しました。

- **デバッガー:**

  - テキスト、XML、HTML、および JSON 文字列のビジュアライザーを追加しました。

- **ウィザード:**

  - 不足している MonoBehaviors を追加しました。

### <a name="bug-fixes"></a>バグ修正

- **全般:**

  - Visual Studio の設定のコントロールの表示を妨げる ReSharper との競合を修正しました。

  - デバッグを妨げる場合がある Xamarin との競合を修正しました。

- **デバッガー:**

  - デバッグ時に Visual Studio の凍結の原因となる問題を修正しました。

  - Visual Studio 2015 内の関数のブレークポイントの問題を修正しました。

  - いくつかの式の評価の問題を修正しました。

## <a name="2200"></a>2.2.0.0

リリース日: 2016 年 2 月 4 日

### <a name="new-features"></a>新機能

- **ウィザード:**

  - **[MonoBehavior 実装]** ウィザードにスマート検索を追加しました。

  - ウィザードがコンテキスト対応になりました。たとえば、NetworkBehavior メッセージは、NetworkBehavior で作業する場合にのみ使用できます。

  - ウィザードの NetworkBehavior メッセージのサポートを追加しました。

- **UI:**

  - MonoBehavior メッセージの可視性を構成するオプションを追加しました。

  - Unity プロジェクトに関連していない Visual Studio のプロパティ ページを削除しました。

### <a name="bug-fixes"></a>バグ修正

- **プロジェクトの生成:**

  - Unity 4.6 での UnityEngine および UnityEditor への参照を修正しました。

  - Unity が OSX 上で実行している場合のプロジェクト ファイルの生成を修正しました。

  - ハッシュ記号 (#) 文字を含むプロジェクト名の処理を修正しました。

  - 生成されるプロジェクトを C# 4 に限定しました。

- **デバッガー:**

  - Unity コルーチン内のデバッグ時の式の評価に関する問題を修正しました。

  - デバッグ時に Visual Studio の凍結の原因となる問題を修正しました。

- **UI:**

  - [Tabs Studio](https://tabsstudio.com/) Visual Studio 拡張機能との非互換性の問題を修正しました。

- **インストーラー:**

  - HKLM レジストリ エントリを作成することで、VSTU のコンピューター全体のインストール (すべてのユーザー向けのインストール) をサポートします。

  - 複数の異なるバージョンの Visual Studio に同じバージョンの VSTU をインストールする際の VSTU のアンインストールに関する問題が修正されました。 VSTU **2015** 2.1.0.0 と VSTU **2013** 2.1.0.0 の両方がインストールされていた場合など。

## <a name="2100"></a>2.1.0.0

リリース日: 2015 年 9 月 8 日

### <a name="new-features"></a>新機能

- Unity 5.2 のサポート

### <a name="bug-fixes"></a>バグ修正

- Unity 4.2 以下でのメニュー項目の表示

- Visual Studio が XML IntelliSense ファイルをロックしている場合にエラー メッセージが表示されなくなりました。

- 条件付き引数がブール値でない場合は、<\<When Changed>> 条件付きブレークポイントを処理します。

- Windows ストア アプリの UnityEngine アセンブリおよび UnityEditor のアセンブリへの参照を修正しました。

- デバッガーでステップ実行するときの次のエラーを修正しました。Unable to step, general exception. (ステップ実行できません。一般例外です。)

- Visual Studio 2015 でのヒット カウント ブレークポイントを修正しました。

## <a name="2000"></a>2.0.0.0

リリース日: 2015 年 7 月 20 日

### <a name="bug-fixes"></a>バグ修正

- **Unity 統合:**

  - DLL とそのデバッグ シンボル (PDB) のインポート時に Visual Studio 2015 で作成されるデバッグ シンボルの変換を修正しました。

  - DLL とそのデバッグ シンボル (PDB) のインポート時には、MDB ファイルも提供されている場合を除いて常に MDB ファイルが生成されます。

  - obj ディレクトリによる Unity プロジェクト ディレクトリの汚染を修正しました。

  - System.Xml.Link および System.Runtime.Serialization への参照の生成を修正しました。

  - プロジェクト ファイル生成 API フックの複数サブスクライバーのサポートを追加しました。

  - 生成対象ファイルの 1 つがロックされている場合でもプロジェクト ファイルの生成が常に完了します。

  - C# プロジェクトに含めるファイルの指定時に、拡張フィルターにワイルドカード * を使用できるようになりました。

- **Visual Studio の統合:**

  - Productivity Power Tools での互換性の問題を修正しました。

  - event および delegate 宣言の周囲での MonoBehavior の生成を修正しました。

- **デバッガー:**

  - デバッグ時にフリーズすることがある問題を修正しました。

  - 特定のスタック フレームでローカルが表示されない問題を修正しました。

  - 空の配列の検査の問題を修正しました。

## <a name="1990---20-preview-2"></a>1.9.9.0 - 2.0 プレビュー 2
リリース日: 2015 年 4 月 2 日

### <a name="new-features"></a>新機能

- **Unity プロジェクト エクスプローラー:**

  - Unity プロジェクト エクスプローラーでファイルの名前を変更すると、クラスの名前が自動的に変更されます ( **[オプション]** ダイアログを参照)。

  - 新しく作成したスクリプトが Unity プロジェクト エクスプローラーで自動的に選択されます。

  - Unity プロジェクト エクスプローラーでアクティブ スクリプトを追跡できます ( **[オプション]** ダイアログを参照)。

  - Visual Studio のソリューション エクスプローラーがデュアル同期されます ( **[オプション]** ダイアログを参照)。

  - Unity プロジェクト エクスプローラーで Visual Studio のアイコンを採用しました。

- **デバッガー:**

  - 保存した、または最近使用したデバッグ ターゲットの一覧から、アクティブ デバッグ ターゲットを選択できます ( **[オプション]** ダイアログを参照)。

  - MonoBehavior メソッドで関数のブレークポイントを作成すると、複数の MonoBehavior クラスに適用されます。

  - デバッガーで [オブジェクト ID の作成] をサポートします。

  - デバッガーでブレークポイントのヒット カウントをサポートします。

  - デバッガーでの例外時の中断をサポートします (試験段階。 **[オプション]** ダイアログを参照)。

  - デバッガーで式を評価するときにオブジェクトと配列の作成をサポートします。

  - デバッガーで式を評価するときに Null 比較をサポートします。

  - デバッガーのウォッチ ウィンドウで、廃止されたメンバーが除外されます。

- **インストーラー:**

  - Visual Studio Tools for Unity 拡張機能の登録を最適化しました。

  - Unity 5 用の Visual Studio Tools for Unity パッケージがインストールされます。

- **ドキュメント:** ドキュメント生成のパフォーマンスが向上しました。

- **ウィザード:** Unity 4.6 および Unity 5 の新しい MonoBehavior メソッドをサポートします。

- **Unity:** プロジェクト ファイルの生成中に .rsp ファイル内の unsafe フラグとカスタム定義が参照されます。

- **UI:** Visual Studio の **[オプション]** ダイアログに Visual Studio Tools for Unity が追加されました。

### <a name="bug-fixes"></a>バグ修正

- **Unity プロジェクト エクスプローラー:**

  - Visual Studio のソリューション エクスプローラーでファイルを移動または名前変更した後、Unity プロジェクト エクスプローラーが適切に更新されます。

  - Unity プロジェクト エクスプローラーでファイルの名前を変更する際に、選択内容が保持されます。

  - Unity プロジェクト エクスプローラーでファイルをダブルクリックしたとき、自動的に展開と折りたたみが発生しなくなりました。

  - 新しく選択したファイルが Unity プロジェクト エクスプローラーで確実に表示されます。

- **デバッガー:**

  - デバッガーで式を評価する際に Visual Studio がフリーズすることがある問題を回避しました。

  - メソッドの呼び出しが、デバッガー内で適切なドメインで実行されます。

- **Unity:**

  - Unity 5 で、UnityVS.OpenFile の場所を修正しました。

  - Unity 5 で、pdb2mdb の場所を修正しました。

  - プロジェクト ファイルの生成中に例外が発生することのある問題を回避しました。

  - OSX 上で Unity を実行する際にフリーズすることのある問題を回避しました。

  - 内部例外を処理するようになりました。

  - Unity のコンソール ログが VS のエラー一覧に送られます。

- **ドキュメント:** 新しい Unity ドキュメントについて、ドキュメントの生成を修正しました。

- **プロジェクト:** フォルダー内でも、必要なときに Unity の .meta ファイルの移動と名前変更が行われるようになりました。

- **ウィザード:** コードを生成する際の MonoBehavior メソッドのパラメーターの順序を修正しました。

- **UI:** コンテキスト メニューおよびアイコンで Visual Studio のテーマをサポートします。

## <a name="1980---20-preview"></a>1.9.8.0 - 2.0 プレビュー
リリース日: 2014 年 11 月 12 日

### <a name="new-features"></a>新機能

- Visual Studio 2015 のサポート。

- Visual Studio 2015 の Unity シェーダー用のコード配色。

- デバッグ時の値の視覚エフェクトが向上しました:

  - ArrayList、List、Hashtable、および Dictionary の視覚エフェクトが向上しました。

  - ウォッチ ビューおよびローカル ビューの表示カテゴリとして非パブリック メンバーと静的メンバーが追加されました。

  - プロパティに対して有効な値フィールドのみを評価するように Unity の SerializedProperty の表示を改善しました。

  - クラスと構造体で DebuggerDisplayAttribute をサポートします。

  - DebuggerTypeProxyAttribute をサポートします。

- ウィザードを使用して MonoBehaviour メソッドを挿入する際に、ユーザーのコーディング規則を優先します。

- UnityVS で生成したプロジェクトで、コンパイル時のテキスト テンプレートのサポートを実装しました。

- UnityVS で生成したプロジェクトで、ResX リソースのサポートを実装しました。

- Unity から Visual Studio のシェーダーを開く操作をサポートします。

### <a name="bug-fixes"></a>バグ修正

- Visual Studio でアタッチして再生がトリガーされた後、Unity でゲームを開始する前にソケットをクリーンアップするようにしました。 これにより、アタッチして再生を使用する際に発生する Unity と VS 間の接続の安定性に関するいくつかの問題が修正されます。

- Unity のフリーズを起こしやすいので、Unity スクリプト エンジンのデバッガー インターフェイスのメソッドを呼び出さないようにしました。 これにより、デバッガーをアタッチした際の Unity のフリーズが修正されます。

- シンボルを使用できないときの呼び出し履歴の表示を修正しました。

- 必要ない場合は、ログのコールバックを登録しないようにしました。

## <a name="1920"></a>1.9.2.0

リリース日: 2014 年 10 月 9 日

### <a name="new-features"></a>新機能

- Unity プレーヤーの検出を改善しました。

- UnityVS のファイル オープン機能を使用する際に、Unity から行番号だけでなくファイル名も受け取るようにしました。

- ローカル ドキュメントが存在しない場合、Unity のオンライン ドキュメントが既定のドキュメントになります。

### <a name="bug-fixes"></a>バグ修正

- ドメインの再読み込み後にブレークポイントがヒットしたときに Unity がクラッシュすることのある潜在的な問題を修正しました。

- ドメインを再読み込みした後、UnityVS の構成ウィンドウまたはバージョン情報ウィンドウを閉じると Unity コンソールに例外が表示される問題を修正しました。

- ローカルに実行されている 64 ビットの Unity の検出を修正しました。

- ウィザードで、Unity のバージョンごとに MonoBehaviour のフィルター処理を行うように修正しました。

- 拡張子のフィルターが空である場合に、プロジェクト ファイルにすべてのアセットが含められるバグを修正しました。

## <a name="1910"></a>1.9.1.0

リリース日: 2014 年 9 月 22 日

### <a name="new-features"></a>新機能

- ブレークポイントをバインドするソースの場所を最適化しました。

- デバッガーの式の評価で、オーバーロードされたメソッドをサポートします。

- デバッガーの式の評価で、プリミティブおよび値型のボックス化をサポートします。

- 匿名メソッドをデバッグするときに、C# のローカル変数環境の再作成をサポートします。

- Visual Studio からファイルを削除または名前変更した場合、.meta ファイルも削除または名前変更されます。

### <a name="bug-fixes"></a>バグ修正

- Visual Studio のテーマの処理を修正しました。 以前は、黒のテーマでダイアログを表示すると内容が空になることがありました。

- Unity の再コンパイル中にデバッガーを接続すると Unity がフリーズする問題を修正しました。

- 別のシステムでコンパイルされたリモート エディターまたはプレーヤーをデバッグする際のブレークポイントを修正しました。

- ブレークポイントがヒットしたときに Visual Studio がクラッシュすることがある問題を修正しました。

- ブレークポイントのバインディングの問題 (ブレークポイントがアンロードされたと表示される) を回避するように修正しました。

- デバッガーでの変数のスコープ処理の問題 (ライブ変数がスコープ外として表示される) を修正しました。

- デバッガーの式の評価で静的メンバーの参照の問題を修正しました。

- デバッガーの式の評価で、静的フィールドおよびプロパティを表示する際の型の表示の問題を修正しました。

- Unity のプロジェクト名に Visual Studio で許容されない特殊文字が含まれている場合のソリューション生成の問題を修正しました (Microsoft Connect 問題番号 #948666)。

- オプションをオフに切り替えた後、コンソール イベントの送信をすぐに停止するように Visual Studio Tools for Unity パッケージを修正しました (Microsoft Connect 問題番号 #933357)。

- UnityVS で生成したプロジェクトで、UnityEngine.UI のような新しい API への参照が適切に再生成されるように、参照の検出を修正しました。

- インストールの破損を避けるため、インストール前に Visual Studio が閉じられていることを要求するようにインストーラーを修正しました。

- VSTU のすべてのバージョン間で共有される適切なスタンドアロン コンポーネントとして Unity 参照アセンブリをインストールするようにインストーラーを修正しました。

- Unity の 64 ビット バージョンの VSTU でスクリプトを開く際の問題を修正しました。

## <a name="1900"></a>1.9.0.0

リリース日: 2014 年 7 月 29 日

### <a name="new-features"></a>新機能

- [Unity デバッガーのアタッチ] ウィンドウで、デバッグするカスタム IP とポートを入力できます。

- Unity をバックグラウンドで実行するかどうかを設定する構成オプションを追加しました。

- ソリューション ファイルとプロジェクト ファイルを生成するか、プロジェクト ファイルのみを生成するかを設定する構成オプションを追加しました。

- スタートアップ ターゲット: [Unity にアタッチ] または [Unity にアタッチして再生] を選択できます。

- デバッガーで多次元配列を表示できます。

- 新しい Unity プレーヤーのデバッグ ポートを処理できます。

- Unity の 4.6 GUI アセンブリのような新しい Unity アセンブリへの参照を処理できます。

- デバッグ時とにローカル変数を適切に表示するためのデコンストラクト クロージャ。

- 生成された反復子変数は、デバッグ時には引数にデコンストラクトされます。

- プロジェクトの再読み込み後に Unity プロジェクト エクスプローラーの状態が保持されます。

- Unity プロジェクト エクスプローラーを現在のドキュメントと同期するコマンドを追加しました。

### <a name="bug-fixes"></a>バグ修正

- 条件付きブレークポイントの条件をデバッガーの開始前に設定した場合の問題を修正しました。

- 警告を回避するように UnityEngine への参照を修正しました。

- Unity ベータ版のバージョン解析の問題を修正しました。

- ブレークポイントのヒット時、またはステップ実行の際に、ローカル変数ウィンドウに変数が表示されない問題を修正しました。

- Visual Studio 2013 で、変数のツールヒントを修正しました。

- Unity 4.5 用の IntelliSense ドキュメントの生成を修正しました。

- ドメインを再読み込み (Unity で再生/停止) した後に、Unity と Visual Studio 間の通信で発生する問題を修正しました。

- Visual Studio のテーマのパーツ処理を修正しました。

> [!IMPORTANT]
> Unity のエコシステムで最もよく利用されている言語は C# です。新しいサンプル アセットは C# で記述されており、Unity のドキュメントの既定言語も今後は C# になります。C# でのエクスペリエンスに重点を移すため、Microsoft では UnityScript と Boo に対する基本的なサポートを終了しました。 その結果、現在のところ VSTU ソリューションは C# のみとなり、読み込みが大幅に高速化しました。

## <a name="1820"></a>1.8.2.0

リリース日: 2014 年 1 月 7 日

### <a name="new-features"></a>新機能

- Mavericks 上の Unity のスクリプト エンジンのネットワーク層で発生するエディターのリモート検出の問題を回避しました。

- リモート Unity プレーヤーを検出するために新しいポートを処理するようにしました。

- 現在のビルド ターゲットに固有の UnityEngine アセンブリを参照します。

- フィルター ファイルの設定を、生成されるプロジェクトに組み込みます。

- Visual Studio のエラー一覧にコンソール ログを送信する機能を無効にする設定を追加しました。 これは、PlayMaker または Console Pro を使用している場合に便利です (コンソール ログの受信先として Unity に登録できるコールバックは 1 つだけなので)。

- mdb デバッグ シンボルの生成を無効にする設定を追加しました。 これは、自分で mdb を生成している場合に便利です。

### <a name="bug-fixes"></a>バグ修正

- 4\.2 以降の Unity から VS 内のファイルを開いた場合に IntelliSense が失われるというバグ再発を修正しました。

- カスタム テーマを取り扱えるように VS のダイアログを修正しました。

- UPE のコンテキスト メニューを閉じる際の問題を修正しました。

- バージョン固有のアセンブリを生成した場合に、同期が失われると Unity がクラッシュする問題を回避するようにしました。

## <a name="1810"></a>1.8.1.0

リリース日: 2013 年 11 月 21 日

### <a name="new-features"></a>新機能

- Unity 4.3 API に対応できるように MonoBehaviour ウィザードを調整しました。

- MonoBehaviour ウィザードで、使用中のバージョンに応じて Unity の API をフィルター処理します。

- Unity 4.1 より後のプロジェクトに System.Xml.Linq への参照を追加します。

- Debug.Log の呼び出しを調整して、StackTrace の開始がメッセージに組み込まれないようにしました。

### <a name="bug-fixes"></a>バグ修正

- Visual Studio で JavaScript ファイルの既定の処理を妨げていたバグを修正しました。

- 実時間の場合に、VS で白いピクセルが現れる問題を修正しました。

- UnityVS.VersionSpecific アセンブリが SCM によって読み取り専用とマークされた場合に、そのアセンブリが削除される問題を修正しました。

- UnityVS パッケージ内のソケットを作成する際に発生する例外を修正しました。

- Visual Studio のアセンブリからストック イメージを読み込む際に Visual Studio がクラッシュする問題を修正しました。

- Unity のソース ビルドに対して UnityVS.VersionSpecific を生成する際のバグを修正しました。

- Unity パッケージでソケットを開く際に発生することのあるフリーズを修正しました。

- プロジェクト名にダッシュ (-) を使用している Unity プロジェクトの処理を修正しました。

- Unity からの開始スクリプトを修正して、Unity 4.2 以降の場合に Alt + Tab キーの動作が混同されないようにしました。

## <a name="1800"></a>1.8.0.0

リリース日: 2013 年 9 月 24 日

### <a name="new-features"></a>新機能

- デバッガーの接続速度が大幅にアップしました。

- Unity 4.2 以降で、ファイルおよび行へのナビゲーションが自動的に処理されます。

- 条件付きブレークポイント。

- プロジェクト ファイル ジェネレーターで T4 テンプレートを取り扱えます。

- 新しい API に対応するように MonBehavior ウィザードを更新しました。

- Unity の型に対する C# の IntelliSense ドキュメント。

- 算術式と論理式の評価。

- リモート デバッグのプレビューでリモート エディターの検出を改善しました。

### <a name="bug-fixes"></a>バグ修正

- デバッガーを切断した後、VS でスレッドがリークするバグを修正しました。

- VS で白いピクセルが現れる問題を修正しました。

- ステータス バーのアイコンをクリックしたときの処理を修正しました。

- Plugins フォルダー内のアセンブリに対する参照の生成を修正しました。

- UnityVS パッケージからソケットを作成したときに例外が発生した場合の問題を修正しました。

- UnityVS の新しいバージョンの検出を修正しました。

- ライセンスの有効期限が切れたときのライセンス マネージャーのプロンプトを修正しました。

- デバッガーをアタッチした際に、VS のプロセス ウィンドウに空のプロセス リストが表示されることのあるバグを修正しました。

- ローカル ビューでブール値を変更する場合の問題を修正しました。

## <a name="1220"></a>1.2.2.0

リリース日: 2013 年 7 月 9 日

### <a name="bug-fixes"></a>バグ修正

- 式の評価で完全修飾名を処理できます。

- Unity のスクリプト エンジンが UnityVS に間違ったスタックフレーム データを送信した場合の例外の処理に関連したフリーズを修正しました。

- Web をターゲットにした場合のビルド プロセスを修正しました。

- Visual Studio の起動時に、スタートアップ時に開くファイルの一覧に削除されたファイルが含まれている場合に発生することのあるエラーを修正しました。

- UnityVS.OpenFile でスクリプト以外のファイル (コンパイルしたシェーダーなど) を取り扱う際の問題を修正しました。

- すべての C# プロジェクトで Boo.Lang と UnityScript.Lang を参照します。

- プロジェクトに特殊文字がある場合のプロジェクト内の参照の生成を修正しました。

- 破棄されたプロジェクトに対するメソッド呼び出しに関して複数の NullReferenceException メッセージ ボックスがトリガーされるという VS の問題を回避しました。

- Unity 4.2 のベータ版のアセンブリの処理を修正しました。

## <a name="1210"></a>1.2.1.0

リリース日: 2013 年 4 月 9 日

### <a name="bug-fixes"></a>バグ修正

- コード補完機能で Unity アセンブリのローカル配置に関して IO エラー (読み取り専用ファイル、または Visual Studio によってロックされているファイル) が発生した場合の問題を修正しました。

- Unity からスクリプトを開いた場合に、Visual Studio で既に開かれているファイルにフォーカスが移らないというバグ再発を修正しました。

- 新しい例外処理のパフォーマンスの問題を修正しました。

- いくつかの外部 DLL 内のブレークポイントのバインディングを修正しました。

## <a name="1200"></a>1.2.0.0

リリース日: 2013 年 3 月 25 日

### <a name="new-features"></a>新機能

- デバッガーの接続速度が大幅にアップしました。

- プロジェクトが大きい場合の Unity プロジェクト エクスプローラーの動作が向上しました。

- 処理された例外と未処理の例外の発生時に中断する (または中断しない) ことについて、Visual Studio の設定を優先します。

- ローカル変数に対する ToString の呼び出しについて、Visual Studio の設定を優先します。

- [デバッグ] メニューに新しく [Unity デバッガーのアタッチ] を追加しました。これを使用すると、Unity プレーヤーでデバッグを行えます。

- ソリューション ファイルの生成時に、UnityVS ソリューションにカスタム プロジェクトが追加されて保持されます。

- キャレット位置の Unity 関数またはメンバーの Unity ドキュメントを表示するために、新しいキーボード ショートカットとして Ctrl + Alt + M → Ctrl + H キーを追加しました。

- Visual Studio からコンパイルするときに、コンパイラ応答ファイル (rsp) を考慮に入れます。

- ジェネレーター メソッドのデバッグ時に変数を表示するためにコンパイラによって生成された型をデコンストラクトします。

- リモート デバッグを簡略化するために、Unity に共有フォルダーを構成する必要性を解消しました。 Windows から Unity プロジェクトへのアクセス許可を持っているだけでよいことになりました。

- カスタム Unity プロファイルを標準 .NET ターゲット プロファイルとしてインストールします。 これにより、ReSharper が表示することのある誤検知がすべて修正されます。

- Unity スクリプト エンジンのバグの回避策を実装したため、適切に登録されていないスレッドでデバッガーが中断しないようになりました。

- ファイルのオープン要求でクラッシュしたときに、ファイルを開くことができると VS が主張した場合の競合状態を回避するために、ファイルのオープン機能を作り直しました。

- UnityVS は、VS がプロジェクトをビルドする際にビルドの更新を求めるようになり、ファイルの保存時には更新を求めないようになりました。

### <a name="bug-fixes"></a>バグ修正

- カスタム .NET プロファイルを修正しました。

- テーマの統合を修正したため、VS 2012 のダーク テーマに関連する問題が修正されました。

- VS 2012 でクイック ビヘイビアー ショートカットを修正しました。

- デバッグ時にメイン スレッド以外でブレークポイントにヒットした場合に発生することのあるステップ実行の問題を修正しました。

- 型エイリアス (int など) の補完機能に関して UnityScript と Boo を修正しました。

- 新しい UnityScript または Boo 文字列を書き込むときの例外を修正しました。

- ソリューションが読み込まれていない場合に Unity メニューを使用したときの例外を修正しました。

- バグ「UVS-48: 二重引用符をタイプするとエラーが発生してすべての機能 (コード補完、構文の強調表示など) が中断されることがある」を修正しました。

- バグ「UVS-46:Visual Studio のエラー一覧をクリックすると、スクリプト ファイル (UnityScript) が重複して開かれる」を修正しました。

- バグ「UVS-42:VS 2012 でステータス バーの Unity 接続のロゴがマウス イベントを処理しない」を修正しました。

- バグ「UVS-44:VS 2012 でクイック MonoBehaviour の Ctrl+ Shift + Q を使用できない」を修正しました。

- バグ「UVS-40:VS2012 の [ダーク] テーマで、ウィンドウがアクティブでないときに Unity プロジェクト エクスプローラーで選択したアイテムが読みにくい」を修正しました。

- バグ「UVS-39:エスケープされた文字列のトークン化の問題」を修正しました。

- バグ「UVS-35:変数を検査する際にオブジェクトに対して ToString が呼び出される」を修正しました。

- バグ「UVS-27:VS2012 で、シンボルへ移動ウィンドウが [ダーク] テーマと一致しない」を修正しました。

- バグ「UVS-11:コルーチンでのローカル」を修正しました。

## <a name="1100---beta-release"></a>1.1.0.0 - ベータ リリース
リリース日: 2013 年 3 月 9 日

## <a name="10130"></a>1.0.13.0
リリース日: 2013 年 1 月 21 日

### <a name="bug-fixes"></a>バグ修正

- デバッグ対象により無効なスレッド イベントが送信される場合に発生することのある Visual Studio のハングアップを修正しました。 これは多くの場合、OSX 上のリモートの Unity をデバッグするときに発生していました。

- 例外によってデバッガーがシャットダウンした場合に発生することのある Visual Studio のハングアップを修正しました。

- C# MonoBehavior が名前空間に含まれている場合の MonoBehavior ヘルパーを修正しました。

- Visual Studio 2012 で UnityScript に対するデバッガーのツールヒントを修正しました。

- Unity からデバッグ定数が変更されただけの場合のプロジェクトの生成を修正しました。

- Unity プロジェクト エクスプローラーでのキーボード ナビゲーションを修正しました。

- エスケープされた文字列の UnityScript での色づけを修正しました。

- Unity の外部で使用された場合に、UnityVS のファイル オープン機能でのプロジェクト名の推測を改善しました。 これは、ユーザーが Unity で UnityVS の代理をするサード パーティのファイル オープン機能を使用している場合に必要になります。

- Unity から UnityVS に長いメッセージが送信された場合の処理を修正しました。 以前は、長いメッセージを処理する UnityVS のメッセージング部分でクラッシュすることがあったため、 Unity から UnityVS のファイルを開けないことがありました。

## <a name="10120"></a>1.0.12.0
リリース日: 2013 年 1 月 3 日

### <a name="bug-fixes"></a>バグ修正

- Visual Studio がブレークポイントを削除するときに発生することのある Visual Studio のハングアップを修正しました。

- Unity がゲーム スクリプトを再コンパイルした後に一部のブレークポイントがヒットしなくなるバグを修正しました。

- ブレークポイントがバインドされていない場合にデバッガーから Visual Studio に適切に通知するように修正しました。

- Visual Studio デバッガーによるネイティブ プログラムのデバッグを妨げることのある登録の問題を修正しました。

- UnityScript および Boo の式を評価するときに発生することのある例外を修正しました。

- Unity で .NET の API レベルを変更した場合にプロジェクト ファイルの更新がトリガーされないというバグ再発を修正しました。

- ユーザー コードがログのコールバック ハンドラーに参加できないという API の不具合を修正しました。

## <a name="10110"></a>1.0.11.0
リリース日: 2012 年 11 月 28 日

### <a name="new-features"></a>新機能

- Unity 4 の公式サポート。

- Unity プロジェクト エクスプローラーからのスクリプトの操作。

- Visual Studio の移動ウィンドウとの統合。

- コンソール メッセージの情報を解析することにより、エラー一覧をクリックするとシンボル付きのスタックフレームの先頭に移動できるようになりました。

- ユーザーがプロジェクトの生成に参加できるようにする API を追加しました。

- ユーザーが LogCallback に参加できるようにする API を追加しました。

### <a name="bug-fixes"></a>バグ修正

- Visual Studio 2012 での Unity プロジェクト エクスプローラーの背景のバグ再発を修正しました。

- 完全な .NET プロファイルを持つユーザーを対象としたプロジェクト生成を修正しました。

- Web ターゲットを持つユーザーのためのプロジェクト生成を修正しました。

- Unity と同様に DEBUG および TRACE コンパイル シンボルを組み込むようにプロジェクト生成を修正しました。

- UnityVS のシンボルへの移動ウィンドウで特殊文字を使用した場合のクラッシュを修正しました。

- Visual Studio のステータス バーに UnityVS のアイコンを挿入できない場合のクラッシュを修正しました。

## <a name="10100"></a>1.0.10.0
リリース日: 2012 年 10 月 9 日

### <a name="bug-fixes"></a>バグ修正

- Visual Studio 2010 での Unity プロジェクト エクスプローラーの背景の問題を修正しました。

- デバッガー インターフェイスが以前にクラッシュした Unity に UnityVS がデバッガーをアタッチしようとした場合に発生することのある Visual Studio のフリーズを修正しました。

- ブレークポイントが設定されている場合に AppDomain の再読み込みが発生すると Visual Studio がフリーズすることのある問題を修正しました。

- Unity からのアセンブリの取得方法を修正することにより、ファイルのロックにより Unity のビルド プロセスが混乱するという問題を回避しました。

## <a name="1090"></a>1.0.9.0

リリース日: 2012 年 10 月 3 日

### <a name="bug-fixes"></a>バグ修正

- Unity プロジェクトに実際の JavaScript アセットが含まれている場合のプロジェクトの生成を修正しました。

- 式の評価でのエラー処理を修正しました。

- 値型のフィールドに新しい値を設定するときの問題を修正しました。

- マウス ポインターをコード エディターから式に移動した場合に発生することのある副作用を修正しました。

- 式の評価のために読み込まれたアセンブリから型を検索する方法を修正しました。

- バグ「UVS-21:Unity オブジェクトへの割り当てを評価しても効果が出ない」を修正しました。

- バグ「UVS-21:Unity Math API へのメソッドの呼び出しを評価すると、無効なポインターが発生する」を修正しました。

## <a name="1080"></a>1.0.8.0

リリース日: 2012 年 9 月 26 日

### <a name="bug-fixes"></a>バグ修正

- UnityVS のスクリプト オープン機能がプロジェクトへのパスを取得する方法を修正することにより、確実に Visual Studio とスクリプトの両方を開けるようにしました。

- デバッグ セッションの実行中にブレークポイントを作成すると Visual Studio がハングアップすることがあるバグを修正しました。

- UnityVS が Visual Studio 2010 に登録される方法を修正しました。

## <a name="1070"></a>1.0.7.0

リリース日: 2012 年 9 月 14 日

### <a name="new-features"></a>新機能

- Visual Studio 2012 のサポート。

### <a name="bug-fixes"></a>バグ修正

- エディターおよびプラグインのプロジェクト ファイルの生成を、Unity の動作と一致するように修正しました。

- Unity 4 での .pdb シンボルの変換を修正しました。

> [!IMPORTANT]
> Visual Studio 2012 をサポートするため、一部のファイルの名前変更や移動を行いました。 Unity をインポートする UnityVS パッケージの名前を、Visual Studio 2010 であるか Visual Studio 2012 であるかに応じて UnityVS 2010 または UnityVS 2012 とするようにしました。 さらに、このバージョンでは、UnityVS プロジェクト ファイルを再生成する必要もあります。

## <a name="1060---internal-build"></a>1.0.6.0 - 内部ビルド
リリース日: 2012 年 9 月 12 日

## <a name="1050"></a>1.0.5.0

リリース日: 2012 年 9 月 10 日

### <a name="bug-fixes"></a>バグ修正

- スクリプトまたはシェーダーに無効な XML 文字がある場合のプロジェクト ファイルの生成を修正しました。

- Unity がアセット サーバーに接続されている場合の Unity インスタンスの検出を修正しました。 この問題が原因で、Unity からのファイルのオープンと Visual Studio デバッガーの自動接続に不具合が起きていました。

## <a name="1040"></a>1.0.4.0

リリース日: 2012 年 9 月 5 日

### <a name="new-features"></a>新機能

- Unity でのデバッグ シンボルの自動変換。

    アセット フォルダーに .NET .dll アセンブリとそれに対応する .pdb があれば、アセンブリを再インポートするだけで、UnityVS により .pdb が変換されて、Unity のスクリプト エンジンが理解できるデバッグ シンボル ファイルになるため、UnityVS から .NET アセンブリにステップインできます。

### <a name="bug-fixes"></a>バグ修正

- Unity 内のメソッドやプロパティによってスローされた例外が原因でデバッグ中に UnityVS がクラッシュする問題を修正しました。

## <a name="1030"></a>1.0.3.0

リリース日: 2012 年 9 月 4 日

### <a name="new-features"></a>新機能

- Unity からファイルを開くために UnityVS を使用することを無効にする新しい構成オプション。

### <a name="bug-fixes"></a>バグ修正

- エディター以外のプロジェクトに対する UnityEditor への参照の生成を修正しました。

- エディター以外のプロジェクトに対する UNITY_EDITOR シンボルの定義を修正しました。

- UnityVS のカスタム ステータス バーが原因で VS がランダムにクラッシュする問題を修正しました。

## <a name="1020"></a>1.0.2.0

リリース日: 2012 年 8 月 30 日

### <a name="bug-fixes"></a>バグ修正

- PythonTools デバッガーとの競合を修正しました。

- Mono.Cecil への参照を修正しました。

- Unity から Unity 4 b7 を使用してスクリプティング アセンブリを取得する方法のバグを修正しました。

## <a name="1010"></a>1.0.1.0

リリース日: 2012 年 8 月 28 日

### <a name="new-features"></a>新機能

- Unity 4.0 のベータ版のプレビュー サポート。

### <a name="bug-fixes"></a>バグ修正

- 例外をスローしているプロパティの検査を修正しました。

- オブジェクトの検証中に基底オブジェクトに降下するときの問題を修正しました。

- MonoBehavior ウィザードの挿入ポイントに空のドロップダウン リストが表示される問題を修正しました。

- アセット フォルダー内の dll について UnityScript と Boo 用に実行される補完機能を修正しました。

## <a name="1000---initial-release"></a>1.0.0.0 - 初期リリース
リリース日: 2012 年 8 月 22 日
