---
title: XAML ホットリロードのトラブルシューティング
description: XAML ホットリロードで発生する可能性のある問題を修正します。
ms.date: 09/04/2019
ms.topic: troubleshooting
helpviewer_keywords:
- xaml edit and continue, troubleshooting
- xaml hot reload, troubleshooting
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: dbfb88113eec35dec72d5c3753dc37775a7a2591
ms.sourcegitcommit: 0e482cfc15f809b564c3de61646f29ecd7bfcba6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/14/2019
ms.locfileid: "70988177"
---
# <a name="troubleshooting-xaml-hot-reload"></a>XAML ホットリロードのトラブルシューティング

このトラブルシューティングガイドでは、XAML ホットリロードが正常に動作しない原因となる問題を解決するための詳細な手順について説明します。

XAML ホットリロードは、WPF アプリと UWP アプリでサポートされています。 オペレーティングシステムとツールの要件の詳細については、「 [Xaml ホットリロードを使用した実行中の xaml コードの書き込みとデバッグ](xaml-hot-reload.md)」を参照してください。

## <a name="hot-reload-is-not-available"></a>ホットリロードは使用できません

アプリのデバッグ中に、アプリ内ツールバーの "ホットリロードが使用できません" というメッセージが表示された場合は、この記事で説明されている手順に従って問題を解決してください。

## <a name="verify-that-xaml-hot-reload-is-enabled"></a>XAML ホットリロードが有効になっていることを確認する

この機能は既定で有効になっています。 アプリのデバッグを開始するときに、アプリ内ツールバーが表示されていることを確認します。これにより、XAML ホットリロードが使用可能であることが確認できます。

![XAML ホットリロードを利用できます](../debugger/media/xaml-hot-reload-available.png)

アプリ内ツールバーが表示されない場合は、**デバッグ** > **オプション** > の **[全般]** を開きます。 [ **Xaml の UI デバッグツールを有効**にする] と [ **xaml ホットリロードを有効に**する] の両方が選択されていることを確認します。

![XAML ホットリロードを有効にする](../debugger/media/xaml-hot-reload-enable.png)

これらのオプションを選択した場合は、[ライブビジュアルツリー (**Windows** > **live ビジュアルツリー**の**デバッグ** > )] に移動し、 **[ランタイムツールをアプリケーションツールバーに表示]** ボタン (左端) が選択されていることを確認します。

![XAML ホットリロードを有効にする](../debugger/media/xaml-hot-reload-show-runtime-tools.png)

## <a name="verify-that-you-use-start-debugging-rather-than-attach-to-process"></a>プロセスにアタッチするのではなく、デバッグの開始を使用することを確認します。

XAML ホットリロードでは、アプリケーションの`ENABLE_XAML_DIAGNOSTICS_SOURCE_INFO`起動時に環境変数が1に設定されている必要があります。 Visual Studio**は、デバッグ** > **開始デバッグ**(または**F5**) コマンドの一部として、これを自動的に設定します。 代わりに **[プロセスにアタッチ]** コマンドを**使用して** > XAML ホットリロードを使用する場合は、環境変数を自分で設定します。

## <a name="verify-that-your-msbuild-properties-are-correct"></a>MSBuild プロパティが正しいことを確認する

既定では、ソース情報はデバッグ構成に含まれています。 これは、プロジェクトファイル (* .csproj など) の MSBuild プロパティによって制御されます。 WPF の場合、プロパティは`XamlDebuggingInformation`です。これは、に`True`設定する必要があります。 UWP の場合、プロパティは`DisableXbfLineInfo`です。これは、に`False`設定する必要があります。 例えば:

WPF

`<XamlDebuggingInformation>True</XamlDebuggingInformation>` 

UWP

`<DisableXbfLineInfo>False</DisableXbfLineInfo>`

## <a name="verify-that-you-are-using-the-correct-build-configuration-name"></a>正しいビルド構成名を使用していることを確認します

XAML ホットリロードをサポートするには、正しい MSBuild プロパティを手動で設定するか (前のセクションを参照)、既定のビルド構成名 (Debug) を使用する必要があります。 MSBuild プロパティを正しく設定しない場合、カスタムビルド構成名は機能しません。また、リリースビルドも実行されません。

## <a name="verify-that-your-xaml-file-has-no-errors"></a>XAML ファイルにエラーがないことを確認する

XAML ファイルで**エラー一覧**にエラーが表示されている場合、Xaml ホットリロードが機能しない可能性があります。

## <a name="see-also"></a>関連項目

[XAML ホットリロードを使用して実行中の XAML コードを記述およびデバッグする](xaml-hot-reload.md)