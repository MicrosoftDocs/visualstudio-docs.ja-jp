---
title: VSTO アドインのパフォーマンスを向上させる
description: Office アプリケーション用に作成した VSTO アドインを最適化して、そのアドインの開始、終了、また、項目を開くなどのタスクの実行をすばやく行えるようにする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 29035f4867421ed3f05e5f0c3a5c196f58b7ab34
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825122"
---
# <a name="improve-the-performance-of-a-vsto-add-in"></a>VSTO アドインのパフォーマンスを向上させる
  Office アプリケーション用に作成した VSTO アドインを最適化して、そのアドインの開始、終了、また、項目を開くなどのタスクの実行を素早く行えるようにして、ユーザー エクスペリエンスを向上させることができます。 VSTO アドインが Outlook を対象にしている場合は、不十分なパフォーマンスが原因で VSTO アドインが無効にされる可能性を低くすることができます。 次の方針を導入すると、VSTO アドインのパフォーマンスを向上させることができます。

- [必要に応じた VSTO アドインの読み込み](#Load)。

- [Windows インストーラーを使用した Office ソリューションの発行](#Publish)。

- [リボン リフレクションのバイパス](#Bypass)。

- [負荷の高い操作を単独の実行スレッドで実行](#Perform)。

  Outlook VSTO アドインを最適化する方法の詳細については、「[VSTO アドインを有効に保つためのパフォーマンス基準](/previous-versions/office/jj228679(v=office.15)#performance-criteria-for-keeping-add-ins-enabled)」を参照してください。

## <a name="load-vsto-add-ins-on-demand"></a><a name="Load"></a> 必要に応じた VSTO アドインの読み込み
 次の状況でのみ読み込まれるように VSTO アドインを構成できます。

- VSTO アドインのインストール後にユーザーがアプリケーションを初めて起動するとき。

- それ以降にアプリケーションを起動した後、ユーザーが初めて VSTO アドインを操作するとき。

  たとえば、ユーザーが **[自分のデータを取得]** というラベルの付いたカスタム ボタンをクリックしたときにワークシートにデータを取り込む VSTO アドインがあるとします。 **[自分のデータを取得]** ボタンがリボンに表示されるように、アプリケーションはこの VSTO アドインを少なくとも 1 回読み込む必要があります。 ただし、ユーザーが次にアプリケーションを起動するときには、この VSTO アドインは読み込まれません。 VSTO アドインが読み込まれるのは、ユーザーが **[自分のデータを取得]** ボタンをクリックしたときのみです。

### <a name="to-configure-a-clickonce-solution-to-load-vsto-add-ins-on-demand"></a>必要に応じて VSTO アドインを読み込むように ClickOnce ソリューションを構成するには

1. **ソリューション エクスプローラー** で、プロジェクト ノードを選択します。

2. メニュー バーで **[表示]**  >  **[プロパティ ページ]** の順に選びます。

3. **[発行]** タブの **[オプション]** をクリックします。

4. **[発行オプション]** ダイアログ ボックスで、 **[Office の設定]** リスト項目を選択し、 **[必要に応じて読み込む]** オプションを選択してから、 **[OK]** をクリックします。

### <a name="to-configure-a-windows-installer-solution-to-load-vsto-add-ins-on-demand"></a>必要に応じて VSTO アドインを読み込むように Windows インストーラー ソリューションを構成するには

1. レジストリで、**_Root_\Software\Microsoft\Office\\_ApplicationName_\Addins\\_Add-in ID_** キーの `LoadBehavior` エントリを **0x10** に設定します。

     詳細については、「[VSTO アドインのレジストリ エントリ](../vsto/registry-entries-for-vsto-add-ins.md)」を参照してください。

### <a name="to-configure-a-solution-to-load-vsto-add-ins-on-demand-while-you-debug-the-solution"></a>ソリューションのデバッグ中に必要に応じて VSTO アドインを読み込むようにソリューションを構成するには

1. **_Root_\Software\Microsoft\Office\\_ApplicationName_\Addins\\_Add-in ID_** キーの `LoadBehavior` エントリを **0x10** に設定するスクリプトを作成します。

     このスクリプトの例を次のコードに示します。

    ```cmd/sh
    [HKEY_CURRENT_USER\Software\Microsoft\Office\Excel\Addins\MyAddIn]
    "Description"="MyAddIn"
    "FriendlyName"="MyAddIn"
    "LoadBehavior"=dword:00000010
    "Manifest"="c:\\Temp\\MyAddIn\\bin\\Debug\\MyAddIn.vsto|vstolocal"

    ```

2. スクリプトを使用してレジストリを更新するビルド後のイベントを作成します。

     次のコードに、ビルド後のイベントに追加できるコマンド文字列の例を示します。

    ```cmd/sh
    regedit /s "$(SolutionDir)$(SolutionName).reg"

    ```

     C# プロジェクト内でビルド後のイベントを作成する方法の詳細については、「[方法 : ビルド イベントを指定する &#40;C&#35;&#41;](../ide/how-to-specify-build-events-csharp.md)」を参照してください。

     Visual Basic プロジェクト内でビルド後のイベントを作成する方法の詳細については、「[方法 : ビルド イベントを指定する &#40;Visual Basic&#41;](../ide/how-to-specify-build-events-visual-basic.md)」を参照してください。

## <a name="publish-office-solutions-by-using-windows-installer"></a><a name="Publish"></a> Windows インストーラーを使用した Office ソリューションの発行
 Windows インストーラーを使用してソリューションを発行する場合は、Visual Studio 2010 Tools for Office ランタイムは、VSTO アドインを読み込むときに次の手順をスキップします。

- マニフェスト スキーマの検証。

- 更新プログラムの自動的な確認。

- 配置マニフェストのデジタル署名の検証。

  > [!NOTE]
  > このアプローチは、ユーザーのコンピューターの安全な場所に VSTO アドインを配置する場合は不要です。

  詳細については、「[Windows インストーラーを使用した Office ソリューションの配置](../vsto/deploying-a-vsto-solution-by-using-windows-installer.md)」を参照してください。

## <a name="bypass-ribbon-reflection"></a><a name="Bypass"></a> リボン リフレクションのバイパス
 [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)] を使用してソリューションをビルドする場合は、ソリューションを配置するときに、ユーザーが Visual Studio 2010 Tools for Office ランタイムの最新バージョンを既にインストールしていることを確認します。 VSTO ランタイムの古いバージョンでは、リボンのカスタマイズを識別するために、ソリューションのアセンブリのリフレクションが実行されていました。 このプロセスを実行すると、VSTO アドインの読み込み速度がさらに低下する可能性があります。

 別の方針として、Visual Studio 2010 Tools for Office ランタイムのどのバージョンを使用する場合でも、リボンのカスタマイズを識別することを目的としたリフレクションを防止することもできます。 この方針に従うには、`CreateRibbonExtensibility` メソッドをオーバーライドし、明示的にリボン オブジェクトを返します。 VSTO アドインにリボンのカスタマイズが何も含まれていない場合は、メソッド内で `null` を返します。

 次の例では、フィールドの値に基づいてリボン オブジェクトを返します。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_ribbon_choose_ribbon_4/ThisWorkbook.vb" id="Snippet1":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_ribbon_choose_ribbon_4/ThisWorkbook.cs" id="Snippet1":::

## <a name="perform-expensive-operations-in-a-separate-execution-thread"></a><a name="Perform"></a> 負荷の高い操作を単独の実行スレッドで実行
 時間を要するタスク (長時間実行されるタスク、データベース接続、または他の種類のネットワークの呼び出しなど) を単独のスレッドで実行することを検討してください。 詳細については、「[Office でのスレッドのサポート](../vsto/threading-support-in-office.md)」を参照してください。

> [!NOTE]
> Office オブジェクト モデルを呼び出すすべてのコードは、メイン スレッドで実行する必要があります。

## <a name="see-also"></a>関連項目

- [VSTO アドインの必要に応じた読み込み](/archive/blogs/andreww/demand-loading-vsto-add-ins)
- [Office アドイン内での CLR の遅延読み込み](/archive/blogs/andreww/delay-loading-the-clr-in-office-add-ins)
- [Visual Studio を使用して Office 用 VSTO アドインを作成する](create-vsto-add-ins-for-office-by-using-visual-studio.md)