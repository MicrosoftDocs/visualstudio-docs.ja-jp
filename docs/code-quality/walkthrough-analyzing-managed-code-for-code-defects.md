---
title: コード障害のためのマネージコードの分析のチュートリアル |Microsoft Docs
ms.date: 01/29/2018
ms.topic: conceptual
helpviewer_keywords:
- code analysis [Visual Studio]
- managed code, analyzing
author: mikadumont
ms.author: midumont
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: ab1e0b890d6241742770ed38ff61fc1c2c0ed2f4
ms.sourcegitcommit: 08c144d290da373df841f04fc799e3133540a541
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2019
ms.locfileid: "72535692"
---
# <a name="walkthrough-use-static-code-analysis-to-find-code-defects"></a>チュートリアル: 静的コード分析を使用したコード障害の検出

このチュートリアルでは、従来のコード分析を使用して、マネージプロジェクトのコード障害を分析します。

この記事では、.NET のデザインガイドラインに準拠するために、レガシ分析を使用して .NET マネージコードアセンブリを分析するプロセスについて説明します。

## <a name="create-a-class-library"></a>クラスライブラリを作成する

1. Visual Studio を開き、**クラスライブラリ (.NET Framework)** テンプレートから新しいプロジェクトを作成します。

1. プロジェクトに**CodeAnalysisManagedDemo**という名前を指定します。

1. プロジェクトが作成されたら、 *Class1.cs*ファイルを開きます。

1. Class1.cs の既存のテキストを次のコードに置き換えます。

   ```csharp
   using System;

   namespace testCode
   {
       public class demo : Exception
       {
           public static void Initialize(int size) { }
           protected static readonly int _item;
           public static int item { get { return _item; } }
       }
   }
   ```

1. Class1.cs ファイルを保存します。

## <a name="analyze-the-project-for-code-defects"></a>プロジェクトを分析してコードの欠陥を分析する

1. **ソリューションエクスプローラー**で CodeAnalysisManagedDemo プロジェクトを選択します。

2. **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

   [CodeAnalysisManagedDemo のプロパティ] ページが表示されます。

3. **[コード分析]** タブをクリックします。

::: moniker range="vs-2017"

4. **[ビルドでコード分析を有効に**する] が選択されていることを確認します。

5. **[この規則セットを実行]** ドロップダウンリストで、 **[Microsoft すべての規則]** を選択します。

::: moniker-end

::: moniker range=">=vs-2019"

4. **[バイナリアナライザー]** セクションで **[ビルド時に実行**] が選択されていることを確認します。

5. **[アクティブな規則]** ドロップダウンリストから、 **[Microsoft すべての規則]** を選択します。

::: moniker-end

6. **[ファイル]** メニューの **[選択した項目を保存]** をクリックし、プロパティページを閉じます。

7. **[ビルド]** メニューの **[CodeAnalysisManagedDemo のビルド]** をクリックします。

    CodeAnalysisManagedDemo プロジェクトビルドの警告は、 **[エラー一覧]** ウィンドウと **[出力]** ウィンドウに表示されます。

## <a name="correct-the-code-analysis-issues"></a>コード分析の問題を修正する

1. **[表示]** メニューの **[エラー一覧]** をクリックします。

    選択した開発者プロファイルによっては、 **[表示]** メニューの **[その他のウィンドウ]** をポイントし、 **[エラー一覧]** を選択しなければならない場合があります。

1. **ソリューション エクスプローラー**で、 **[すべてのファイルを表示]** をクリックします。

1. [プロパティ] ノードを展開し、 *AssemblyInfo.cs*ファイルを開きます。

1. 警告を修正するには、次のヒントを使用します。

   [CA1014: CLSCompliantAttribute にアセンブリをマーク](../code-quality/ca1014.md)する: AssemblyInfo.cs ファイルの末尾にコード `[assembly: CLSCompliant(true)]` を追加します。

   [CA1032: 標準の例外コンストラクターを実装](../code-quality/ca1032.md)します。コンストラクター `public demo (String s) : base(s) { }` をクラス `demo` に追加します。

   [CA1032: 標準の例外コンストラクターを実装](../code-quality/ca1032.md)します。コンストラクター `public demo (String s, Exception e) : base(s, e) { }` をクラス `demo` に追加します。

   [CA1032: 標準の例外コンストラクターを実装](../code-quality/ca1032.md)します。クラスのデモにコンストラクター `protected demo (SerializationInfo info, StreamingContext context) : base(info, context) { }` を追加します。 また、<xref:System.Runtime.Serialization?displayProperty=fullName> の `using` ステートメントも追加する必要があります。

   [CA1032: 標準の例外コンストラクターを実装](../code-quality/ca1032.md)します。コンストラクター `public demo () : base() { }` をクラス `demo` に追加します。

   [CA1709: 識別子は大文字にする必要があり](../code-quality/ca1709.md)ます。 `testCode` 名前空間の大文字と小文字の区別を `TestCode` に変更します。

   CA1709: 識別子の大文字と小文字を[正しく指定する必要があり](../code-quality/ca1709.md)ます。メンバーの名前を `Demo` に変更してください。

   CA1709: 識別子の大文字と小文字を[正しく指定する必要があり](../code-quality/ca1709.md)ます。メンバーの名前を `Item` に変更してください。

   [CA1710: 識別子には正しいサフィックスが](../code-quality/ca1710.md)必要です: クラスの名前とそのコンストラクターを `DemoException` に変更してください。

   [CA2237: SerializableAttribute を使用して ISerializable 型をマーク](../code-quality/ca2237.md)します。クラス `demo` に `[Serializable ()]` 属性を追加します。

   [CA2210: アセンブリには有効な厳密な名前が必要](../code-quality/ca2210.md)です。厳密な名前のキーを持つ ' CodeAnalysisManagedDemo ' に署名してください。

   1. **[プロジェクト]** メニューの **[CodeAnalysisManagedDemo のプロパティ]** をクリックします。

      プロジェクトのプロパティが表示されます。

   1. **[署名]** タブを選択します。

   1. **[アセンブリの署名]** チェックボックスをオンにします。

   1. **[文字列名キーファイルを選択]** してください ボックスの一覧で、[ **\<new >** ] を選択します。

      **[厳密な名前キーの作成]** ダイアログボックスが表示されます。

   1. **[キーファイル名]** に「 **testkey**」と入力します。

   1. パスワードを入力し、[ **OK]** を選択します。

   1. **ファイル** メニューの **選択した項目の保存** をクリックし、プロパティページ を閉じます。

   すべての変更を完了すると、Class1.cs ファイルは次のようになります。

   ```csharp
   using System;
   using System.Runtime.Serialization;

   namespace TestCode
   {
       [Serializable()]
       public class DemoException : Exception
       {
           public DemoException () : base() { }
           public DemoException(String s) : base(s) { }
           public DemoException(String s, Exception e) : base(s, e) { }
           protected DemoException(SerializationInfo info, StreamingContext context) : base(info, context) { }

           public static void Initialize(int size) { }
           protected static readonly int _item;
           public static int Item { get { return _item; } }
       }
   }
   ```

1. プロジェクトをリビルドします。

## <a name="exclude-code-analysis-warnings"></a>コード分析の警告を除外する

1. 残りの各警告について、次の操作を行います。

    1. **エラー一覧**で警告を選択します。

    1. 右クリックメニュー (コンテキストメニュー) で、[抑制**ファイル内の** >  を**非**表示にする] を選択します。

1. プロジェクトをリビルドします。

     プロジェクトがビルドされ、警告やエラーは発生しません。

## <a name="see-also"></a>関連項目

[マネージコードのコード分析](../code-quality/code-analysis-for-managed-code-overview.md)
