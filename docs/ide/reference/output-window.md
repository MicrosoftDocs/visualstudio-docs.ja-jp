---
title: '[出力] ウィンドウ'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.build.output
- vs.debug.output
- vs.output
helpviewer_keywords:
- Output window, about Output window
- Output window
- Toolbox, removing controls
ms.assetid: d8931d88-250e-4db4-963f-2c5b3e99b45f
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f8866b4a2518c8c4d58f26b625e45a0188498021
ms.sourcegitcommit: 12f2851c8c9bd36a6ab00bf90a020c620b364076
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2019
ms.locfileid: "66746527"
---
# <a name="output-window"></a>[出力] ウィンドウ

**出力**ウィンドウには、統合開発環境 (IDE: Integrated Development Environment) のさまざまな機能のステータス メッセージが表示されます。 **出力**ウィンドウを開くには、メニュー バーで、 **[表示]**  >  **[出力]** の順にクリックします (または、**Ctrl**+**Alt**+**O** キーを押します)。

## <a name="toolbar"></a>ツール バー

次のコントロールは、**出力**ウィンドウのツール バーに表示されます。

### <a name="show-output-from"></a>[出力元の表示]

1 つ以上の出力ペインを表示します。 IDE のどのツールが **[出力]** ウィンドウを使用してユーザーにメッセージを配布するかに応じて、複数の情報ペインを使用できる場合があります。

### <a name="find-message-in-code"></a>コード内のメッセージ検索

コード エディター内のカーソル位置を、選択されたビルド エラーのある行まで移動させます。

### <a name="go-to-previous-message"></a>[前のメッセージに移動]

**[出力]** ウィンドウ内のフォーカスを前のビルド エラーへ移し、コード エディターのカーソル位置をそのビルド エラーがある行へ移動させます。

### <a name="go-to-next-message"></a>次のメッセージに移動

**[出力]** ウィンドウ内のフォーカスを次のビルド エラーへ移し、コード エディターのカーソル位置をそのビルド エラーがある行へ移動させます。

### <a name="clear-all"></a>[すべてクリア]

**出力**ペインのすべてのテキストを消去します。

### <a name="toggle-word-wrap"></a>[[右端で折り返す] の設定/解除]

**出力**ペインでのワード ラップ機能のオンとオフを切り替えます。 ワード ラップ機能が有効になっていると、表示エリアより長いテキストは次の行に折り返されて表示されます。

## <a name="output-pane"></a>出力ウィンドウ

**[出力元の表示]** の一覧で選択された**出力**ペインは、このボックスで選択された項目の出力結果を表示します。

## <a name="route-messages-to-the-output-window"></a>出力ウィンドウにメッセージをルーティングする

プロジェクトをビルドしたときに必ず**出力**ウィンドウが表示されるようにするには、 **[オプション]** ダイアログ ボックスの **[プロジェクトおよびソリューション]**  >  **[全般]** ページで、 **[ビルド開始時に出力ウィンドウを表示]** をオンにします。 次に、編集のためにコード ファイルを開けた状態で、**出力**ウィンドウのエントリを選択するために**出力**ウィンドウのツール バーの **[次のメッセージに移動]** および **[前のメッセージに移動]** をクリックします。 この動作を続けると、コード エディターのカーソル位置が、選択した問題が発生したコード行へ移動します。

[コマンド ウィンドウ](../../ide/reference/command-window.md)で実行できる一部の IDE 機能およびコマンドでは、**出力**ウィンドウへ出力結果が送られます。 *.bat* ファイルや *.com* ファイルなどの外部ツールからの出力は、通常コマンド ウィンドウで表示されますが、[[外部ツールの構成]](../../ide/managing-external-tools.md) の **[出力ウィンドウを使用]** オプションをオンにすると**出力**ウィンドウに送られます。 他の種類のメッセージの多くも **[出力]** ペインで表示できます。 たとえば、ストアド プロシージャの Transact-SQL 構文を対象のデータベースに対してチェックすると、その結果が **[出力]** ウィンドウに表示されます。

また、実行時に診断メッセージを **[出力]** ペインに書き出すことのできる、独自のアプリケーションをプログラムすることも可能です。 これを行うには、<xref:System.Diagnostics.Debug> クラスのメンバーまたは .NET API の <xref:System.Diagnostics> 名前空間にある <xref:System.Diagnostics.Trace> クラスを使用します。 <xref:System.Diagnostics.Debug> クラスのメンバーは、ソリューションまたはプロジェクトのデバッグ構成をビルドするときの出力結果を表示します。<xref:System.Diagnostics.Trace> クラスのメンバーは、デバッグ構成またはリリース構成のどちらかをビルドするときの出力結果を表示します。 詳細については、[出力ウィンドウの診断メッセージ](../../debugger/diagnostic-messages-in-the-output-window.md)に関するページを参照してください。

C++ では、警告とエラー メッセージ、およびその合計数を**出力**ウィンドウで表示できる、カスタム ビルド ステップおよびビルド イベントを作成できます。 出力結果の任意の行で **F1** キーを押すと、適切なヘルプ トピックが表示されます。 詳細については、[カスタム ビルド ステップの出力の書式設定](/cpp/build/reference/formatting-the-output-of-a-custom-build-step-or-build-event)に関する記事を参照してください。

## <a name="scroll-behavior"></a>スクロールの動作

**出力**ウィンドウで自動スクロールを使用していて、マウスや方向キーを使用して移動すると、自動スクロールが停止します。 自動スクロールを再開するには、**Ctrl**+**End** キーを押します。

## <a name="see-also"></a>関連項目

- [出力ウィンドウの診断メッセージ](../../debugger/diagnostic-messages-in-the-output-window.md)
- [方法: 出力ウィンドウを制御する](https://msdn.microsoft.com/Library/91aebd15-8854-4a7a-9f7d-57376fb4e858)
- [コンパイルとビルド](../../ide/compiling-and-building-in-visual-studio.md)
- [ビルド構成について](../../ide/understanding-build-configurations.md)
- [クラス ライブラリの概要](/dotnet/standard/class-library-overview)