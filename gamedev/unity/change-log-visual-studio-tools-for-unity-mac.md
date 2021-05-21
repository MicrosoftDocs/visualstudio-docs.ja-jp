---
title: 変更ログ (Visual Studio Tools for Unity、Mac) | Microsoft Docs
description: Visual Studio Tools for Unity、Mac の変更ログを確認します。 バージョン 1.0.0.0 から 2.7.0.0 以降にかけて行われた変更を確認します。
ms.custom: ''
ms.date: 3/1/2021
ms.technology: vs-unity-tools
ms.prod: visual-studio-dev16
ms.topic: conceptual
ms.assetid: 33a6ac54-d997-4308-b5a0-af7387460849
author: therealjohn
ms.author: johmil
manager: crdun
ms.workload:
- unity
ms.openlocfilehash: f11c5c1407d16d7a82a9d8d24e6a8dd3a04e57eb
ms.sourcegitcommit: 5654b7a57a9af111a6f29239212d76086bc745c9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/03/2021
ms.locfileid: "101683372"
---
# <a name="change-log-visual-studio-tools-for-unity-mac"></a>変更ログ (Visual Studio Tools for Unity、Mac)

Visual Studio Tools for Unity の変更ログです。

## <a name="2920"></a>2.9.2.0
リリース日: 2021 年 3 月 2 日

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - Unity メッセージ ダイアログでの検索の強調表示を修正しました。

  - Unity プロジェクトのツリー ビューの安定性の問題を修正しました。

- **デバッグ:**

  - 条件付きブレークポイントの処理を修正しました。

## <a name="2910"></a>2.9.1.0
リリース日: 2021 年 2 月 9 日

### <a name="new-features"></a>新機能

- **統合:**

  - IDE での Unity のテストの実行とデバッグのサポートを追加しました。

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

  - Unity メッセージ ダイアログの安定性の問題を修正しました。

  - ENU 以外の言語のさまざまな UI の問題を修正しました。

  - [`UNT0018`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0018.md) 診断に関する安定性の問題を修正しました。

- **デバッグ:**

  - `Trace` メソッドを使用するときに VM が切断される問題を修正しました。

- **評価:**

  - 例外をスローする古いプロパティのフィルター処理を修正しました。

## <a name="2900"></a>2.9.0.0
リリース日: 2021 年 1 月 20 日

### <a name="new-features"></a>新機能

- **統合:**

  - `raytrace shaders`、`UXML`、および `USS` のファイルのサポートを追加しました。

  - (コルーチンとして使用されているすべてのメソッドの) Unity メッセージ API を更新しました。

  - Android SDK 検出を更新しました。

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - コルーチンと `AssetPostprocessor.OnAssignMaterialModel` に対して間違った警告を出す、[`UNT0006`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0006.md) 診断を修正しました。

## <a name="2840"></a>2.8.4.0
リリース日: 2020 年 12 月 15 日

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - Unity イベント作成ウィザードを閉じる際の信頼性の問題を修正しました。

## <a name="2830"></a>2.8.3.0
リリース日: 2020 年 11 月 10 日

### <a name="bug-fixes"></a>バグ修正

- **デバッガー:**

  - ソリューションに VSTU プロジェクトが存在しない場合の Unity へのアタッチを修正しました。

## <a name="2820"></a>2.8.2.0
リリース日: 2020 年 10 月 27 日

### <a name="new-features"></a>新機能

- **統合:**

  - `MonoBehaviour` だけでなく `Component` を継承するすべてに適用されるように、[`UNT0010`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0010.md) 診断を改善しました。

## <a name="2810"></a>2.8.1.0
リリース日: 2020 年 10 月 13 日

### <a name="new-features"></a>新機能

- **評価:**

  - 呼び出しによる暗黙的な変換のサポートが追加されました。 以前は、エバリュエーターによって厳密な型チェックが適用され、`Failed to find a match for method([parameters...])` 警告メッセージが生成されていました。

- **統合:**

  - [`UNT0018`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0018.md) 診断が追加されました。 `Update`、`FixedUpdate`、`LateUpdate`、または `OnGUI` のようなパフォーマンスが重要なメッセージでは、`System.Reflection` 機能を使用しないでください。

  - [`USP0003`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0003.md) および [`USP0005`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0005.md) サプレッサーを改善し、すべての `AssetPostprocessor` 静的メソッドがサポートされるようになりました。

  - `CS8618` 用の [`USP0016`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0016.md) サプレッサーが追加されました。 `C# 8.0` によって、null 許容参照型と null 非許容参照型が導入されます。 `UnityEngine.Object` から継承する型の初期化検出はサポートされず、エラーが発生します。

  - 現在、Unity 2019.x と 2020.x+ の両方で、同じプレーヤーおよび asmdef プロジェクト生成メカニズムを使用しています。
  
  - ウィザードを使用して Unity メッセージを生成するときのユーザー エクスペリエンスが向上しました。

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - コメント内のメッセージが予期せずに完了することを修正しました。

## <a name="2800"></a>2.8.0.0 
リリース日: 2020 年 9 月 14 日

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - Unity 2019.x でのプレーヤー プロジェクト生成を修正しました。

## <a name="2710"></a>2.7.1.0
リリース日: 2020 年 8 月 5 日

### <a name="new-features"></a>新機能

- **統合:**

  - Unity メッセージ API を 2019.4 に更新しました。

  - `CA1823` 用の [`USP0013`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0013.md) サプレッサーが追加されました。 `SerializeField` または `SerializeReference` 属性を持つプライベート フィールドを未使用としてマークすることはできません (FxCop)。
  
  - `CA1822` 用の [`USP0014`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0014.md) サプレッサーが追加されました。 Unity メッセージを `static` 修飾子の候補としてフラグ設定することはできません (FxCop)。

  - `CA1801` 用の [`USP0015`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0015.md) サプレッサーが追加されました。 使用されていないパラメーターを Unity メッセージから削除することはできません (FxCop)。
  
  - [`USP0009`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0009.md) サプレッサーに `MenuItem` サポートを追加しました。  

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - 追加のかっこやメソッド引数と共に動作しない [`USP0001`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0001.md) および [`USP0002`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0002.md) サプレッサーを修正しました。
  
  - Unity の設定で自動更新が無効になっている場合でも資産データベースの更新が強制される問題を修正しました。

## <a name="2700"></a>2.7.0.0
リリース日: 2020 年 6 月 23 日

### <a name="new-features"></a>新機能

- **統合:**

  - Unity によってソリューションとプロジェクトが再生成されるときに、ソリューション フォルダーを保持するためのサポートを追加しました。

  - [`UNT0015`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0015.md) 診断が追加されました。 `InitializeOnLoadMethod` または `RuntimeInitializeOnLoadMethod` 属性を使用して、不適切なメソッド シグネチャを検出します。

  - [`UNT0016`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0016.md) 診断が追加されました。 文字列リテラルである最初の引数と共に `Invoke`、`InvokeRepeating`、`StartCoroutine`、または `StopCoroutine` を使用するのは、タイプ セーフではありません。

  - [`UNT0017`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0017.md) 診断が追加されました。 `SetPixels` の呼び出しは低速です。

### <a name="bug-fixes"></a>バグ修正

- **デバッガー:**

  - ゲームが古い Mono ランタイムで実行されている間のブレークポイントの作成を修正しました (作成後すぐにブレークポイントのバインドが試みられます)。 
  
- **統合:**

  - Unity メッセージ ウィザードでメッセージをフィルター処理するときに、選択項目がリセットされません。
  
  - 次の規則で [`USP0004`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0004.md)、[`USP0006`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0006.md)、および [`USP0007`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0007.md) サプレッサーを修正しました: SerializeField 属性で修飾されたすべてのフィールドの `IDE0044` (読み取り専用)、`IDE0051` (未使用)、`CS0649` (未割り当て) が抑制されます。 `Unity.Object` を拡張したすべての型のパブリック フィールドの `CS0649` (未割り当て) が抑制されます。

  - [`UNT0014`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0014.md) のジェネリック型パラメーターのチェックを修正しました。

- **評価:**

  - 列挙型での等価比較を修正しました。

## <a name="2610"></a>2.6.1.0
リリース日: 2020 年 5 月 19 日

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - Unity 側でメッセージング サーバーを作成できない場合に警告します。

  - ライトウェイト コンパイル中にアナライザーを適切に実行します。

  - Unity Hub のインストールを含むように API ドキュメントを修正しました。
  
  - デバッガー ビジュアライザーのクラッシュを修正しました。

## <a name="2600"></a>2.6.0.0
リリース日: 2020 年 4 月 14 日

### <a name="new-features"></a>新機能

- **統合:**

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
  
  - Null 値の処理を修正しました。  

## <a name="2520"></a>2.5.2.0

リリース日: 2020 年 3 月 23 日

### <a name="bug-fixes"></a>バグ修正

- **デバッガー:**

  - アタッチ時のスレッドの登録を修正しました。

## <a name="2510"></a>2.5.1.0

リリース日: 2020 年 3 月 3 日

### <a name="new-features"></a>新機能

- **統合:**

  - `IDE0051` 用の [`USP0008`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0008.md) サプレッサーが追加されました。 Invoke、InvokeRepeating、StartCoroutine、または StopCoroutine で使用されるプライベート メソッドを未使用としてマークすることはできません。

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - OnDrawGizmos と OnDrawGizmosSelected のドキュメントを修正しました。

- **評価:**

  - ラムダ引数の検査を修正しました。

## <a name="2501"></a>2.5.0.1

リリース日: 2020 年 2 月 19 日

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - [`UNT0006`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0006.md) の不適切なメッセージの署名に対する診断チェックを修正しました。 複数のレベルの継承を含む型を検査すると、この診断は次のメッセージで失敗します: `warning AD0001: Analyzer 'Microsoft.Unity.Analyzers.MessageSignatureAnalyzer' threw an exception of type 'System.ArgumentException' with message 'An item with the same key has already been added`。

## <a name="2500"></a>2.5.0.0

リリース日: 2020 年 1 月 22 日

### <a name="new-features"></a>新機能

- **統合:**

  - HLSL ファイルのサポートが追加されました。
  
  - 新しいフォルダー ダイアログ UI に切り替えました。
  
  - 設定を新しいアクセス可能なプロパティ グリッドに切り替えました。

  - `IDE0051` 用の [`USP0006`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0006.md) サプレッサーが追加されました。 `SerializeField` 属性を持つプライベート フィールドを未使用としてマークすることはできません。

  - `CS0649` 用の [`USP0007`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0007.md) サプレッサーが追加されました。 `SerializeField` 属性を持つフィールドを未割り当てとしてマークすることはできません。  

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - プロジェクトの生成を修正しました (`GenerateTargetFrameworkMonikerAttribute` ターゲットは常に正しく配置されていませんでした)。

- **評価:**

  - 文字列の評価を修正しました (ToString() 呼び出しを使用しません)

## <a name="2420"></a>2.4.2.0

リリース日: 2019 年 12 月 3 日

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - 診断のユーザー定義インターフェイスを修正しました。

  - クイック ヒントの間違った形式の式を修正しました。
  
## <a name="2410"></a>2.4.1.0

リリース日: 2019 年 11 月 6 日

### <a name="new-features"></a>新機能

- **統合:**

  - Unity バックグラウンド プロセスのサポートを追加しました。 (デバッガーは子プロセスではなくメイン プロセスに自動接続できます)。

  - Unity メッセージのクイック ヒントを追加しました。関連するドキュメントが表示されます。

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - タグ比較アナライザー `UNT0002` の、高度なバイナリ式および呼び出し式を修正しました。

### <a name="deprecated-features"></a>非推奨の機能

- **統合:**

  - 今後、Visual Studio Tools for Unity では Visual Studio 2017 以降のみがサポートされます。

## <a name="2400"></a>2.4.0.0

リリース日: 2019 年 10 月 15 日

### <a name="new-features"></a>新機能

- **統合:**

  - すべての Unity メッセージに対して `IDE0060` (未使用パラメーター) 用の [`USP0005`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0005.md) サプレッサーが追加されました。

  - `TooltipAttribute` でタグ付けされたフィールド用のクイック ヒントを追加しました。 (これは、このフィールドを使用する単純な get アクセサーに対しても機能します)。

## <a name="2330"></a>2.3.3.0

リリース日: 2019 年 9 月 23 日

### <a name="new-features"></a>新機能

- **統合:**

  - 未使用パラメーターを削除するためのクイック修正が IDE に表示されないよう、IDE0060 用に新しい非表示機能が追加されました。
    - `IDE0060` の `USP0005`:Unity メッセージは Unity ランタイムによって呼び出されます。

## <a name="2320"></a>2.3.2.0

リリース日: 2019 年 9 月 16 日

### <a name="new-features"></a>新機能

- **統合:**

  - Unity に固有の新しい診断を追加することによって、Visual Studio が Unity プロジェクトをより深く理解できるようにしました。 また、Unity プロジェクトには適用されない一般的な C# 診断を抑制することで、IDE をよりスマートにしました。 たとえば、IDE では、インスペクター変数 `readonly` を変更するクイック修正は表示されません。これにより、Unity エディターで変数を変更できなくなります。
    - `UNT0001`:Unity メッセージは空の場合でもランタイムによって呼び出されます。それらのメッセージを宣言する場合は、不要な処理を Unity ランタイムが回避するようにしないでください。
    - `UNT0002`:文字列の等価性を使用したタグ比較は、組み込みの CompareTag メソッドよりも遅くなります。
    - `UNT0003`:型の安全性のため、GetComponent のフォームは汎用的なものを使用することが推奨されています。
    - `UNT0004`:更新メッセージはフレームレートに依存しているため、Time.fixedDeltaTime ではなく Time.deltaTime instead を使用する必要があります。
    - `UNT0005`:FixedUpdate メッセージはフレームレートに依存しないため、Time.deltaTime ではなく Time.fixedDeltaTime を使用する必要があります。
    - `UNT0006`:この Unity メッセージに対して無効なメソッド署名が検出されました。
    - `UNT0007`:Unity では、null 合体演算子と互換性のない、Unity オブジェクト用の null 比較演算子がオーバーライドされます。
    - `UNT0008`:Unity では、null 反映演算子と互換性のない、Unity オブジェクト用の null 比較演算子がオーバーライドされます。
    - `UNT0009`:InitializeOnLoad 属性をクラスに適用する場合は、静的コンストラクターを指定する必要があります。 InitializeOnLoad 属性を使用すると、エディターの起動時にそれが確実に呼び出されます。
    - `UNT0010`:MonoBehaviours は、AddComponent() を使用してのみ作成する必要があります。 MonoBehaviour はコンポーネントであり、GameObject にアタッチする必要があります。
    - `UNT0011`:ScriptableObject は CreateInstance() を使用してのみ作成する必要があります。 Unity メッセージ メソッドを処理するには、Unity エンジンによって ScriptableObject を作成する必要があります。
    - `IDE0029` の `USP0001`:Unity オブジェクトでは、null 合体演算子を使用しないでください。
    - `IDE0031` の `USP0002`:Unity オブジェクトでは null 反映演算子を使用しなきでください。
    - `IDE0051` の `USP0003`:Unity メッセージは Unity ランタイムによって呼び出されます。
    - `IDE0044` の `USP0004`:SerializeField 属性を持つフィールドを読み取り専用にしないでください。

## <a name="2310"></a>2.3.1.0

リリース日: 2019 年 9 月 4 日

### <a name="new-features"></a>新機能

- **評価:**

  - 型の表示を改善するためのサポートが追加されました。すなわち、`List'1[[System.Object, <corlib...>]]` ではなく `List<object>` になりました。

  - ポインター メンバー アクセスのサポートが追加されました。すなわち、`p->data->member` のようになりました。

  - 配列初期化子での暗黙的な変換のサポートが追加されました。すなわち、`new byte [] {1,2,3,4}` のようになりました。

  - バイト配列と文字列を検査するときの 16 進エディターのサポートが追加されました。

## <a name="2300"></a>2.3.0.0

リリース日: 2019 年 8 月 13 日

### <a name="bug-fixes"></a>バグ修正

- **評価:**

  - 例外とともにステップ実行の問題を修正しました。

  - 擬似識別子 ($exception など) の評価を修正しました。

  - 無効なアドレスを逆参照するときにクラッシュしないようにします。  

  - アンロードされた AppDomain の問題を修正しました。

## <a name="2200"></a>2.2.0.0

リリース日: 2019 年 7 月 25 日

### <a name="bug-fixes"></a>バグ修正

- **評価:**

  - IntPtr 型を使用した検査を修正しました。

- **デバッガー:**

  - キャッチポイントと関数のブレークポイントの処理を修正した。

## <a name="2130"></a>2.1.3.0

リリース日: 2019 年 7 月 9 日

### <a name="new-features"></a>新機能

- **デバッガー:**

  - 例外のサブクラスをキャッチするためのサポートを追加しました。

  - MDS プロトコル 2.51 のサポートが追加されました。

- **統合:**

  - asmdef ファイルのサポートが追加されました。

  - テンプレートからファイルが追加されたときに名前変更モードに切り替えます (Unity エディターの動作を模倣するため)。

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - Unity プレーヤーとの通信中の誤った形式のメッセージの処理を修正しました。

- **評価:**

  - 式の名前空間の処理を修正しました。

## <a name="2120"></a>2.1.2.0

リリース日: 2019 年 7 月 2 日

### <a name="bug-fixes"></a>バグ修正

- **評価:**

  - 解析できない式に関するエラー報告を修正しました。

## <a name="2110"></a>2.1.1.0

リリース日: 2019 年 6 月 27 日

### <a name="new-features"></a>新機能

- **統合:**

  - MonoBehaviour API を 2019.1 に更新しました。

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - Unity プロジェクト エクスプ ローラーのパフォーマンスを修正しました。

  - ライトウェイト ビルドが有効な場合に、警告とエラーが出力に報告されることを修正しました。

  - ライトウェイト ビルドのパフォーマンスを修正しました。

## <a name="2100"></a>2.1.0.0

リリース日: 2019 年 6 月 20 日

### <a name="new-features"></a>新機能

- **統合:**

  - IntelliSense エラーと警告の使用を優先して、Unity プロジェクトのフル ビルドを無効にしました。 Indeed Unity では、Unity が内部で実行していることを表すクラス ライブラリ プロジェクトによって Visual Studio ソリューションが作成されます。 ただし、Visual Studio でのビルドの結果は、Unity によって使用されたり、選択されたりすることはありません。それらのコンパイル パイプラインが閉じているためです。 Visual Studio でのビルドによって、何もしなくてもリソースが消費されます。 フル ビルドに依存するツールまたは設定があるため、フル ビルドを必要とする場合は、この最適化を無効にできます ([設定]/[Tools for Unity]/[プロジェクトのフル ビルドを無効にする])。
  
  - UPE での Unity パッケージのサポートを追加しました。 参照されているパッケージ (`Packages` フォルダー内の manifest.json を使用して) とローカル パッケージ (`Packages` フォルダーに埋め込まれた) のみが表示されます。

## <a name="2021"></a>2.0.2.1

リリース日: 2019 年 5 月 30 日

### <a name="new-features"></a>新機能

- **統合:**

  - Unity 実行ターゲット用のカスタム アイコンが追加されました。

## <a name="2020"></a>2.0.2.0

リリース日: 2019 年 4 月 2 日

### <a name="new-features"></a>新機能

- **統合:**

  - 保存時に Unity のアセット データベースを自動更新するサポートを追加しました。 これは既定で有効になっており、Visual Studio 内にスクリプトを保存するときに Unity 側での再コンパイルをトリガーします。 Unity\Refresh Unity の AssetDatabase に対しては、保存時に Tools\Options\Tools にあるこの機能を無効にできます。

  - オフライン ドキュメントに適切な Unity インストールを設定するためのサポートが追加されました。

  - 新しいエディター用のコンテキスト メニューが追加されました。

### <a name="bug-fixes"></a>バグ修正

- **デバッガー:**

  - アセンブリのフィルター処理と空フレームによるフレームの検査が修正されました。

## <a name="2011"></a>2.0.1.1
 
 リリース日: 2019 年 3 月 26 日

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - 一時的に Mono を既定とし、このリリース限定で使用可能なデバッガーとしました。

## <a name="2006"></a>2.0.0.6

リリース日: 2019 年 3 月 26 日

### <a name="new-features"></a>新機能

- **統合:**

  - "Unity にアタッチして再生" にサポートを追加しました。

## <a name="2005"></a>2.0.0.5

リリース日: 2019 年 3 月 20 日

### <a name="new-features"></a>新機能

- **Project Generation:**

  - ソリューション ファイルを処理するときに、外部のプロパティを保持します。
  
- **評価:**

  - 別名で修飾された名前 (現在のところグローバル名前空間のみ) のサポートを追加しました。 そのため、式エバリュエーターで形式 global::namespace.type を使用した型を受け付けるようになりました。

  - `pointer[index]` 形式のサポートを追加しました。これはポインター逆参照 `*(pointer+index)` 形式と同じ意味です。

## <a name="2004"></a>2.0.0.4

リリース日: 2019 年 3 月 5 日

### <a name="new-features"></a>新機能

- **統合:**

  - `ScriptableObject` API を更新しました。

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - テンプレートから名前空間を削除しました。

## <a name="2003"></a>2.0.0.3
 
 リリース日: 2019 年 3 月 5 日

### <a name="new-features"></a>新機能

- **Project Generation:**

  - パブリック フィールドとシリアル化されたフィールドで、警告が発行されなくなりました。 `CS0649` および `IDE0051` のメッセージを作成していた Unity プロジェクトでは、これらのコンパイラの警告を自動抑制しました。

- **統合:**

  - 複数の Unity プロセスが実行されている場合に、特定のインスタンスへのアタッチを要求します。

- **評価:**

  - ローカル関数のサポートを追加しました。

### <a name="bug-fixes"></a>バグ修正

- **デバッガー:**

  - 古いプロトコル バージョン使用時の名前付き引数に対するカスタム属性の読み取りを修正しました。

## <a name="2002"></a>2.0.0.2

リリース日: 2019 年 2 月 4 日

### <a name="new-features"></a>新機能

- **統合:**

  - MonoBehaviour API を更新しました。

### <a name="bug-fixes"></a>バグ修正

- **デバッガー:**

  - デバッガーでのプリミティブ値の設定を修正しました。

## <a name="2001"></a>2.0.0.1

リリース日: 2018 年 12 月 4 日

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - インストール パッケージの内容を修正しました。

## <a name="2000"></a>2.0.0.0
 リリース日: 2018 年 12 月 4 日

### <a name="new-features"></a>新機能

- **デバッガー:**

  - Mac 上の Unity デバッガーを Windows の同じコア Unity デバッガーに置き換えました。

  - 式の評価には、NRefactory よりも Roslyn を使用するように置き換えました。

  - ポインターへのサポートを追加しました: 逆参照、キャスト、およびポインターの算術演算 (これには、Unity 2018.2+ および新しいランタイムの両方が必要です)。

  - (C++ の場合のように) 配列ポインター ビューのサポートを追加しました。 ポインター式を取得してから、コンマと表示する要素数を付け加えます。

  - 非同期のコンストラクトのサポートを追加しました。

  - 擬似変数のサポートを追加しました (例外とオブジェクト識別子)。

### <a name="bug-fixes"></a>バグ修正

- **デバッガー:**

  - 形式が正しくないかサポートされていない式での式の評価を修正しました。

## <a name="1700"></a>1.7.0.0

リリース日: 2018 年 11 月 13 日

### <a name="new-features"></a>新機能

- **デバッガー:**

  - アタッチ ダイアログにクライアント情報を追加しました (IP、コンピューター名)。

### <a name="bug-fixes"></a>バグ修正

- **デバッガー:**

  - Unity のデバッガー エンジンとの通信に使用されるライブラリでのデッドロックを修正しました。このバグによって、特に [Unity にアタッチ] を選択した場合やゲームを再起動したときに、Visual Studio または Unity がフリーズしていました。

- **統合:**

  - 別のデフォルト エディターが選択されたときの Unity プラグイン アクティベーションを修正しました。

  - Unity ファイルのテンプレート作成を修正しました。

## <a name="1602"></a>1.6.0.2

リリース日: 2018 年 7 月 24 日

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - Unity により修正された Unity パフォーマンス バグの回避策がロールバックされました。

## <a name="1601"></a>1.6.0.1

リリース日: 2018 年 7 月 10 日

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - シェーダー コードの配色のサポートを修正しました。

## <a name="1600"></a>1.6.0.0

リリース日: 2018 年 6 月 26 日

### <a name="bug-fixes"></a>バグ修正

- **ウィザード:**

  - OnApplicationFocus メッセージのタイポを修正しました。

- **Project Generation:**

  - Unity のパフォーマンスのバグの一時的な回避策: プロジェクト生成時の MonoIslands のキャッシュ。

  - 今後、新しい Unity ランタイムを使用するときにはポータブル pdb を mdb に変換しないでください。

## <a name="1502"></a>1.5.0.2

リリース日: 2018 年 4 月 18 日

### <a name="new-features"></a>新機能

- **統合:**

  - 基本的なシェーダー コードの補完機能のサポートが追加されました。

  - シェーダー ファイル内でのコメント切り替えのサポートが追加されました。

## <a name="1501"></a>1.5.0.1

リリース日: 2018 年 3 月 28 日

### <a name="new-features"></a>新機能

- **統合:**

  - Unity プロジェクト エクスプローラーが追加テンプレート対応になりました。

## <a name="1500"></a>1.5.0.0

リリース日: 2018 年 3 月 21 日

### <a name="new-features"></a>新機能

- **統合:**

  - USB 経由で Android プレーヤーを検出し、接続できるようになりました。

## <a name="1403"></a>1.4.0.3

リリース日: 2018 年 3 月 5 日

### <a name="new-features"></a>新機能

- **Project Generation:**

  - Unity 2018.1 の新しいプロジェクト ジェネレーターのサポートが追加されました。

- **統合:**

  - 専用設定のオプション パネルが追加されました。

## <a name="1402"></a>1.4.0.2

リリース日: 2018 年 1 月 24 日

### <a name="bug-fixes"></a>バグ修正

- **Project Generation:**

  - Mono バージョンの検出を修正しました。

- **統合:**

  - 2018.1 とプラグインのアクティブ化のタイミングの問題を修正しました。

  - 新しいプレーヤーを検出したときの通知を修正しました。

## <a name="1401"></a>1.4.0.1

リリース日: 2018 年 1 月 23 日

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - ダブルクリックによるフォルダーの展開/折りたたみを修正しました。

## <a name="1400"></a>1.4.0.0

リリース日: 2017 年 12 月 13 日

### <a name="new-features"></a>新機能

- **Project Generation:**

  - .NET Standard のサポートを追加しました。

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - pdb から mdb への自動デバッグ シンボル変換を修正済み

## <a name="1301"></a>1.3.0.1

リリース日: 2017 年 12 月 12 日

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - 配列のサイズを変更するときに、インスペクターに影響する EditorPrefs.GetBool への間接的な呼び出しを修正しました。

- **ウィザード:**

  - roslyn コンテキストは、メソッドの挿入前に更新されます。

## <a name="1300"></a>1.3.0.0

リリース日: 2017 年 11 月 20 日

### <a name="new-features"></a>新機能

- **ウィザード:**

  - "Unity メッセージの実装" ウィザードを追加しました。

  - VS for Mac 7.4 で新しい入力候補 API のサポートが追加されました。

## <a name="1200"></a>1.2.0.0

リリース日: 2017 年 10 月 23 日

### <a name="new-features"></a>新機能

- **デバッガー:**

  - ポータブル デバッグ シンボル ファイルのサポートが追加されました。

### <a name="bug-fixes"></a>バグ修正

- **Project Generation:**

  - アセンブリのファイル名に余分な .dll 拡張子が誤って追加される問題を修正しました。

  - 既定値が 'true' になったので、AllowAttachedDebuggingOfEditor Unity フラグを強要しません。

## <a name="1103"></a>1.1.0.3

リリース日: 2017 年 10 月 23 日

### <a name="new-features"></a>新機能

- **Project Generation:**

  - .NET 4.6 プロファイルのサポートが追加されました。

## <a name="1102"></a>1.1.0.2

リリース日: 2017 年 8 月 8 日

### <a name="new-features"></a>新機能

- **デバッガー:**

  - アタッチする Unity がわからない場合、[プロセスにアタッチ] ダイアログを開始します。

- **Project Generation:**

  - Unity 5.6 の使用時にはアンセーフ コンパイル スイッチが常に有効になります。

## <a name="1101"></a>1.1.0.1

リリース日: 2017 年 7 月 20 日

### <a name="new-features"></a>新機能

- **統合:**

  - ローカライズされたリソースのサポートが追加されました。

## <a name="1100"></a>1.1.0.0

リリース日: 2017 年 7 月 12 日

### <a name="new-features"></a>新機能

- **統合:**

  - [プロセスにアタッチ] ウィンドウからプレーヤーやエディターにアタッチできるようになりました。

- **Project Generation:**

  - mcs.rsp ファイルを使用したアセンブリ名の参照が修正されました。

  - assembly.json コンパイル単位のサポートが追加されました。

  - API レベルの定義が修正されました。

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - コンパイル時のシェーダー エラー メッセージを修正しました。

## <a name="1001"></a>1.0.0.1

リリース日: 2017 年 5 月 4 日

### <a name="bug-fixes"></a>バグ修正

- **統合:**

  - ハイブリッド プロジェクトと標準プロジェクトのアクティブ ドキュメント追跡を修正しました。

## <a name="1000"></a>1.0.0.0

リリース日: 2017 年 5 月 3 日
