---
title: XAML ホット リロードのトラブルシューティング
description: XAML ホット リロードで発生する可能性のある問題を解決します。
ms.date: 09/04/2019
ms.topic: troubleshooting
helpviewer_keywords:
- xaml edit and continue, troubleshooting
- xaml hot reload, troubleshooting
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 4e13fd71c9d53ef49d7f7372986bfabc29c62747
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99890449"
---
# <a name="troubleshooting-xaml-hot-reload"></a>XAML ホット リロードのトラブルシューティング

このトラブルシューティング ガイドで説明する詳細な手順に従うと、XAML ホット リロードの正常な動作を妨げるほとんどの問題が解決されるはずです。

XAML ホット リロードは、WPF アプリと UWP アプリでサポートされています。 オペレーティング システムとツールの要件の詳細については、[XAML ホット リロードを使用した実行中の XAML コードの作成とデバッグ](xaml-hot-reload.md)に関する記事を参照してください。

## <a name="hot-reload-is-not-available"></a>ホット リロードを使用できない

アプリのデバッグ中に、アプリ内のツール バーに "ホットリロードを使用できない" というメッセージが表示される場合は、この記事で説明されている手順に従って問題を解決します。

## <a name="verify-that-xaml-hot-reload-is-enabled"></a>XAML ホット リロードが有効になっていることを確認する

この機能は、既定で有効になっています。 アプリのデバッグを始めるときに、アプリ内ツール バーが表示されていることを確認します。これは、XAML ホット リロードが使用可能であることを示します。

![XAML ホット リロードは利用可能](../debugger/media/xaml-hot-reload-available.png)

アプリ内ツール バーが表示されない場合は、 **[デバッグ]**  >  **[オプション]**  >  **[全般]** を開きます。 **[XAML の UI デバッグ ツールを有効にする]** と **[XAML ホット リロードを有効にする]** の両方のオプションがオンになっていることを確認します。

![Visual Studio のデバッグ オプション ウィンドウのスクリーンショット。 [全般] デバッグ オプションが選択され、[XAML ホット リロードを有効にする] オプションがオンになっています。](../debugger/media/xaml-hot-reload-enable.png)

これらのオプションを選択した後、[ライブ ビジュアル ツリー] に移動し ( **[デバッグ]**  >  **[ウィンドウ]**  >  **[ライブ ビジュアル ツリー]** )、 **[アプリケーションでランタイム ツールを表示]** ツールバー ボタン (左端) が選択されていることを確認します。

![[アプリケーションでランタイム ツールを表示] ボタンが選択されている [ライブ ビジュアル ツリー] ウィンドウの上部にあるツール バーのスクリーンショット。](../debugger/media/xaml-hot-reload-show-runtime-tools.png)

## <a name="verify-that-you-use-start-debugging-rather-than-attach-to-process"></a>[プロセスにアタッチ] ではなく [デバッグの開始] を使用していることを確認する

XAML ホット リロードを使用するには、アプリケーションの開始時に環境変数 `ENABLE_XAML_DIAGNOSTICS_SOURCE_INFO` が 1 に設定されている必要があります。 これは、 **[デバッグ]**  >  **[デバッグの開始]** (または **F5** キー) コマンドの一部として、Visual Studio により自動的に設定されます。 代わりに **[デバッグ]**  >  **[プロセスにアタッチ]** コマンド XAML ホット リロードを使用したい場合は、環境変数を自分で設定します。

> [!NOTE]
> 環境変数を設定するには、[スタート] ボタンを使用して "環境変数" を検索し、 **[システム環境変数の編集]** を選択します。 表示されるダイアログ ボックスで **[環境変数]** を選択し、ユーザー変数として追加して、値を `1` に設定します。 クリーンアップするには、デバッグが完了したら変数を削除します。

## <a name="verify-that-your-msbuild-properties-are-correct"></a>MSBuild のプロパティが正しいことを確認する

既定では、ソース情報はデバッグ構成に含まれています。 それは、プロジェクト ファイル (*.csproj など) 内の MSBuild のプロパティによって制御されます。 WPF の場合、プロパティは `XamlDebuggingInformation` であり、それが `True` に設定されている必要があります。 UWP の場合、プロパティは `DisableXbfLineInfo` であり、それが `False` に設定されている必要があります。 次に例を示します。

WPF:

`<XamlDebuggingInformation>True</XamlDebuggingInformation>`

UWP:

`<DisableXbfLineInfo>False</DisableXbfLineInfo>`

## <a name="verify-that-you-are-using-the-correct-build-configuration-name"></a>正しいビルド構成名を使用していることを確認する

XAML ホット リロードがサポートされるように正しい MSBuild プロパティを手動で設定するか (前のセクションを参照)、既定のビルド構成名 (Debug) を使用する必要があります。 MSBuild プロパティが正しく設定されていない場合、カスタム ビルド構成名は機能せず、リリース ビルドも機能しません。

## <a name="verify-that-your-xaml-file-has-no-errors"></a>XAML ファイルにエラーがないことを確認する

XAML ファイルの **[エラー一覧]** にエラーが表示されている場合、XAML ホット リロードが機能しない可能性があります。

## <a name="see-also"></a>関連項目

[XAML ホット リロードで実行中の XAML コードを記述し、デバッグする](xaml-hot-reload.md)
