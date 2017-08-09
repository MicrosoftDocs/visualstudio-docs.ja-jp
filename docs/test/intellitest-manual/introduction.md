---
title: "概要 | Microsoft IntelliTest 開発者テスト ツール | Microsoft Docs"
ms.custom: 
ms.date: 05/02/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- IntelliTest, Visual Studio IntelliTest developer testing tool
ms.assetid: A7B98509-7ACA-4E25-BD1B-BBC98742F028
caps.latest.revision: 56
ms.author: douge
manager: douge
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: Human Translation
ms.sourcegitcommit: 45d36934cf1c46902cac566203cddf4a118b7fe4
ms.openlocfilehash: a10125710bc36917842a26caebda5b5e7ac8b7fb
ms.contentlocale: ja-jp
ms.lasthandoff: 06/02/2017

---
# <a name="overview-of-microsoft-intellitest"></a>Microsoft IntelliTest の概要

IntelliTest は早い段階でバグを発見することができ、テストのメンテナンス コストを削減します。 自動化された透過的なテスト アプローチを使用することで、IntelliTest は .NET コードのテストの候補スイートを生成できます。 テスト スイートの生成は、指定する*正確性プロパティ*によってより細かく指示することができます。 IntelliTest はテスト対象のコードの進化に伴って、テスト スイートを自動的にさらに進化させます。

**特性のテスト**  
IntelliTest では、従来の単体テストのスイートの観点から、コードの動作を決定することができます。 このようなテスト スイートは、レガシ コードや馴染みのないコードのリファクタリングに伴う複雑さへの取り組みの基盤を形成する回帰スイートとして使用できます。

**ガイドによるテスト入力の生成**  
IntelliTest はオープン コード分析と制約解決のアプローチを使用して、正確なテスト入力値を自動的に生成します。通常、ユーザーの介入は必要ありません。 複雑なオブジェクトの種類に対しては、ファクトリを自動的に生成します。 要件に合わせてファクトリを拡張および構成して、テスト入力の生成を指示できます。 コードでアサーションとして指定した正確性プロパティも、テスト入力生成をさらに指示するために自動的に使用されます。

**IDE の統合**  
IntelliTest は、Visual Studio IDE に完全に統合されています。 テスト スイートの生成中に収集されたすべての情報 (自動的に生成された入力、コードからの出力、生成されたテスト ケース、およびその成功または失敗のステータスなど) は、Visual Studio IDE 内に表示されます。 Visual Studio IDE を離れることなく、コードの修正と IntelliTest の再実行を簡単に反復することができます。 テストは単体テスト プロジェクトとしてソリューションに保存でき、保存後は Visual Studio テスト エクスプ ローラーで自動的に検出されます。

**既存のテスト手法の補完**  
IntelliTest を使用して、既に従っている既存のテスト手法を補完します。

テストする場合:

* プリミティブ データ、またはプリミティブ データの配列に対するアルゴリズム:
  * [パラメーター化した単体テスト](test-generation.md#parameterized-unit-testing)を記述する
* コンパイラなどの複雑なデータに対するアルゴリズム:
  * まず、IntelliTest でデータの抽象表現を生成してから、それをアルゴリズムにフィードする
  * IntelliTest で[カスタム オブジェクトの作成](input-generation.md#objects)とデータの不変性を使用してインスタンスを構築してから、アルゴリズムを呼び出す
* データ コンテナー:
  * [パラメーター化した単体テスト](test-generation.md#parameterized-unit-testing)を記述する
  * IntelliTest で[カスタム オブジェクトの作成](input-generation.md#objects)とデータの不変性を使用してインスタンスを構築してから、コンテナーのメソッドを呼び出し、不変性を再チェックする
  * パラメーター値に応じて、実装の異なるメソッドを呼び出す[パラメーター化した単体テスト](test-generation.md#parameterized-unit-testing)を記述する
* 既存のコード ベース:
  * Visual Studio の IntelliTest ウィザードを使用して、[パラメーター化した単体テスト (PUT)](test-generation.md#parameterized-unit-testing) のセットを生成して開始する

<a name="hello-world"></a>
## <a name="the-hello-world-of-intellitest"></a>IntelliTest の Hello World

IntelliTest はテスト済みのプログラムに関連する入力を検索します。つまり、これを使用して有名な **Hello World!**  文字列を生成できます。 これは、C# MSTest ベースのテスト プロジェクトを作成し、**Microsoft.Pex.Framework** への参照を追加していることを前提としています。 別のテスト フレームワークを使用している場合は、C# クラス ライブラリを作成し、プロジェクトの設定方法に関するテスト フレームワークのドキュメントを参照してください。

次の例は、**value** という名前のパラメーターで 2 つの制約を作成して、IntelliTest が必要な文字列を生成できるようにします。

```
using System;
using Microsoft.Pex.Framework; 
using Microsoft.VisualStudio.TestTools.UnitTesting; 

[TestClass]
public partial class HelloWorldTest {
    [PexMethod]
    public void HelloWorld([PexAssumeNotNull]string value) {
        if (value.StartsWith("Hello")
            && value.EndsWith("World!")
            && value.Contains(" "))
            throw new Exception("found it!");
    }
}
```

コンパイルして実行すると、IntelliTest は次のようなテストのセットを生成します。

1. ""
2. "\0\0\0\0\0"
3. "Hello"
4. "\0\0\0\0\0\0"
5. "Hello\0"
6. "Hello\0\0"
7. "Hello\0World!"
8. "Hello World!"

[このページ](https://docs.microsoft.com/en-gb/visualstudio/test/generate-unit-tests-for-your-code-with-intellitest#Anchor_0)で、生成されたテストが保存される場所を理解してください。
生成されたテスト コードには、次のようなテストを含める必要があります。

```
[TestMethod]
[PexGeneratedBy(typeof(global::HelloWorldTest))]
[PexRaisedException(typeof(Exception))]
public void HelloWorldThrowsException167()
{
    this.HelloWorld("Hello World!");
}
```

とても簡単ですね。

<a name="limitations"></a>
## <a name="limitations"></a>制限事項

このセクションでは、IntelliTest の制限事項について説明します。

* [非決定論的](#nondeterminism)
* [同時実行](#concurrency)
* [ネイティブ .NET コード](#native-code)
* [プラットフォーム](#platform)
* [言語](#language)
* [シンボリック推論](#symbolic-reasoning)
* [スタック トレース](#incorrect-stack)

<a name="nondeterminism"></a>
### <a name="nondeterminism"></a>非決定論的

IntelliTest は、分析対象のプログラムが決定論的であると仮定します。 そうでない場合、IntelliTest は探索の範囲に達するまでサイクルを繰り返します。

プログラムが IntelliTest が制御できない入力に依存している場合、IntelliTest はそのプログラムを非決定論的と見なします。

IntelliTest は、[パラメーター化した単体テスト](test-generation.md#parameterized-unit-testing)に提供された入力と、[PexChoose](static-helper-classes.md#pexchoose) から取得された入力を制御します。 その意味で、アンマネージ コードまたはインストルメント化されていないコードへの呼び出しの結果も、インストルメント化されたプログラムの "入力" として見なされますが、IntelliTest はそれらを制御できません。 プログラムの制御フローがこれらの外部ソースからの特定の値に依存している場合、IntelliTest はれまでにカバーされていない領域に向かってプログラムを "誘導" することはできません。 

さらに、プログラムの再実行時に外部ソースからの値が変わる場合は、そのプログラムは非決定論的と見なされます。 このような場合、IntelliTest はプログラムの実行に対する制御を失い、検索がきわめて非効率的になります。

これが発生しても、はっきりとわからない場合があります。 次に例を示します。

* **GetHashCode()** メソッドの結果は、アンマネージ コードによって提供され、予測できません。
* **System.Random** クラスは現在のシステム時刻を使用してせいかくにランダムな値を提供します。
* **System.DateTime** クラスは、明らかに IntelliTest の制御下にない現在の時刻を提供します。

<a name="concurrency"></a>
### <a name="concurrency"></a>同時実行

IntelliTest はマルチスレッド プログラムを処理しません。

<a name="native-code"></a>
### <a name="native-code-net-code-that-is-not-instrumented"></a>インストルメント化されないネイティブ コード (.NET コード)

IntelliTest は、**P/Invoke** を通じて呼び出される x86 命令などのネイティブ コードを理解しません。 これらの呼び出しを[制約ソルバー](input-generation.md#constraint-solver)に渡すことができる制約に変換する方法もわかりません。 .NET コードの場合でも、インストルメント化するコードしか分析できません。 IntelliTest は、リフレクション ライブラリを含む **mscorlib** の特定の部分をインストルメント化できません。 **DynamicMethod** はインストルメント化できません。 

提案される回避策は、動的アセンブリ内でこのようなメソッドが配置されている種類のテスト モードを持つことです。 ただし、一部のメソッドがインストルメント化されない場合でも、IntelliTest はできるだけ多くのインストルメント化されたコードをカバーしようとします。

<a name="platform"></a>
### <a name="platform"></a>プラットフォーム

IntelliTest は、X86、32 ビットの .NETframework でのみサポートされます。

<a name="language"></a>
### <a name="language"></a>言語

原則として、IntelliTest は .NET 言語で記述された任意の .NET プログラムを分析できますが、 Visual Studio では、C# のみサポートします。

<a name="symbolic-reasoning"></a>
### <a name="symbolic-reasoning"></a>シンボリック推論

IntelliTest は自動[制約ソルバー](input-generation.md#constraint-solver)を使用して、テストとテスト対象のプログラムに関連する値を判断します。 ただし、制約ソルバーの機能は、今までそうだったように、限定されており、これは今後も変わらないでしょう。

<a name="incorrect-stack"></a>
### <a name="slightly-incorrect-stack-traces"></a>スタック トレースの (軽微な) 誤り

IntelliTest はインストルメント化された各メソッドで "rethrow" 例外をキャッチするため、スタック トレースの行番号は正しくなくなります。 これは "rethrow" 命令の設計による制限です。

<a name="further-reading"></a>
## <a name="further-reading"></a>関連項目

* MSDN の [初心者向けのブログ記事](https://blogs.msdn.microsoft.com/visualstudioalm/2014/11/19/introducing-smart-unit-tests/)
* [IntelliTest でのコードの単体テストの生成](https://docs.microsoft.com/en-gb/visualstudio/test/generate-unit-tests-for-your-code-with-intellitest)

## <a name="got-feedback"></a>フィードバックをお寄せください

ご意見や機能に関するご要望を **[UserVoice](https://visualstudio.uservoice.com/forums/121579-visual-studio-2015/category/157869-test-tools?query=IntelliTest)** で投稿してください。

