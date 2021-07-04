---
title: shim を使用してアプリを分離する (単体テスト)
description: shim 型を使用して、特定のメソッドの呼び出しを、テストの一部として作成したコードに迂回させる方法について説明します。 shim を使用すると、すべての呼び出しで一定の結果を返すことができます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.author: mikejo
manager: jmartens
author: mikejo5000
dev_langs:
- CSharp
- VB
ms.openlocfilehash: 72a976ccd487abdfa2c6501c0dcafee07dc5f4ae
ms.sourcegitcommit: 4b2b6068846425f6964c1fd867370863fc4993ce
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/12/2021
ms.locfileid: "112042861"
---
# <a name="use-shims-to-isolate-your-app-for-unit-testing"></a>shim を使用して単体テストのためにアプリを分離する

**Shim 型** は、テスト中のコンポーネントを環境から分離するために Microsoft Fakes Framework が使用する 2 つのテクノロジのうちの 1 つです。 Shim は、特定のメソッドの呼び出しを、テストの一部として作成したコードに迂回させます。 多くのメソッドは、外部の状況に応じて異なる結果を返しますが、shim はテストの制御下にあり、すべての呼び出しで一定の結果を返すことができます。 これにより、テストを簡単に記述できるようになります。

*shim* を使用して、ソリューションの一部ではないアセンブリからコードを分離します。 ソリューションの各コンポーネントを分離するには、*スタブ* を使用します。

概要と "クイック スタート" ガイドについては、「[Microsoft Fakes を使用したテストでコードを分離する](../test/isolating-code-under-test-with-microsoft-fakes.md)」を参照してください。

**必要条件**

- Visual Studio Enterprise
- .NET Framework プロジェクト
::: moniker range=">=vs-2019"
- Visual Studio 2019 Update 6 でプレビューされた .NET Core、.NET 5.0、および SDK スタイルのプロジェクトのサポートは、Update 8 で既定で有効になっています。 詳細については、「[.NET Core および SDK スタイルのプロジェクトのための Microsoft Fakes](/visualstudio/releases/2019/release-notes#microsoft-fakes-for-net-core-and-sdk-style-projects)」を参照してください。
::: moniker-end

## <a name="example-the-y2k-bug"></a>例: Y2K バグ

2000 年 1 月 1 日に例外をスローするメソッドについて考えてみましょう。

```csharp
// code under test
public static class Y2KChecker {
    public static void Check() {
        if (DateTime.Now == new DateTime(2000, 1, 1))
            throw new ApplicationException("y2kbug!");
    }
}
```

このメソッドのテストが難しいのは、プログラムが `DateTime.Now` メソッドに依存しているためです。このメソッドは、コンピューターのクロックに依存する、環境依存の非確定的なメソッドです。 さらに、`DateTime.Now` は静的なプロパティであるため、ここではスタブ型を使用できません。 この問題は、単体テストで分離の問題があることを示します。直接データベース API を呼び出したり、Web サービスと通信したりするプログラムは、単体テストを行うことが困難です。それらのロジックが環境に依存するためです。

そこで、shim 型を使用する必要があります。 shim 型には、任意の .NET メソッドをユーザー定義のデリゲートに迂回させるしくみがあります。 shim 型は Fakes ジェネレーターによってコード生成され、新しいメソッドの実装を指定するために、shim 型と呼ばれるデリゲートを使用します。

次のテストは、`ShimDateTime` という shim 型を使用して DateTime.Now のカスタム実装を提供する方法を示しています。

```csharp
//unit test code
// create a ShimsContext cleans up shims
using (ShimsContext.Create()) {
    // hook delegate to the shim method to redirect DateTime.Now
    // to return January 1st of 2000
    ShimDateTime.NowGet = () => new DateTime(2000, 1, 1);
    Y2KChecker.Check();
}
```

## <a name="how-to-use-shims"></a>Shim の使用方法

まず、Fakes アセンブリを追加します。

1. **ソリューション エクスプローラー** で。 
    - 古い .NET Framework プロジェクト (非 SDK スタイル) の場合は、単体テスト プロジェクトの **[参照]** ノードを展開します。
    ::: moniker range=">=vs-2019"
    - .NET Framework、.NET Core、または .NET 5.0 がターゲットである SDK スタイルのプロジェクトの場合は、 **[依存関係]** ノードを展開し、 **[アセンブリ]** 、 **[プロジェクト]** 、または **[パッケージ]** でフェイク化するアセンブリを見つけます。
    ::: moniker-end
    - Visual Basic で作業している場合、 **[参照]** ノードを表示するには、**ソリューション エクスプローラー** ツールバーの **[すべてのファイルを表示]** を選択します。

2. 作成する shim に対応するクラス定義が含まれているアセンブリを選択します。 たとえば、shim が **DateTime** の場合は、**System.dll** を選択します。

3. ショートカット メニューで、 **[Fakes アセンブリに追加]** を選択します。

### <a name="use-shimscontext"></a>ShimsContext を使用する

単体テスト フレームワークで shim 型を使用する場合は、shim の有効期間を制御するために、テスト コードを `ShimsContext` でラップします。 そうしなかった場合、shim は AppDomain のシャットダウンまで存続します。 `ShimsContext` を作成するための最も簡単な方法は、次のコードに示すように、静的な `Create()` メソッドを使用することです。

```csharp
//unit test code
[Test]
public void Y2kCheckerTest() {
  using(ShimsContext.Create()) {
    ...
  } // clear all shims
}
```

各 shim コンテキストを適切に破棄することが重要です。 原則としては、登録した shim を適切に消去するために、`using` ステートメント内で `ShimsContext.Create` を呼び出します。 たとえば、`DateTime.Now` メソッドを常に 2000 年 1 月 1 日を返すデリゲートに置き換えるテスト メソッドのために shim を登録する場合があります。 テスト メソッド内で登録済み shim を消去し忘れた場合、テスト実行の残りの部分では、`DateTime.Now` 値として常に 2000 年 1 月 1 日が返されます。 これは、予想外で、混乱を招く可能性があります。

### <a name="write-a-test-with-shims"></a>shim を使用してテストを作成する

テスト コード内で、フェイク メソッドに *detour* を挿入します。 次に例を示します。

```csharp
[TestClass]
public class TestClass1
{
        [TestMethod]
        public void TestCurrentYear()
        {
            int fixedYear = 2000;

            using (ShimsContext.Create())
            {
              // Arrange:
                // Detour DateTime.Now to return a fixed date:
                System.Fakes.ShimDateTime.NowGet =
                () =>
                { return new DateTime(fixedYear, 1, 1); };

                // Instantiate the component under test:
                var componentUnderTest = new MyComponent();

              // Act:
                int year = componentUnderTest.GetTheCurrentYear();

              // Assert:
                // This will always be true if the component is working:
                Assert.AreEqual(fixedYear, year);
            }
        }
}
```

```vb
<TestClass()> _
Public Class TestClass1
    <TestMethod()> _
    Public Sub TestCurrentYear()
        Using s = Microsoft.QualityTools.Testing.Fakes.ShimsContext.Create()
            Dim fixedYear As Integer = 2000
            ' Arrange:
            ' Detour DateTime.Now to return a fixed date:
            System.Fakes.ShimDateTime.NowGet = _
                Function() As DateTime
                    Return New DateTime(fixedYear, 1, 1)
                End Function

            ' Instantiate the component under test:
            Dim componentUnderTest = New MyComponent()
            ' Act:
            Dim year As Integer = componentUnderTest.GetTheCurrentYear
            ' Assert:
            ' This will always be true if the component is working:
            Assert.AreEqual(fixedYear, year)
        End Using
    End Sub
End Class
```

Shim クラスの名前は、元の型名の先頭に `Fakes.Shim` を付けることで構成されます。

shim は、テスト対象のアプリケーションのコードに *detours* を挿入することによって機能します。 元のメソッドへの呼び出しがどこで行われても、Fakes システムによって迂回され、実際のメソッドではなく shim コードが呼び出されます。

迂回の作成と削除は実行時に行われる点に注意してください。 常に `ShimsContext` の有効期間内で迂回を作成する必要があります。 これを破棄すると、これがアクティブなときに作成したすべての shim が削除されます。 このようにするための最善の方法は、`using` ステートメントの内部で対処することです。

Fakes 名前空間が存在しないことを示すビルド エラーが表示される場合があります。 このエラーは、他のコンパイル エラーがあるときに表示されることがあります。 他のエラーを修正すると、表示されなくなります。

## <a name="shims-for-different-kinds-of-methods"></a>さまざまな種類のメソッドの shim

shim 型では、任意の .NET メソッド (静的メソッドまたは非仮想メソッドを含む) を独自のデリゲートに置き換えることができます。

### <a name="static-methods"></a>静的メソッド

shim を静的メソッドにアタッチするプロパティは、shim 型に備わっています。 各プロパティには、デリゲートを対象のメソッドにアタッチするために使用されるセッターだけが存在します。 たとえば、クラス `MyClass` に静的メソッド `MyMethod` があるとします。

```csharp
//code under test
public static class MyClass {
    public static int MyMethod() {
        ...
    }
}
```

常に 5 を返す `MyMethod` に shim をアタッチできます。

```csharp
// unit test code
ShimMyClass.MyMethod = () => 5;
```

### <a name="instance-methods-for-all-instances"></a>インスタンス メソッド (すべてのインスタンス用)

静的メソッドと同様に、インスタンス メソッドはすべてのインスタンスに対して shim を適用できます。 これらの shim をアタッチするプロパティは、混乱を避けるために、AllInstances という名前の、入れ子になった型に配置されます。 たとえば、クラス `MyClass` にインスタンス メソッド `MyMethod` があるとします。

```csharp
// code under test
public class MyClass {
    public int MyMethod() {
        ...
    }
}
```

どのインスタンスかにかかわらず、常に 5 を返す `MyMethod` に shim をアタッチできます。

```csharp
// unit test code
ShimMyClass.AllInstances.MyMethod = () => 5;
```

ShimMyClass の生成された型の構造は、次のコードのようになります。

```csharp
// Fakes generated code
public class ShimMyClass : ShimBase<MyClass> {
    public static class AllInstances {
        public static Func<MyClass, int>MyMethod {
            set {
                ...
            }
        }
    }
}
```

この場合、Fakes によって実行時インスタンスがデリゲートの第 1 引数として渡されることに注意してください。

### <a name="instance-methods-for-one-runtime-instance"></a>インスタンス メソッド (1 つの実行時インスタンス用)

インスタンス メソッドには、呼び出しのレシーバーに応じて異なるデリゲートによって shim を適用することもできます。 そうすることで、同じインスタンス メソッドに、インスタンスの型に応じて異なる動作をさせることができます。 これらの shim を設定するプロパティは、shim 型自体のインスタンス メソッドです。 インスタンス化された各 shim 型も、shim が適用された型の生のインスタンスに関連付けられます。

たとえば、クラス `MyClass` にインスタンス メソッド `MyMethod` があるとします。

```csharp
// code under test
public class MyClass {
    public int MyMethod() {
        ...
    }
}
```

MyMethod には 2 つの shim 型をセットアップし、1 つ目は常に 5 を返し、2 つ目は常に 10 を返すようにすることができます。

```csharp
// unit test code
var myClass1 = new ShimMyClass()
{
    MyMethod = () => 5
};
var myClass2 = new ShimMyClass { MyMethod = () => 10 };
```

ShimMyClass の生成された型の構造は、次のコードのようになります。

```csharp
// Fakes generated code
public class ShimMyClass : ShimBase<MyClass> {
    public Func<int> MyMethod {
        set {
            ...
        }
    }
    public MyClass Instance {
        get {
            ...
        }
    }
}
```

shim が適用された実際の型のインスタンスには、Instance プロパティを通じてアクセスできます。

```csharp
// unit test code
var shim = new ShimMyClass();
var instance = shim.Instance;
```

shim 型では、shim が適用された型への暗黙的な変換も行われるため、通常は shim 型を単純にそのまま使用できます。

```csharp
// unit test code
var shim = new ShimMyClass();
MyClass instance = shim; // implicit cast retrieves the runtime instance
```

### <a name="constructors"></a>コンストラクター

shim 型を将来的なオブジェクトにアタッチするために、コンストラクターにも shim を適用できます。 各コンストラクターは、shim 型の静的メソッド Constructor として公開されます。 たとえば、コンストラクターが整数を受け取るクラス `MyClass` があるとします。

```csharp
// code under test
public class MyClass {
    public MyClass(int value) {
        this.Value = value;
    }
    ...
}
```

値ゲッターが呼び出されたときに、コンストラクター内の値にかかわらず、将来的なすべてのインスタンスが -5 を返すように、コンストラクターの shim 型をセットアップします。

```csharp
// unit test code
ShimMyClass.ConstructorInt32 = (@this, value) => {
    var shim = new ShimMyClass(@this) {
        ValueGet = () => -5
    };
};
```

各 shim 型は 2 つのコンストラクターを公開します。 新規のインスタンスが必要な場合には既定のコンストラクターを使用し、shim のみのコンストラクターでは shim が適用されたインスタンスを引数として受け取るコンストラクターを使用する必要があります。

```csharp
// unit test code
public ShimMyClass() { }
public ShimMyClass(MyClass instance) : base(instance) { }
```

ShimMyClass の生成された型の構造は、次のコードのようになります。

```csharp
// Fakes generated code
public class ShimMyClass : ShimBase<MyClass>
{
    public static Action<MyClass, int> ConstructorInt32 {
        set {
            ...
        }
    }

    public ShimMyClass() { }
    public ShimMyClass(MyClass instance) : base(instance) { }
    ...
}
```

### <a name="base-members"></a>基本メンバー

基本メンバーの shim プロパティにアクセスするには、基本型の shim を作成し、基本 shim クラスのコンストラクターへのパラメーターとして子インスタンスを渡します。

たとえば、クラス `MyBase` にインスタンス メソッド `MyMethod` とサブタイプ `MyChild` があるとします。

```csharp
public abstract class MyBase {
    public int MyMethod() {
        ...
    }
}

public class MyChild : MyBase {
}
```

`MyBase` の shim をセットアップするには、新しい `ShimMyBase` shim を作成します。

```csharp
// unit test code
var child = new ShimMyChild();
new ShimMyBase(child) { MyMethod = () => 5 };
```

子 shim 型は、基本 shim コンストラクターにパラメーターとして渡されるときに、暗黙的に子インスタンスに変換されることに注意してください。

ShimMyChild と ShimMyBase の生成された型の構造は、次のコードのようになります。

```csharp
// Fakes generated code
public class ShimMyChild : ShimBase<MyChild> {
    public ShimMyChild() { }
    public ShimMyChild(Child child)
        : base(child) { }
}
public class ShimMyBase : ShimBase<MyBase> {
    public ShimMyBase(Base target) { }
    public Func<int> MyMethod
    { set { ... } }
}
```

### <a name="static-constructors"></a>静的コンストラクター

shim 型は、型の静的コンストラクターに shim を適用するために、静的メソッド `StaticConstructor` を公開します。 静的コンストラクターは 1 回だけ実行されるため、型のいずれかのメンバーがアクセスされる前に shim が構成されるようにする必要があります。

### <a name="finalizers"></a>ファイナライザー

ファイナライザーは、Fakes ではサポートされません。

### <a name="private-methods"></a>プライベート メソッド

Fakes コード ジェネレーターは、シグネチャに参照可能な型だけを持つプライベート メソッドの shim プロパティを作成します。つまり、パラメーターの型と戻り値の型が参照可能です。

### <a name="binding-interfaces"></a>バインド インターフェイス

shim が適用された型がインターフェイスを実装する場合、コード ジェネレーターは、そのインターフェイスのすべてのメンバーを一度にバインドできるメソッドを生成します。

たとえば、`IEnumerable<int>` を実装する `MyClass` クラスがあるとします。

```csharp
public class MyClass : IEnumerable<int> {
    public IEnumerator<int> GetEnumerator() {
        ...
    }
    ...
}
```

Bind メソッドを呼び出すことで、MyClass の `IEnumerable<int>` の実装に shim を適用できます。

```csharp
// unit test code
var shimMyClass = new ShimMyClass();
shimMyClass.Bind(new List<int> { 1, 2, 3 });
```

ShimMyClass の生成された型の構造は、次のコードのようになります。

```csharp
// Fakes generated code
public class ShimMyClass : ShimBase<MyClass> {
    public ShimMyClass Bind(IEnumerable<int> target) {
        ...
    }
}
```

## <a name="change-the-default-behavior"></a>既定の動作の変更

生成された各 shim 型は、`ShimBase<T>.InstanceBehavior` プロパティを通じて、`IShimBehavior` インターフェイスのインスタンスを保持します。 明示的に shim が適用されていないインスタンス メンバーをクライアントが呼び出すたびに、この動作が使用されます。

この動作が明示的に設定されていない場合は、静的な `ShimBehaviors.Current` プロパティによって返されるインスタンスが使用されます。 既定では、このプロパティは `NotImplementedException` 例外をスローする動作を返します。

この動作は、任意の shim インスタンスの `InstanceBehavior` プロパティを設定することによって、いつでも変更できます。 たとえば、次のスニペットは、何も行わないか、戻り値の型の既定値 `default(T)` を返す動作の shim を変更します。

```csharp
// unit test code
var shim = new ShimMyClass();
//return default(T) or do nothing
shim.InstanceBehavior = ShimBehaviors.DefaultValue;
```

静的 `ShimBehaviors.Current` プロパティを設定することによって `InstanceBehavior` プロパティが明示的に設定されていない、shim が適用されているすべてのインスタンスの動作を、グローバルに変更することもできます。

```csharp
// unit test code
// change default shim for all shim instances
// where the behavior has not been set
ShimBehaviors.Current = ShimBehaviors.DefaultValue;
```

## <a name="detect-environment-accesses"></a>環境アクセスの検出

`ShimBehaviors.NotImplemented` 動作を、対応する shim 型の静的プロパティ `Behavior` に割り当てることによって、特定の型のすべてのメンバー (静的メソッドも含む) に動作をアタッチすることができます。

```csharp
// unit test code
// assigning the not implemented behavior
ShimMyClass.Behavior = ShimBehaviors.NotImplemented;
// shorthand
ShimMyClass.BehaveAsNotImplemented();
```

## <a name="concurrency"></a>コンカレンシー

shim 型は、AppDomain のすべてのスレッドに適用され、スレッド アフィニティを持ちません。 これは、同時実行をサポートするテスト ランナーを使用する場合に重要となります。 shim 型を含むテストを同時に実行することはできません。 このプロパティが Fakes ランタイムによって強制されることはありません。

## <a name="call-the-original-method-from-the-shim-method"></a>shim メソッドからの元のメソッドの呼び出し

メソッドに渡されたファイル名を検証した後で、ファイル システムにテキストを書き込む場合を想像してみてください。 この場合は、shim メソッドの途中で元のメソッドを呼び出します。

この問題を解決するための 1 つ目の方法は、次のコードのように、デリゲートと `ShimsContext.ExecuteWithoutShims()` を使用して元のメソッドへの呼び出しをラップすることです。

```csharp
// unit test code
ShimFile.WriteAllTextStringString = (fileName, content) => {
  ShimsContext.ExecuteWithoutShims(() => {

      Console.WriteLine("enter");
      File.WriteAllText(fileName, content);
      Console.WriteLine("leave");
  });
};
```

もう 1 つの方法は、shim を null に設定して元のメソッドを呼び出し、shim を復元することです。

```csharp
// unit test code
ShimsDelegates.Action<string, string> shim = null;
shim = (fileName, content) => {
  try {
    Console.WriteLine("enter");
    // remove shim in order to call original method
    ShimFile.WriteAllTextStringString = null;
    File.WriteAllText(fileName, content);
  }
  finally
  {
    // restore shim
    ShimFile.WriteAllTextStringString = shim;
    Console.WriteLine("leave");
  }
};
// initialize the shim
ShimFile.WriteAllTextStringString = shim;
```

## <a name="systemenvironment"></a>System.Environment

<xref:System.Environment?displayProperty=fullName> に shim を適用するには、mscorlib.fakes ファイルの **Assembly** 要素の後に次の内容を追加します。

```xml
<ShimGeneration>
    <Add FullName="System.Environment"/>
</ShimGeneration>
```

ソリューションをリビルドしたら、<xref:System.Environment?displayProperty=fullName> クラスのメソッドとプロパティに shim を適用できるようになります。次に例を示します。

```csharp
System.Fakes.ShimEnvironment.GetCommandLineArgsGet = ...
```

## <a name="limitations"></a>制限事項

.NET 基底クラス ライブラリ **mscorlib**、.NET Framework の **System**、および .NET Core または .NET 5.0 の **System.Runtime** のすべての型で shim を使用できるわけではありません。

## <a name="see-also"></a>参照

- [Microsoft Fakes を使用したテストでコードを分離する](../test/isolating-code-under-test-with-microsoft-fakes.md)
- [Peter Provost のブログ: Visual Studio 2012 の shim](http://www.peterprovost.org/blog/2012/04/25/visual-studio-11-fakes-part-2)
- [1 時間 16 分の動画: Visual Studio 2012 で Fakes を利用し、テスト不可能なコードをテストする](https://channel9.msdn.com/Events/TechEd/Europe/2012/DEV411)
