---
title: Visual Studio Tools for Unity を使用する | Microsoft Docs
description: Visual Studio Tools for Unity の統合と生産性の機能を使用する方法について説明します。 また、Unity 開発用の Visual Studio デバッガーも使用します。
ms.custom: ''
ms.date: 07/03/2018
ms.technology: vs-unity-tools
ms.prod: visual-studio-dev16
ms.topic: how-to
ms.assetid: e67ec9a2-a449-413e-8930-9a471bd43a06
author: therealjohn
ms.author: johmil
manager: crdun
ms.workload:
- unity
zone_pivot_groups: platform
ms.openlocfilehash: 9a89f83ecaa4545eb6151c7a92e76a08708c3855
ms.sourcegitcommit: f4b49f1fc50ffcb39c6b87e2716b4dc7085c7fb5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2020
ms.locfileid: "94341287"
---
# <a name="use-visual-studio-tools-for-unity"></a>Visual Studio Tools for Unity を使用する

このセクションでは、Visual Studio Tools for Unity の統合と生産性の機能の使用法、および Unity 開発における Visual Studio デバッガーの使用法について取り上げます。

## <a name="open-unity-scripts-in-visual-studio"></a>Visual Studio で Unity スクリプトを開く

Visual Studio を [Unity の外部エディターとして設定](getting-started-with-visual-studio-tools-for-unity.md#configure-unity-to-use-visual-studio)した後、Unity エディターからスクリプトをダブルクリックすると、自動的に Visual Studio が起動するか Visual Studio に切り替わり、選択したスクリプトが開きます。

または、Unity の **[Assets]\(アセット\) > [Open C# Project]\(C# プロジェクトを開く\)** メニューを選択することで、ソース エディターでスクリプトを開かずに Visual Studio を起動できます。

:::zone pivot="windows"
![Visual Studio で C# プロジェクトを開く](../media/vs/vstu-open-csharp-project.png)
:::zone-end
:::zone pivot="macos"
![Visual Studio for Mac で C# プロジェクトを開く](../media/vsm/vstu-open-csharp-project.png)
:::zone-end

## <a name="unity-documentation-access"></a>Unity のドキュメントへのアクセス

Visual Studio から簡単に Unity スクリプトに関するドキュメントにアクセスできます。 Visual Studio Tools for Unity は、ローカルの API ドキュメントを見つけられない場合、ドキュメントをオンラインで検索することを試みます。

:::zone pivot="windows"
- Visual Studio で、情報を必要とする Unity API を選択するか、その上にカーソルを置き、**Ctrl**+**Alt**+**M** キー、**Ctrl**+**H** キーの順に押します。
- キー バインドの代わりに **[ヘルプ] > [Unity API リファレンス]** メニューを使用することもできます。
![Visual Studio の [Unity API リファレンス] メニュー](../media/vs/help-unity-documentation.png)
:::zone-end
:::zone pivot="macos"
- Visual Studio for Mac で、情報を必要とする Unity API を選択するか、その上にカーソルを置き、**Cmd**+ **'** キーを押します。
- キー バインドの代わりに **[ヘルプ] > [Unity API リファレンス]** メニューを使用することもできます。
![Visual Studio for Mac の [Unity API リファレンス] メニュー](../media/vsm/help-unity-documentation.png)
:::zone-end

## <a name="intellisense-for-unity-api-messages"></a>Unity API メッセージ用の IntelliSense

IntelliSense コード補完により、MonoBehaviour スクリプト内に Unity メッセージを簡単に実装でき、Unity API の学習に役立ちます。 Unity メッセージ用の IntelliSense を使うには:

1. `MonoBehaviour` から派生するクラスの本体内部の新しい行にカーソルを置きます。

2. Unity メッセージの名前 (`OnTriggerEnter` など) の入力を始めます。

3. 「**ontri**」まで入力すると、IntelliSense による候補の一覧が表示されます。

:::zone pivot="windows"

![Visual Studio での IntelliSense の使用](../media/vs/intellisense-example.png)  

:::zone-end

4. 一覧での選択は、次の 3 つの方法で変更できます。

    - **上** および **下** 方向キーを使います。

    - 目的の項目をマウスでクリックします。

    - 目的の項目の名前の入力を続けます。

5. IntelliSense で選んだ Unity メッセージと必要なパラメーターを挿入するには、次のようにします。

    - **Tab** キーを押します。

    - **Enter** キーを押します。

    - 選んだ項目をダブルクリックします。

:::zone pivot="windows"

![Visual Studio で IntelliSense から Unity メッセージを挿入する](../media/vs/vstu-intellisense2.png)

:::zone-end

## <a name="unity-monobehavior-scripting-wizard"></a>Unity MonoBehavior のスクリプト作成ウィザード

MonoBehavior ウィザードを使用して、Unity API のすべてのメソッドの一覧を表示し、空の定義を簡単に実装できます。 この機能は、Unity API で使用できる新機能をまだ学習しているときに、特に **[メソッド コメントの生成]** オプションが有効になっている場合に役に立ちます。

MonoBehavior ウィザードを使用して空の MonoBehavior メソッド定義を作成するには:

1. Visual Studio で、メソッドの挿入位置にカーソルを合わせてから、**Ctrl**+**Shift**+**M** キーを押して MonoBehavior ウィザードを起動します。 Visual Studio for Mac で、**Cmd**+**Shift**+**M** キーを押します。

2. **[スクリプト メソッドの作成]** ウィンドウで、追加する各メソッドの名前の横にあるチェック ボックスをオンにします。

3. **[Framework のバージョン]** ドロップダウンを使用して、目的のバージョンを選択します。

4. 既定では、メソッドは、カーソルの位置に挿入されます。 または、 **[挿入ポイント]** ドロップダウンの値を目的の位置に変更することで、クラス内に既に実装されている任意のメソッドの後ろに挿入することを選択できます。

5. 選択したメソッドについてウィザードがコメントを生成するように指定するには、 **[メソッドのコメントを生成]** チェック ボックスをオンにします。 これらのコメントは、メソッドを呼び出すタイミングやメソッドの全般的な役割について説明するためのものです。

6. **[OK]** ボタンを選択すると、ウィザードが終了し、コードにメソッドが挿入されます。

:::zone pivot="windows"

![Visual Studio の MonoBehavior ウィザードのダイアログ。](../media/vs/vstu-monobehavior-wizard.png)
:::zone-end
:::zone pivot="macos"

![Visual Studio for Mac の MonoBehavior ウィザードのダイアログ。](../media/vsm/vstu-monobehavior-wizard.png)
:::zone-end   

## <a name="unity-project-explorer"></a>Unity プロジェクト エクスプローラー
Unity Project Explorer にはすべての Unity プロジェクト ファイルとディレクトリが、Unity エディターで表示されるのと同じ方法で表示されます。 これは、通常の Visual Studio ソリューション エクスプローラーを使用して Unity スクリプト間を移動するのとは異なります。そこではそれらが Visual Studio によって生成されるプロジェクトとソリューションに編成されます。

:::zone pivot="windows"
- Visual Studio のメイン メニューで、 **[表示] > [Unity プロジェクト エクスプローラー]** を選択します。 キーボード ショートカット: **Alt**+**Shift**+**E**
![[Unity プロジェクト エクスプローラー] ウィンドウを表示する。](../media/vs/unity-project-explorer.png)
:::zone-end
:::zone pivot="macos"
- Visual Studio for Mac では、Unity プロジェクトを開くと、Solution Pad がこのように自動的に動作します。
:::zone-end
## <a name="unity-debugging"></a>Unity のデバッグ

Visual Studio Tools for Unity では、Visual Studio の強力なデバッガーを使用して、Unity プロジェクトのエディター スクリプトとゲーム スクリプトの両方をデバッグできます。

### <a name="debug-in-the-unity-editor"></a>Unity エディターでのデバッグ

#### <a name="start-debugging"></a>[デバッグ開始]
:::zone pivot="windows"

1. **[Unity にアタッチ]** というラベルの付いた **[再生]** ボタンをクリックするか、キーボード ショートカット **F5** を使用して、Visual Studio を Unity に接続します。
![Visual Studio で [再生] をクリックする](../media/vs/vstu-play-button.png)

:::zone-end
:::zone pivot="macos"

1. **[再生]** ボタンをクリックするか、**Command + Return** キーまたは **F5** キーを押して、Visual Studio を Unity に接続します。
![Visual Studio for Mac で [再生] をクリックする](../media/vsm/using-vsmac-tools-unity-image5.png)

:::zone-end

2. Unity に切り替えた後、 **[Play]\(再生\)** ボタンをクリックしてエディターでゲームを実行します。
:::zone pivot="windows"
![Windows 上の Unity で [Play]\(再生\) をクリックする](../media/vs/vstu-unity-play-button.png)
:::zone-end
:::zone pivot="macos"
![macOS 上の Unity で [Play]\(再生\) をクリックする](../media/vsm/using-vsmac-tools-unity-image6.png)
:::zone-end

3. Visual Studio に接続しながら Unity エディターでゲームを実行しているときに、ブレークポイントに達すると、ゲームの実行は一時停止し、ゲームがブレークポイントにヒットしたコード行が Visual Studio に表示されます。

#### <a name="stop-debugging"></a>デバッグの停止

:::zone pivot="windows"

Visual Studio の **[停止]** ボタンをクリックするか、キーボード ショートカット **Shift + F5** を使用します。
![Visual Studio で [停止] をクリックする](../media/vs/vstu-stop-debugger.png)

:::zone-end
:::zone pivot="macos"

Visual Studio for Mac で **[停止]** ボタンをクリックするか、**Shift + Command + Return** キーを押します。
![Visual Studio for Mac で [停止] をクリックする](../media/vsm/using-vsmac-tools-unity-image7.png)

:::zone-end

Visual Studio でのデバッグの詳細については、「[First look at the Visual Studio Debugger](/debugger/debugger-feature-tour.md)」(Visual Studio デバッガーを初めて使用する) を参照してください。

#### <a name="attach-to-unity-and-play"></a>Unity にアタッチして再生

さらに使いやすくするために、 **[Unity にアタッチ]** ボタンを **[Unity にアタッチして再生]** モードに変更できます。

:::zone pivot="windows"

1. **[Unity にアタッチ]** ボタンの横の小さな **下向き矢印** をクリックします。
2. ドロップダウン メニューから **[Unity にアタッチして再生]** を選択します。
   ![Visual Studio のアタッチして再生のオプション](../media/vs/vstu-attach-and-play.png)

[再生] ボタンのラベルが **[Unity にアタッチして再生]** になります。 これで、このボタンをクリックするか、キーボード ショートカット **F5** を使用すると、Visual Studio デバッガーにアタッチされるだけでなく、自動的に Unity エディターに切り替わり、エディターでゲームが実行されます。

:::zone-end
:::zone pivot="macos"
Visual Studio for Mac から直接 **[Unity にアタッチして再生]** 構成を選択すると、デバッグの開始と Unity エディターでの再生を 1 回の手順でを完了できます。

![Visual Studio for Mac で [Unity にアタッチして再生] を選択する](../media/vsm/using-vsmac-tools-unity-image8.png)
:::zone-end

> [!NOTE]
> **[Unity にアタッチして再生]** 構成を使用してデバッグを開始した場合、 **[停止]** ボタンでも Unity エディターを停止できます。

### <a name="debug-unity-player-builds"></a>Unity プレーヤー ビルドのデバッグ

Unity プレーヤーの開発ビルドを Visual Studio でデバッグできます。

#### <a name="enable-script-debugging-in-a-unity-player"></a>Unity プレーヤーでのスクリプトのデバッグを有効にする

1. Unity で、 **[File]\(ファイル\) > [Build Settings]\(ビルド設定\)** を選択して、ビルド設定を開きます。
2. [Build Settings]\(ビルド設定\) ウィンドウで、 **[Development Build]\(開発ビルド\)** と **[Script Debugging]\(スクリプトのデバッグ\)** の各チェック ボックスをオンにします。

   ![デバッグのための Unity のビルド設定を構成します。](../media/vs/vstu-debugging-build-settings.png "vstu_debugging_build_settings")

#### <a name="select-a-unity-instance-to-attach-the-debugger-to"></a>デバッガーをアタッチする Unity インスタンスを選択する

:::zone pivot="windows"

- Visual Studio のメイン メニューで、 **[デバッグ] > [Attach Unity Debugger]\(Unity デバッガーにアタッチ\)** を選択します。

   ![Unity のデバッガーをアタッチします。](../media/vs/vstu-debugging-attach-unity-debugger.png "vstu_debugging_attach_unity_debugger")

   **[Unity のインスタンスの選択]** ダイアログには、接続できる各 Unity インスタンスに関する情報が表示されます。

   ![接続する Unity のインスタンスを選択します。](../media/vs/vstu-attach-debugger.png "vstu_connection_to_unity")

   **プロジェクト**

   Unity のこのインスタンスで実行されている Unity プロジェクトの名前。

   **コンピューター** Unity のこのインスタンスが実行されているコンピューターまたはデバイスの名前。

   Unity のこのインスタンスが Unity エディターの一部として実行されている場合は **Type** **Editor** です。Unity のこのインスタンスがスタンドアロン プレーヤーの場合は **Player** です。

   **ポート** Unity のこのインスタンスが通信に使用している UDP ソケットのポート番号。

> [!IMPORTANT]
> Visual Studio Tools for Unity と Unity インスタンスは UDP ネットワーク ソケット上で通信を行っているため、それを許可するルールがファイアウォールで必要になる場合があります。 その場合は、プロンプトが表示され、VSTU と Unity が通信できるように、接続を承認する必要があります。

:::zone-end
:::zone pivot="macos"

- Visual Studio for Mac の上部のメニューで、 **[実行] > [プロセスにアタッチ]** を選択します。 
- **[プロセスにアタッチ]** ダイアログの下部にある [デバッガー] ドロップダウン メニューで **[Unity デバッガー]** オプションを選択します。
- 一覧から Unity インスタンスを選択し、 **[アタッチ]** ボタンをクリックします。

:::zone-end

### <a name="debug-a-dll-in-your-unity-project"></a>Unity プロジェクトの DLL のデバッグ

多くの Unity 開発者は、コード コンポーネントを外部 DLL として作成し、自分で開発した機能を他のプロジェクトと簡単に共有できるようにしています。 Visual Studio Tools for Unity では、これらの DLL のコードを Unity プロジェクトの他のコードとシームレスにデバッグできます。

> [!NOTE]
> 現時点で、Visual Studio Tools for Unity はマネージド DLL のみをサポートしています。 C++ で記述された DLL など、ネイティブ コード DLL のデバッグはサポートしていません。

ここで説明するシナリオは、ソース コードを持っていることを前提としている点に注意してください。つまり、自分のファースト パーティ コードを開発しているか再利用している場合、またはサード パーティ製のライブラリのソース コードを持っている場合に、作成する Unity プロジェクトを DLL として配置することを計画しているというケースです。 このシナリオは、ソース コードを持っていない DLL のデバッグには適用されません。

#### <a name="to-debug-a-managed-dll-project-used-in-your-unity-project"></a>Unity プロジェクトで使用されるマネージド DLL プロジェクトをデバッグするには

1. Visual Studio Tools for Unity によって生成された Visual Studio のソリューションに、既存の DLL プロジェクトを追加します。 あまり一般的な方法ではありませんが、Unity プロジェクトのコード コンポーネントが含まれた新しいマネージド DLL プロジェクトを開始することもできます。その場合は、Visual Studio のソリューションに新しいマネージド DLL プロジェクトを代わりに追加します。

   ![既存の DLL プロジェクトをソリューションに追加します。](../media/vs/vstu-debugging-dll-add-existing.png "vstu_debugging_dll_add_existing")

   どちらの場合も Visual Studio Tools for Unity によってプロジェクト参照が保持されるため、プロジェクト ファイルとソリューション ファイルを再生成する必要がある場合でも、これらの手順は 1 回実行するだけ済みます。

2. DLL プロジェクトで、適切な Unity フレームワーク プロファイルを参照します。 Visual Studio では、DLL プロジェクトのプロパティで、 **[対象のフレームワーク]** プロパティを、使用している Unity フレームワークのバージョンに設定します。 これは、Unity フル、Micro、または Web 基底クラス ライブラリなど、プロジェクトが対象とする API 互換性と一致する Unity 基底クラス ライブラリです。 この設定により、他のフレームワークまたは互換性レベルに存在するが、使用している Unity フレームワークのバージョンには存在しないフレームワーク メソッドを DLL が呼び出すことを防止できます。

> [!NOTE]
> Unity のレガシ ランタイムを使用している場合にのみ、以下が必要です。 新しい Unity ランタイムを使用している場合は、このような専用の 3.5 プロファイルを使用する必要はありません。 お使いの Unity バージョンと互換性のある .NET 4.x プロファイルを使用してください。

   ![Unity フレームワークに、DLL のターゲット フレームワークを設定します。](../media/vs/vstu-debugging-dll-target-framework.png "vstu_debugging_dll_target_framework")

3. DLL は、Unity プロジェクトのアセット フォルダーにコピーします。 Unity では、アセットとは、Unity のアプリと一緒にパッケージ化され、実行時に読み込めるように配置されるファイルのことです。 DLL は実行時にリンクされるので、DLL はアセットとして配置する必要があります。 アセットとして配置するには、Unity エディターは DLL を Unity プロジェクトの Assets フォルダー内に置く必要があります。 これを実行するには、次の 2 つの方法があります。

   - DLL プロジェクトのビルド設定を変更して、出力 DLL ファイルと PDB ファイルを出力フォルダーから Unity プロジェクトの **Assets** フォルダーにコピーするビルド後タスクを組み込みます。

   - DLL プロジェクトのビルド設定を変更して、出力フォルダーを自分の Unity プロジェクトの **Assets** フォルダーに設定します。 DLL ファイルと PDB ファイルの両方が **Assets** フォルダーに置かれます。

   PDB ファイルには DLL のデバッグのシンボルや、DLL コードからソース コード フォームへのマップが格納されているため、デバッグには PDB ファイルが必要です。 レガシ ランタイムをターゲットにしている場合、Visual Studio Tools for Unity は、DLL と PDB からの情報を使用して DLL.MDB ファイルを作成します。このファイルは、レガシ Unity スクリプト エンジンが使用するデバッグ シンボル形式になっています。 新しいランタイムをターゲットにしていて、Portable-PDB を使用している場合、新しい Unity ランタイムは Portable-PDB をネイティブで使用できるため、Visual Studio Tools for Unity ではシンボル変換が試行されません。

   PDB 生成の詳細については、[ここ](/debugger/how-to-set-debug-and-release-configurations.md)を参照してください。 新しいランタイムをターゲットにしている場合は、Portable-PDB を適切に生成するために、[Debugging Information]\(デバッグ情報\) が [移植可能] に設定されていることを確認します。 レガシ ランタイムをターゲットにしている場合は、[全体] を使用する必要があります。

4. コードをデバッグします。 これで、Unity プロジェクトのソース コードと DLL ソース コードを一緒にしてデバッグできるようになりました。ブレークポイントやコードのステップ実行など、いつも使用しているデバッグ機能をすべて使用できます。

## <a name="keyboard-shortcuts"></a>キーボード ショートカット

キーボード ショートカットを使用すると、Visual Studio Tools for Unity の機能に素早くアクセスできます。 使用できるショートカットの概要を次に示します。

:::zone pivot="windows"

|コマンド|ショートカット|シュートカット コマンド名|
|-------------|--------------|---------------------------|
|MonoBehavior ウィザードを開く|**Ctrl**+**Shift**+**M**|**EditorContextMenus.CodeWindow.ImplementMonoBehaviours**|
|Unity プロジェクト エクスプローラーを開く|**Alt**+**Shift**+**E**|**View.UnityProjectExplorer**|
|Unity のドキュメントにアクセスする|**Ctrl**+**Alt**+**M、Ctrl**+**H**|**Help.UnityAPIReference**|
|Unity のデバッガー (プレーヤーまたはエディター) にアタッチする|**_既定値なし_**|**Debug.AttachUnityDebugger**|

既定値では不便な場合は、ショートカット キーの組み合わせを変更できます。 変更方法については、「[Visual Studio でのキーボード ショートカットの識別とカスタマイズ](/docs/ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md)」を参照してください。

:::zone-end
:::zone pivot="macos"

|コマンド|ショートカット|シュートカット コマンド名|
|-------------|--------------|---------------------------|
|MonoBehavior ウィザードを開く|**Cmd**+**Shift**+**M**|**EditorContextMenus.CodeWindow.ImplementMonoBehaviours**|
|Unity のドキュメントにアクセスする|**Cmd+'**|**Help.UnityAPIReference**|

既定値では不便な場合は、ショートカット キーの組み合わせを変更できます。 変更方法については、「[IDE のカスタマイズ](/mac/customizing-the-ide#key-bingings)」を参照してください。

:::zone-end
