---
title: Visual Studio の通知と進行状況 | Microsoft Docs
description: ソフトウェア開発タスクに関して Visual Studio で何が起こっているかをユーザーに通知するいくつかの方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: f0ef65e9-0f1f-45f4-9f25-6e2398691168
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a6b273c1ee2ee83c713500d972ecab27a67b3145
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105068545"
---
# <a name="notifications-and-progress-for-visual-studio"></a>Visual Studio の通知と進行状況
## <a name="notification-systems"></a><a name="BKMK_NotificationSystems"></a> 通知システム

### <a name="overview"></a>概要
 Visual Studio でのソフトウェア開発タスクに関して何が起こっているかをユーザーに通知するには、いくつかの方法があります。

 任意の種類の通知を実装する場合:

- **通知の数は、効果的な最小限に抑えるようにしてください。** 通知メッセージは、Visual Studio の大半のユーザー、または特定の機能または機能分野のユーザーに適用する必要があります。 通知を過剰に使用すると、ユーザーが混乱したり、システムの使いやすさが損なわれたりする可能性があります。

- ユーザーが適切に状況を把握し、より複雑な選択を行って、さらなるアクションの実行ができるように、**明確でアクション可能なメッセージが表示されていることを確認してください。**

- **同期メッセージと非同期メッセージを適切に表示してください。** 同期通知は、Web サービスがクラッシュした場合やコードの例外がスローされた場合など、早急に対処する必要があることを示します。 モーダル ダイアログ ボックスなどの入力を必要とする方法で、ユーザーに対しこれらの状況をすぐに通知する必要があります。 非同期通知は、ビルド操作が完了したときや Web サイトの配置が終了したときなど、ユーザーが認識しておく必要があるが、すぐに操作する必要がないことを示します。 これらのメッセージは、よりアンビエントで、ユーザーのタスク フローを中断しないようにする必要があります。

- モーダル ダイアログは、メッセージを確認したり、ダイアログに表示された決定を行う前に、**ユーザーがそれ以上のアクションを実行できないようにするために必要な場合にのみ使用してください。**

- **有効でなくなったアンビエントな通知は削除してください。** 通知された問題に対処するアクションが既に実行されている場合は、ユーザーに通知を閉じるように要求しないでください。

- **通知によって、誤った相関関係が発生する可能性があることに注意してください。** ユーザーは、実際には因果関係がないのに、1 つまたは複数のアクションによって通知がトリガーされたと思い込んでしまうことがあります。 通知メッセージでは、コンテキスト、トリガー、通知元を明確にしてください。

### <a name="choosing-the-right-method"></a>適切な方法の選択
 この表を使用すると、メッセージをユーザーに通知する適切な方法を選択するのに役立ちます。

|メソッド|vmmblue_2|使用しない|
|------------|---------|----------------|
|[モーダル エラー メッセージ ダイアログ](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ModalErrorMessageDialogs)|続行する前にユーザーの応答が必要な場合に使用します。|ユーザーをブロックしてフローを中断する必要がない場合は使用しないでください。 メッセージを別の邪魔にならない方法で表示できる場合は、モーダル ダイアログの使用を避けてください。|
|[IDE ステータス バー](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_IDEStatusBar)|処理の状態に関するアンビエントなテキスト情報がある場合に使用します。|単独で使用しないでください。 別のフィードバック メカニズムと組み合わせて使用するのが最適です。|
|[埋め込まれた情報バー](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_EmbeddedInfobar)|ツール ウィンドウまたはドキュメント ウィンドウで、進行状況、エラー状態、結果、またはアクション可能な情報の通知に使用します。|情報が情報バーが配置されている場所に関連していない場合は使用しないでください。<br /><br /> ドキュメント ウィンドウとツール ウィンドウの外部では使用しないでください。|
|[マウス カーソルの変更](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_MouseCursorChanges)|処理が進行中であることを通知するために使用できます。 また、ドラッグとドロップの進行中や、マウス カーソルが特定のモード (描画モードなど) になったときなど、マウスの状態変化を通知するためにも使用されます。|短時間の進行状況の変更や、カーソルの揺れが発生する可能性がある場合 (たとえば、処理全体ではなく、実行時間の長い処理の一部に関連付けられている場合など) には使用しないでください。|
|[進行状況インジケーター](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_NotSysProgressIndicators)|進行状況を報告する必要がある場合に使用します (確定的または不確定のいずれか)。 さまざまな進行状況インジケーターの種類と、それぞれに特定の使用法があります。 「[進行状況インジケーター](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ProgressIndicators)」を参照してください。||
|[Visual Studio の通知ウィンドウ](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_VSNotificationsToolWindow)|[通知] ウィンドウは、一般には拡張可能ではありません。 ただし、ライセンスに関する重大な問題や、Visual Studio またはパッケージの更新に関する情報通知など、Visual Studio に関するさまざまなメッセージを伝達するために使用されます。|他の種類の通知には使用しないでください。|
|[エラー一覧](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ErrorList)|発生している問題が現在ユーザーが開いているソリューションに直接関連している場合 (エラー、警告、情報)、コードに対するアクションの実行が必要になる場合があります。<br /><br /> これには、たとえば次のものが含まれます。<br /><br /> - コンパイラ メッセージ (エラー、警告、情報)<br /><br /> - コードに関するコード アナライザーと診断のメッセージ<br /><br /> - ビルド メッセージ<br /><br /> プロジェクト ファイルまたはソリューション ファイルに関連する問題には適切な場合がありますが、最初にソリューション エクスプローラーの通知を検討してください。|ユーザーが開いているソリューション コードとの関係がない項目には使用しないでください。|
|エディターの通知: 電球|開いているファイルに存在する問題を解決できる修正がある場合に使用します。<br /><br /> リファクタリングなど、ユーザーのコードに対して必要に応じて実行されるクイック アクションをホストするためにも電球を使用する必要がありますが、その場合、"通知スタイル" は表示されないことに注意してください。|開いているファイルとの関係がない項目には使用しないでください。|
|エディターの通知: 波線|開いているコードの特定の範囲に関する問題についてユーザーに警告 (たとえば、エラーを示す赤い波線) するために使用します。|開いているコードの特定の範囲に関連しない項目には使用しないでください。|
|[埋め込まれたステータス バー](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_EmbeddedStatusBars)|特定のツール ウィンドウ、ドキュメント ウィンドウ、またはダイアログ ウィンドウのコンテキスト内のコンテンツまたはプロセスに関連する状態を表示するために使用します。|特定のウィンドウ内のコンテンツとの関係がない一般的な製品通知、プロセス、または項目には使用しないでください。|
|[Windows トレイの通知](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_WindowsTray)|アウト プロセス プロセスやコンパニオン アプリケーションの通知を表示するために使用します。|IDE に関連する通知には使用しないでください。|
|[通知バブル](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_NotificationBubbles)|IDE の **外部** のリモート プロセスや変化を通知するのに使用します。|IDE **内部** のプロセスをユーザーに通知するための手段として使用しないでください。|

### <a name="notification-methods"></a>通知の方法

#### <a name="modal-error-message-dialogs"></a><a name="BKMK_ModalErrorMessageDialogs"></a> モーダル エラー メッセージ ダイアログ
 モーダル エラー メッセージ ダイアログは、ユーザーの確認または操作を必要とするエラー メッセージを表示するのに使用します。

 ![モーダル エラー メッセージ](../../extensibility/ux-guidelines/media/0901-01_modalerrormessage.png "0901-01_ModalErrorMessage")

 **データベースへの接続文字列が無効であることをユーザーに警告するモーダル エラー メッセージ ダイアログ**

#### <a name="ide-status-bar"></a><a name="BKMK_IDEStatusBar"></a> IDE ステータス バー
 ユーザーがステータス バーのテキストに気付く可能性は、総合的なコンピューター エクスペリエンスと、Windows プラットフォームに関する特定のエクスペリエンスに関連しています。 Visual Studio の顧客基盤はどちらの分野にも精通している傾向がありますが、知識豊富な Windows ユーザーでさえステータス バーの変更を見逃してしまう可能性があります。 そのため、ステータス バーは、情報提供の目的で、または他の場所に表示される情報の冗長な手がかりとして使用するのが最適です。 ユーザーがすぐに解決する必要がある重要な情報は、ダイアログまたは [通知] ツール ウィンドウに表示されます。

 Visual Studio のステータス バーは、複数の種類の情報を表示できるように設計されています。 フィードバック、デザイナー、進行状況バー、アニメーション、およびクライアントの領域に分割されます。

 フィードバック領域とデザイナー領域は常に表示されます。 進行状況バーとアニメーション領域は常に動的で、ユーザー コンテキストに基づいています。 デザイナー領域の静的な幅は、テキスト メッセージに付随するリソースから取得される文字列の長さによって決まります。 これにより、コードを変更しなくても、幅のサイズをローカライズできます。 英語の場合、この文字列の幅は約 220 ピクセルです。 デザイナー領域は正常に動作し、残りの領域はフィードバック領域に取り込まれます。

 また、ステータス バーは色分けされており、IDE がデバッグ モードになっている場合など、さまざまな IDE の状態の変化を伝えることで、視覚的な注目性と機能的な価値を追加します。

 ![IDE ステータス バーの色の変更](../../extensibility/ux-guidelines/media/0901-02_idestatusbar.png "0901-02_IDEStatusBar")

 **IDE ステータス バーの色**

#### <a name="embedded-infobar"></a><a name="BKMK_EmbeddedInfobar"></a> 埋め込まれた情報バー
 ドキュメント ウィンドウまたはツール ウィンドウの上部にある情報バーを使用して、状態や条件をユーザーに通知することができます。 また、コマンドを提供することで、ユーザーが簡単にアクションを実行できるようにすることもできます。 情報バーは標準のシェル コントロールです。 独自に作成することは、IDE 内の他のものと矛盾した動作や表示となるので、避けてください。 実装の詳細と使用方法のガイダンスについては、「[情報バー](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars)」を参照してください。

 ![埋め込まれた情報バー](../../extensibility/ux-guidelines/media/0901-03_embeddedinfobar.png "0901-03_EmbeddedInfobar")

 **IDE がデバッグ履歴モードであり、エディターが標準デバッグ モードの場合と同じように応答しないことをユーザーに警告する、ドキュメント ウィンドウに埋め込まれた情報バー。**

#### <a name="mouse-cursor-changes"></a><a name="BKMK_MouseCursorChanges"></a> マウス カーソルの変更
 マウス カーソルを変更する場合は、VSColor サービスに関連付けられていて、既にカーソルに結び付けられている色を使用します。 カーソルの変更は、進行中の操作を示すために使用できます。また、ドラッグ、ドロップ、またはオブジェクトの選択に使用できるターゲットの上にユーザーがカーソルを置いたときのヒット ゾーンも示します。

 ビジーと待機のマウス カーソルは、使用可能なすべての CPU 時間を操作のために予約する必要がある場合にのみ使用して、ユーザーがそれ以上入力できないようにします。 ほとんどの場合、マルチスレッドを使用して適切に作成されたアプリケーションで、ユーザーが他の操作を実行できない時間はめったに発生しません。

 カーソルの変更は、他の場所に表示される情報の冗長な手がかりとして有効であることに注意してください。 特にユーザーが対処する必要がある重要な情報を伝達しようとする場合は、ユーザーとコミュニケーションを取る唯一の方法としてカーソルの変更に依存しないようにしてください。

#### <a name="progress-indicators"></a><a name="BKMK_NotSysProgressIndicators"></a> 進行状況インジケーター
 進行状況インジケーターは、完了までに数秒以上かかる処理中にユーザー フィードバックを表示するために重要です。 進行状況インジケーターは、インプレース (進行中のアクションの開始点の近くに)、埋め込みステータス バー、モーダル ダイアログ ボックス、または Visual Studio ステータス バーに表示できます。 使用と実装については、「[進行状況インジケーター](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ProgressIndicators)」のガイダンスに従ってください。

#### <a name="visual-studio-notifications-window"></a><a name="BKMK_VSNotificationsToolWindow"></a> Visual Studio の通知ウィンドウ
 Visual Studio の [通知] ウィンドウは、ライセンス、環境 (Visual Studio)、拡張機能、および更新プログラムについて開発者に通知するために使用します。 ユーザーは、個々の通知を無視したり、特定の種類の通知を無視したりすることができます。 無視される通知の一覧は、 **[ツール] > [オプション]** ページで管理されます。

 [通知] ウィンドウは現在拡張可能ではありません。

 ![Visual Studio の通知ウィンドウ](../../extensibility/ux-guidelines/media/0901-06_vsnotificationswindow.png "0901-06_VSNotificationsWindow")

 **Visual Studio の通知ツール ウィンドウ**

#### <a name="error-list"></a><a name="BKMK_ErrorList"></a> エラー一覧
 エラー一覧内の通知は、コンパイル時またはビルド処理中に発生したエラーと警告を示し、ユーザーがコード内でその特定のコード エラーに移動できるようにします。

 ![エラー一覧](../../extensibility/ux-guidelines/media/0901-08_errorlist.png "0901-08_ErrorList")

 **Visual Studio のエラー一覧**

#### <a name="embedded-status-bars"></a><a name="BKMK_EmbeddedStatusBars"></a> 埋め込まれたステータス バー
 IDE ステータス バーは、クライアント領域のコンテキストがアクティブなドキュメント ウィンドウに設定され、ユーザーのコンテキストやシステムの応答に応じて情報が更新される動的なものであるため、情報を継続的に表示し続けたり、長期間の非同期処理のステータスを表示したりすることは困難です。 たとえば、IDE ステータス バーは、複数実行に対するテストの実行結果の通知や、すぐにアクション可能な項目の選択には適していません。 このような状態情報は、ユーザーが選択を行ったり処理を開始したりするドキュメントまたはツール ウィンドウのコンテキストで保持することが重要です。

 ![埋め込まれたステータス バー](../../extensibility/ux-guidelines/media/0901-09_embeddedstatusbar.png "0901-09_EmbeddedStatusBar")

 **Visual Studio の埋め込まれたステータス バー**

#### <a name="windows-tray-notifications"></a><a name="BKMK_WindowsTray"></a> Windows トレイの通知
 Windows の通知領域は、Windows タスク バーのシステム クロックの横にあります。 多くのユーティリティおよびソフトウェア コンポーネントにはこの領域のアイコンが用意されているため、ユーザーは画面の解像度の変更やソフトウェア更新プログラムの取得など、システム全体のタスクのコンテキスト メニューを取得できます。

 環境レベルの通知は、Windows の通知領域ではなく、Visual Studio の通知ハブに表示されます。

#### <a name="notification-bubbles"></a><a name="BKMK_NotificationBubbles"></a> 通知バブル
 通知バブルは、エディターまたはデザイナー内の情報として、または Windows の通知領域の一部として表示できます。 ユーザーは、これらのバブルを後で解決できる問題として認識します。これは、重要でない通知の利点です。 バブルは、ユーザーがすぐに解決する必要がある重要な情報には適していません。 Visual Studio で通知バブルを使用する場合は、[通知バブルに関する Windows デスクトップのガイダンス](/windows/desktop/uxguide/mess-notif)に従ってください。

 ![通知バブル](../../extensibility/ux-guidelines/media/0901-07_notificationbubbles.png "0901-07_NotificationBubbles")

 **Visual Studio で使用される Windows の通知領域の通知バブル**

## <a name="progress-indicators"></a><a name="BKMK_ProgressIndicators"></a> 進行状況インジケーター

### <a name="overview"></a>概要
 進行状況インジケーターは、ユーザー フィードバックを表示するための通知システムの重要な部分です。 処理と操作が完了したことをユーザーに通知します。 使い慣れたインジケーターの種類には、進行状況バー、スピン カーソル、およびアニメーション アイコンが含まれます。 進行状況インジケーターの種類と配置は、報告される内容や、処理または操作が完了するまでにかかる時間など、コンテキストによって異なります。

#### <a name="factors"></a>考慮すべき要素
 どのインジケーターの種類が適切であるかを判断するには、次の要素を決定する必要があります。

1. **タイミング:** 操作にかかる時間の長さ

2. **モダリティ:** 操作が環境に対してモーダル (処理が完了するまで UI をロックする) かどうか

3. **永続的または一時的:** 進行状況の最終的な結果を報告したり、後で表示したりする必要があるかどうか

4. **確定的または不確定:** 操作終了時刻と進行状況を計算できるかどうか

5. **グラフィックまたはテキストの場所:** 進行状況または処理がインライン、メッセージの本文、またはツリー コントロールなどの特定のコントロールでキャプチャされているかどうか

6. **近接:** 進行状況を、関連付けられている UI の近くに配置するかどうか (たとえば、遠くにある可能性のあるステータス バーに表示してもよいか、処理を開始したボタンの近くにある必要があるか)。

#### <a name="determinate-progress"></a>確定的な進行状況

|進行状況の種類|使用するタイミングと方法|メモ|
|-------------------|-------------------------|-----------|
|進行状況バー (確定的)|5 秒を超えると予想される期間。<br /><br /> 処理の詳細の説明テキストを含めることができます。|テキストをアニメーションに埋め込ま **ない** でください。|
|情報バー|コンテキスト UI に関連付けられたメッセージング。 「[情報バー](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars)」を参照してください。<br /><br /> 処理の詳細の説明テキストを含めることができます。|複数の処理を示す必要がある場合に、複数の情報バーを使用 **しない** でください。 代わりに、積み上げ進行状況バーを使用してください。|
|[出力ウィンドウ]|一時的な通知: ユーザーが完了後に詳細を **確認** する、アプリレベルの処理。|ユーザーが後でデータを参照する必要がある場合は、使用 **しない** でください。|
|ログ ファイル|完了後に詳細を **保存** することが重要な場合、非一時的な通知と組み合わせて使用します。||
|ステータス バー|一時的な通知: ユーザーが完了後に詳細を **必要としない**、アプリレベルの処理。<br /><br /> 埋め込まれた進行状況バーを含みます。<br /><br /> 処理の詳細の説明テキストを含めることができます。||

#### <a name="indeterminate-progress"></a>不確定な進行状況

|進行状況の種類|使用するタイミングと方法|メモ|
|-------------------|-------------------------|-----------|
|進行状況バー (不確定)|5 秒を超えると予想される期間。<br /><br /> 処理の詳細の説明テキストを含めることができます。|テキストをアニメーションに埋め込ま **ない** でください。|
|Ant (アニメーション化された水平方向のドット)|サーバーへのラウンド トリップ。<br /><br /> 親コンテナー上部のコンテキスト近くの位置に配置されます。|親がコンテナー全体でない場合は使用 **しない** でください。|
|スピナー (進行状況リング)|コンテキスト UI に関連付けられている処理、または領域が考慮される場合。<br /><br /> 処理の詳細の説明テキストを含めることができます。||
|情報バー|コンテキスト UI に関連付けられたメッセージング。 「[情報バー](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars)」を参照してください。|複数の処理を示す必要がある場合に、複数の情報バーを使用 **しない** でください。 代わりに、積み上げ進行状況バーを使用してください。|
|[出力ウィンドウ]|一時的な通知: ユーザーが完了後に詳細を **確認** する、アプリレベルの処理。|セッション間で永続化する必要がある情報には使用 **しない** でください。|
|ログ ファイル|完了後に詳細を **保存** することが重要な場合、非一時的な通知と組み合わせて使用します。||
|ステータス バー|一時的な通知: ユーザーが完了後に詳細を **必要としない**、アプリレベルの処理。<br /><br /> 埋め込まれた進行状況バーを含みます。<br /><br /> 処理の詳細の説明テキストを含めることができます。||

### <a name="progress-indicator-types"></a>進行状況インジケーターの種類

#### <a name="progress-bars"></a>進行状況バー

##### <a name="indeterminate"></a>Indeterminate
 ![不確定な進行状況バー](../../extensibility/ux-guidelines/media/0901-04_indeterminate.png "0901-04_Indeterminate")

 **不確定な進行状況バー**

 "不確定" とは、操作または処理の全体的な進行状況を判断できないことを意味します。 無制限の時間を必要とする操作や、不明な数のオブジェクトにアクセスする操作には、不確定な進行状況バーを使用します。 起こっていることに合わせて、説明テキストを使用します。 タイムアウトを使用して、時間ベースで操作を制限します。 不確定な進行状況バーは、アニメーションを使用して進行していることを示しますが、その他の情報は提供しません。 精度が不十分な可能性があるという理由だけで、不確定な進行状況バーを選択しないでください。

##### <a name="determinate"></a>Determinate
 ![確定的な進行状況バー](../../extensibility/ux-guidelines/media/0901-05_determinate.png "0901-05_Determinate")

 **確定的な進行状況バー**

 "確定的" とは、その時間を正確に予測できない場合でも、操作または処理に一定の時間がかかることを意味します。 完了が明確に示されます。 操作が完了していない場合は、進行状況バーを 100% にしないでください。 確定的な進行状況バーのアニメーションは、0% から 100% まで左から右に動きます。

 操作中は、進行状況インジケーターを逆に移動させないでください。 バーは操作の開始時には徐々に進み、操作の終了時には 100% に到達する必要があります。 進行状況バーの位置は、関連するステップの数に関係なく、操作全体の所要時間をユーザーに示すためのものです。

##### <a name="concurrent-reporting-stacked-progress-bars"></a>同時実行報告 (積み上げ進行状況バー)
 操作に長い時間がかかる場合 (通常は数分)、2 つの進行状況バーを使用できます。1 つは操作の全体的な進行状況、もう 1 つは現在のステップの進行状況を示します。 たとえば、セットアップ プログラムによって多数のファイルがコピーされている場合、1 つの進行状況バーを使用して処理全体にかかる時間を示し、2 つ目の進行状況バーを使用して現在のファイルまたはディレクトリの何パーセントがコピーされているかを示すことができます。 積み上げ進行状況バーを使用して、同時に 5 個を超える操作または処理を報告しないでください。 同時に報告する操作または処理が 5 を超える場合は、[キャンセル] ボタンのあるモーダル ダイアログ ボックスを使用して、進行状況の詳細を出力ウィンドウに報告します。

##### <a name="textual-descriptions"></a>説明テキスト
 起こっている内容と完了までの推定所要時間に合わせて、説明テキストを使用します。 操作の所要時間を判断できない場合、進行状況バーではなく、アニメーション化されたアイコンがフィードバックを表示するためのより良い選択肢である可能性があります。

 Visual Studio には、ステータス バーに標準の進行状況バーが用意されており、Visual Studio に統合されているすべての製品で使用できます。 進行状況バーのアニメーション中に何が起こっているかを説明テキストで表示するために、ステータス バーのテキストを更新できます。

#### <a name="other-progress-indicators"></a>その他の進行状況インジケーター

##### <a name="ants-animated-horizontal-dots"></a>Ant (アニメーション化された水平方向のドット)
 ![進行状況 Ant](../../extensibility/ux-guidelines/media/0903-01_ants.png "0903-01_Ants")

 "Ant" は、アニメーション化された水平方向のドットで、不確定なラウンドトリップ サーバー処理の視覚的な参照を表示します。

##### <a name="spinner-progress-ring"></a>スピナー (進行状況リング)
 ![進行状況スピナー](../../extensibility/ux-guidelines/media/0903-02_spinner.png "0903-02_Spinner")

 スピナー ("進行状況リング" とも呼ばれます) は、主にコンテキスト UI に関連して使用される不確定な進行状況インジケーターです。 テキスト カテゴリのヘッダー、メッセージング、コントロールなど、関連するコンテンツに近接したスピナーを表示します。

##### <a name="cursor-feedback"></a>カーソル フィードバック
 2 - 7 秒かかる操作の場合は、カーソル フィードバックを表示します。 通常、これはオペレーティング システムによって用意されている待機カーソルを使用することを意味します。 詳細については、MSDN の記事「[Cursors.Wait プロパティ](/dotnet/api/system.windows.input.cursors.wait)」を参照してください。

#### <a name="progress-indicator-locations"></a>進行状況インジケーターの場所

##### <a name="status-bar"></a>ステータス バー
 ステータス バーは、ユーザーの作業を中断することなく、ユーザーにメッセージや有用な情報を表示するためにアプリケーションが使用できる場所です。 進行状況のステータスは、通常、ウィンドウの下部に表示され、進行状況の程度に関するメッセージと進行状況バーのインジケーターを組み合わせたツールヒント ペインになります。

 ![進行状況バー付きのステータス バー](../../extensibility/ux-guidelines/media/0903-03_statusbarprogressbar.png "0903-03_StatusBarProgressBar")

 **進行状況バー付きのステータス バー**

 ![メッセージング付きのステータス バー](../../extensibility/ux-guidelines/media/0903-04_statusbarmessage.png "0903-04_StatusBarMessage")

 **説明テキスト付きのステータス バー**

##### <a name="infobar"></a>情報バー
 ステータス バーと同様に、情報バーにはコンテキストの通知とメッセージングの機能があります。これは、進行状況バーやスピナーなどの不確定な進行状況インジケーターと組み合わせて使用することもできます。 情報バーは、詳細レベルの進捗状況や確定的な進行状況に使用すべきではありません。 「[情報バー](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars)」を参照してください。

 ![進行状況バーとメッセージング付きの情報バー](../../extensibility/ux-guidelines/media/0903-05_infobar.png "0903-05_InfoBar")

 **進行状況バーと説明テキスト付きの情報バー**

 ![ウィンドウ内の情報バー](../../extensibility/ux-guidelines/media/0903-06_infobarinwindow.png "0903-06_InfoBarInWindow")

##### <a name="inline"></a>インライン
 インラインの進行状況は、任意の種類の進行状況ローダーによって表すことができます。 通常、進行状況インジケーターはメッセージングとペアになっていますが、これは必須ではありません。

 ![インラインの進行状況スピナー](../../extensibility/ux-guidelines/media/0903-07_inlinespinner.png "0903-07_InlineSpinner")

 **スピナーと説明テキストの組み合わせ**

 ![インラインの積み上げ進行状況バー](../../extensibility/ux-guidelines/media/0903-08_inlinestackedprogress.png "0903-08_InlineStackedProgress")

 **確定的な積み上げ進行状況バー**

 ![インラインの進行状況メッセージング](../../extensibility/ux-guidelines/media/0903-09_inlinetext.png "0903-09_InlineText")

 **サーバー エクスプローラーのインライン テキスト: 更新しています...**

##### <a name="tool-windows"></a>ツール ウィンドウ
 グローバルの進行状況は、ツール バーのすぐ下に配置されている不確定な進行状況バーで表されます。

 ![グローバルで不確定な進行状況バー](../../extensibility/ux-guidelines/media/0903-23_globalindeterminate.png "0903-23_GlobalIndeterminate")

 **チーム エクスプローラーのグローバルで不確定な進行状況バー**

##### <a name="dialogs"></a>ダイアログ
 ダイアログには、任意の種類の進行状況ローダーを含めることができます。 進行状況インジケーターは、メッセージングと組み合わせたり、複数レベルの進行状況インジケーターを組み合わせて、詳細で副次的な処理を表現したりすることができます。

 ![複数の種類の進行状況インジケーターがあるダイアログ](../../extensibility/ux-guidelines/media/0903-11_dialog.png "0903-11_Dialog")

 **同時実行処理と複数の種類の進行状況インジケーターを含む Visual Studio ダイアログ**

 ![進行状況ローダーとメッセージングを含むダイアログ](../../extensibility/ux-guidelines/media/0903-12_dialog2.png "0903-12_Dialog2")

 **進行状況ローダーとメッセージング インライン コマンド実行を含む Visual Studio ダイアログ**

##### <a name="document-well"></a>ドキュメント ウェル
 ドキュメント ウェルでは、複数の種類の進行状況ローダーをコントロールと組み合わせて表示できます。

 ![ドキュメント ウェル内の進行状況メッセージング](../../extensibility/ux-guidelines/media/0903-13_documentwell.png "0903-13_DocumentWell")

 **ツールバーの下の不確定な進行状況バー**

##### <a name="output-window"></a>[出力ウィンドウ]
 出力ウィンドウは、インライン テキスト メッセージングを介して、処理の進行状況と実行中の進行状況の状態を扱うのに適しています。 ステータス バーは、出力ウィンドウの進行状況の報告と共に使用する必要があります。

 ![出力ウィンドウ内の進行状況メッセージング](../../extensibility/ux-guidelines/media/0903-14_outputwindow.png "0903-14_OutputWindow")

 **進行中の処理の状態と待機メッセージングを含む出力ウィンドウ**

## <a name="infobars"></a><a name="BKMK_Infobars"></a> 情報バー

### <a name="overview"></a>概要
 情報バーは、ユーザーが注意する場所の近くにインジケーターを表示し、共有の情報バー コントロールを使用することで、視覚的な外観とユーザー操作の一貫性を確保します。

 ![情報バー](../../extensibility/ux-guidelines/media/0904-01_infobar.png "0904-01_Infobar")

 **Visual Studio の情報バー**

#### <a name="appropriate-uses-for-an-infobar"></a>情報バーの適切な使用

- 現在のコンテキストに関連する、非ブロッキングであるが重要なメッセージをユーザーに表示するため

- デバッグ履歴など、UI が特定の状態または条件にあり、ユーザー操作に何らかの影響を与えることを示すため

- 拡張機能によりパフォーマンス上の問題が発生しているなど、システムによって問題が検出されたことをユーザーに通知するため

- ファイルにタブとスペースが混在していることをエディターで検出した場合など、ユーザーが簡単にアクションを実行できるようにするため

##### <a name="do"></a>次の処理が必要です。

- 情報バーのメッセージ テキストは短く、要領を得たものにする。

- リンクとボタンのテキストは簡潔にする。

- ユーザーに提示する "アクション" オプションが最小限で、必要なアクションのみを表示する。

##### <a name="dont"></a>禁止事項:

- ツール バーに配置する必要がある標準コマンドを用意するために、情報バーを使用する。

- モーダル ダイアログの代わりに情報バーを使用する。

- ウィンドウの外にフローティング メッセージを作成する。

- 同じウィンドウ内の複数の場所で複数の情報バーを使用する。

#### <a name="can-multiple-infobars-show-at-the-same-time"></a>複数の情報バーを同時に表示できますか。
 はい。複数の情報バーを同時に表示できます。 表示は先着順となり、最初の情報バーが上端に表示され、追加の情報バーが下に表示されます。

 ユーザーには、一度に最大 3 つの情報バーが表示されます。その後、さらに多くの情報バーが使用可能になると、情報バーの領域がスクロール可能になります。

### <a name="creating-an-infobar"></a>情報バーの作成
 情報バーには、左から右方向に 4 つのセクションがあります。

- **アイコン:** ここに、情報バーに表示するアイコン (警告アイコンなど) を追加します。

- **テキスト:** ユーザーが置かれているシナリオや状況を説明するテキストを追加し、必要に応じて、テキスト内にリンクを作成できます。 テキストは簡潔にするようにしてください。

- **アクション:** このセクションには、ユーザーが情報バーで実行できるアクションのリンクとボタンが含まれている必要があります。

- **[閉じる] ボタン:** 右側の最後のセクションには、[閉じる] ボタンを含めることができます。

#### <a name="creating-a-standard-infobar-in-managed-code"></a>マネージド コードでの標準の情報バーの作成
 InfoBarModel クラスを使用すると、情報バーのデータ ソースを作成できます。 次の 4 つのコンストラクターのいずれかを使用します。

```
public InfoBarModel(IEnumerable<IVsInfoBarTextSpan> textSpans, ImageMoniker image = default(ImageMoniker), bool isCloseButtonVisible = true);

```

```
public InfoBarModel(string text, ImageMoniker image = default(ImageMoniker), bool isCloseButtonVisible = true);

```

```
public InfoBarModel(IEnumerable<IVsInfoBarTextSpan> textSpans, IEnumerable<IVsInfoBarActionItem> actionItems, ImageMoniker image = default(ImageMoniker), bool isCloseButtonVisible = true);

```

```
public InfoBarModel(string text, IEnumerable<IVsInfoBarActionItem> actionItems, ImageMoniker image = default(ImageMoniker), bool isCloseButtonVisible = true);
```

 次に示すのは、ハイパーリンク、アクション ボタン、およびアイコンと共にテキストを使用して InfoBarModel を作成する例です。

 ![ハイパーリンクを含むページ](../../extensibility/ux-guidelines/media/0904-02_infobarhyperlink.png "0904-02_InfobarHyperlink")

```
var infoBar = new InfoBarModel(
    textSpans: new[]
    {
        new InfoBarTextSpan("This is a "),
        new InfoBarHyperlink("hyperlink"),
        new InfoBarTextSpan(" InfoBar.")
    },
    actionItems: new[]
    {
        new InfoBarButton("Click Me")
    },
    image: KnownMonikers.StatusInformation,
    isCloseButtonVisible: true);

```

#### <a name="creating-a-standard-infobar-in-native-code"></a>ネイティブ コードでの標準の情報バーの作成
 ネイティブ コードで情報バーを実現するために、IVsInfoBar インターフェイスを実装します。

```
public interface IVsInfoBar
{
    IVsInfoBarActionItemCollection ActionItems { get; }
    ImageMoniker Image { get; }
    bool IsCloseButtonVisible { get; }
    IVsInfoBarTextSpanCollection TextSpans { get; }
}

```

#### <a name="getting-an-infobar-uielement-from-an-infobar"></a>情報バーからの情報バー UIElement の取得
 InfoBarModel または IVsInfoBar の実装は、UI に表示するために UIElement に変換する必要があるデータ モデルです。 UIElement は、SVsInfoBarUIFactory または IVsInfoBarUIFactory サービスを使用して取得できます。

```
private bool TryCreateInfoBarUI(IVsInfoBar infoBar, out IVsInfoBarUIElement uiElement)
{
    IVsInfoBarUIFactory infoBarUIFactory = serviceProvider.GetService(typeof(SVsInfoBarUIFactory)) as IVsInfoBarUIFactory;
    if (infoBarUIFactory == null)
    {
        uiElement = null;
        return false;
    }

    uiElement = infoBarUIFactory.CreateInfoBar(infoBar);
    return uiElement != null;
}
```

### <a name="placement"></a>配置
 情報バーは、次の 1 つ以上の場所に表示できます。

- ツール ウィンドウ

- ドキュメント タブ内

> [!IMPORTANT]
> 情報バーを配置して、グローバル コンテキストに関するメッセージを表示することができます。 これは、ツールバーとドキュメント ウェルの間に表示されます。 IDE の "制御できない動き" に関する問題が発生するため、この方法は推奨されません。絶対に必要かつ適切でない限り、回避する必要があります。

#### <a name="placing-an-infobar-in-a-toolwindowpane"></a>ToolWindowPane 内への情報バーの配置
 ToolWindowPane.AddInfoBar(IVsInfoBar) メソッドを使用して、ツール ウィンドウに情報バーを追加できます。 この API では、IVsInfoBar (InfoBarModel が既定の実装)、または IVsUIElement のいずれかを追加できます。

#### <a name="placing-an-infobar-in-a-document-or-non-toolwindowpane"></a>ドキュメントまたは非 ToolWindowPane 内への情報バーの配置
 任意の IVsWindowFrame に情報バーを配置するには、VSFPROPID_InfoBarHost プロパティを使用して、フレームの IVsInfoBarHost を取得し、情報バーの UIElement を追加します。

```
private void AddInfoBar(IVsWindowFrame frame, IVsUIElement uiElement)
{
    IVsInfoBarHost infoBarHost;
    if (TryGetInfoBarHost(frame, out infoBarHost))
    {
        infoBarHost.AddInfoBar(uiElement);
    }
}
private bool TryGetInfoBarHost(IVsWindowFrame frame, out IVsInfoBarHost infoBarHost)
{
    object infoBarHostObj;
    if (ErrorHandler.Failed(frame.GetProperty((int)__VSFPROPID7.VSFPROPID_InfoBarHost, out infoBarHostObj)))
    {
        infoBarHost = null;
        return false;
    }

    infoBarHost = infoBarHostObj as IVsInfoBarHost;
    return infoBarHost != null;
}

```

#### <a name="placing-an-infobar-in-the-main-window"></a>メイン ウィンドウ内への情報バーの配置
 メイン ウィンドウに情報バーを配置するには、IVsShell サービスの VSSPROPID_MainWindowInfoBarHost を使用してメイン ウィンドウの IVsInfoBarHost を取得し、そこに情報バーの UIElement を追加します。

### <a name="will-i-know-when-the-user-takes-action-in-my-infobar"></a>ユーザーが情報バーでアクションを実行したときに、それを知ることができますか。
 はい。すべてのイベント アクションは情報バーの作成者に返されます。 次に、情報バーのユーザー選択に基づいて IDE でアクションを実行するのは、情報バーの作成者に任されます。 [閉じる] ボタンがクリックされたホストからは、情報バーが自動的に削除されますが、閉じた後に他の情報バーを削除する必要がある場合は、追加の作業が必要になります。 また、テレメトリは各情報バーによって個別にログに記録される必要があります。

#### <a name="receiving-infobar-events-in-a-toolwindowpane"></a>ToolWindowPane での情報バー イベントの受信
 ToolWindowPane には、2 つのイベントがあります。 ToolWindowPane の情報バーが閉じたときに、InfoBarClosed イベントが発生します。 InfoBarActionItemClicked イベントは、情報バー内のハイパーリンクまたはボタンがクリックされたときに発生します。

#### <a name="receiving-infobar-events-directly-from-the-uielement"></a>UIElement からの情報バー イベントの直接受信
 IVsInfoBarUIElement.Advise を使用すると、情報バーの UIElement から直接イベントをサブスクライブできます。 IVsInfoBarUIEvents を実装すると、作成者はクローズ イベントとクリック イベントを受け取ることができます。

```
public interface IVsInfoBarUIEvents
{
    void OnActionItemClicked(IVsInfoBarUIElement infoBarUIElement, IVsInfoBarActionItem actionItem);
    void OnClosed(IVsInfoBarUIElement infoBarUIElement);
}

```

## <a name="error-validation"></a><a name="BKMK_ErrorValidation"></a> エラーの検証
 必須フィールドがスキップされた場合や、データが不適切な形式で入力された場合など、ユーザーが有効でない情報を入力した場合は、ブロッキングのポップアップ エラー ダイアログを使用するのではなく、コントロールの検証またはフィードバックをコントロールの近くで使用することをお勧めします。

### <a name="field-validation"></a>Field validation
 フォームとフィールドの検証は、コントロール、アイコン、およびツールヒントの 3 つのコンポーネントで構成されています。 いくつかの種類のコントロールでこれを使用できますが、例としてテキスト ボックスを使用します。

 ![フィールドの検証 &#40;空白&#41;](../../extensibility/ux-guidelines/media/0905-01_fieldvalidation.png "0905-01_FieldValidation")

 フィールドが必須の場合は、 **\<Required>** と表示される透かしのテキストがあり、フィールドの背景が薄い黄色 (VSColor: `Environment.ControlEditRequiredBackground`) で、前景が灰色 (VSColor: `Environment.ControlEditRequiredHintText`) である必要があります。

 !["必須" のラベルを持つフィールドの検証](../../extensibility/ux-guidelines/media/0905-02_fieldvalidationrequired.png "0905-02_FieldValidationRequired")

 フォーカスが別のコントロールに移動したとき、ユーザーが [OK] コミット ボタンをクリックしたとき、またはユーザーがドキュメントまたはフォームを保存したときに、コントロールが "*無効なコンテンツとして入力された*" 状態にあると、プログラムで判断されます。

 無効なコンテンツの状態と判断されると、コントロール内またはそのすぐ横にアイコンが表示されます。 アイコンまたはコントロールのいずれかにマウス ポインターを置くと、エラーを説明するツールヒントが表示されます。 また、無効な状態を引き起こしているコントロールの周囲に 1 ピクセルの枠線が表示されます。

 ![フィールドの検証のレイアウトの仕様](../../extensibility/ux-guidelines/media/0905-03_layoutspecs.png "0905-03_LayoutSpecs")

 **フィールドの検証のレイアウトの仕様**

#### <a name="acceptable-variations-for-icon-location"></a>アイコンの場所の許容バリエーション
 検証エラーをユーザーに通知する必要がある独特のケースは無数にあります。 UI のコントロールの種類と構成を考慮して、状況に適したアイコンの配置を選択します。

 ![アイコンの場所の適切な場所](../../extensibility/ux-guidelines/media/0905-04_iconlocation.png "0905-04_IconLocation")

 **フィールド検証のアイコンの場所の許容バリエーション**

#### <a name="validation-requiring-a-round-trip-to-a-server-or-network-connection"></a>サーバーまたはネットワーク接続へのラウンド トリップを必要とする検証
 場合によっては、コンテンツを確認するためにサーバーへのラウンド トリップが必要となり、ユーザーの進捗状況、検証済み、エラーの状態を表示することが重要になります。 次の図では、このケースと推奨される UI の例を示しています。

 ![サーバーへのラウンド トリップに関連する検証](../../extensibility/ux-guidelines/media/0905-05_roundtrip.png "0905-05_RoundTrip")

 **サーバーへのラウンド トリップに関連する検証**

 "検証しています..." や "再試行" というテキストを格納するためには、コントロールの右側に十分な領域を用意する必要があることに注意してください。

#### <a name="in-place-warning-text"></a>インプレース警告テキスト
 エラー メッセージをコントロールの近くに配置する余地がある場合、これはツールヒントを単独で使用するよりも望ましい方法です。

 ![インプレース警告](../../extensibility/ux-guidelines/media/0905-06_inplacewarning.png "0905-06_InPlaceWarning")

 **インプレース警告テキスト**

#### <a name="watermarks"></a>透かし
 コントロールまたはウィンドウ全体がエラー状態になることがあります。 このような場合は、透かしを使用してエラーを示します。

 ![ウォーターマーク](../../extensibility/ux-guidelines/media/0905-07_watermark.png "0905-07_Watermark")

 **フィールドの検証への透かし**
