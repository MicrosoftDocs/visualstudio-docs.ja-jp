---
title: JavaScript コンソール コマンド |Microsoft Docs
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- JavaScript Console commands [Windows Store apps]
- JavaScript debugging, console [Windows Store apps]
- debugging JavaScript, console [Windows Store apps]
ms.assetid: 359e2b24-6bb7-48e7-8b55-b570df0cb774
caps.latest.revision: 50
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e0bc4597c5be26e25f79edc0784bb1fddd9baa76
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2018
ms.locfileid: "47546311"
---
# <a name="javascript-console-commands"></a>JavaScript Console commands
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックの最新バージョンをご覧[JavaScript Console commands](https://docs.microsoft.com/visualstudio/debugger/javascript-console-commands)します。  
  
Windows および Windows Phone に適用されます] (../Image/windows_and_phone_content.png"windows_and_phone_content")  
  
 Visual Studio では、JavaScript コンソール ウィンドウでコマンドを使用して、メッセージを送信したり他のタスクを実行したりすることができます。 そのウィンドウを使用する方法を示す例については、次を参照してください。[クイック スタート: JavaScript のデバッグ](../debugger/quickstart-debug-javascript-using-the-console.md)します。 このトピックの情報は、Windows ストア アプリ、Windows Phone ストア アプリ、および Visual Studio Tools for Apache Cordova を使用して作成されたアプリに適用されます。 Cordova アプリでサポートされているコンソール コマンドについては、次を参照してください。[アプリのデバッグ](http://msdn.microsoft.com/library/c2a4a1d4-a4e8-47ec-811f-ad207c54f4d1)します。 Internet Explorer F12 ツールのコンソールの使用については、 [このトピック](http://msdn.microsoft.com/library/ie/dn255006.aspx)を参照してください。  
  
 JavaScript コンソール ウィンドウが閉じられた場合開けることを選択して、Visual Studio でデバッグ中**デバッグ** > **Windows** > **JavaScriptコンソール**します。  
  
> [!NOTE]
>  デバッグ セッション中にウィンドウが使用できない場合、プロジェクトのデバッグのプロパティで、デバッガーの種類が **Script** であることを確認してください。  
  
## <a name="console-object-commands"></a>コンソール オブジェクト コマンド  
 次の表に、JavaScript コンソール ウィンドウで使用する、またはコードからコンソールにメッセージを送信するために使用する、 `console` オブジェクトのコマンドの構文を示します。 このオブジェクトには多数の形式があるので、必要に応じて情報メッセージとエラー メッセージを区別できます。  
  
 console という名前のローカル オブジェクトとの混同を避ける必要がある場合は、長いコマンド形式である `window.console.[command]` を使用できます。  
  
> [!TIP]
>  古いバージョンの Visual Studio は、コマンドの完全なセットをサポートしていません。 サポートされているコマンドを簡単に確認するには、コンソール オブジェクトで IntelliSense を使用してください。  
  
|コマンド|説明|例|  
|-------------|-----------------|-------------|  
|`assert(expression, message)`|`expression` が **false**と評価された場合にメッセージを送信します。|`console.assert((x == 1), "assert message: x != 1");`|  
|`clear()`|コンソール ウィンドウからメッセージ (スクリプト エラー メッセージなど) をクリアし、コンソール ウィンドウに表示されているスクリプトもクリアします。 コンソールの入力プロンプトに入力したスクリプトはクリアされません。|`console.clear();`|  
|`count(title)`|カウント コマンドが呼び出された回数をコンソール ウィンドウに送信します。 `title`オプションにより、カウントの呼び出しはそれぞれ一意に識別されます。<br /><br /> コンソール ウィンドウの既存のエントリは `title` パラメーター (存在する場合) により識別され、カウント コマンドによって更新されます。 新しいエントリは作成されません。|`console.count();`<br /><br /> `console.count("inner loop");`|  
|`debug(message)`|`message` をコンソール ウィンドウに送信します。<br /><br /> このコマンドは console.log と同じものです。<br /><br /> このコマンドを使用して渡されたオブジェクトは、文字列値に変換されます。|`console.debug("logging message");`|  
|`dir(object)`|指定されたオブジェクトをコンソール ウィンドウに送信し、それをオブジェクトのビジュアライザーに表示します。 ビジュアライザーを使用して、コンソール ウィンドウのプロパティを検査できます。|`console.dir(obj);`|  
|`dirxml(object)`|指定された XML ノード `object` をコンソール ウィンドウに送信し、それを XML ノード ツリーとして表示します。|`console.dirxaml(xmlNode);`|  
|`error(message)`|`message` をコンソール ウィンドウに送信します。 メッセージ テキストは赤で表示され、その前にエラー シンボルが付きます。<br /><br /> このコマンドを使用して渡されたオブジェクトは、文字列値に変換されます。|`console.error("error message");`|  
|`group(title)`|コンソール ウィンドウに送信されたメッセージのグループ化を開始し、オプションの `title` をグループ ラベルとして送信します。 グループは入れ子にでき、コンソール ウィンドウのツリー ビューに表示されます。<br /><br /> グループ* のコマンドを使うと、コンポーネント モデルを使用する場合などのシナリオで、コンソール ウィンドウの出力を容易に表示することができます。|`console.group("Level 2 Header");` <br /> `console.log("Level 2");` <br /> `console.group();` <br /> `console.log("Level 3");` <br /> `console.warn("More of level 3");` <br /> `console.groupEnd();` <br /> `console.log("Back to level 2");` <br /> `console.groupEnd();` <br /> `console.debug("Back to the outer level");`|  
|`groupCollapsed(title)`|コンソール ウィンドウに送信されたメッセージのグループ化を開始し、オプションの `title` をグループ ラベルとして送信します。 `groupCollapsed` を使用して送信されたグループは、既定では折りたたまれたビューで表示されます。 グループは入れ子にでき、コンソール ウィンドウのツリー ビューに表示されます。|使用法は `group` コマンドと同じです。<br /><br /> `group` のコマンドの例を参照してください。|  
|`groupEnd()`|現在のグループを終了します。<br /><br /> 要件:<br /><br /> Visual Studio 2013|`group` のコマンドの例を参照してください。|  
|`info(message)`|`message` をコンソール ウィンドウに送信します。 メッセージの前に情報シンボルが付きます。|`console.info("info message");`<br /><br /> 他の例については、このトピックで後述する「 [Formatting console.log output](#ConsoleLog) 」を参照してください。|  
|`log(message)`|`message` をコンソール ウィンドウに送信します。<br /><br /> オブジェクトを渡すと、このコマンドによりオブジェクトがコンソール ウィンドウに送信され、オブジェクトのビジュアライザーに表示されます。 ビジュアライザーを使用して、コンソール ウィンドウのプロパティを検査できます。|`console.log("logging message");`|  
|`msIsIndependentlyComposed(element)`|Web アプリで使用されます。 JavaScript を使用したストア アプリではサポートされていません。|サポートされていません。|  
|`profile(reportName)`|Web アプリで使用されます。 JavaScript を使用したストア アプリではサポートされていません。|サポートされていません。|  
|`profileEnd()`|Web アプリで使用されます。 JavaScript を使用したストア アプリではサポートされていません。|サポートされていません。|  
|`select(element)`|指定された HTML を選択します。`element`で、 [DOM Explorer](../debugger/quickstart-debug-html-and-css.md)します。|console.select (要素);|  
|`time (name)`|`name` オプション パラメーターによって識別されるタイマーを開始します。 `console.timeEnd`と共に使用すると、 `time` から `timeEnd`までの経過時間を計算し、 `name` 文字列をプレフィックスとして使用して、結果 (ミリ秒単位) をコンソールに送信します。 アプリ コードのインストルメンテーションを有効にして、パフォーマンスを測定するために使用します。|`console.time("app start");  app.start();  console.timeEnd("app start");`|  
|`timeEnd(name)`|`name` オプション パラメーターによって識別されるタイマーを停止します。 `time` コンソール コマンドを参照してください。|`console.time("app start"); app.start(); console.timeEnd("app start");`|  
|`trace()`|スタック トレースをコンソール ウィンドウに送信します。 このトレースには、完全なコール スタックと、ファイル名、行番号、列番号などの情報が含まれます。|`console.trace();`|  
|`warn(message)`|`message` をコンソール ウィンドウに送信します。メッセージの前に警告シンボルが付きます。<br /><br /> このコマンドを使用して渡されたオブジェクトは、文字列値に変換されます。|`console.warn("warning message");`|  
  
## <a name="miscellaneous-commands"></a>その他のコマンド  
 JavaScript コンソール ウィンドウでは、以下のコマンドも使用できます (コードからは使用できません)。  
  
|コマンド|説明|例|  
|-------------|-----------------|-------------|  
|`$0`, `$1`, `$2`, `$3`, `$4`|指定された要素をコンソール ウィンドウに返します。 `$0` は DOM Explorer で現在選択されている要素を返し、`$1` は DOM Explorer で直前に選択されていた要素を返します。同様に、最大で 4 つ前に選択されていた要素を返します。|$3|  
|`$(id)`|要素を ID で返します。 これは `document.getElementById(id)`のショートカット コマンドであり、 `id` は要素の ID を表す文字列です。|`$("contenthost")`|  
|`$$(selector)`|CSS セレクター構文を使用して、指定されたセレクターと一致する要素の配列を返します。 これは `document.querySelectorAll()`のショートカット コマンドです。|`$$(".itemlist")`|  
|`cd()`<br /><br /> `cd(window)`|式の評価のコンテキストを、既定であるページのトップレベル ウィンドウから指定したフレームのウィンドウに変更できます。 `cd()` をパラメーターの指定なしで呼び出すと、コンテキストがトップレベル ウィンドウに戻ります。|`cd();`<br /><br /> `cd(myframe);`|  
|`select(element)`|指定された要素を選択します。 [DOM Explorer](../debugger/quickstart-debug-html-and-css.md)します。|`select(document.getElementById("element"));`<br /><br /> `select($("element"));`<br /><br /> `select($1);`|  
|`dir(object)`|指定されたオブジェクトのビジュアライザーを返します。 ビジュアライザーを使用して、コンソール ウィンドウのプロパティを検査できます。|`dir(obj);`|  
  
## <a name="checking-whether-a-console-command-exists"></a>コンソール コマンドが存在するかどうかを確認  
 特定のコマンドを使用する前に、それが存在するかどうかを確認できます。 この例では `console.log` コマンドの存在を確認します。 `console.log` が存在する場合には、コードはそれを呼び出します。  
  
```javascript  
if (console && console.log) {  
    console.log("msg");  
}  
  
```  
  
## <a name="examining-objects-in-the-javascript-console-window"></a>JavaScript コンソール ウィンドウを使ったオブジェクトの検査  
 JavaScript コンソール ウィンドウを使用すると、スコープ内のオブジェクトと対話できます。 コンソール ウィンドウでスコープ外のオブジェクトを検査するには、コードから `console.log` 、 `console.dir`、または他のコマンドを使用します。 または、コードでブレークポイントを設定 (**[ブレークポイント]** > **Insert [ブレークポイント]** の順にクリック) すると、コンソール ウィンドウからスコープ内のオブジェクトと対話できます。  
  
##  <a name="ConsoleLog"></a> Console.log 出力の書式設定  
 複数の引数を `console.log`に渡すと、コンソールはその引数を配列として処理し、出力を連結します。  
  
```javascript  
var user = new Object();  
user.first = "Fred";  
user.last = "Smith";  
  
console.log(user.first, user.last);  
// Output:  
// Fred Smith  
  
```  
  
 `console.log` は出力をフォーマットする代替パターン "printf" もサポートします。 代替パターンを最初の引数に使用すると、他の引数は、使用された順番で指定されたパターンを置き換えるために使用されます。  
  
 次の代替パターンがサポートされています。  
  
-   %s - 文字列  
     %i - 整数  
     %d - 整数  
     %f - 浮動小数  
     %o - オブジェクト  
     %b - バイナリ  
     %x - 16 進数  
     %e - 指数  
  
 ここでは、 `console.log`で代替パターンを使った例をいくつか示します。  
  
```javascript  
var user = new Object();  
user.first = "Fred";  
user.last = "Smith";  
user.age = 10.01;  
console.log("Hi, %s %s!", user.first, user.last);  
console.log("%s is %i years old!", user.first, user.age);  
console.log("%s is %f years old!", user.first, user.age);  
  
// Output:  
// Hi, Fred Smith!  
// Fred is 10 years old!  
// Fred is 10.01 years old!  
```  
  
## <a name="see-also"></a>関連項目  
 [クイック スタート: JavaScript をデバッグします。](../debugger/quickstart-debug-javascript-using-the-console.md)   
 [クイック スタート: HTML および CSS のデバッグ](../debugger/quickstart-debug-html-and-css.md)



