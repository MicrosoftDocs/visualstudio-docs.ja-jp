---
title: 'チュートリアル: JavaScript を使用して SDK を作成する | Microsoft Docs'
description: このチュートリアルを使用して、JavaScript を使用し、Visual Studio 拡張機能として簡単な数値演算 SDK を作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: a8c89d5d-5b78-4435-817f-c5f25ca6d715
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3b9a3d9e84731fe0c2526b69f60cdda1b1487583
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080386"
---
# <a name="walkthrough-create-an-sdk-using-javascript"></a>チュートリアル: JavaScript を使用して SDK を作成する
このチュートリアルでは、JavaScript を使用し、Visual Studio 拡張機能 (VSIX) として簡単な数値演算 SDK を作成する方法について説明します。  このチュートリアルは、次の部分に分かれています。

- [SimpleMathVSIX 拡張機能 SDK プロジェクトを作成するには](../extensibility/walkthrough-creating-an-sdk-using-javascript.md#createSimpleMathVSIX)

- [SDK を使用するサンプル アプリを作成するには](../extensibility/walkthrough-creating-an-sdk-using-javascript.md#createSampleApp)

  JavaScript の場合、クラス ライブラリ プロジェクトの種類はありません。 このチュートリアルでは、サンプルの *arithmetic.js* ファイルを VSIX プロジェクトに直接作成します。 実際には、VSIX プロジェクトに配置する前に、まず JavaScript と CSS ファイルを Windows ストア アプリとして作成してテストすることをお勧めします (たとえば、**空のアプリケーション** テンプレートを使用して)。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「[Visual Studio SDK](../extensibility/visual-studio-sdk.md)」を参照してください。

## <a name="to-create-the-simplemathvsix-extension-sdk-project"></a><a name="createSimpleMathVSIX"></a> SimpleMathVSIX 拡張機能 SDK プロジェクトを作成するには

1. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。

2. テンプレート カテゴリの一覧で、 **[Visual C#]** の下の **[拡張性]** を選択し、 **[VSIX プロジェクト]** テンプレートを選択します。

3. **[名前]** テキスト ボックスに「`SimpleMathVSIX`」を指定して、 **[OK]** ボタンを選択します。

4. **Visual Studio パッケージ ウィザード** が表示されたら、**ウェルカム** ページで **[次へ]** をクリックします。次に、**1/7 ページ** で **[完了]** ボタンをクリックします。

     **マニフェスト デザイナー** が開きますが、このチュートリアルが複雑にならないように、マニフェスト ファイルを直接変更します。

5. **ソリューション エクスプローラー** で、**source.extension.vsixmanifest** ファイルのショートカット メニューを開き、 **[コードの表示]** を選択します。 このコードを使用して、ファイル内の既存のコンテンツを置き換えます。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <PackageManifest Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema/2011" xmlns:d="http://schemas.microsoft.com/developer/vsx-schema-design/2011">
      <Metadata>
        <Identity Id="SimpleMathVSIX" Version="1.0" Language="en-US" Publisher="myname" />
        <DisplayName>Simple Math</DisplayName>
        <Description>Does basic arithmetic calculations.</Description>
      </Metadata>
      <Installation Scope="Global" AllUsers="true">
        <InstallationTarget Id="Microsoft.ExtensionSDK" TargetPlatformIdentifier="Windows" TargetPlatformVersion="v8.0" SdkName="SimpleMath" SdkVersion="1.0" />
      </Installation>
      <Dependencies>
        <Dependency Id="Microsoft.Framework.NDP" DisplayName="Microsoft .NET Framework" d:Source="Manual" Version="4.5" />
      </Dependencies>
      <Assets>
        <Asset Type="Microsoft.ExtensionSDK" d:Source="File" Path="SDKManifest.xml" />
      </Assets>
    </PackageManifest>
    ```

6. **ソリューション エクスプローラー** で、**SimpleMathVSIX** プロジェクトのショートカット メニューを開き、 **[追加]**  >  **[新しい項目]** を選択します。

7. **[データ]** カテゴリで **[XML ファイル]** を選択し、ファイルに `SDKManifest.xml` という名前を付けて、 **[追加]** ボタンをクリックします。

8. **ソリューション エクスプローラー** で、**SDKManifest.xml** ファイルのショートカット メニューを開き、 **[開く]** を選択して、**XML エディター** でファイルを表示します。

9. **SDKManifest.xml** ファイルに次のコードを追加します。

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <FileList
      DisplayName="Simple Math"
      MinVSVersion="14.0"
      AppliesTo="JavaScript+WindowsAppContainer"
      SupportsMultipleVersions="Error"
      MoreInfo="https://msdn.microsoft.com/">

      <!-- JS -->
      <File Content="js\arithmetic.js" />
    </FileList>

    ```

10. **ソリューション エクスプローラー** で、**SDKManifest.xml** ファイルのショートカット メニューの **[プロパティ]** を選択します。

11. **[プロパティ]** ウィンドウで、 **[VSIX に含める]** プロパティを **[True]** に設定します。

12. **ソリューション エクスプローラー** の **SimpleMathVSIX** プロジェクトのショートカット メニューで、 **[追加]**  >  **[新しいフォルダー]** を選択して、フォルダーに `Redist` という名前を付けます。

13. Redist の下にサブフォルダーを追加して、次のフォルダー構造を作成します。

     *\Redist\CommonConfiguration\Neutral\SimpleMath\js\\*

14. **\js\\** フォルダーのショートカット メニューで、 **[追加]**  >  **[新しい項目]** を選択します。

15. **[Visual C# アイテム]** で、 **[Web]** カテゴリを選択し、 **[JavaScript ファイル]** 項目を選択します。 ファイルに `arithmetic.js` という名前を付けて、 **[追加]** ボタンを選択します。

16. *arithmetic.js* に次のコードを挿入します。

    ```csharp
    (function (global) {
        "use strict";
        global.Arithmetic = {
            add: function (firstNumber, secondNumber) {
                return firstNumber + secondNumber;
            },

            subtract: function (firstNumber, secondNumber) {
                return firstNumber - secondNumber;
            },

            multiply: function (firstNumber, secondNumber) {
                return firstNumber * secondNumber;
            },

            divide: function (firstNumber, secondNumber) {
                return firstNumber / secondNumber;
            }
        };
    })(this);

    ```

17. **ソリューション エクスプローラー** で、**arithmetic.js** ファイルのショートカット メニューの **[プロパティ]** を選択します。 次のプロパティを変更します。

    - **[VSIX に含める]** プロパティを **[True]** に設定します。

    - **[出力ディレクトリにコピー]** プロパティを **[常にコピーする]** に設定します。

18. **ソリューション エクスプローラー** で、**SimpleMathVSIX** プロジェクトのショートカット メニューの **[ビルド]** を選択します。

19. ビルドが正常に完了したら、プロジェクトのショートカット メニューで **[エクスプローラーでフォルダーを開く]** を選択します。 **\bin\debug\\** に移動し、`SimpleMathVSIX.vsix` を実行してインストールします。

20. **[インストール]** を選択して、インストールを完了します。

21. Visual Studio を再起動します。

## <a name="to-create-a-sample-app-that-uses-the-sdk"></a><a name="createSampleApp"></a> SDK を使用するサンプル アプリを作成するには

1. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。

2. テンプレート カテゴリの一覧で、 **[JavaScript]** の下にある **[Windows ストア]** を選択し、 **[空のアプリケーション]** テンプレートを選択します。

3. **[名前]** ボックスに、`ArithmeticUI` を指定します。 **[OK]** を選択します。

4. **ソリューション エクスプローラー** で、 **[ArithmeticUI]** プロジェクトのショートカット メニューを開いて、 **[追加]**  >  **[参照]** を選択します。

5. **[Windows]** の下で **[拡張機能]** を選択し、 **[単純な数値演算]** が表示されることを確認します。

6. **[単純な数値演算]** チェック ボックスをオンにして、 **[OK]** ボタンをクリックします。

7. **ソリューション エクスプローラー** の **[参照]** に、 **[単純な数値演算]** の参照が表示されていることに注意してください。 これを展開して、**arithmetic.js** を含む **\js\\** フォルダーがあることを確認します。 **arithmetic.js** を開いて、ソース コードがインストールされていることを確認できます。

8. 次のコードを使用して *default.htm* の内容を置き換えます。

   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <meta charset="utf-8" />
       <title>ArithmeticUI</title>

       <!-- WinJS references -->
       <link href="//Microsoft.WinJS.1.0/css/ui-dark.css" rel="stylesheet" />
       <script src="//Microsoft.WinJS.1.0/js/base.js"></script>
       <script src="//Microsoft.WinJS.1.0/js/ui.js"></script>

       <!-- ArithmeticUI references -->
       <link href="/css/default.css" rel="stylesheet" />
       <script src="/js/default.js"></script>
       <script src="/SimpleMath/js/arithmetic.js"></script>
   </head>
   <body>
       <form>
       <div id="calculator" class="ms-grid">
           <input name="firstNumber" id="firstNumber" type="number" step="any">
           <div id="operators">
               <button class="operator" type="button">+</button>
               <button class="operator" type="button">-</button>
               <button class="operator" type="button">*</button>
               <button class="operator" type="button">/</button>
           </div>
           <input id="secondNumber" type="number">
           <button class="calculate" type="button">=</button>
           <input id="result" type="number" name="result" disabled="" readonly="">
       </div>
       </form>
   </body>
   </html>
   ```

9. 次のコードを使用して *\js\default.js* の内容を置き換えます。

    ```csharp
    (function () {
        "use strict";

        var app = WinJS.Application;
        var operation = null;

        function calculateResult() {
            var firstNumber = parseFloat(document.querySelector("#firstNumber").value),
                secondNumber = parseFloat(document.querySelector("#secondNumber").value),
                result = 0;

            if (isNaN(firstNumber) || isNaN(secondNumber)) {
                result = 0;
            }
            else {
                switch (operation) {
                    case "+":
                        result = Arithmetic.add(firstNumber, secondNumber);
                        break;
                    case "-":
                        result = Arithmetic.subtract(firstNumber, secondNumber);
                        break;
                    case "*":
                        result = Arithmetic.multiply(firstNumber, secondNumber);
                        break;
                    case "/":
                        result = Arithmetic.divide(firstNumber, secondNumber);
                        break;
                    default:
                }
            }
            document.querySelector("#result").value = result.toString();
        }

        app.onactivated = function (args) {
            document.querySelector("#calculator").addEventListener("click", function (event) {
                if (event.target.tagName.toLowerCase() === "button") {
                    switch (event.target.className) {
                        case "operator":
                            operation = event.target.innerText;
                            break;
                        case "calculate":
                            calculateResult();
                            break;
                        default:
                            break;
                    }
                }
            });
        };

        app.start();
    })();
    ```

10. *\css\default.css* の内容を次のコードに置き換えます。

    ```xml
    form {
        display: -ms-grid;
        -ms-grid-rows: 1fr auto 1fr;
        -ms-grid-columns: 1fr auto 1fr;
        height: 100%;
        width: 100%;
    }

    button, input[type=number] {
        margin-right: 5px;
        -ms-grid-row-align: center;
    }

    #calculator {
        -ms-grid-column: 2;
        -ms-grid-row: 2;
        display: -ms-grid;
        -ms-grid-rows: 1fr;
        -ms-grid-columns: auto min-content auto auto auto;
    }

    .ms-grid input {
        width: 5em;
    }

    #firstNumber {
        -ms-grid-column: 1;
        -ms-grid-row-align: center;
    }

    #operators {
        -ms-grid-column: 2;
        -ms-grid-row-align: center;
    }

        #operators button.operator {
            margin-bottom: 5px;
            height: 40px;
        }

    #secondNumber {
        -ms-grid-column: 3;
    }

    button.calculate {
        -ms-grid-column: 4;
        -ms-grid-row-align: center;
        height: 40px;
    }

    #result {
        -ms-grid-column: 5;
    }

    ```

11. **F5** キーを押して、アプリをビルドして実行します。

12. アプリの UI で、任意の 2 つの数値を入力し、操作を選択して、 **=** ボタンを選択します。 正しい結果が表示されます。

## <a name="see-also"></a>関連項目
- [ソフトウェア開発キットを作成する](../extensibility/creating-a-software-development-kit.md)
