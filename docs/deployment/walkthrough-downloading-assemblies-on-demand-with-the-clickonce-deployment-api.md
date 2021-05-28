---
title: 必要に応じてアセンブリをダウンロードする (ClickOnce API)
description: ClickOnce アプリケーションの特定のアセンブリをオプションとしてマークし、共通言語ランタイムで必要になったときにそれらをダウンロードする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- assemblies, downloading [ClickOnce]
- ClickOnce deployment, on-demand download
- on-demand assemblies, ClickOnce
ms.assetid: d20e2789-8621-4806-b5b7-841122da1456
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 316be1f0a8fa881f781d983cfe9ed663e5907749
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216905"
---
# <a name="walkthrough-download-assemblies-on-demand-with-the-clickonce-deployment-api"></a>チュートリアル: ClickOnce 配置 API を使用して必要に応じてアセンブリをダウンロードする
既定では、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションに含まれるすべてのアセンブリは、アプリケーションの初回実行時にダウンロードされます。 ただし、アプリケーションには少数のユーザーにしか使われない部分が含まれることがあります。 その場合は、そのような型を作成するときにだけアセンブリをダウンロードすることができます。 以下のチュートリアルでは、アプリケーション内の特定のアセンブリに "オプション" マークを付ける方法、および共通言語ランタイム (CLR) でそのアセンブリが必要なときに <xref:System.Deployment.Application> 名前空間にあるクラスを使用してアセンブリをダウンロードする方法について説明します。

> [!NOTE]
> これを行うには、アプリケーションが完全な信頼で実行する必要があります。

## <a name="prerequisites"></a>前提条件
 このチュートリアルを実行するには、次のいずれかのコンポーネントが必要になります。

- Windows SDK。 Windows SDK は、Microsoft ダウンロード センターからダウンロードできます。

- 見ることができます。

## <a name="create-the-projects"></a>プロジェクトを作成する

#### <a name="to-create-a-project-that-uses-an-on-demand-assembly"></a>オンデマンド アセンブリを使用するプロジェクトを作成するには

1. ClickOnceOnDemand という名前のディレクトリを作成します。

2. Windows SDK コマンド プロンプトまたは [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] コマンド プロンプトを開きます。

3. ClickOnceOnDemand ディレクトリに変更します。

4. 次のコマンドを使って、公開キーと秘密キーのペアを生成します。

   ```cmd
   sn -k TestKey.snk
   ```

5. メモ帳などのテキスト エディターを使って、`Message` という名前の単一プロパティを持つ、`DynamicClass` という名前のクラスを定義します。

    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_Winforms/ClickOnceLibrary/VB/Class1.vb" id="Snippet1":::
    :::code language="csharp" source="../snippets/csharp/VS_Snippets_Winforms/ClickOnceLibrary/CS/Class1.cs" id="Snippet1":::

6. 使用する言語に応じて、テキストを *ClickOnceLibrary.cs* または *ClickOnceLibrary.vb* というファイル名にし、*ClickOnceOnDemand* ディレクトリに保存します。

7. ファイルをアセンブリにコンパイルします。

   ```csharp
   csc /target:library /keyfile:TestKey.snk ClickOnceLibrary.cs
   ```

   ```vb
   vbc /target:library /keyfile:TestKey.snk ClickOnceLibrary.vb
   ```

8. アセンブリの公開キー トークンを取得するには、次のコマンドを使用します。

   ```cmd
   sn -T ClickOnceLibrary.dll
   ```

9. テキスト エディターを使って新しいファイルを作成し、次のコードを入力します。 このコードでは、必要に応じて ClickOnceLibrary アセンブリをダウンロードする Windows フォーム アプリケーションが作成されます。

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_Winforms/ClickOnceOnDemandCmdLine/CS/Form1.cs" id="Snippet1":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_Winforms/ClickOnceOnDemandCmdLine/VB/Form1.vb" id="Snippet1":::

10. コードで、<xref:System.Reflection.Assembly.LoadFile%2A> への呼び出しを探します。

11. `PublicKeyToken` を、先ほど取得した値に設定します。

12. ファイルを *Form1.cs* または *Form1.vb* として保存します。

13. 次のコマンドを使って、実行可能ファイルにコンパイルします。

    ```csharp
    csc /target:exe /reference:ClickOnceLibrary.dll Form1.cs
    ```

    ```vb
    vbc /target:exe /reference:ClickOnceLibrary.dll Form1.vb
    ```

## <a name="mark-assemblies-as-optional"></a>アセンブリをオプションとしてマークする

#### <a name="to-mark-assemblies-as-optional-in-your-clickonce-application-by-using-mageuiexe"></a>MageUI.exe を使ってアセンブリを ClickOnce アプリケーションでのオプションとしてマークするには

1. *MageUI.exe* を使用し、「[チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)」の説明に従って、アプリケーション マニフェストを作成します。 アプリケーション マニフェストについては、次の設定を使用します。

    - アプリケーション マニフェストの名前は `ClickOnceOnDemand` にします。

    - **[ファイル]** ページの *[ClickOnceLibrary.dll]* 行で、 **[ファイルの種類]** 列を **[なし]** に設定します。

    - **[ファイル]** ページの *[ClickOnceLibrary.dll]* 行で、 **[グループ]** 列に「`ClickOnceLibrary.dll`」と入力します。

2. *MageUI.exe* を使用し、「[チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)」の説明に従って、配置マニフェストを作成します。 配置マニフェストについては、次の設定を使用します。

    - 配置マニフェストの名前は `ClickOnceOnDemand` にします。

## <a name="testing-the-new-assembly"></a>新しいアセンブリをテストする

#### <a name="to-test-your-on-demand-assembly"></a>オンデマンド アセンブリをテストするには

1. [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] の配置を Web サーバーにアップロードします。

2. 配置マニフェストの URL を入力して、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] を使って配置されたアプリケーションを Web ブラウザーから起動します。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーション `ClickOnceOnDemand` を呼び出し、adatum.com のルート ディレクトリにアップロードした場合、URL は次のようになります。

   ```
   http://www.adatum.com/ClickOnceOnDemand/ClickOnceOnDemand.application
   ```

3. メイン フォームが表示されたら、 <xref:System.Windows.Forms.Button>をクリックします。 メッセージ ボックス ウィンドウに "Hello, World!" という文字列が表示されます。

## <a name="see-also"></a>関連項目
- <xref:System.Deployment.Application.ApplicationDeployment>