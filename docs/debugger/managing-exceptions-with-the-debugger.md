---
title: デバッガーでの例外の管理 | Microsoft Docs
description: デバッガーが中断する例外を指定する方法、デバッガーを中断するポイント、中断を処理する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 10/09/2018
ms.topic: how-to
f1_keywords:
- vs.debug.exceptions
- vs.debug.exceptions.find
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- run-time errors
- exception handling, during debugging
- errors [debugger]
- debugger, runtime errors
- On Error-style error handlers
- exceptions, Win32
- run-time errors, debugging
- Win32, exceptions
- run time, exceptions
- error handling
- debugging [Visual Studio], exception handling
- common language runtime, exceptions
- native run-time checks
- exceptions, debugging
ms.assetid: 43a77fa8-37d0-4c98-a334-0134dbca4ece
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 89795df3a4c6b87c6a878cd07a072027f880e660
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390425"
---
# <a name="manage-exceptions-with-the-debugger-in-visual-studio"></a>Visual Studio のデバッガーでの例外の管理

例外は、プログラムの実行中に発生したエラー状態を示します。 中断する例外または例外のセット、またはデバッガーが中断するポイント (つまり、デバッガーでの一時停止) をデバッガーに指定できます。 デバッガーが中断すると、例外がスローされた場所が示されます。 例外を追加または削除することもできます。 Visual Studio でソリューションを開いた状態で、 **[デバッグ]、[Windows]、[例外設定]** を使用して、 **[例外設定]** ウィンドウを開きます。

最も重要な例外に応答するハンドラーを指定します。 例外にハンドラーを追加する方法については、[より良い C# コードを書くことでバグを修正する](../debugger/write-better-code-with-visual-studio.md)に関する記事を参照してください。 また、一部の例外で実行が常に中断されるようにデバッガーを構成する方法についても学習してください。

例外が発生すると、 **[出力]** ウィンドウに例外メッセージが書き込まれます。 次のような場合、実行が中断される場合があります。

- 処理されない例外がスローされた。
- デバッガーがハンドラーが呼び出される前に実行を中断するように構成されている。
- [マイ コードのみ](../debugger/just-my-code.md)を設定済みで、ユーザー コードで処理されないすべての例外でデバッガーの実行が中断されるように設定されている。

> [!NOTE]
> ASP.NET は、エラー ページをブラウザーに表示する最上位の例外ハンドラーを持っています。 **マイ コードのみ** がオフの場合、実行は中断されません。 例については、以下の「[ユーザーが処理しない例外での続行をデバッガーに指定する](#BKMK_UserUnhandled)」をご覧ください。

<!-- Two consecutive notes are intentional here...-->

> [!NOTE]
> Visual Basic アプリケーションのデバッガーでは、すべてのエラーが例外として管理されます。On Error 形式のエラー ハンドラーを使用している場合でもそうです。

## <a name="tell-the-debugger-to-break-when-an-exception-is-thrown"></a>例外がスローされたときに中断するようにデバッガーに指定する

例外がスローされた時点でデバッガーが実行を中断するように指定して、ハンドラーが呼び出される前に例外を調査することができます。

**[例外設定]** ウィンドウ ( **[デバッグ] > [Windows] > [例外設定]** ) で、 **[共通言語ランタイム例外]** などの例外のカテゴリのノードを展開します。 次に、**System.AccessViolationException** などのそのカテゴリの特定の例外のチェックボックスをオンにします。 例外のカテゴリ全体を選択することもできます。

![チェック済みの AccessViolationException](../debugger/media/exceptionsettingscheckaccess.png "ExceptionSettingsCheckAccess")

> [!TIP]
> 特定の例外を見つけるには、 **[例外設定]** ツールバーの **[検索]** ウィンドウを使用するか、検索を使用して特定の名前空間 (たとえば **System.IO**) をフィルター処理します。

**[例外設定]** ウィンドウで例外を選択すると、処理されているかどうかに関係なく、例外がスローされた箇所でデバッガーの実行が中断されます。 この例外は初回例外と呼ばれます。 例として、いくつかのシナリオを以下に示します。

- 次の C# コンソール アプリケーションで、Main メソッドは `try/catch` ブロック内で **AccessViolationException** をスローします。

  ```csharp
  static void Main(string[] args)
  {
      try
      {
          throw new AccessViolationException();
          Console.WriteLine("here");
      }
      catch (Exception e)
      {
          Console.WriteLine("caught exception");
      }
      Console.WriteLine("goodbye");
  }
  ```

  **[例外設定]** で **[AccessViolationException]** のチェック ボックスをオンにした場合、このコードをデバッガーで実行すると、`throw` 行で実行が中断されます。 実行は続行することができます。 コンソールには、次の行が両方とも表示される必要があります。

  ```cmd
  caught exception
  goodbye
  ```

  しかし、`here` 行は表示されません。

- C# コンソール アプリケーションでは、2 つのメソッドを持つクラスを使用してクラス ライブラリが参照されます。 1 番目のメソッドが例外をスローしてそれを処理している間、2 番目のメソッドが同じ例外をスローしますが、それを処理しません。

  ```csharp
  public class Class1
  {
      public void ThrowHandledException()
      {
          try
          {
              throw new AccessViolationException();
          }
          catch (AccessViolationException ave)
          {
              Console.WriteLine("caught exception" + ave.Message);
          }
      }

      public void ThrowUnhandledException()
      {
          throw new AccessViolationException();
      }
  }
  ```

  コンソール アプリケーションの Main() メソッドを次に示します。

  ```csharp
  static void Main(string[] args)
  {
      Class1 class1 = new Class1();
      class1.ThrowHandledException();
      class1.ThrowUnhandledException();
  }
  ```

  **[例外設定]** で **[AccessViolationException]** のチェック ボックスをオンにした場合、このコードをデバッガーで実行すると、**ThrowHandledException()** と **ThrowUnhandledException()** の両方の `throw` 行で実行が中断されます。

例外設定を既定に復元するには、次のように **[一覧を既定の設定に復元]** ボタンを選択します。

![[例外設定] を既定に戻す](../debugger/media/restoredefaultexceptions.png "RestoreDefaultExceptions")

## <a name="tell-the-debugger-to-continue-on-user-unhandled-exceptions"></a><a name="BKMK_UserUnhandled"></a>ユーザーが処理しない例外での続行をデバッガーに指定する

[マイ コードのみ](../debugger/just-my-code.md)を使用して .NET コードまたは JavaScript コードをデバッグする場合、ユーザー コードでは処理されない、他の場所で処理される例外では中断しないよう、デバッガーで指定できます。

1. **[例外設定]** ウィンドウで、列ラベルを右クリックしてショートカット メニューを開き、 **[列の表示] > [追加のアクション]** を選択します。 (このコマンドは、**マイ コードのみ** をオフにしている場合は表示されません)。 **[追加のアクション]** という名前の 3 番目の列が表示されます。

   ![[追加のアクション] 列](../debugger/media/additionalactionscolumn.png "AdditionalActionsColumn")

   この列に **[ユーザー コードで処理されない場合は続行]** と表示される例外の場合、ユーザー コードで処理されない、他の場所で処理される例外の場合はデバッガーは続行されます。

2. 特定の例外でこの設定を変更するには、その例外を選択し、右クリックしてショートカット メニューを表示し、 **[ユーザー コードで処理されない場合は続行]** を選択します。 また、すべての共通言語ランタイムの例外など、例外のカテゴリ全体を設定変更することもできます。

   ![**[ユーザー コードで処理されない場合は続行]** 設定](../debugger/media/continuewhenunhandledinusercodesetting.png "ContinueWhenUnhandledInUserCodeSetting")

たとえば、ASP.NET Web アプリケーションは、例外を HTTP 500 状態コードに変換して処理します ([ASP.NET Web API での例外の処理](/aspnet/web-api/overview/error-handling/exception-handling))。この場合、例外の原因を特定できないことがあります。 次の例では、ユーザー コードは、 `String.Format()` をスローする <xref:System.FormatException>を呼び出します。 実行は次のように中断されます。

![ユーザーで処理されない例外での中断](../debugger/media/exceptionunhandledbyuser.png "ExceptionUnhandledByUser")

## <a name="add-and-delete-exceptions"></a>例外を追加および削除する

例外は追加および削除することができます。 カテゴリから例外の種類を削除するには、その例外を選択し、 **[例外設定]** ツールバーの **[Delete the selected exception from the list]** \(一覧から選択した例外を削除します\) ボタン (マイナス記号) を選択します。 または、その例外を右クリックし、ショートカット メニューの **[削除]** を選択します。 例外の削除は、例外のオフと同じ効果があります。すなわち、該当する例外がスローされても、デバッガーは中断されません。

例外を追加するには:

1. **[例外設定]** ウィンドウで、例外カテゴリの 1 つ (たとえば、 **[共通言語ランタイム]** ) を選択します。

2. **[Add an exception to the selected category]** \(選択したカテゴリに例外を追加します\) ボタン (プラス記号) を選択します。

   ![**[Add an exception to the selected category]\(選択したカテゴリに例外を追加します\)** ボタン](../debugger/media/addanexceptiontotheselectedcategorybutton.png "AddAnExceptionToTheSelectedCategoryButton")

3. 例外名 (例: **System.UriTemplateMatchException**) を入力します。

   ![例外名を入力する](../debugger/media/typetheexceptionname.png "TypeTheExceptionName")

   例外が一覧 (アルファベット順の) に追加され、自動的にオンになります。

GPU メモリ アクセス例外、JavaScript ランタイム例外、または Win32 例外のカテゴリに例外を追加する場合は、そのエラー コードと説明を含めます。

> [!TIP]
> スペルを確認してください。 **[例外設定]** ウィンドウでは、追加された例外の存在について確認が行われません。 したがって、「**Sytem.UriTemplateMatchException**」と入力した場合は、その例外のエントリ (**System.UriTemplateMatchException** のエントリではなく) が表示されます。

例外の設定はソリューションの .suo ファイルに保持され、特定のソリューションに適用されます。 複数のソリューションの間で、特定の例外設定を再利用することはできません。 これで、追加された例外だけが存続することになります。削除された例外は存続しません。 例外を追加してから、ソリューションをいったん閉じて、再度開いた場合、その例外は表示されたままです。 しかし、例外を削除してから、ソリューションをいったん閉じて、再度開いた場合、例外は再表示されます。

**[例外設定]** ウィンドウでは、C# の汎用的な例外タイプをサポートしていますが、Visual Basic の汎用的な例外タイプはサポートしていません。 `MyNamespace.GenericException<T>`のような例外が発生したときに実行が中断されるようにするには、例外を **[MyNamespace.GenericException`1]** として追加する必要があります。 すなわち、次のようなコードの例外を作成した場合:

```csharp
public class GenericException<T> : Exception
{
    public GenericException() : base("This is a generic exception.")
    {
    }
}
```

前の手順を使用して、 **[例外設定]** に例外を追加できます。

![一般的な例外の追加](../debugger/media/addgenericexception.png "AddGenericException")

## <a name="add-conditions-to-an-exception"></a>例外に条件を追加する

**[例外設定]** ウィンドウを使用すると、例外に条件を設定できます。 現在サポートされているのは、例外の条件としてモジュール名を含めるか除外するかです。 モジュール名を条件として設定すると、特定のコード モジュールのみで例外を中断させることができます。 特定のモジュールで中断されないように選択することも可能です。

> [!NOTE]
> 例外に対する条件の追加は、[!include[vs_dev15](../misc/includes/vs_dev15_md.md)] 以降でサポートされています。

条件付きの例外を追加するには:

1. [例外設定] ウィンドウで **[条件の編集]** ボタンを選択するか、例外を右クリックして **[条件の編集]** を選択します。

   ![例外の条件](../debugger/media/dbg-conditional-exception.png "DbgConditionalException")

2. 例外に必要な条件を追加するには、新しい条件ごとに **[条件の追加]** を選択します。 条件の行が追加表示されます。

   ![例外用の追加の条件](../debugger/media/extraconditionsforanexception.png "ExtraConditionsForAnException")

3. 条件行ごとにモジュール名を入力し、比較演算子リストを **[次の値と等しい]** または **[次の値と等しくない]** に変更します。 モジュールを複数指定したい場合は、名前にワイルドカード ( **\\\*** ) を指定することも可能です。

4. 条件を削除する場合は、条件行の末尾の **X** を選択します。

## <a name="see-also"></a>関連項目

- [例外後の実行の継続](../debugger/continuing-execution-after-an-exception.md)<br/>
- [方法: 例外の後にシステム コードを調べる](../debugger/how-to-examine-system-code-after-an-exception.md)<br/>
- [方法: ネイティブ ランタイム チェックを使用する](../debugger/how-to-use-native-run-time-checks.md)<br/>
- [デバッガーでのはじめに](../debugger/debugger-feature-tour.md)
