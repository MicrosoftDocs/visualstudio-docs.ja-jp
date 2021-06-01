---
title: XAML ホット リロードを使用して XAML を作成してデバッグする
description: XAML ホット リロード (XAML エディット コンティニュ) を使用すると、アプリを実行しながら XAML コードを変更できます
ms.date: 09/23/2020
ms.topic: conceptual
helpviewer_keywords:
- xaml edit and continue
- xaml hot reload
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 11257561deecdbce4606207c3d59012a6d7c3d09
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99880321"
---
# <a name="write-and-debug-running-xaml-code-with-xaml-hot-reload-in-visual-studio"></a>Visual Studio での XAML ホットリロードを使用した実行中の XAML コードの作成とデバッグ

XAML ホット リロードを使用すると、アプリを実行しながら XAML コードを変更でき、WPF または UWP アプリのユーザー インターフェイス (UI) を構築するのに役立ちます。 ホット リロードは、Visual Studio と Blend for Visual Studio の両方で使用できます。 この機能を使用すると、実行中のアプリのデータ コンテキスト、認証状態、およびデザイン時にシミュレートするのが困難なその他の現実世界の複雑さを利用して、XAML コードを段階的にビルドおよびテストできます。 XAML ホット リロードのトラブルシューティングに関するヘルプが必要な場合は、代わりに「[XAML ホット リロードのトラブルシューティング](xaml-hot-reload-troubleshooting.md)」を参照してください。

> [!NOTE]
> Xamarin.Forms を使用している場合は、「[Xamarin.Forms の XAML ホット リロード](/xamarin/xamarin-forms/xaml/hot-reload)」を参照してください。

XAML ホット リロードは、次のような場合に特に役立ちます。

* アプリをデバッグ モードで開始した後に、XAML コードで見つかった UI の問題を修正する。

* アプリのランタイム コンテキストを利用しながら、開発中のアプリ用の新しい UI コンポーネントを構築する。

|サポートされているアプリケーションの種類|オペレーティング システムとツール|
|-|-|-|
|Windows Presentation Foundation (WPF) |.NET Framework 4.6 以降と .NET Core</br>Windows 7 以上 |
|ユニバーサル Windows アプリ (UWP)|Windows 10 以降と  [Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk) 14393 以降 |

次の図は、ライブ ビジュアル ツリーを使用してソース コードを開いた後、XAML ホット リロードを使用してボタンのテキストと色を変更する方法を示したものです。

![XAML ホット リロード](../debugger/media/xaml-hot-reload-using.gif)

> [!NOTE]
> Visual Studio の XAML ホット リロードは、現在、Visual Studio または Blend for Visual Studio でデバッガーをアタッチしてアプリケーションを実行している場合にのみサポートされます (**F5** キーまたは **[デバッグの開始]** )。 [環境変数を手動で設定](xaml-hot-reload-troubleshooting.md#verify-that-you-use-start-debugging-rather-than-attach-to-process)しない限り、[プロセスへのアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)を使用してこのエクスペリエンスを有効にすることはできません。

## <a name="known-limitations"></a>既知の制限事項

XAML ホット リロードには次のような既知の制限事項があります。 発生した制限を回避するには、デバッガーを停止して、操作を完了します。

|制限事項|WPF|UWP|Notes|
|-|-|-|-|
|アプリ実行中の、コントロールへのイベントの接続|サポートされていません|サポートされていません|エラーを参照: *Ensure Event Failed* (イベント確認失敗)。 WPF では、既存のイベント ハンドラーを参照できます。 UWP アプリでは、既存のイベント ハンドラーの参照はサポートされていません。|
|リソース ディクショナリ内のリソース オブジェクトの作成 (アプリのページやウィンドウ、*App.xaml* など)|Visual Studio 2019 Update 2 以降でサポートされます|サポートされています|例: `StaticResource` として使用するための、リソース ディクショナリへの `SolidColorBrush` の追加。</br>注: リソース ディクショナリへの静的リソース、スタイル コンバーター、その他の要素の記述は、XAML ホット リロードの使用中に適用または使用できます。 リソースの作成のみがサポートされていません。</br> リソース ディクショナリの `Source` プロパティの変更。|
|アプリ実行中の、新しいコントロール、クラス、ウィンドウ、その他のファイルのプロジェクトへの追加|サポートされていません|サポートされていません|なし|
|NuGet パッケージの管理 (パッケージの追加、削除、更新)|サポートされていません|サポートされていません|なし|
|{x:Bind} マークアップ拡張を使用するデータ バインディングの変更|なし|Visual Studio 2019 以降でサポートされます|これには、Windows 10 バージョン 1809 (ビルド 10.0.17763) が必要です。 Visual Studio 2017 以前のバージョンではサポートされていません。|
|x:Uid ディレクティブの変更はサポートされていない|なし|サポートされていません|なし|
|複数のプロセス | サポートされています | サポートされています | Visual Studio 2019 [バージョン 16.6](/visualstudio/releases/2019/release-notes-v16.6) 以降でサポートされます |

## <a name="error-messages"></a>エラー メッセージ

XAML ホット リロードの使用中に、次のエラーが発生する場合があります。

|エラー メッセージ|説明|
|-|-|
|Ensure Event Failed (イベント確認失敗)|このエラーは、コントロールの 1 つにイベントを接続しようとしていることを示します。これは、アプリケーションの実行中はサポートされません。|
|この変更は XAML ホット リロードではサポートされておらず、デバッグ セッション中に適用されません。|このエラーは、行おうとしている変更が XAML ホット リロードでサポートされていないことを示します。 デバッグ セッションを停止し、変更してから、デバッグ セッションを再開してください。 サポートされていないシナリオをサポートしてほしい場合は、[Visual Studio Developer Community](https://aka.ms/feedback/suggest?space=8) の新しい [機能の提案] オプションを使用してください。 |

## <a name="see-also"></a>関連項目

* [XAML ホット リロードのトラブルシューティング](xaml-hot-reload-troubleshooting.md)
* [Xamarin.Forms 用の XAML ホット リロード](/xamarin/xamarin-forms/xaml/hot-reload)
* [エディット コンティニュ (Visual C#)](../debugger/edit-and-continue-visual-csharp.md)
