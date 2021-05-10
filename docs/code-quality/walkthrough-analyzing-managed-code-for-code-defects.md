---
title: 'チュートリアル: マネージド コードの分析によるコード障害の検出 | Microsoft Docs'
ms.date: 01/29/2018
description: レガシ コード分析を使用して .NET マネージド コード アセンブリを分析する方法を説明します。 不具合や、.NET デザインガイドラインに準拠していることを確認する方法がわかります。
ms.custom: SEO-VS-2020
ms.topic: conceptual
helpviewer_keywords:
- code analysis [Visual Studio]
- managed code, analyzing
author: mikadumont
ms.author: midumont
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: b9895dc8926f1bb5c7d33e792168ca46297c8196
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99859607"
---
# <a name="walkthrough-use-static-code-analysis-to-find-code-defects"></a>チュートリアル: 静的コード分析を使用したコード障害の検出

このチュートリアルでは、レガシ コード分析を使用して、マネージド プロジェクトのコード障害を分析します。

この記事では、.NET のデザイン ガイドラインに準拠するために、レガシ 分析を使用して .NET マネージド コード アセンブリを分析するプロセスを説明します。

## <a name="create-a-class-library"></a>クラス ライブラリを作成する

1. Visual Studio を開き、**クラス ライブラリ (.NET Framework)** テンプレートから新しいプロジェクトを作成します。

1. プロジェクトに **CodeAnalysisManagedDemo** という名前を付けます。

1. プロジェクトが作成されたら、*Class1.cs* ファイルを開きます。

1. Class1 内の既存のテキストを、次のコードに置き換えます。

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

## <a name="analyze-the-project-for-code-defects"></a>プロジェクトを分析してコード障害を分析する

1. **ソリューション エクスプローラー** で CodeAnalysisManagedDemo プロジェクトを選択します。

2. **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

   CodeAnalysisManagedDemo のプロパティ ページが表示されます。

3. **[コード分析]** タブをクリックします。

::: moniker range="vs-2017"

4. **[ビルドに対するコード分析の有効化]** がオンになっていることを確認します。

5. **[この規則セットを実行]** ドロップダウン リストで **[Microsoft のすべての規則]** を選択します。

::: moniker-end

::: moniker range=">=vs-2019"

4. **[バイナリ アナライザー]** セクションで **[ビルド時に実行]** がオンになっていることを確認します。

5. **[アクティブな規則]** ドロップダウン リストで **[Microsoft のすべての規則]** を選択します。

::: moniker-end

6. **[ファイル]** メニューの **[選択された項目を保存します]** をクリックし、プロパティ ページを閉じます。

7. **[ビルド]** メニューの **[CodeAnalysisManagedDemo のビルド]** をクリックします。

    CodeAnalysisManagedDemo プロジェクトのビルドの警告が、 **[エラー一覧]** ウィンドウと **[出力]** ウィンドウに表示されます。

## <a name="correct-the-code-analysis-issues"></a>コード分析の問題を修正する

1. **[表示]** メニューの **[エラー一覧]** を選択します。

    選択した開発者プロファイルによっては、 **[表示]** メニューの **[その他のウィンドウ]** をポイントし、 **[エラー一覧]** を選択しなければならない場合があります。

1. **ソリューション エクスプローラー** で、**[すべてのファイルを表示]** をクリックします。

1. [プロパティ] ノードを展開し、*AssemblyInfo.cs* ファイルを開きます。

1. 次のヒントを使用して警告を修正します。

   [CA1014: アセンブリに CLSCompliantAttribute のマークを付ける](/dotnet/fundamentals/code-analysis/quality-rules/ca1014): AssemblyInfo.cs ファイルの末尾にコード `[assembly: CLSCompliant(true)]` を追加します。

   [CA1032: 標準の例外コンストラクターを実装する](/dotnet/fundamentals/code-analysis/quality-rules/ca1032): コンストラクター `public demo (String s) : base(s) { }` をクラス `demo` に追加します。

   [CA1032: 標準の例外コンストラクターを実装する](/dotnet/fundamentals/code-analysis/quality-rules/ca1032): コンストラクター `public demo (String s, Exception e) : base(s, e) { }` をクラス `demo` に追加します。

   [CA1032: 標準の例外コンストラクターを実装する](/dotnet/fundamentals/code-analysis/quality-rules/ca1032): クラスのデモにコンストラクター `protected demo (SerializationInfo info, StreamingContext context) : base(info, context) { }` を追加します。 <xref:System.Runtime.Serialization?displayProperty=fullName> 用の `using` ステートメントも追加する必要があります。

   [CA1032: 標準の例外コンストラクターを実装する](/dotnet/fundamentals/code-analysis/quality-rules/ca1032): コンストラクター `public demo () : base() { }` をクラス `demo` に追加します。

   [CA1709: 識別子の大文字と小文字の表記を修正する](../code-quality/ca1709.md): 名前空間 `testCode` の表記を `TestCode` に変更します。

   [CA1709: 識別子の大文字と小文字の表記を修正する](../code-quality/ca1709.md): メンバーの名前を `Demo` に変更します。

   [CA1709: 識別子の大文字と小文字の表記を修正する](../code-quality/ca1709.md): メンバーの名前を `Item` に変更します。

   [CA1710: 識別子のサフィックスを修正する](/dotnet/fundamentals/code-analysis/quality-rules/ca1710): クラスの名前とそのコンストラクターを `DemoException` に変更します。

   [CA2237: ISerializable 型に SerializableAttribute のマークを付ける](/dotnet/fundamentals/code-analysis/quality-rules/ca2237): `[Serializable ()]` 属性をクラス `demo` に追加します。

   [CA2210: 有効で厳密な名前がアセンブリには必要](../code-quality/ca2210.md): 'CodeAnalysisManagedDemo' の署名に、厳密な名前のキーを使用します。

   1. **[プロジェクト]** メニューで **[CodeAnalysisManagedDemo プロパティ]** を選択します。

      プロジェクトのプロパティが表示されます。

   1. **[署名]** タブを選択します。

   1. **[アセンブリの署名]** チェック ボックスをオンにします。

   1. **[厳密な名前のキー ファイルを選択してください]** の一覧で **\<New>** を選択します。

      **[厳密な名前キーの作成]** ダイアログ ボックスが表示されます。

   1. **[キー ファイル名]** に「**TestKey**」と入力します。

   1. パスワードを入力し、 **[OK]** をクリックします。

   1. **[ファイル]** メニューの **[選択された項目を保存します]** を選択し、プロパティ ページを閉じます。

   すべての変更を完了すると、Class1.cs ファイルは、次のようになります。

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

    1. **[エラー一覧]** で警告を選択します。

    1. 右クリック メニュー (コンテキスト メニュー) で **[抑制]**  >  **[抑制ファイル内]** を選択します。

1. プロジェクトをリビルドします。

     プロジェクトが、警告やエラーが発生することなくビルドされます。

## <a name="see-also"></a>関連項目

[マネージド コードのコード分析](../code-quality/code-analysis-for-managed-code-overview.md)
