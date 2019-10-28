---
title: IntelliTrace 機能 |Microsoft Docs
ms.date: 09/19/2018
ms.topic: conceptual
helpviewer_keywords:
- IntelliTrace, debugging with events
- IntelliTrace, recording execution history
- debugging [Visual Studio ALM], recording execution history
- IntelliTrace, turn off
- IntelliTrace, navigating event and call history
- IntelliTrace, saving your session
- IntelliTrace, enabling
- IntelliTrace, start debugging
- IntelliTrace, debugging with events and call information
- IntelliTrace, disabling
- IntelliTrace, turn on
- debugging [Visual Studio ALM], IntelliTrace
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bcdb1b2b6dc4b64d180eb03fc76b26b4ef16e9d0
ms.sourcegitcommit: 257fc60eb01fefafa9185fca28727ded81b8bca9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72911414"
---
# <a name="intellitrace-features-c-visual-basic-c"></a>IntelliTrace の機能C#(、Visual Basic C++、)

IntelliTrace を使用すると、イベントとアプリケーションを呼び出すメソッドとを記録することができます。この機能により、さまざまな実行ポイントでの状態 (呼び出し履歴およびローカル変数の値) を確認することができます。 通常どおりデバッグを開始します。 IntelliTrace は既定でオンになっており、 **[イベント]** タブの下にある 新しい **[診断ツール]** ウィンドウに intellitrace が記録されている情報を確認できます。イベントを選択し、[**履歴デバッグのアクティブ化] をクリックします。** このイベントに記録された呼び出し履歴とローカル変数を表示します。

ステップ バイ ステップの説明については、「[チュートリアル: IntelliTrace の使用](../debugger/walkthrough-using-intellitrace.md)」を参照してください。

IntelliTrace は Visual Studio Enterprise Edition で使用できますが、Visual Studio Professional Edition または Community Edition では使用できません。

IntelliTrace がオンになっていることを確認するには、 **[ツール] > [オプション] > [IntelliTrace]** の順にオプション ページを開きます。 **[IntelliTrace を有効にする]** は既定でオンになります。

> [!NOTE]
> **[IntelliTrace]** オプション ページ上のすべての設定の適用範囲は、個々のプロジェクトまたはソリューションではなく、Visual Studio 全体となります。 これらの設定に加えた変更は、Visual Studio のすべてのインスタンス、すべてのデバッグ セッション、あるいはすべてのプロジェクトまたはソリューションに適用されます。

## <a name="ChooseEvents"></a>IntelliTrace が記録するイベント (C#、Visual Basic) を選択します

特定の IntelliTrace イベントの記録はオンまたはオフにすることができます。

デバッグ中の場合、デバッグを停止します。 [**ツール] > [intellitrace > Intellitrace イベント] > [オプション]** にアクセスします。 IntelliTrace で記録するイベントを選択します。

## <a name="Snapshots"></a>スナップショットの収集C#(、Visual Basic C++、)

これは既定では有効になっていませんが、IntelliTrace はすべてのブレークポイントとデバッガーステップイベントでアプリケーションのスナップショットをキャプチャできます。また、これらのスナップショットは、デバッグの履歴セッションで確認できます。 スナップショットを使用すると、アプリケーションの完全な状態を確認できます。 スナップショットのキャプチャを有効にするには、[**ツール] > [intellitrace > 全般] > [オプション**] にアクセスし、 **[intellitrace スナップショット (マネージとネイティブ)]** を選択します。 詳細については、[IntelliTrace を使用して以前のアプリの状態を検査する](../debugger/view-historical-application-state.md)方法に関するページを参照してください。

スナップショットは Visual Studio Enterprise 2017 バージョン15.5 以降で使用できます。また、Windows 10 の記念日またはそれ以降の更新プログラムが必要です。  .NET Core アプリと ASP.NET Core アプリの場合は、Visual Studio Enterprise 2017 バージョン15.7 が必要です。 Windows を対象とするネイティブアプリの場合は、Visual Studio Enterprise 2017 バージョン 15.9 Preview 2 が必要です。

## <a name="GoingFurther"></a>IntelliTrace イベントと呼び出し情報の収集C#(、Visual Basic)

これは既定では有効になっていませんが、IntelliTrace ではイベントと共にメソッドの呼び出しを記録できます。 メソッド呼び出しの収集を有効にするには、[**ツール] > [intellitrace > 全般] > [オプション**] をクリックし、 **[intellitrace イベントと呼び出し情報 (マネージのみ)]** を選択します。

呼び出し情報は現在、.NET Core と ASP.NET Core アプリでは使用できません。

これにより、呼び出し履歴が表示され、コード内で呼び出しの前後を移動できるようになります。 IntelliTrace は、メソッド名、メソッド エントリ、および終了ポイントなどのデータと、特定のパラメーター値および戻り値を記録します。

> [!TIP]
> このオプションは既定では有効になっていません。かなりのオーバーヘッドが追加されるためです。 IntelliTrace はアプリケーションが行うすべてのメソッド呼び出しを先に取得する必要があるだけでなく、それを画面に表示したりディスクに保存したりする上で大量のデータ セットを処理する必要があります。
>
> パフォーマンスのオーバーヘッドは、IntelliTrace で記録するイベントの一覧を制限することで、さらに収集するモジュール数を最小限に抑えることで、減らすことができます。 詳細については、「[IntelliTrace が呼び出し情報をどの程度記録するかの制御](../debugger/intellitrace-features.md#ControlCallData)」を参照してください。

### <a name="use-the-navigation-gutter"></a>ナビゲーション余白を使用する

コード ウィンドウの左側に表示されるナビゲーション余白を使用することができます。 ナビゲーション余白が表示されていない場合は、 **[ツール] > [オプション] > [IntelliTrace] > [詳細設定]** の順に選択し、 **[デバッグ モードでナビゲーション余白を表示する]** を選択します。

ナビゲーション余白を使用すれば、デバッグ履歴モードでメソッド呼び出しとイベントの中を前後に移動することができます。 デバッグ履歴の詳細については、「[デバッグ履歴](../debugger/historical-debugging.md)」を参照してください。 以下のようなコマンドがあります。

|||
|-|-|
|**デバッガー コンテキストをここに設定**|これが表示される呼び出しタイム フレームにデバッグ コンテキストを設定します。<br /><br /> このアイコンは、現在の呼び出し履歴にのみ表示されます。|
|**呼び出しサイトに戻る**|ポインターとデバッグ コンテキストを現在の関数が呼び出された場所に戻します。<br /><br /> ライブ デバッグ モードの場合は、このコマンドでデバッグ履歴をオンにします。 元の実行中断場所に戻ると、デバッグ履歴はオフになり、ライブ デバッグがオンになります。|
|**前の呼び出しまたは IntelliTrace イベントへ移動**|ポインターとデバッグ コンテキストを前の呼び出しまたはイベントに戻します。<br /><br /> ライブ デバッグ モードの場合は、このコマンドでデバッグ履歴をオンにします。|
|**ステップ イン**|現在選択されている関数にステップインします。<br /><br /> このコマンドは、デバッグ履歴モード中にのみ使用できます。|
|**次の呼び出しまたは IntelliTrace イベントへ移動**|ポインターとデバッグ コンテキストを IntelliTrace データが存在する次の呼び出しまたはイベントまで進めます。<br /><br /> このコマンドは、デバッグ履歴モード中にのみ使用できます。|
|**ライブ モードへ移動**|ライブ デバッグ モードに戻ります。|

### <a name="search-for-a-line-or-method-in-intellitrace"></a>行またはメソッドを IntelliTrace で検索する

メソッドを検索できるのは、メソッド呼び出し情報が有効になっている場合に限られます。 特定の行またはメソッドの IntelliTrace 履歴を検索することができます。 デバッガーの実行が停止したら、関数本文内を右クリックしてコンテキスト メニューを表示し、 **[この行を IntelliTrace で検索]** または **[このメソッドを IntelliTrace で検索]** のいずれかをクリックします。

### <a name="ControlCallData"></a>IntelliTrace が呼び出し情報をどの程度記録するかの制御

既定では、IntelliTrace はソリューションで使用されるすべてのモジュールについて情報を記録します。 関心のあるモジュールに関してのみ、呼び出し情報を記録するように IntelliTrace を設定できます。 **[ツール] > [オプション] > [IntelliTrace] > [モジュール]** の順に選択し、IntelliTrace に含めるモジュールまたは IntelliTrace から除外するモジュールを指定できます。 指定したモジュールから発生したイベントと、関心のあるモジュール内で発生したメソッド呼び出しだけが IntelliTrace で収集されます。

複数のモジュールを追加するには、ワイルドカード文字 * を文字列の先頭または末尾に使用します。 モジュール名には、アセンブリ名ではなくファイル名を使用してください。 ファイル パスは使用できません。

モジュールの数は最小限に抑えるようにしてください。 そうすれば、収集するデータが少なくなるので、パフォーマンスが向上します。 また、処理すべきデータが少なくなるので、UI のノイズが減少します。

## <a name="SaveSession"></a>IntelliTrace データをファイル (C#、Visual Basic、 C++) に保存する

デバッグ中にアプリケーションが中断状態にある場合は、 **[デバッグ] > [IntelliTrace] > [IntelliTrace セッションの保存]** の順に選択して、IntelliTrace によって収集されたデータを保存することができます。 アプリケーションがまだ実行中の場合またはデバッグが停止状態の場合、メニュー項目は無効であるため、IntelliTrace で収集されたデータを保存することはできません。

ファイルに自動的に保存されるように IntelliTrace を構成するには、 **[ツール] > [オプション] > [IntelliTrace] > [詳細設定]** の順に選択し、 **[IntelliTrace 記録をこのディレクトリに保存する]** を選択します。 生成するファイルの設定サイズを構成することもできます。その場合、IntelliTrace は領域が足りなくなると古いデータから順に上書きしていきます。 Visual Studio では、ファイルが自動保存されるときと Visual Studio のホスティング プロセス (vshost.exe) をオンにしたときに、IntelliTrace セッションごとに 2 つのファイルが作成されます。

> [!TIP]
> ファイルが必要なくなった場合は、ディスク領域を節約するためにファイルの保存を自動的にオフにします。 既存のファイルは削除されません。 いつでも必要に応じてコンテキスト メニューからファイルに保存することができます。

IntelliTrace データをファイルに保存する場合は、IntelliTrace が収集対象としたプロセスごとに 1 つの .itrace ファイルが得られます。 .itrace ファイルは Visual Studio で開くことができます。それには、 **[ファイル] > [開く] > [ファイル]** の順に選択し、[ファイルを開く] ダイアログ ボックスから .itrace ファイルを選択します。 詳細については、「[保存された IntelliTrace データの使用](../debugger/using-saved-intellitrace-data.md)」を参照してください。

## <a name="blogs"></a>ブログ

[IntelliTrace in Visual Studio Enterprise 2015 (Visual Studio Enterprise2015 の IntelliTrace)](https://devblogs.microsoft.com/devops/intellitrace-in-visual-studio-ultimate-2015/)

[Visual Studio 2015 での IntelliTrace を使用したライブデバッグのチュートリアル (テキストエディター)](https://devblogs.microsoft.com/devops/walkthrough-of-live-debugging-using-intellitrace-in-visual-studio-2015-text-editor/)

[Visual Studio 2015 (ソーシャルクラブ) での IntelliTrace を使用したライブデバッグのチュートリアル](https://devblogs.microsoft.com/devops/walkthrough-of-live-debugging-using-intellitrace-in-visual-studio-2015-social-club/)

[Visual Studio Enterprise 2015 の IntelliTrace が attach をサポートするようになりました。](https://devblogs.microsoft.com/devops/intellitrace-in-visual-studio-enterprise-2015-now-supports-attach/)

[IntelliTrace スタンドアロンコレクターを使用して windows サービスからデータを収集する](https://devblogs.microsoft.com/devops/collect-data-from-a-windows-service-using-the-intellitrace-standalone-collector/)

[IntelliTrace 収集計画の編集](https://devblogs.microsoft.com/devops/editing-the-intellitrace-collection-plan)

[IntelliTrace を使用したカスタム TraceSource とデバッグ](https://devblogs.microsoft.com/devops/custom-tracesource-and-debugging-using-intellitrace/)

[Active Directory アカウントで実行されている IntelliTrace スタンドアロンコレクターとアプリケーションプール](https://devblogs.microsoft.com/devops/intellitrace-standalone-collector-and-application-pools-running-under-active-directory-accounts/)

## <a name="forums"></a>フォーラム

[Visual Studio Debugger](https://social.msdn.microsoft.com/Forums/en-US/home)

## <a name="videos"></a>ビデオ

[IntelliTrace エクスペリエンス](https://channel9.msdn.com/Series/Visual-Studio-2015-Enterprise-Videos/IntelliTrace-Experience)

[Historical Debugging with IntelliTrace in Microsoft Visual Studio Ultimate 2015](https://channel9.msdn.com/events/Ignite/2015/BRK3716)
