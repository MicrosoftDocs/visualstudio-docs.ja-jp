---
title: 'チュートリアル: シンプルな C# コンソール アプリを拡張する'
description: Visual Studio で C# コンソール アプリを開発する方法について、ステップ バイ ステップで説明します。
ms.custom: vs-acquisition, get-started
ms.date: 04/15/2021
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
ms.topic: tutorial
ms.devlang: CSharp
author: ghogen
ms.author: ghogen
manager: jmartens
monikerRange: '>=vs-2019'
dev_langs:
- CSharp
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: c7c38ed40143064090535735b2050dd31904d608
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390178"
---
# <a name="tutorial-extend-a-simple-c-console-app"></a>チュートリアル: シンプルな C# コンソール アプリを拡張する

このチュートリアルでは、最初のパートで作成したコンソール アプリを、Visual Studio を使用して拡張する方法について説明します。 複数のプロジェクトの管理やサードパーティ パッケージの参照など、日々の開発に必要な Visual Studio の機能についていくつか説明します。

このシリーズの[最初のパート](tutorial-console.md)を完了している場合は、電卓コンソール アプリは既に用意できています。  パート 1 をスキップするには、GitHub リポジトリからプロジェクトを開くところから始めます。 C# 電卓アプリは、[vs-tutorial-samples リポジトリ](https://github.com/MicrosoftDocs/vs-tutorial-samples)にあるので、「[チュートリアル: リポジトリからプロジェクトを開く](../tutorial-open-project-from-repo.md)」に記載されている手順に従うと開始することができます。

## <a name="add-a-new-project"></a>新しいプロジェクトの追加

実際のコードでは、1 つのソリューション内で多くのプロジェクトを連携させる必要があります。 ここで、電卓アプリに別のプロジェクトを追加してみましょう。 これは、一部の電卓関数を備えたクラス ライブラリとなります。

1. Visual Studio では、トップレベルのメニュー コマンド **[ファイル]**  >  **[追加]**  >  **[新しいプロジェクト]** を使用して新しいプロジェクトを追加することができますが、既存のプロジェクト名 ("プロジェクト ノード" と呼ばれます) を右クリックし、プロジェクトのショートカット メニュー (またはコンテキスト メニュー) を開くこともできます。 このショートカット メニューでは、さまざまな方法でご自分のプロジェクトに機能を追加することができます。 そのため、**ソリューション エクスプローラー** でご自分のプロジェクト ノードを右クリックし、 **[追加]**  >  **[新しいプロジェクト]** の順に選択します。

1. C# プロジェクト テンプレート **[クラス ライブラリ (.NET Standard)]** を選択します。

   ![[クラス ライブラリ] プロジェクト テンプレートの選択のスクリーンショット](media/vs-2019/calculator2-add-project-dark.png)

1. [プロジェクト名] として「**CalculatorLibrary**」と入力し、 **[作成]** を選択します。 ここでも、プロンプトが表示されたら .NET 3.1 を選択します。 Visual Studio によって、新しいプロジェクトが作成され、ソリューションに追加されます。

   ![CalculatorLibrary クラス ライブラリ プロジェクトが追加されているソリューション エクスプローラーのスクリーンショット。](media/vs-2019/calculator2-solution-explorer-with-class-library-dark2.png)

1. *Class1.cs* を使用するのでなく、ファイルの名前を **CalculatorLibrary.cs** に変更します。 **ソリューション エクスプローラー** 内で該当する名前をクリックして名前を変更するか、右クリックして **[名前変更]** を選択するか、または **F2** キーを押します。

   ファイル内の `Class1` への参照名を変更するかどうかを確認するメッセージが表示される場合があります。 後の手順でコードを置き換えるので、どのように答えてもかまいません。

1. ここで、新しいクラス ライブラリによって公開される API を最初のプロジェクトが使用できるように、プロジェクト参照を追加する必要があります。  最初のプロジェクト内の **[依存関係]** ノードを右クリックし、 **[プロジェクト参照の追加]** を選択します。

   ![[プロジェクト参照の追加] 項目のスクリーンショット](media/vs-2019/calculator2-add-project-reference-dark.png)

   **[参照マネージャー]** ダイアログ ボックスが表示されます。 このダイアログ ボックスを使用すると、ご自分のプロジェクトに必要なアセンブリと COM DLL に加えて、他のプロジェクトへの参照を追加できます。

   ![[参照マネージャー] ダイアログ ボックスのスクリーンショット](media/vs-2019/calculator2-ref-manager-dark.png)

1. **[参照マネージャー]** ダイアログ ボックスで、 **[CalculatorLibrary]** プロジェクトのチェックボックスをオンにして、 **[OK]** を選択します。  プロジェクト参照は、**ソリューション エクスプローラー** で **[プロジェクト]** ノードの下に表示されます。

   ![プロジェクト参照が表示されているソリューション エクスプローラーのスクリーンショット](media/vs-2019/calculator2-solution-explorer-with-project-reference-dark2.png)

1. *Program.cs* 内で、`Calculator` クラスとそのコード全体を選択し、**CTRL + X** キーを押して Program.cs からそれを切り取ります。 次に、**CalculatorLibrary** にある *CalculatorLibrary.cs* の `CalculatorLibrary` 名前空間にコードを貼り付けます。 次に、Calculator クラスを `public` にして、ライブラリの外部に公開します。 *CalculatorLibrary.cs* 内のコードは、次のコードのようになります。

   ```csharp
   using System;

    namespace CalculatorLibrary
    {
        public class Calculator
        {
            public static double DoOperation(double num1, double num2, string op)
            {
                double result = double.NaN; // Default value is "not-a-number" which we use if an operation, such as division, could result in an error.

                // Use a switch statement to do the math.
                switch (op)
                {
                    case "a":
                        result = num1 + num2;
                        break;
                    case "s":
                        result = num1 - num2;
                        break;
                    case "m":
                        result = num1 * num2;
                        break;
                    case "d":
                        // Ask the user to enter a non-zero divisor.
                        if (num2 != 0)
                        {
                            result = num1 / num2;
                        }
                        break;
                    // Return text for an incorrect option entry.
                    default:
                        break;
                }
                return result;
            }
        }
    }
   ```

1. 最初のプロジェクトには参照がありますが、Calculator.DoOperation 呼び出しが解決されないというエラーが表示されます。 これは、CalculatorLibrary が異なる名前空間にあるためです。したがって、完全修飾参照のためには `CalculatorLibrary` 名前空間を追加します。

   ```csharp
   result = CalculatorLibrary.Calculator.DoOperation(cleanNum1, cleanNum2, op);
   ```

   代わりに、using ディレクティブをファイルの先頭に追加してみてください。

   ```csharp
   using CalculatorLibrary;
   ```

   この変更を行えば、呼び出しサイトから CalculatorLibrary 名前空間を削除できるようになりますが、今度はあいまいさが生じます。 `Calculator` は CalculatorLibrary 内のクラスでしょうか、それとも Calculator は名前空間でしょうか?  あいまいさを解決するには、名前空間 `CalculatorProgram` の名前を変更します。

   ```csharp
   namespace CalculatorProgram
   ```

## <a name="reference-net-libraries-write-to-a-log"></a>.NET ライブラリを参照する: ログに書き込む

1. ここで、すべての操作に関するログを追加し、それをテキスト ファイルに書き込むとします。 .NET `Trace` クラスによって、この機能が提供されます (これは基本的な出力デバッグ手法にも役立ちます)。Trace クラスは System.Diagnostics にあります。また、`StreamWriter` のような System.IO クラスが必要になるため、まず、using ディレクティブを *CalculatorLibrary.cs* の一番上に追加します。

   ```csharp
   using System.IO;
   using System.Diagnostics;
   ```

1. Trace クラスがどのように使用されているのかを確認するには、filestream に関連付けられているクラスの参照を維持する必要があります。 つまり、電卓はオブジェクトとしてより適切に動作するので、*CalculatorLibrary.cs* の Calculator クラスの先頭に、コンストラクターを追加してみましょう。

   ```csharp
   public Calculator()
        {
            StreamWriter logFile = File.CreateText("calculator.log");
            Trace.Listeners.Add(new TextWriterTraceListener(logFile));
            Trace.AutoFlush = true;
            Trace.WriteLine("Starting Calculator Log");
            Trace.WriteLine(String.Format("Started {0}", System.DateTime.Now.ToString()));
        }

    public double DoOperation(double num1, double num2, string op)
        {
   ```

1. さらに、静的な `DoOperation` メソッドをメンバー メソッドに変更し、`static` キーワードを削除する必要があります。  また、ログ用に各計算に出力を追加します。結果、DoOperation のコードは次のようになります。

   ```csharp
   public double DoOperation(double num1, double num2, string op)
   {
        double result = double.NaN; // Default value is "not-a-number" which we use if an operation, such as division, could result in an error.

        // Use a switch statement to do the math.
        switch (op)
        {
            case "a":
                result = num1 + num2;
                Trace.WriteLine(String.Format("{0} + {1} = {2}", num1, num2, result));
                break;
            case "s":
                result = num1 - num2;
                Trace.WriteLine(String.Format("{0} - {1} = {2}", num1, num2, result));
                break;
            case "m":
                result = num1 * num2;
                Trace.WriteLine(String.Format("{0} * {1} = {2}", num1, num2, result));
                break;
            case "d":
                // Ask the user to enter a non-zero divisor.
                if (num2 != 0)
                {
                    result = num1 / num2;
                    Trace.WriteLine(String.Format("{0} / {1} = {2}", num1, num2, result));
                }
                    break;
            // Return text for an incorrect option entry.
            default:
                break;
        }
        return result;
    }
   ```

1. ここで *Program.cs* に戻ると、静的な呼び出しに赤い波線のフラグが付けられています。 これを修正するには、`while (!endApp)` ループの直前に次の行を追加して、`calculator` 変数を作成します。

   ```csharp
   Calculator calculator = new Calculator();
   ```

   次のように、`DoOperation` の呼び出しサイトを変更します。これにより、小文字の `calculator` という名前のオブジェクトが参照されるため、これは静的メソッドの呼び出しではなく、メンバー呼び出しになります。

   ```csharp
   result = calculator.DoOperation(cleanNum1, cleanNum2, op);
   ```

1. プログラムをもう一度実行します。完了したら、プロジェクト ノードを右クリックし、 **[エクスプローラーでフォルダーを開く]** を選択して、エクスプローラーを下方の出力フォルダーまで移動します。 それは *bin/Debug/netcoreapp3.1* である可能性があります。*calculator.log* ファイルを開きます。

    ```output
    Starting Calculator Log
    Started 7/9/2020 1:58:19 PM
    1 + 2 = 3
    3 * 3 = 9
    ```

この時点で、*CalculatorLibrary.cs* は次のようになります。

```csharp
using System;
using System.IO;
using System.Diagnostics;


namespace CalculatorLibrary
{
    public class Calculator
    {

        public Calculator()
        {
            StreamWriter logFile = File.CreateText("calculator.log");
            Trace.Listeners.Add(new TextWriterTraceListener(logFile));
            Trace.AutoFlush = true;
            Trace.WriteLine("Starting Calculator Log");
            Trace.WriteLine(String.Format("Started {0}", System.DateTime.Now.ToString()));
        }

        public double DoOperation(double num1, double num2, string op)
        {
            double result = double.NaN; // Default value is "not-a-number" which we use if an operation, such as division, could result in an error.

            // Use a switch statement to do the math.
            switch (op)
            {
                case "a":
                    result = num1 + num2;
                    Trace.WriteLine(String.Format("{0} + {1} = {2}", num1, num2, result));
                    break;
                case "s":
                    result = num1 - num2;
                    Trace.WriteLine(String.Format("{0} - {1} = {2}", num1, num2, result));
                    break;
                case "m":
                    result = num1 * num2;
                    Trace.WriteLine(String.Format("{0} * {1} = {2}", num1, num2, result));
                    break;
                case "d":
                    // Ask the user to enter a non-zero divisor.
                    if (num2 != 0)
                    {
                        result = num1 / num2;
                        Trace.WriteLine(String.Format("{0} / {1} = {2}", num1, num2, result));
                    }
                    break;
                // Return text for an incorrect option entry.
                default:
                    break;
            }
            return result;
        }
    }
}
```

*Program.cs* は次のようになります。

```csharp
using System;
using CalculatorLibrary;

namespace CalculatorProgram
{
   
    class Program
    {
        static void Main(string[] args)
        {
            bool endApp = false;
            // Display title as the C# console calculator app.
            Console.WriteLine("Console Calculator in C#\r");
            Console.WriteLine("------------------------\n");

            Calculator calculator = new Calculator();
            while (!endApp)
            {
                // Declare variables and set to empty.
                string numInput1 = "";
                string numInput2 = "";
                double result = 0;

                // Ask the user to type the first number.
                Console.Write("Type a number, and then press Enter: ");
                numInput1 = Console.ReadLine();

                double cleanNum1 = 0;
                while (!double.TryParse(numInput1, out cleanNum1))
                {
                    Console.Write("This is not valid input. Please enter an integer value: ");
                    numInput1 = Console.ReadLine();
                }

                // Ask the user to type the second number.
                Console.Write("Type another number, and then press Enter: ");
                numInput2 = Console.ReadLine();

                double cleanNum2 = 0;
                while (!double.TryParse(numInput2, out cleanNum2))
                {
                    Console.Write("This is not valid input. Please enter an integer value: ");
                    numInput2 = Console.ReadLine();
                }

                // Ask the user to choose an operator.
                Console.WriteLine("Choose an operator from the following list:");
                Console.WriteLine("\ta - Add");
                Console.WriteLine("\ts - Subtract");
                Console.WriteLine("\tm - Multiply");
                Console.WriteLine("\td - Divide");
                Console.Write("Your option? ");

                string op = Console.ReadLine();

                try
                {
                    result = calculator.DoOperation(cleanNum1, cleanNum2, op); 
                    if (double.IsNaN(result))
                    {
                        Console.WriteLine("This operation will result in a mathematical error.\n");
                    }
                    else Console.WriteLine("Your result: {0:0.##}\n", result);
                }
                catch (Exception e)
                {
                    Console.WriteLine("Oh no! An exception occurred trying to do the math.\n - Details: " + e.Message);
                }

                Console.WriteLine("------------------------\n");

                // Wait for the user to respond before closing.
                Console.Write("Press 'n' and Enter to close the app, or press any other key and Enter to continue: ");
                if (Console.ReadLine() == "n") endApp = true;

                Console.WriteLine("\n"); // Friendly linespacing.
            }
            return;
        }
    }
}
```

## <a name="add-a-nuget-package-write-to-a-json-file"></a>NuGet パッケージを追加する: JSON ファイルに書き込む

1. ここで、操作を JSON 形式で出力するとします。これは、オブジェクト データを格納するための一般的で移植可能な形式です。 その機能を実装するには、NuGet パッケージ Newtonsoft.Json を参照する必要があります。 NuGet パッケージは、.NET クラス ライブラリを配布するための主要な手段です。 **ソリューション エクスプローラー** で、CalculatorLibrary プロジェクトの **[依存関係]** ノードを右クリックし、 **[NuGet パッケージの管理]** を選択します。

   ![ショートカット メニューの [NuGet パッケージの管理] のスクリーンショット](media/vs-2019/calculator2-manage-nuget-packages-dark2.png)

   NuGet パッケージ マネージャーが開きます。

   ![NuGet パッケージ マネージャーのスクリーンショット](media/vs-2019/calculator2-nuget-package-manager-dark.png)

1. Newtonsoft.Json パッケージを検索し、 **[インストール]** を選択します。

   ![Newtonsoft NuGet パッケージ情報のスクリーンショット](media/vs-2019/calculator2-nuget-newtonsoft-json-dark2.png)

   そのパッケージがダウンロードされ、ご自分のプロジェクトに追加されます。**ソリューション エクスプローラー** 内の [参照] ノードに新しいエントリが表示されます。

1. *CalculatorLibrary.cs* の先頭に System.IO と Newtonsoft.Json パッケージ用の using ディレクティブを追加します。

   ```csharp
   using Newtonsoft.Json;
   ```

1. ここで、電卓のコンストラクターを次のコードに置き換え、JsonWriter メンバー オブジェクトを作成します。

   ```csharp
        JsonWriter writer;

        public Calculator()
        {
            StreamWriter logFile = File.CreateText("calculatorlog.json");
            logFile.AutoFlush = true;
            writer = new JsonTextWriter(logFile);
            writer.Formatting = Formatting.Indented;
            writer.WriteStartObject();
            writer.WritePropertyName("Operations");
            writer.WriteStartArray();
        }
   ```

1. `DoOperation` メソッドを変更して、JSON ライター コードを追加します。

   ```csharp
        public double DoOperation(double num1, double num2, string op)
        {
            double result = double.NaN; // Default value is "not-a-number" which we use if an operation, such as division, could result in an error.
            writer.WriteStartObject();
            writer.WritePropertyName("Operand1");
            writer.WriteValue(num1);
            writer.WritePropertyName("Operand2");
            writer.WriteValue(num2);
            writer.WritePropertyName("Operation");
            // Use a switch statement to do the math.
            switch (op)
            {
                case "a":
                    result = num1 + num2;
                    writer.WriteValue("Add");
                    break;
                case "s":
                    result = num1 - num2;
                    writer.WriteValue("Subtract");
                    break;
                case "m":
                    result = num1 * num2;
                    writer.WriteValue("Multiply");
                    break;
                case "d":
                    // Ask the user to enter a non-zero divisor.
                    if (num2 != 0)
                    {
                        result = num1 / num2;
                        writer.WriteValue("Divide");
                    }
                    break;
                // Return text for an incorrect option entry.
                default:
                    break;
            }
            writer.WritePropertyName("Result");
            writer.WriteValue(result);
            writer.WriteEndObject();

            return result;
        }
   ```

1. ユーザーが操作データの入力を完了したら、JSON 構文を完了するためのメソッドを追加する必要があります。

   ```csharp
    public void Finish()
    {
        writer.WriteEndArray();
        writer.WriteEndObject();
        writer.Close();
    }
   ```

1. さらに、*Program.cs* 内で、最後に Finish への呼び出しを追加します。

   ```csharp
            // And call to close the JSON writer before return
            calculator.Finish();
            return;
        }
   ```

1. アプリをビルドして実行します。いくつかの操作を入力したら、'n' コマンドを使用してアプリを適切に閉じます。  ここで、calculatorlog.json ファイルを開くと、次のような内容が表示されます。

   ```json
   {
    "Operations": [
        {
        "Operand1": 2.0,
        "Operand2": 3.0,
        "Operation": "Add",
        "Result": 5.0
        },
        {
        "Operand1": 3.0,
        "Operand2": 4.0,
        "Operation": "Multiply",
        "Result": 12.0
        }
    ]
   }
   ```

## <a name="debug-set-and-hit-a-breakpoint"></a>デバッグ: ブレークポイントを設定してヒットする

Visual Studio のデバッガーは強力なツールであり、コードを 1 ステップずつ実行して、プログラミングが間違っている箇所を正確に発見することができます。 そのようにして、コードで行う必要がある修正について理解します。 Visual Studio を使用すると、プログラムを実行し続けられるように、一時的な変更を行うことができます。

1. *Program.cs* で、次のコードの左側の余白をクリックします (または、ショートカット メニューを開いて **[ブレークポイント]**  >  **[ブレークポイントの挿入]** を選択するか、**F9** キーを押します)。

   ```csharp
   result = calculator.DoOperation(cleanNum1, cleanNum2, op);
   ```

   表示される赤い円は、ブレークポイントを示します。 ブレークポイントを使用すると、アプリを一時停止して、コードを調べることができます。 コードの任意の実行可能な行に、ブレークポイントを設定できます。

   ![ブレークポイントの設定のスクリーンショット](media/vs-2019/calculator-2-debug-set-breakpoint.png)

1. アプリをビルドし、実行します。

1. 実行中のアプリで、計算用にいくつかの値を入力します。

   - 最初の値として、「**8**」と入力します。
   - 2 番目の値として、「**0**」と入力します。
   - 演算子には「**d**」と入力して、どうなるか見てみましょう。

   アプリは、ブレークポイントを作成した場所で一時停止します。これは、左側の黄色いポインターと、強調表示されたコードによって示されます。 強調表示されたコードはまだ実行されていません。

   ![ブレークポイントにヒットしたスクリーンショット](media/vs-2019/calculator-2-debug-hit-breakpoint.png)

   これで、アプリは一時停止しているので、アプリケーションの状態を調べることができます。

## <a name="debug-view-variables"></a>デバッグ: 変数を表示する

1. 強調表示されたコードで、`cleanNum1` や `op` などの変数をポイントします。 これらの変数の現在の値 (それぞれ`8` と `d`) が、データヒントに表示されます。

   ![データヒントの表示のスクリーンショット](media/vs-2019/calculator-2-debug-view-datatip.png)

   デバッグ時には、変数に予想されるとおりの値が保持されているかどうかを確認することが、問題の修正に不可欠なことがよくあります。

2. 下のペインで、 **[ローカル]** ウィンドウを確認します。 (閉じている場合は、 **[デバッグ]**  >  **[ウィンドウ]**  >  **[ローカル]** を選択して開きます)。

   [ローカル] ウィンドウには、現在スコープ内にある各変数およびその値と型が表示されます。

   ![[ローカル] ウィンドウのスクリーンショット](media/vs-2019/calculator-2-debug-locals-window.png)

3. **[自動変数]** ウィンドウを見てください。

   [自動変数] ウィンドウは **[ローカル]** ウィンドウと似ていますが、アプリが一時停止している現在のコード行の直前と直後における変数が表示されます。

   次に、デバッガーでコードを一度に 1 ステートメントだけ実行します。これは "*ステップ実行*" と呼ばれます。

## <a name="debug-step-through-code"></a>デバッグ: コードをステップ実行する

1. **F11** キーを押します (または、 **[デバッグ]**  >  **[ステップイン]** )。

   [ステップイン] コマンドを使用すると、アプリの現在のステートメントが実行された後、次の実行可能なステートメント (通常は次のコード行) に進みます。 左側の黄色いポインターは、常に現在のステートメントを示しています。

   ![ステップイン コマンドのスクリーンショット](media/vs-2019/calculator-2-debug-step-into.png)

   ちょうど、`Calculator` クラスの `DoOperation` メソッドにステップインしたところです。

1. 階層的なプログラム フローを確認するには、 **[呼び出し履歴]** ウィンドウを見ます。 (閉じている場合は、 **[デバッグ]**  >  **[ウィンドウ]**  >  **[呼び出し履歴]** を選択します)。

   ![呼び出し履歴のスクリーンショット](media/vs-2019/calculator-2-debug-call-stack.png)

   このビューには、黄色のポインターによって示される現在の `Calculator.DoOperation` メソッドが表示されており、2 番目の行には、それを呼び出した *Program.cs* の `Main` メソッドの関数が示されています。 **[呼び出し履歴]** ウィンドウには、メソッドおよび関数が呼び出されている順番が表示されます。 また、ショートカット メニューからは、 **[ソース コードへ移動]** など、デバッガーの多くの機能にアクセスできます。

1. アプリが `switch` ステートメントで一時停止するまで、**F10** キーを何回か押します (または、 **[デバッグ]**  >  **[ステップ オーバー]** )。

   ```csharp
   switch (op)
   {
   ```

   [ステップ オーバー] コマンドは [ステップ イン] コマンドに似ていますが、現在のステートメントが関数を呼び出しの場合、呼び出された関数のコードはデバッガーによって実行され、関数から戻るまで実行が中断しない点が異なります。 特定の関数に関心がない場合は、ステップ オーバーを使用してコード内をすばやく移動できます。

1. もう一度 **F10** キーを押して、アプリが次のコード行で一時停止するようにします。

   ```csharp
   if (num2 != 0)
   {
   ```

   このコードにおいては、0 による除算のケースが調べられてます。 アプリを続行すると、一般例外 (エラー) がスローされますが、これをバグと見なし、実際に返される値をコンソールで表示するなど、他の何らかの操作を実行するとします。 1 つの方法として、デバッガーのエディット コンティニュと呼ばれる機能を使用して、コードを変更した後、デバッグを続けることができます。 ただし、ここでは実行フローを一時的に変更するための別の方法を紹介します。

## <a name="debug-test-a-temporary-change"></a>デバッグ: 一時的な変更をテストする

1. 現在は `if (num2 != 0)` ステートメントで一時停止している黄色のポインターを選択し、それを次のステートメントにドラッグします。

   ```csharp
   result = num1 / num2;
   ```

   これにより、アプリは `if` ステートメントを完全にスキップするため、ゼロで除算した場合に何が起きるかを確認できます。

1. **F10** キーを押してコード行を実行します。

1. `result` 変数をポイントすると、`Infinity` という値が格納されていることがわかります。

   C# の場合、 `Infinity` は 0 で除算した場合の結果です。

1. **F5** キーを押します (または **[デバッグ]**  >  **[デバッグの続行]** )。

   算術演算の結果として、無限大記号がコンソールに表示されます。

1. "n" コマンドを使用して、アプリを適切に閉じます。

## <a name="code-complete"></a>完成したコード

次に、すべての手順が完了した後の、*CalculatorLibrary.cs* ファイルの完全なコードを示します。

```csharp
using System;
using System.IO;
using System.Diagnostics;
using Newtonsoft.Json;

namespace CalculatorLibrary
{
    public class Calculator
    {

        JsonWriter writer;

        public Calculator()
        {
            StreamWriter logFile = File.CreateText("calculatorlog.json");
            logFile.AutoFlush = true;
            writer = new JsonTextWriter(logFile);
            writer.Formatting = Formatting.Indented;
            writer.WriteStartObject();
            writer.WritePropertyName("Operations");
            writer.WriteStartArray();
        }

        public double DoOperation(double num1, double num2, string op)
        {
            double result = double.NaN; // Default value is "not-a-number" which we use if an operation, such as division, could result in an error.
            writer.WriteStartObject();
            writer.WritePropertyName("Operand1");
            writer.WriteValue(num1);
            writer.WritePropertyName("Operand2");
            writer.WriteValue(num2);
            writer.WritePropertyName("Operation");
            // Use a switch statement to do the math.
            switch (op)
            {
                case "a":
                    result = num1 + num2;
                    writer.WriteValue("Add");
                    break;
                case "s":
                    result = num1 - num2;
                    writer.WriteValue("Subtract");
                    break;
                case "m":
                    result = num1 * num2;
                    writer.WriteValue("Multiply");
                    break;
                case "d":
                    // Ask the user to enter a non-zero divisor.
                    if (num2 != 0)
                    {
                        result = num1 / num2;
                        writer.WriteValue("Divide");
                    }
                    break;
                // Return text for an incorrect option entry.
                default:
                    break;
            }
            writer.WritePropertyName("Result");
            writer.WriteValue(result);
            writer.WriteEndObject();

            return result;
        }

        public void Finish()
        {
            writer.WriteEndArray();
            writer.WriteEndObject();
            writer.Close();
        }
    }
}
```

そしてこちらが、*Program.cs* のコードです。 

```csharp
using System;
using CalculatorLibrary;

namespace CalculatorProgram
{
   
    class Program
    {
        static void Main(string[] args)
        {
            bool endApp = false;
            // Display title as the C# console calculator app.
            Console.WriteLine("Console Calculator in C#\r");
            Console.WriteLine("------------------------\n");

            Calculator calculator = new Calculator();
            while (!endApp)
            {
                // Declare variables and set to empty.
                string numInput1 = "";
                string numInput2 = "";
                double result = 0;

                // Ask the user to type the first number.
                Console.Write("Type a number, and then press Enter: ");
                numInput1 = Console.ReadLine();

                double cleanNum1 = 0;
                while (!double.TryParse(numInput1, out cleanNum1))
                {
                    Console.Write("This is not valid input. Please enter an integer value: ");
                    numInput1 = Console.ReadLine();
                }

                // Ask the user to type the second number.
                Console.Write("Type another number, and then press Enter: ");
                numInput2 = Console.ReadLine();

                double cleanNum2 = 0;
                while (!double.TryParse(numInput2, out cleanNum2))
                {
                    Console.Write("This is not valid input. Please enter an integer value: ");
                    numInput2 = Console.ReadLine();
                }

                // Ask the user to choose an operator.
                Console.WriteLine("Choose an operator from the following list:");
                Console.WriteLine("\ta - Add");
                Console.WriteLine("\ts - Subtract");
                Console.WriteLine("\tm - Multiply");
                Console.WriteLine("\td - Divide");
                Console.Write("Your option? ");

                string op = Console.ReadLine();

                try
                {
                    result = calculator.DoOperation(cleanNum1, cleanNum2, op); 
                    if (double.IsNaN(result))
                    {
                        Console.WriteLine("This operation will result in a mathematical error.\n");
                    }
                    else Console.WriteLine("Your result: {0:0.##}\n", result);
                }
                catch (Exception e)
                {
                    Console.WriteLine("Oh no! An exception occurred trying to do the math.\n - Details: " + e.Message);
                }

                Console.WriteLine("------------------------\n");

                // Wait for the user to respond before closing.
                Console.Write("Press 'n' and Enter to close the app, or press any other key and Enter to continue: ");
                if (Console.ReadLine() == "n") endApp = true;

                Console.WriteLine("\n"); // Friendly linespacing.
            }
            calculator.Finish();
            return;
        }
    }
}
```

## <a name="next-steps"></a>次の手順

これでこのチュートリアルは完了です。 さらに詳しく学習するには、引き続き以下のチュートリアルをご覧ください。

> [!div class="nextstepaction"]
> [さらに C# チュートリアルを続ける](/dotnet/csharp/tutorials/)

> [!div class="nextstepaction"]
> [Visual Studio IDE の続行の概要](/../visual-studio-ide.md)

## <a name="see-also"></a>関連項目

- [C# IntelliSense](../../ide/visual-csharp-intellisense.md)
- [Visual Studio での C# コードのデバッグについて理解する](tutorial-debugger.md)
