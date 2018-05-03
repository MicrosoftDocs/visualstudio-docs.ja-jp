---
title: Visual Studio IntelliSense
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vc.tools.intellisense
helpviewer_keywords:
- Quick info
- Parameter info
- Complete word
- List members
- IntelliSense [Visual Studio]
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 48aa6cea8deec13bdf5dd43f83528daf5492e3d0
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="using-intellisense-in-visual-studio"></a>Visual Studio での IntelliSense の使用

IntelliSense とは、メンバーの一覧、パラメーター ヒント、クイック ヒント、入力候補など多数の機能を指す総称です。 これらの機能により、使用中のコードに関する情報の確認、入力中のパラメーターの追跡、プロパティおよびメソッドの呼び出しの追加などが、わずかなキーストロークで可能になります。

IntelliSense には、言語によって異なる要素が多数あります。 各言語の IntelliSense の詳細については、「[関連項目](#see-also)」セクションに示されているトピックを参照してください。

## <a name="list-members"></a>リスト メンバー

トリガーの文字 (マネージ コードではピリオド (`.`)、C++ では `::`) を入力すると、型 (または名前空間) の有効なメンバーが一覧表示されます。 文字の入力を続けると、一覧にフィルターが適用され、その文字で始まるか、名前の中の*いずれか*の単語がその文字で始まるメンバーだけが含まれます。 IntelliSense は "キャメル ケース" 照合も実行します。メンバー内の各キャメル ケースの単語の最初の文字を入力するだけで、それに一致するメンバーが表示されます。

項目を選択した後、**Tab** キーを押すか空白を入力することによって、その項目をコードに挿入できます。 項目を選択してピリオドを入力した場合、項目がピリオドの前に表示され、ピリオドによって別のメンバー一覧が表示されます。 項目を選択した場合、挿入する前に、項目のクイック ヒントが表示されます。

メンバーの一覧で、左側にあるアイコンは、名前空間、クラス、関数、変数など、メンバーの種類を表します。 アイコンの一覧については、「[[クラス ビュー] ウィンドウとオブジェクト ブラウザーのアイコン](../ide/class-view-and-object-browser-icons.md)」を参照してください。 一覧が長い場合は、**PageUp** キーまたは **PageDown** キーを使用して、一覧内を上下に移動できます。

![Visual Studio のメンバー一覧](../ide/media/vs2015_intellisense.png "vs2015_Intellisense")

**メンバーの一覧**機能を起動するには、**CTRL** + **J** キーを押すか、**[編集]** > **[IntelliSense]** > **[メンバーの一覧]** の順に選択するか、エディターのツール バーで **[メンバーの一覧]** を選択します。 空白行または認識可能なスコープの外で呼び出された場合、メンバー一覧にはグローバル名前空間にあるシンボルが表示されます。

既定でメンバーの一覧を無効にする (明確に指定しなければ表示されないようにする) には、**[ツール]** > **[オプション]** > **[すべての言語]** の順にクリックし、**[自動メンバー表示]** をオフにします。 特定の言語に対してのみメンバーの一覧を無効にするには、その言語の **[全般]** 設定で指定します。

入力したテキストのみがコードに挿入される提案モードに変更することもできます。 たとえば、一覧にない識別子を入力して **Tab** キーを押すと、完了モードでは、入力した識別子がエントリに置き換わります。 完了モードと提案モードを切り替えるには、**Ctrl** + **Alt** + **Space** キーを押すか、**[編集]** > **[IntelliSense]** > **[完了モードの切り替え]** の順に選択します。

## <a name="parameter-info"></a>パラメーター ヒント

パラメーター ヒントでは、メソッド、属性、ジェネリック型パラメーター (C#)、またはテンプレート (C++) で必要とされるパラメーターの数、名前、およびデータ型について情報を確認できます。

太字のパラメーターは、入力した関数で次に必要なパラメーターを表しています。 オーバーロードされた関数の場合、↑キーと↓キーを使用して、オーバーロードごとに異なるパラメーター情報を表示できます。

![パラメーター ヒント](../ide/media/vs2015_param_info.png "VS2015_param_Info")

関数やパラメーターに XML ドキュメント コメントによる注釈を付けると、そのコメントがパラメーター ヒントとして表示されます。 詳細については、「[XML コード コメントの追加](../ide/supplying-xml-code-comments.md)」を参照してください。

パラメーター ヒントを手動で起動するには、**[編集]** > **[IntelliSense]** > **[パラメーター ヒント]** の順にクリックするか、**Ctrl** + **Shift** + **Space** キーを押すか、エディターのツール バーで **[パラメーター ヒント]** ボタンを選択します。

## <a name="quick-info"></a>クイック ヒント

クイック ヒントでは、コード内の識別子の宣言全体が表示されます。

![Visual Studio のクイック ヒント](../ide/media/vs2015_quick_info.png "VS2015_Quick_info")

**[メンバーの一覧]** ボックスからメンバーを選択した場合も、クイック ヒントが表示されます。

![C&#35; コード ファイルのパラメーター情報](../ide/media/vs2015_paraminfo.png "VS2015_ParamInfo")

クイック ヒントを手動で起動するには、**[編集]** > **[IntelliSense]** > **[クイック ヒント]** の順に選択するか、**Ctrl** + **I** キーを押すか、エディターのツール バーで **[クイック ヒント]** を選択します。

関数がオーバーロードされている場合、IntelliSense では一部のオーバーロード形式の情報が表示されないことがあります。

C++ コードのクイック ヒントをオフにするには、**[ツール]** > **[オプション]** > **[テキスト エディター]** > **[C/C++]** > **[詳細設定]** の順に移動し、**[自動クイック ヒント]** を `false` に設定します。

## <a name="complete-word"></a>入力候補

入力候補では、特定できる部分まで変数名、コマンド名、または関数名を入力すると、残りの部分が補完されます。 入力候補を起動するには、**[編集]** > **[IntelliSense]** > **[入力候補]** の順に選択するか、**Ctrl** + **Space** キーを押すか、エディターのツール バーで **[入力候補]** を選択します。

## <a name="intellisense-options"></a>IntelliSense オプション

IntelliSense オプションは、既定でオンになっています。 これらを無効にするには、**[ツール]** > **[オプション]** > **[テキスト エディター]** の順に選択し、**[パラメーター ヒント]** をオフにするか、メンバーの一覧機能が不要であれば **[自動メンバー表示]** をオフにします。

## <a name="troubleshooting-intellisense"></a>IntelliSense のトラブルシューティング

IntelliSense オプションは、状況によっては意図どおりに機能しません。

**カーソルがコード エラーより下にある。** 不完全な関数または他のエラーが、コードの中でカーソルより上の位置に存在する場合は、IntelliSense でコード要素を解析できず、IntelliSense を使用できない可能性があります。 この問題は、該当するコードをコメント アウトすることで解決できます。

**カーソルがコード コメント内にある。** カーソルがソース ファイルのコメント内にある場合は、IntelliSense を使用できません。

**カーソルがリテラル文字列内にある。** 次の例のように、リテラル文字列を囲む二重引用符内にカーソルがある場合は、IntelliSense を使用できません。

```cpp
MessageBox( hWnd, "String literal|")
```

**自動オプションがオフになっている。** 既定では、IntelliSense は自動的に動作しますが、無効にすることもできます。 入力候補がオフになっている場合でも、IntelliSense 機能は起動できます。

## <a name="see-also"></a>関連項目

- [Visual Basic の IntelliSense](../ide/visual-basic-specific-intellisense.md)
- [C# IntelliSense](../ide/visual-csharp-intellisense.md)
- [JavaScript IntelliSense](../ide/javascript-intellisense.md)
- [コードの作成とリファクタリング (C++)](/cpp/ide/writing-and-refactoring-code-cpp)
- [XML コード コメントの追加](../ide/supplying-xml-code-comments.md)