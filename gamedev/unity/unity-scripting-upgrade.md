---
title: Unity で.NET 4.x を使用する
description: Unity で .NET 4.x を使用する方法について説明します。 .NET 4.x スクリプティング ランタイムを有効にします。 .NET の互換性を利用します。 構文と言語の新機能を確認します。
author: therealjohn
ms.author: johmil
ms.date: 08/29/2018
ms.topic: how-to
ms.assetid: E2C9420F-A5D5-4472-9020-2B63FB27A133
ms.technology: vs-unity-tools
ms.prod: visual-studio-dev16
ms.workload:
- unity
ms.openlocfilehash: c1b745e4a1da85324b2dc73e30bebb873e2d0720
ms.sourcegitcommit: bbed6a0b41ac4c4a24e8581ff3b34d96345ddb00
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2020
ms.locfileid: "96559811"
---
# <a name="using-net-4x-in-unity"></a>Unity で.NET 4.x を使用する

Unity のスクリプトの基になっている C# と .NET は、Microsoft が 2002 年に最初にそれをリリースして以来、更新され続けています。 しかし、Unity の開発者は、C# 言語および .NET Framework に追加され続けている新機能の絶え間ない流れを知らない場合があります。 これは、Unity 2017.1 以前、何年も更新がない .NET 3.5 と同等のスクリプティング ランタイムが Unity で使用されていたためです。

Unity には、Unity 2017.1 のリリースで、.NET 4.6 にアップグレードされた、C# 6 と互換性のある試験段階のバージョンのスクリプティング ランタイムが実装されました。 Unity 2018.1 では .NET 4.x と同等のランタイムは試験段階とは見なされなくなり、一方、古い .NET 3.5 と同等のランタイムはレガシ バージョンと見なされるようになりました。 そして Unity 2018.3 のリリースでは、Unity はアップグレードされたスクリプティング ランタイムを既定の選択とすることとし、さらに C# 7 まで更新することを計画しています。 このロードマップの詳細および最新の更新については、Unity の [ブログ投稿](https://blogs.unity3d.com/2018/07/11/scripting-runtime-improvements-in-unity-2018-2/)をお読みになるか、同社の「[Experimental Scripting Previews forum](https://forum.unity.com/forums/experimental-scripting-previews.107/)」 (試験段階のスクリプティングのプレビュー フォーラム) を参照してください。 それまでは、以下のセクションで、.NET 4.x スクリプティング ランタイムで現在使用できる新機能を確認し学習してください。

## <a name="prerequisites"></a>前提条件

* [Unity 2017.1 以上](https://unity3d.com/) (2018.2 推奨)
* [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)

## <a name="enabling-the-net-4x-scripting-runtime-in-unity"></a>Unity で .NET 4.x スクリプティング ランタイムを有効にする

.NET 4.x スクリプティング ランタイムを有効にするには、次の手順を実行します。

1. **[Edit]\(編集\)、[Project Settings]\(プロジェクトの設定\)、[Player]\(プレーヤー\)** の順に選択し、Unity Inspector で [PlayerSettings]\(プレーヤー設定\) を開きます。

1. **[Configuration]** \(構成\) 見出しの下で、**[Scripting Runtime Version]** \(スクリプティング ランタイム バージョン\) ドロップダウンをクリックし、**[.NET 4.x Equivalent]** \(.NET 4.x と同等\) を選択します。 Unity を再起動するように求められます。

![.NET 4.x 同等を選択する](media/vs/vstu-scripting-runtime-version.png)

## <a name="choosing-between-net-4x-and-net-standard-20-profiles"></a>.NET 4.x および .NET Standard 2.0 プロファイルのいずれかを選ぶ

.NET 4.x と同等のスクリプティング ランタイムに切り替えたら、[PlayerSettings]\(プレーヤー設定\) (**[Edit]\(編集\)、[Project Settings]\(プロジェクトの設定\)、[Player]\(プレーヤー\)**) のドロップダウン メニューを使用して、**[Api Compatibility Level]** \(API の互換性レベル\) を指定することができます。 2 つのオプションがあります。

* **.NET Standard 2.0**: このプロファイルは、.NET Foundation により発行されている [.NET Standard 2.0 プロファイル](https://github.com/dotnet/standard/blob/master/docs/versions/netstandard2.0.md)と一致します。 Unity では、新しいプロジェクトに .NET Standard 2.0 を推奨しています。 これは .NET 4.x よりも小規模で、サイズに制限のあるプラットフォームで好都合です。 また、Unity では、Unity がサポートしているすべてのプラットフォームで、このプロファイルをサポートすることをコミットしています。

* **.NET 4.x**: このプロファイルでは、最新の .NET 4 API にアクセスできます。 これには、.NET Framework クラス ライブラリで利用できるすべてのコードを含み、また .NET Standard 2.0 のプロファイルも同様にサポートしています。 .NET Standard 2.0 のプロファイルに含まれていない一部の API がプロジェクトで必要な場合は、.NET 4.x のプロファイルを使用します。 ただし、この API の一部は Unity のすべてのプラットフォームでサポートされていない場合があります。

これらのオプションの詳細については、Unity の[ブログ投稿](https://blogs.unity3d.com/2018/03/28/updated-scripting-runtime-in-unity-2018-1-what-does-the-future-hold/)を参照してください。

### <a name="adding-assembly-references-when-using-the-net-4x-api-compatibility-level"></a>.NET 4.x API 互換性レベルの使用時にアセンブリ参照を追加する

**[Api Compatibility Level]** \(API の互換性レベル\) ドロップダウンの .NET Standard 2.0 設定を使用する場合、API プロファイルのすべてのアセンブリが参照され利用可能です。 ただし、より大きな .NET 4.x プロファイルを使用する場合、Unity に付属するアセンブリの一部は既定で参照できません。 これらの API を使用するには、手動でアセンブリ参照を追加する必要があります。 Unity に付属するアセンブリは、Unity エディターのインストールの **MonoBleedingEdge/lib/mono** ディレクトリを参照してください。

![MonoBleedingEdge ディレクトリ](media/vs/vstu-monobleedingedge.png)

たとえば、.NET 4.x プロファイルを使用していて、`HttpClient` を使用したい場合、System.Net.Http.dll に対するアセンブリ参照を追加する必要があります。 これがない場合、アセンブリ参照がないことがコンパイラーによって通知されます。

![アセンブリ参照がない](media/vs/vstu-missing-reference.png)

Visual Studio では Unity のプロジェクトが開かれるたびに、.csproj と .sln のファイルが再生成されます。 そのため、プロジェクトを開くときに失われてしまうので、Visual Studio に直接アセンブリ参照を追加できません。 代わりに、**csc.rsp** という特別なテキスト ファイルを使用する必要があります。

1. ご使用の Unity のプロジェクトのルートの **Assets** ディレクトリに **csc.rsp** という名前の新しいテキスト ファイルを作成します。

1. 空のテキスト ファイルの最初の行に、`-r:System.Net.Http.dll` と入力しファイルを保存します。 "System.Net.Http.dll" は、参照が見つからない含まれているすべてのアセンブリに置き換えることができます。

1. Unity エディターを再起動します。

## <a name="taking-advantage-of-net-compatibility"></a>.NET との互換性を利用する

Unity のユーザーは、NET 4.x スクリプティング ランタイムで、新しい C# の構文と言語機能に加え、従来の .NET 3.5 スクリプティング ランタイムとは互換性がない .NET パッケージの大規模なライブラリにアクセスできるようになります。

### <a name="add-packages-from-nuget-to-a-unity-project"></a>NuGet から Unity プロジェクトにパッケージを追加する

[NuGet](https://www.nuget.org/) は、.NET のパケット マネージャーです。 NuGet は Visual Studio に統合されています。 ただし、Unity のプロジェクトで NuGet のパッケージを追加するには、特別な手順が必要です。 これは、Unity でプロジェクトを開いた場合、その Visual Studio のプロジェクト ファイルが再生成され、必要な構成が元に戻されてしまうためです。 NuGet から Unity のプロジェクトにパッケージを追加するには、次を実行します。

1. NuGet を参照し、追加する互換性パッケージを探します (.NET Standard 2.0 または .NET 4.x)。 この例では、JSON を使用する場合の一般的なパッケージである [Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/) を .NET Standard 2.0 プロジェクトに追加する例を示します。

1. **[ダウンロード]** ボタンをクリックします。

    ![ダウンロード ボタン](media/vs/vstu-nuget-download.png)

1. ダウンロードしたファイルを探し、拡張子を **.nupkg** から **.zip** に変更します。

1. zip ファイル内の **lib/netstandard2.0** ディレクトリに移動し、**Newtonsoft.Json.dll** ファイルをコピーします。

1. Unity プロジェクトのルートの **Assets** フォルダーに、**Plugins** という名前の新しいフォルダーを作成します。 Plugins は Unity の特別なフォルダーの名前です。 詳細については、[Unity のドキュメント](https://docs.unity3d.com/Manual/Plugins.html)を参照してください。

1. **Newtonsoft.Json.dll** ファイルを Unity のプロジェクトの **Plugins** ディレクトリに貼り付けます。

1. ご使用の Unity のプロジェクトの **Assets** ディレクトリに **link.xml** という名前のファイルを作成し、次の XML を追加します。  これにより、IL2CPP プラットフォームへのエクスポート時に、Unity のバイトコードの削除プロセスで必要なデータが削除されなくなります。  この手順はこのライブラリに特有のものですが、リフレクションを同様な方法で使用するその他のライブラリで問題が発生する可能性があります。  詳細については、このトピックについて [Unity の文書](https://docs.unity3d.com/Manual/IL2CPP-BytecodeStripping.html)を参照してください。

    ```xml
    <linker>
      <assembly fullname="System.Core">
        <type fullname="System.Linq.Expressions.Interpreter.LightLambda" preserve="all" />
      </assembly>
    </linker>
    ```

すべてを配置したら、Json.NET パッケージを使用できるようになります。

```csharp
using Newtonsoft.Json;
using UnityEngine;

public class JSONTest : MonoBehaviour
{
    class Enemy
    {
        public string Name { get; set; }
        public int AttackDamage { get; set; }
        public int MaxHealth { get; set; }
    }
    private void Start()
    {
        string json = @"{
            'Name': 'Ninja',
            'AttackDamage': '40'
            }";

        var enemy = JsonConvert.DeserializeObject<Enemy>(json);

        Debug.Log($"{enemy.Name} deals {enemy.AttackDamage} damage.");
        // Output:
        // Ninja deals 40 damage.
    }
}
```

これは、依存関係がないライブラリを使用する単純な例です。 NuGet パッケージが他の NuGet パッケージに依存する場合、これらの依存関係を手動でダウンロードし、同じ方法でプロジェクトに追加する必要があります。

## <a name="new-syntax-and-language-features"></a>構文と言語の新機能

Unity の開発者は、更新されたスクリプトのランタイムを使用して、C# 6 と、多数の新しい言語機能と構文を使用できます。

### <a name="auto-property-initializers"></a>自動プロパティ初期化子

Unity の .NET 3.5 スクリプティング ランタイムの自動プロパティ初期化子では、初期化されていないプロパティをすばやく簡単に定義できますが、初期化はスクリプトの他の場所で起こる必要があります。 .NET 4.x ランタイムでは、同じ行で自動プロパティを初期化できるようになりました。

```csharp
// .NET 3.5
public int Health { get; set; } // Health has to be initialized somewhere else, like Start()

// .NET 4.x
public int Health { get; set; } = 100;
```

### <a name="string-interpolation"></a>文字列補間

以前の .NET 3.5 ランタイムでは、文字列の連結に面倒な構文が必要でした。 .NET 4.x ランタイムでは、[`$` 文字列補間](/dotnet/csharp/language-reference/tokens/interpolated)機能によって、より直接的で読み取り可能な構文の文字列に式を挿入することができるようになりました。

```csharp
// .NET 3.5
Debug.Log(String.Format("Player health: {0}", Health)); // or
Debug.Log("Player health: " + Health);

// .NET 4.x
Debug.Log($"Player health: {Health}");
```

### <a name="expression-bodied-members"></a>式形式のメンバー

.NET 4.x ランタイムでより新しい C# 構文が利用可能になったことにより、関数の本文を[ラムダ式](/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions)で置き換え、より簡潔にすることができます。

```csharp
// .NET 3.5
private int TakeDamage(int amount)
{
    return Health -= amount;
}

// .NET 4.x
private int TakeDamage(int amount) => Health -= amount;
```

また、読み取り専用のプロパティに、式形式のメンバーを使用することもできます。

```csharp
// .NET 4.x
public string PlayerHealthUiText => $"Player health: {Health}";
```

### <a name="task-based-asynchronous-pattern-tap"></a>タスク ベースの非同期パターン (TAP)

[非同期プログラミング](/dotnet/csharp/async)では、アプリケーションが応答しなくならないようにしながら、時間のかかる操作を行うことができます。 この機能では、時間のかかる操作の結果に依存するコードが続行される前に、その操作が終わるのを待つこともできます。 たとえば、ファイルの読み込みやネットワーク操作の完了を待つことができます。

Unity では、非同期プログラミングは通常[コルーチン](https://docs.unity3d.com/Manual/Coroutines.html)で実行されます。 ただし、C# 5 以降の .NET 開発で推奨されるのは、[System.Threading.Task](/dotnet/api/system.threading.tasks.task) で `async` と `await` のキーワードを使用する[タスクベースの非同期パターン (TAP)](/dotnet/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap) の方法となりました。 つまり、`async` 関数では、残りのアプリケーションのアップデートをブロックせずに、タスクの完了を `await` できます。

```csharp
// Unity coroutine
using UnityEngine;
public class UnityCoroutineExample : MonoBehaviour
{
    private void Start()
    {
        StartCoroutine(WaitOneSecond());
        DoMoreStuff(); // This executes without waiting for WaitOneSecond
    }
    private IEnumerator WaitOneSecond()
    {
        yield return new WaitForSeconds(1.0f);
        Debug.Log("Finished waiting.");
    }
}
```

```csharp
// .NET 4.x async-await
using UnityEngine;
using System.Threading.Tasks;
public class AsyncAwaitExample : MonoBehaviour
{
    private async void Start()
    {
        Debug.Log("Wait.");
        await WaitOneSecondAsync();
        DoMoreStuff(); // Will not execute until WaitOneSecond has completed
    }
    private async Task WaitOneSecondAsync()
    {
        await Task.Delay(TimeSpan.FromSeconds(1));
        Debug.Log("Finished waiting.");
    }
}
```

Unity 固有のニュアンスでは、TAP は開発者が考慮すべき複雑なテーマです。 そのため、TAP は Unity のコルーチンにすべての状況で置き換えられるものではありません。ただし、利用できるもう 1 つのツールではあります。 この機能の範囲はこの記事では説明しませんが、一般的なベスト プラクティスおよびヒントを以下に示します。

#### <a name="getting-started-reference-for-tap-with-unity"></a>Unity で TAP を使用開始する

次に、Unity で TAP の使用を開始する場合のヒントを示します。

* 待機することが期待されている非同期関数には、[`Task`](/dotnet/api/system.threading.tasks.task) または [`Task<TResult>`](/dotnet/api/system.threading.tasks.task-1) の戻り値の型が必要です。
* タスクを戻す非同期関数には、その名前に **"Async"** のサフィックスが設定されている必要があります。 "Async" のサフィックスは、関数が常に待機している必要があることを示します。
* 従来の同期コードから非同期関数を実行する関数には、`async void` の戻り値の型のみを使用します。 このような関数は、それだけでは待機できず、名前に "Async" のサフィックスがあるべきではありません。
* Unity は UnitySynchronizationContext を使用し、既定でメインのスレッドで async 関数が実行されるのを保証します。 Unity の API には、メインのスレッド外ではアクセスできません。
* [`Task.Run`](/dotnet/api/system.threading.tasks.task.run) や [`Task.ConfigureAwait(false)`](/dotnet/api/system.threading.tasks.task.configureawait) などのメソッドを使用し、バックグラウンド スレッドでタスクを実行することが可能です。 この手法は、パフォーマンスの向上のためにメインのスレッドからコストの高い操作をオフロードする場合に便利です。 ただし、バックグラウンド スレッドを使用すると、[競合状態](https://wikipedia.org/wiki/Race_condition)など、デバッグが困難な問題につながる可能性があります。
* Unity の API には、メインのスレッド外ではアクセスできません。
* スレッドを使用するタスクは、Unity WebGL のビルドではサポートされていません。

#### <a name="differences-between-coroutines-and-tap"></a>コルーチンと TAP 間の違い

コルーチンと TAP / async-await の間には重要な違いがあります。

* コルーチンは、値を返すことはできませんが、`Task<TResult>` はできます。
* `yield` は、コルーチンでエラー処理を困難にするので、try-catch ステートメントに入れることができません。 ただし、TAP で try-catch は動作します。
* Unity のコルーチンの機能は、MonoBehaviour から派生しないクラスでは利用できません。 TAP はそのようなクラスの非同期プログラミングに最適です。
* 現時点では、Unity で完全にコルーチンに代わるものとして TAP を提案していません。 プロファイリングは、いかなるプロジェクトでも、1 つのアプローチに対する他のアプローチの特定の結果を知ることのできる唯一の方法です。

> [!NOTE]
> Unity 2018.2 以降、改行ポイントを使用した非同期メソッドのデバッグは完全にはサポートされていません。ただし、[この機能は Unity 2018.3](https://twitter.com/jbevain/status/900043560665235456) で期待されています。

### <a name="nameof-operator"></a>nameof 演算子

`nameof` 演算子は、変数、型、メンバーの文字列名を取得します。 `nameof` は、エラーの記録、列挙型の文字列名の取得などで便利です。

```csharp
// Get the string name of an enum:
enum Difficulty {Easy, Medium, Hard};
private void Start()
{
    Debug.Log(nameof(Difficulty.Easy));
    RecordHighScore("John");
    // Output:
    // Easy
    // playerName
}
// Validate parameter:
private void RecordHighScore(string playerName)
{
    Debug.Log(nameof(playerName));
    if (playerName == null) throw new ArgumentNullException(nameof(playerName));
}
```

### <a name="caller-info-attributes"></a>呼び出し元情報属性

[呼び出し元情報属性](/dotnet/csharp/programming-guide/concepts/caller-information)では、メソッドの呼び出し元の情報を得ることができます。 呼び出し元情報属性では、使用する各パラメーターの既定値を提供する必要があります。

```csharp
private void Start ()
{
    ShowCallerInfo("Something happened.");
}
public void ShowCallerInfo(string message,
        [System.Runtime.CompilerServices.CallerMemberName] string memberName = "",
        [System.Runtime.CompilerServices.CallerFilePath] string sourceFilePath = "",
        [System.Runtime.CompilerServices.CallerLineNumber] int sourceLineNumber = 0)
{
    Debug.Log($"message: {message}");
    Debug.Log($"member name: {memberName}");
    Debug.Log($"source file path: {sourceFilePath}");
    Debug.Log($"source line number: {sourceLineNumber}");
}
// Output:
// Something happened
// member name: Start
// source file path: D:\Documents\unity-scripting-upgrade\Unity Project\Assets\CallerInfoTest.cs
// source line number: 10
```

### <a name="using-static"></a>Using static

[Using static](/dotnet/csharp/language-reference/keywords/using-static) では、そのクラス名を入力せずに、静的な関数を使用できます。 using static では、同じクラスからのいくつかの静的な関数を使用する必要がある場合、領域と時間を節約できます。

```csharp
// .NET 3.5
using UnityEngine;
public class Example : MonoBehaviour
{
    private void Start ()
    {
        Debug.Log(Mathf.RoundToInt(Mathf.PI));
        // Output:
        // 3
    }
}
```

```csharp
// .NET 4.x
using UnityEngine;
using static UnityEngine.Mathf;
public class UsingStaticExample: MonoBehaviour
{
    private void Start ()
    {
        Debug.Log(RoundToInt(PI));
        // Output:
        // 3
    }
}
```

## <a name="il2cpp-considerations"></a>IL2CPP に関する考慮事項

iOS などのプラットフォームにゲームをエクスポートする場合、Unity ではその IL2CPP エンジンを使用して IL を C++ コードに "トランスパイル" します。その後、それはターゲット プラットフォームのネイティブ コンパイラーを使用して、コンパイルされます。 このシナリオには、リフレクションの部分や `dynamic` キーワードの用途など、サポートされていないいくつかの .NET 機能があります。 この機能の使用は、ご自分のコードで制御できますが、サードパーティー製の DLL および SDK が Unity と IL2CPP を念頭に入れて記述されていない場合、問題が発生することがあります。 このトピックの詳細については、Unity のサイトで[スクリプティングの制限](https://docs.unity3d.com/Manual/ScriptingRestrictions.html)に関する文書を参照してください。

また、上の Json.NET の例で示したとおり、Unity は IL2CPP のエクスポート処理時に、未使用のコードを除去しようとします。  リフレクションを使用するライブラリでこれが問題となることは通常はありませんが、実行時に呼び出されるプロパティまたはメソッドが偶発的に除去される場合があり、これはエクスポート時には判断できません。  これらの問題を解決するには、削除プロセスを実行しないアセンブリおよび名前空間の一覧が記述された **link.xml** ファイルをプロジェクトに追加します。  完全な詳細については、[Unity でのバイトコードの削除](https://docs.unity3d.com/Manual/IL2CPP-BytecodeStripping.html)に関する文書を参照してください。

## <a name="net-4x-sample-unity-project"></a>.NET 4.x の Unity のサンプル プロジェクト

このサンプルには、いくつかの .NET 4.x の機能例が含まれています。 プロジェクトをダウンロードしたり、[GitHub](https://github.com/Microsoft/unity-scripting-upgrade) でソース コードを参照することができます。

## <a name="additional-resources"></a>その他のリソース

* [Unity ブログ - Unity 2018.2 でのスクリプティング ランタイムの機能強化](https://blogs.unity3d.com/2018/07/11/scripting-runtime-improvements-in-unity-2018-2/)
* [C# の歴史](/dotnet/csharp/whats-new/csharp-version-history)
* [C# 6 の新機能](/dotnet/csharp/whats-new/csharp-6)
* [コルーチンおよび TAP を使用した Unity での非同期プログラミング](/archive/blogs/appconsult/unity-coroutine-tap-en-us)
* [Unity 2017 でのコルーチンの代わりの Async-Await](http://www.stevevermeulen.com/index.php/2017/09/using-async-await-in-unity3d-2017/)
* [Unity フォーラム - 試験段階のスクリプティングのプレビュー](https://forum.unity.com/forums/experimental-scripting-previews.107/)