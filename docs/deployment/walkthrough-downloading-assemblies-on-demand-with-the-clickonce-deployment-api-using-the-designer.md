---
title: デザイナー (ClickOnce API) を使用し、必要に応じてアセンブリをダウンロードする
description: デザイナーを使用して ClickOnce アプリケーションの特定のアセンブリをオプションとしてマークし、共通言語ランタイムで必要になったときにそれらをダウンロードする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- assemblies, downloading [ClickOnce]
- Windows applications, ClickOnce deployments
- ClickOnce deployment, on-demand download
- on-demand assemblies, ClickOnce
ms.assetid: 59a0dd5f-1cab-4f2f-b780-0ab7399905d5
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 7bb30b26e859708d295a31bd45b310897e4bcaac
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216996"
---
# <a name="walkthrough-download-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer"></a>チュートリアル: デザイナーを使用し、ClickOnce 配置 API を使用して必要に応じてアセンブリをダウンロードする
既定では、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションに含まれるすべてのアセンブリが、アプリケーションを初めて実行したときにダウンロードされます。 ただし、アプリケーションには少数のユーザーにしか使われない部分が含まれることがあります。 その場合は、そのような型を作成するときにだけアセンブリをダウンロードすることができます。 以下のチュートリアルでは、アプリケーション内の特定のアセンブリに "オプション" マークを付ける方法、および共通言語ランタイムでそのアセンブリが必要なときに <xref:System.Deployment.Application> 名前空間にあるクラスを使用してアセンブリをダウンロードする方法について説明します。

> [!NOTE]
> これを行うには、アプリケーションが完全な信頼で実行する必要があります。

> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[リセット設定](../ide/environment-settings.md#reset-settings)」を参照してください。

## <a name="create-the-projects"></a>プロジェクトを作成する

### <a name="to-create-a-project-that-uses-an-on-demand-assembly-with-visual-studio"></a>Visual Studio でオンデマンド アセンブリを使用するプロジェクトを作成するには

1. [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]で新しい Windows フォーム プロジェクトを作成します。 **[ファイル]** メニューの **[追加]** をポイントし、**[新しいプロジェクト]** をクリックします。 ダイアログ ボックスで **[クラス ライブラリ]** プロジェクトを選択し、名前を `ClickOnceLibrary`に設定します。

   > [!NOTE]
   > Visual Basic でプロジェクトのプロパティを変更し、このプロジェクトのルート名前空間を `Microsoft.Samples.ClickOnceOnDemand` または他の適切な名前空間にすることをお勧めします。 わかりやすくするため、このチュートリアルでは 2 つのプロジェクトを同じ名前空間にします。

2. `DynamicClass` という名前のプロパティを 1 つ持つ `Message`という名前のクラスを定義します。

    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_Winforms/ClickOnceLibrary/VB/Class1.vb" id="Snippet1":::
    :::code language="csharp" source="../snippets/csharp/VS_Snippets_Winforms/ClickOnceLibrary/CS/Class1.cs" id="Snippet1":::

3. **ソリューション エクスプローラー** で Windows フォーム プロジェクトを選択します。 <xref:System.Deployment.Application> アセンブリに対する参照および `ClickOnceLibrary` プロジェクトに対するプロジェクト参照を追加します。

   > [!NOTE]
   > Visual Basic でプロジェクトのプロパティを変更し、このプロジェクトのルート名前空間を `Microsoft.Samples.ClickOnceOnDemand` または他の適切な名前空間にすることをお勧めします。 わかりやすくするため、このチュートリアルでは 2 つのプロジェクトを同じ名前空間にします。

4. フォームを右クリックし、メニューの **[コードの表示]** をクリックして、次の参照をフォームに追加します。

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_Winforms/ClickOnceOnDemand/CS/Form1.cs" id="Snippet1":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_Winforms/ClickOnceOnDemand/VB/Form1.vb" id="Snippet1":::

5. このアセンブリをオンデマンドでダウンロードする次のコードを追加します。 このコードでは、 <xref:System.Collections.DictionaryBase.Dictionary%2A> ジェネリック クラスを使用してアセンブリのセットをグループ名にマップする方法を示します。 このチュートリアルではダウンロードするアセンブリが 1 つだけなので、グループに含まれるアセンブリは 1 つのみです。 実際のアプリケーションでは、アプリケーションの 1 つの機能に関連するすべてのアセンブリを同時にダウンロードすることがあります。 マッピング テーブルを使用すると、機能に属しているすべての DLL をダウンロード グループ名に関連付けることにより、これを簡単に実行できます。

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_Winforms/ClickOnceOnDemand/CS/Form1.cs" id="Snippet2":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_Winforms/ClickOnceOnDemand/VB/Form1.vb" id="Snippet2":::

6. **[表示]** メニューの **[ツールボックス]** をクリックします。 <xref:System.Windows.Forms.Button> ツールボックス **からフォームに** をドラッグします。 ボタンをダブルクリックして、 <xref:System.Windows.Forms.Control.Click> イベント ハンドラーに次のコードを追加します。

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_Winforms/ClickOnceOnDemand/CS/Form1.cs" id="Snippet3":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_Winforms/ClickOnceOnDemand/VB/Form1.vb" id="Snippet3":::

## <a name="mark-assemblies-as-optional"></a>アセンブリをオプションとしてマークする

### <a name="to-mark-assemblies-as-optional-in-your-clickonce-application-by-using-visual-studio"></a>Visual Studio を使用して ClickOnce アプリケーションでアセンブリをオプションとしてマークするには

1. **ソリューション エクスプローラー** で Windows フォーム プロジェクトを右クリックし、 **[プロパティ]** をクリックします。 **[発行]** タブを選択します。

2. **[アプリケーション ファイル]** ボタンをクリックします。

3. *ClickOnceLibrary.dll* のリストを探します。 **[発行の状況]** ドロップダウン ボックスを **[含む]** に設定します。

4. **[グループ]** ドロップダウン ボックスを展開し、 **[新規]** を選択します。 新しいグループ名として「 `ClickOnceLibrary` 」と入力します。

5. 「[方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)」の説明に従って、アプリケーションの発行を続行します。

### <a name="to-mark-assemblies-as-optional-in-your-clickonce-application-by-using-manifest-generation-and-editing-tool--graphical-client-mageuiexe"></a>マニフェストの生成および編集ツールを使用して ClickOnce アプリケーションでアセンブリをオプションとしてマークするには — グラフィカル クライアント (MageUI.exe)

1. 「[チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)」の説明に従って、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] マニフェストを作成します。

2. MageUI.exe を終了する前に、配置のアプリケーション マニフェストを含むタブを選択し、そのタブで **[ファイル]** タブを選択します。

3. アプリケーション ファイルの一覧で ClickOnceLibrary.dll を探し、 **[ファイルの種類]** 列を **[なし]** に設定します。 **[グループ]** 列に「 `ClickOnceLibrary.dll`」と入力します。

## <a name="test-the-new-assembly"></a>新しいアセンブリをテストする

オンデマンド アセンブリをテストするには

1. [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]で配置されたアプリケーションを起動します。

2. メイン フォームが表示されたら、 <xref:System.Windows.Forms.Button>をクリックします。 メッセージ ボックスに "Hello, World!" と表示されます。

## <a name="see-also"></a>関連項目

- <xref:System.Deployment.Application.ApplicationDeployment>
