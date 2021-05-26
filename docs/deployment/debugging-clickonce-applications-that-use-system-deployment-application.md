---
title: System.Deployment.Application を使用する ClickOnce アプリをデバッグする
description: System.Deployment.Application によって提供される配置オブジェクト モデルにアクセスして、高度な ClickOnce 配置機能を使用およびカスタマイズする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, debugging
- debugging, ClickOnce applications
- debugging, System.Deployment
- deploying applications [ClickOnce], debugging
ms.assetid: 86f31948-2ca8-47c0-8e8b-c2b817bbf79f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d6a014afff6c26b8cfe8f4f7fae508f78ef5905f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99912245"
---
# <a name="debug-clickonce-applications-that-use-systemdeploymentapplication"></a>System.Deployment.Application を使用する ClickOnce アプリケーションのデバッグ
[!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] では、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置を使用して、アプリケーションの更新方法を構成できます。 ただし、高度な [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置機能を使用したり、カスタマイズしたりする必要がある場合は、<xref:System.Deployment.Application> によって提供される配置オブジェクト モデルにアクセスする必要があります。 <xref:System.Deployment.Application> API は、次のような高度なタスクに使用できます。

- アプリケーションでの "今すぐ更新" オプションの作成

- さまざまなアプリケーション コンポーネントの条件付きオンデマンド ダウンロード

- アプリケーションに直接統合される更新プログラム

- クライアント アプリケーションが常に最新の状態であることの保証

  <xref:System.Deployment.Application> API は [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] テクノロジを使用してアプリケーションが配置されている場合にのみ機能するため、それらをデバッグする唯一の方法は、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] を使用してアプリケーションを配置し、それにアタッチしてデバッグすることです。 このコードはアプリケーションの起動時に実行されることが多く、デバッガーをアタッチする前に実行されるため、デバッガーを早期にアタッチするのが難しい可能性があります。 解決策として、更新チェック コードまたはオンデマンド コードの前に中断 (Visual Basic プロジェクトの場合は停止) を配置します。

  推奨されるデバッグの手法は次のとおりです。

1. 開始する前に、シンボル (.pdb) ファイルとソース ファイルがアーカイブされていることを確認します。

2. アプリケーションのバージョン 1 を配置します。

3. 新しい空のソリューションを作成します。 **[ファイル]** メニューから **[新規作成]**、**[プロジェクト]** の順にクリックします。 **[新しいプロジェクト]** ダイアログ ボックスで、 **[その他のプロジェクトの種類]** ノードを開き、 **[Visual Studio ソリューション]** フォルダーを選択します。 **[テンプレート]** ペインで **[空のソリューション]** を選択します。

4. この新しいソリューションのプロパティに、アーカイブされたソースの場所を追加します。 **ソリューション エクスプローラー** で、ソリューション ノードを右クリックし、 **[プロパティ]** をクリックします。 **[プロパティ ページ]** ダイアログ ボックスで、 **[デバッグ ソース ファイル]** を選択し、アーカイブされたソース コードのディレクトリを追加します。 ソース ファイルのパスは .pdb ファイルに記録されているため、これを行わないと、デバッガーによって古いソース ファイルが検出されます。 デバッガーで古いソース ファイルが使用されている場合、ソースが一致しないことを通知するメッセージが表示されます。

5. デバッガーが *.pdb* ファイルを検出できることを確認します。 それらをアプリケーションと共に配置した場合は、デバッガーによって自動的に検出されます。 常に、対象のアセンブリの隣が最初に確認されます。 それ以外の場合は、 **[シンボル ファイル (.pdb) の場所]** にアーカイブ パスを追加する必要があります (このオプションにアクセスするには、 **[ツール]** メニューの **[オプション]** をクリックし、 **[デバッグ]** ノードを開いて **[シンボル]** をクリックします)。

6. `CheckForUpdate` から `Download`/`Update` までのメソッド呼び出しの動作をデバッグします。

    たとえば、更新コードは次のようになります。

   ```vb
       Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click
           If My.Application.Deployment.IsNetworkDeployed Then

               If (My.Application.Deployment.CheckForUpdate()) Then

                   My.Application.Deployment.Update()
                   Application.Restart()

               End If

           End If
       End Sub
   ```

7. バージョン 2 を配置します。

8. バージョン 2 の更新プログラムをダウンロードするときに、デバッガーをバージョン 1 アプリケーションにアタッチしてみます。 代わりに、`System.Diagnostics.Debugger.Break` メソッド (Visual Basic では単に `Stop`) を使用することもできます。 これらのメソッド呼び出しは運用コードに残さないでください。

    たとえば、Windows フォーム アプリケーションを開発中であり、更新ロジックを含むこのメソッドのイベント ハンドラーがあるとします。 それをデバッグするには、ボタンを押す前にアタッチし、ブレークポイントを設定するだけでかまいません (必ず適切なアーカイブ ファイルを開き、そこにブレークポイントを設定してください)。

   <xref:System.Deployment.Application.ApplicationDeployment.IsNetworkDeployed%2A> プロパティを使用して <xref:System.Deployment.Application> API を呼び出すのは、アプリケーションが配置されている場合だけです。[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] でのデバッグ中に、この API を呼び出すことはできません。

## <a name="see-also"></a>関連項目
- <xref:System.Deployment.Application>