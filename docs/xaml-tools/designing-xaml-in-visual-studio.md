---
title: Visual Studio と Blend for Visual Studio での XAML の設計
titleSuffix: ''
description: XAML で UI とエクスペリエンスを構築するための Visual Studio と Blend for Visual Studio のビジュアル デザイン ツールの機能について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/28/2020
ms.topic: conceptual
ms.assetid: 288e2415-9fcf-408e-bc35-9848315e14fd
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.openlocfilehash: fc6c05b925c8dac5c488ce3eea79ca683b590b72
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99876421"
---
# <a name="design-xaml-in-visual-studio-and-blend-for-visual-studio"></a>Visual Studio および Blend for Visual Studio での XAML の設計

Visual Studio と Blend for Visual Studio の両方には、さまざまなアプリの種類に合わせて XAML を使用して魅力的なユーザー インターフェイスとリッチ メディア体験を構築するための視覚的なツールが用意されています。 両方の統合開発環境 (IDE) は、Visual XAML エディター (デザイナー) などの共通の機能セットを共有しています。 WPF プラットフォームと UWP プラットフォームをサポートする Blend for Visual Studio には、ビジュアルの状態をデザインし、アニメーションを作成するための追加ツールがあります。

Visual Studio と Blend for Visual Studio を自在に切り替えることができるだけでなく、両方の IDE で同時に同じプロジェクトを開くこともできます。 ある IDE で XAML ファイルに保存した変更は、他の IDE に切り替える際に、自動再読み込みを使用して適用できます。 いずれかの IDE で **[ツール]** 、 **[オプション]** 、 **[環境]** 、 **[ドキュメント]** の順に移動し、リロード動作を制御できます。

## <a name="installation"></a>インストール

- WPF アプリを作成するには、Visual Studio に **.NET デスクトップ開発** ワークロードをインストールします。 Blend for Visual Studio もインストールされます。

     ![Visual Studio インストーラーからの .NET デスクトップ開発ワークロードのスクリーンショット](../xaml-tools/media/dotnet-desktop-dev-workload.png)

- UWP アプリを作成するには、Visual Studio に **ユニバーサル Windows プラットフォーム開発** ワークロードをインストールします。 Blend for Visual Studio もインストールされます。

     ![Visual Studio インストーラーからのユニバーサル Windows プラットフォーム開発ワークロードのスクリーンショット](../xaml-tools/media/uwp-workload.png)

- Xamarin.Forms アプリを作成するには、Visual Studio に **.NET によるモバイル開発** ワークロードをインストールするには Blend for Visual Studio はインストールされて *いません*。Blend では、Xamarin.Forms アプリがサポートされません。

     ![Visual Studio インストーラーからの .NET ワークロードを使用したモバイル開発のスクリーンショット](../xaml-tools/media/mobile-dev-dotnet-workload.png)

## <a name="shared-capabilities"></a>共有機能

最も基本的な開発タスクに関しては、わずかな違いがいくつかあるものの、Visual Studio と Blend for Visual Studio で同一のウィンドウおよび機能のセットを共有しています。 いくつかの特徴を次に示します。

- **IntelliSense:** いずれの IDE でも、ステートメント入力候補など、IntelliSense 機能がサポートされています。

- **デバッグ:** 実行中のアプリをデバッグするためにブレークポイントを設定したり、[ホット リロード](../xaml-tools/xaml-hot-reload.md)を利用してアプリの実行中に XAML コードを変更したりするなど、[Visual Studio](inspect-xaml-properties-while-debugging.md) と [Blend for Visual Studio](../xaml-tools/debug-xaml-in-blend.md) でデバッグすることができます。 Visual Studio とデバッグ機能の一貫性を保つため、Blend for Visual Studio には Visual Studio の大半のデバッグ ウィンドウとツールバーが含まれています。

- **ファイルの再読み込み:** XAML ファイルは Visual Studio または Blend for Visual Studio で編集できます。 編集後に保存されたファイルは、IDE を切り替えると自動的に再読み込みされます。 いずれかの IDE で **[ツール]** 、 **[オプション]** 、 **[環境]** 、 **[ドキュメント]** の順に移動し、リロード動作を制御できます。

- **レイアウトの同期と設定:** Visual Studio または Blend for Visual Studio のためのデザイン カスタマイズ ツール ウィンドウのレイアウトや設定は、同じ個人用アカウントでサインインしたとき、デバイスやバージョンの間で同期されます。 [複数のコンピューター間での設定の同期](../ide/synchronized-settings-in-visual-studio.md)に関するページを参照してください。

## <a name="advanced-capabilities-in-blend-for-visual-studio"></a>Blend for Visual Studio での高度な機能

生産性を高めるため、次のようなタスクには Blend for Visual Studio の使用をご検討ください。 Blend for Visual Studio が Visual Studio デザイナーまたはコード単独より多くの機能を提供する領域は以下のとおりです。

| タスク | Visual Studio | Blend for Visual Studio | 詳細情報 |
| - | - | - | - |
| **ビジュアルの状態をデザインする** | ビジュアルの状態のデザインに便利なツールはありません。プログラミングで作成する必要があります。 | デザイン ツールを使用し、コントロールの状態に基づき、コントロールの外観を変更します。 | [ビジュアルの状態](modify-the-style-of-objects-in-blend.md#visual-states) |
| **アニメーションを作成する** |アニメーション用のデザイン ツールはないため、プログラムで作成する必要があります。 これを行うには、WPF におけるアニメーションおよびタイミング システムを理解し、広範なコーディングの専門知識を持っている必要があります。|アニメーションを視覚的に作成し、Blend for Visual Studio でプレビューできます。 これは、コーディングでアニメーションを構築するよりもすばやく正確です。 ユーザーとの対話を処理するトリガーを追加できるほか、コードに切り替えてイベント ハンドラーとその他の機能を追加することができます。|[オブジェクトのアニメーション化](../xaml-tools/animate-objects-in-xaml-designer.md)|
|**簡単に操作できるよう、図形やテキストをパスに変換する**|サポートされていません。|図形 (四角形、楕円など) をパスに変換することで、図形に対して軽微な変更や劇的な変更を行えます。そうすることで、より良い編集コントロールができます。 形状を変更したり、パスを結合するとともに、複数の図形から複合パスを作成することができます。<br /><br />さらに、テキスト ブロックをパスに変換して、ベクター イメージとして操作することもできます。|[図形とパスの描画](../xaml-tools/draw-shapes-and-paths.md)|
|**コントロール、テンプレート、スタイルを編集する**|コーディングおよび WPF のスタイルとテンプレートの知識が必要です。|イメージをコントロールに変換します。<br /><br />コントロール、スタイル、テンプレートを数回マウスでクリックするだけで変更するには、テンプレート編集ツールを使用します。<br /><br />たとえば、Blend for Visual Studio のスタイル リソースを使用して一般的な WPF コントロール (ボタン、リスト ボックス、スクロール バー、メニューなど) を実装し、Blend for Visual Studio で色、スタイル、または基になるテンプレートを直接変更できます。 次に、必要な場合はコードに切り替えてタッチを仕上げます。|[オブジェクト スタイルを変更する](modify-the-style-of-objects-in-blend.md)|
|**UI をデータに接続する**|SQL Server データベース、WCF または Web サービス、オブジェクト、SharePoint リストなどのリソースからデータ ソースを作成し、そのデータ ソースを UI コントロールにバインドできます。<br /><br />デザイン時のデータは、対話型のデザイン エクスペリエンスのため手動で作成する必要があります。|.NET Framework アプリのために、試作品とテストのためのサンプル データを簡単に作成します。 準備ができたら、ライブ データに切り替えます。<br /><br />Blend for Visual Studio のデータ生成機能は並外れており (その場で迅速かつ簡単に、名前、番号、URL、写真の追加が可能)、多くの時間を節約できます。<br /><br />ライブ データの場合は、UI コントロールを XML ファイルまたは任意の CLR データ ソースにバインドできます。|[データの表示](display-data-in-blend.md)|

高度な XAML デザインの詳細については、「[Blend for Visual Studio を使用して UI を作成する](../xaml-tools/creating-a-ui-by-using-blend-for-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [XAML の概要](xaml-overview.md)
- [Blend for Visual Studio 概要](creating-a-ui-by-using-blend-for-visual-studio.md)
