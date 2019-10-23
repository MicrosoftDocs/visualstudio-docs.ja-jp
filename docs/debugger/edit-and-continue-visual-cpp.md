---
title: エディットコンティニュ (C++) |Microsoft Docs
ms.date: 05/31/2018
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Edit and Continue [C++]
- debugging [C++], Edit and Continue
- C/C++, Edit and Continue
ms.assetid: 1815251e-a877-433e-9e5e-69bd9ba254c7
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 0ebe31267ee666250fbaeda73f1678051f1d4727
ms.sourcegitcommit: 485ffaedb1ade71490f11cf05962add1718945cc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72435857"
---
# <a name="edit-and-continue-c"></a>エディットコンティニュ (C++)
プロジェクトでC++は、エディットコンティニュを使用できます。 エディットコンティニュの制限事項については、「[サポートされてC++いるコード変更 ()](../debugger/supported-code-changes-cpp.md) 」を参照してください。

Visual studio 2015 update 3 の機能強化の詳細については、「 [ C++ visual studio 2015 update 3 でのエディットコンティニュ](https://devblogs.microsoft.com/cppblog/c-edit-and-continue-in-visual-studio-2015-update-3/)」を参照してください。

 Visual Studio 2013 Update 3 で導入された [/Zo (最適化されたデバッグ機能の強化)](/cpp/build/reference/zo-enhance-optimized-debugging) コンパイラ オプションは、[/Od (無効 (デバッグ))](https://msdn.microsoft.com/library/aafb762y.aspx) オプションなしでコンパイルされたバイナリの .pdb (シンボル) ファイルに情報を追加します。

 **/Zo**は、エディットコンティニュを無効にします。 「[方法: 最適化されたコードをデバッグする](../debugger/how-to-debug-optimized-code.md)」をご覧ください。

## <a name="BKMK_Enable_or_disable_automatic_invocation_of_Edit_and_Continue"></a> エディット コンティニュを有効または無効にする
 現在のデバッグ セッション中に適用しないコードの編集を行う場合は、エディット コンティニュの自動起動を無効にすることもできます。 自動エディット コンティニュをもう一度有効にすることもできます。

> [!IMPORTANT]
> 必要なビルド設定と機能の互換性に関するその他の情報については、「 [ C++ Visual Studio 2015 Update 3 でのエディットコンティニュ](https://devblogs.microsoft.com/cppblog/c-edit-and-continue-in-visual-studio-2015-update-3/)」を参照してください。

1. デバッグセッションを使用している場合は、デバッグを停止します (**Shift + F5**)。

2. **[ツール]** メニューの **[オプション]** をクリックします。

3. **[オプション]** ダイアログ ボックスで、 **[デバッグ] > [全般]** を選択します。

4. 有効にするには、[**エディットコンティニュを有効**にする] を選択します。 無効にするには、このチェックボックスをオフにします。

5. **[エディット コンティニュ]** グループで、 **[ネイティブのエディット コンティニュを有効にする]** チェック ボックスをオンまたはオフにします。

   この設定を変更すると、作業するすべてのプロジェクトに影響します。 この設定の変更後にアプリケーションをリビルドする必要はありません。 アプリケーションをコマンド ラインまたはメイクファイルでビルドしていますが、Visual Studio 環境でデバッグする場合、 **/ZI** オプションを設定すると、引き続きエディット コンティニュを使用できます。

## <a name="BKMK_How_to_apply_code_changes_explicitly"></a> コード変更を明示的に適用する方法
 でC++は、エディットコンティニュは2つの方法でコード変更を適用できます。 実行コマンドを選択した場合、コード変更は暗黙的に適用できます。 **[コード変更を適用]** を使用した場合は明示的に適用できます。

 コード変更を明示的に適用する場合、プログラムは中断モードのままとなり実行されません。

- コードの変更を明示的に適用するには、 **[デバッグ]** メニューで **[コード変更を適用]** を選択します。

## <a name="BKMK_How_to_stop_code_changes"></a> コード変更を停止する方法
 エディット コンティニュがコード変更を適用するプロセスを実行している間、その操作は中断できます。

 コードの変更内容の適用を停止するには

- **[デバッグ]** メニューの **[コード変更の適用を停止]** をクリックします。

  このメニュー項目は、コード変更の適用中にのみ表示されます。

  このオプションを選択すると、コードの変更内容は一切コミットされません。

## <a name="BKMK_How_to_reset_the_point_of_execution"></a> 実行ポイントをリセットする方法
 コードを変更してエディット コンティニュでその変更内容を適用すると、実行ポイントが新しい位置に移動する場合があります。 [エディット コンティニュ] では、実行ポイントができるだけ正確に位置付けられますが、結果が常に正しいとは限りません。

 でC++は、実行ポイントが変更されたことを示すダイアログボックスが表示されます。 デバッグを継続する前に、位置が正しいかどうかを確認する必要があります。 位置が正しくない場合は、 **[次のステートメントの設定]** を使用します。 詳しくは、「 [次に実行されるステートメントを設定する](https://msdn.microsoft.com/library/y740d9d3.aspx#BKMK_Set_the_next_statement_to_execute)」をご覧ください。

## <a name="BKMK_How_to_work_with_stale_code"></a> 古いコードを操作する方法
 場合により、エディット コンティニュがコード変更を直ちに適用して実行可能にできないことがありますが、デバッグを続行すると、後でコード変更が適用できるようになる場合もあります。 これは、現在の関数を呼び出す関数を編集した場合や、呼び出し履歴上の関数に 64 バイトを超える新しい変数を追加した場合に発生します。

 このような場合、変更が適用されるまで、デバッガーは元のコードを続けて実行します。 古いコードは、一時的なソース ファイル ウィンドウとして、 `enc25.tmp`などのタイトルで別のソース ウィンドウに表示されます。 編集されたソース コードは、元のソース ウィンドウに表示されます。 古いコードを編集しようとすると、警告メッセージが表示されます。

## <a name="see-also"></a>参照
- [サポートされているコード変更 (C++)](../debugger/supported-code-changes-cpp.md)