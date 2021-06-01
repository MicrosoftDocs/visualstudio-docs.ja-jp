---
title: ClickOnce を使用して Office ソリューションを配置する
description: ClickOnce を使用すると、より少ない手順で Office ソリューションを配置できます。 更新プログラムを発行する場合は、ソリューションはそれらを自動的に検出してインストールします。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, deploying solutions
- ClickOnce deployment [Office development in Visual Studio], deploying solutions
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 03b4f3d2f1a342f6c1977d616793634500850e7a
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828619"
---
# <a name="deploy-an-office-solution-by-using-clickonce"></a>ClickOnce を使用して Office ソリューションを配置する
  ClickOnce を使用する場合は、少しの手順で Office ソリューションを配置できます。 更新プログラムを発行する場合は、ソリューションはそれらを自動的に検出してインストールします。 ただし、ClickOnce を使用する場合は、コンピューターのユーザーごとに、ソリューションを個別にインストールする必要があります。 したがって、複数のユーザーが同じコンピューターでソリューションを実行する場合は、Windows インストーラー ( *.msi*) の使用を検討する必要があります。

## <a name="in-this-topic"></a>このトピックの内容

- [ソリューションの発行](#Publish)

- [ソリューションに信頼を付与する方法の決定](#Trust)

- [ユーザーによるソリューションのインストールの支援](#Helping)

- [ソリューションのドキュメントをエンド ユーザーのコンピューターに配置 (ドキュメント レベルのカスタマイズのみ)](#Put)

- [ソリューションのドキュメントを、SharePoint を実行しているサーバーに配置 (ドキュメント レベルのカスタマイズのみ)](#SharePoint)

- [カスタム インストーラーを作成する](#Custom)

- [更新プログラムを発行する](#Update)

- [ソリューションのインストール場所の変更](#Location)

- [ソリューションを以前のバージョンにロールバック](#Roll)

  Windows インストーラー ファイルを作成して Office ソリューションを配置する方法について詳しくは、「[Windows インストーラーを使用した Office ソリューションの配置](../vsto/deploying-a-vsto-solution-by-using-windows-installer.md)」をご覧ください。

## <a name="publish-the-solution"></a><a name="Publish"></a> ソリューションを発行する
 ソリューションは、**発行ウィザード** または **プロジェクト デザイナー** を使用して発行できます。 この手順では、発行オプションの完全なセットが利用できる **プロジェクト デザイナー** を使用します。 「[発行ウィザード &#40;Visual Studio での Office 開発&#41;](../vsto/publish-wizard-office-development-in-visual-studio.md)」を参照してください。

#### <a name="to-publish-the-solution"></a>ソリューションを発行するには

1. **ソリューション エクスプローラー** で、自分のプロジェクトに合わせて名前を付けたノードを選択します。

2. メニュー バーで、 **[プロジェクト]**、[ *ProjectName* **のプロパティ]**」を参照してください。

3. 次の図に示すように、**プロジェクト デザイナー** で **[発行]** タブを選択します。

    ![プロジェクト デザイナーの [発行] タブ](../vsto/media/vsto-publishtab.png "プロジェクト デザイナーの [発行] タブ")

4. **[発行フォルダーの場所 (FTP サーバーまたはファイル パス)]** ボックスに、**プロジェクト デザイナー** によってソリューション ファイルをコピーするフォルダーのパスを入力します。

    次のいずれかの種類のパスを入力できます。

   - ローカル パス (たとえば、*C:\FolderName\FolderName*)。

   - ネットワーク上にあるフォルダーの汎用名前付け規則 (UNC) パス (たとえば、 *\\\ServerName\FolderName*)。

   - 相対パス (たとえば、プロジェクトが既定で公開されるフォルダーである *PublishFolder\\* )。

5. **[インストール フォルダーの URL]** ボックスに、エンド ユーザーが目にすることになる、ソリューションの完全修飾パスを入力します。

    まだ位置が確定していない場合は、このフィールドに何も入力しないでください。 既定では、ClickOnce はこのフォルダーの中で、ユーザーがソリューションをインストールするための更新プログラムを検索します。

6. **[必須コンポーネント]** ボタンをクリックします。

7. **[必須コンポーネント]** ダイアログ ボックスの **[必須コンポーネントをインストールするセットアップ プログラムを作成する]** チェック ボックスをオンにします。

8. **[インストールする必須コンポーネントを選択する]** リストで、 **[Windows インストーラー 4.5]** 、および適切な .NET Framework パッケージに対応するチェック ボックスをオンにします。

    たとえば、ソリューションが [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] を対象とする場合は、 **[Windows インストーラー 4.5]** と **[Microsoft .NET Framework 4.5 Full]** の各チェック ボックスをオンにします。

9. ソリューションが .NET Framework 4.5 を対象とする場合は、 **[Visual Studio 2010 Tools for Office Runtime]** チェック ボックスもオンにします。

    > [!NOTE]
    > 既定では、このチェック ボックスは表示されません。 このチェック ボックスを表示するには、ブートストラップ パッケージを作成する必要があります。 [Visual Studio 2012 を使用した Office 2013 VSTO アドイン用のブートストラップ パッケージの作成](create-vsto-add-ins-for-office-by-using-visual-studio.md)に関する記事を参照してください。

10. **[必須コンポーネントのインストール場所を指定してください]** の下に表示されるオプションのいずれかを選択し、 **[OK]** をクリックします。

     各オプションの説明を次の表に示します。

    |オプション|説明|
    |------------|-----------------|
    |**必須コンポーネントをコンポーネントの開発元の Web サイトからダウンロードする**|ユーザーは、販売元からこれらの必須コンポーネントをダウンロードしてインストールするように求められます。|
    |**アプリケーションと同じ場所から必須コンポーネントをダウンロードする**|必要なソフトウェアは、ソリューションと共にインストールされます。 このオプションを選択すると、Visual Studio はすべての必須パッケージを発行場所に自動的にコピーします。 このオプションを使用するには、必須パッケージが開発用コンピューターに存在する必要があります。|
    |**次の場所から必須コンポーネントをダウンロード**|Visual Studio は、指定した場所にすべての必須パッケージをコピーし、ソリューションと共にそれらをインストールします。|

     「[[必須コンポーネント] ダイアログ ボックス](../ide/reference/prerequisites-dialog-box.md)」を参照してください。

11. **[更新プログラム]** ボタンをクリックし、各エンド ユーザーが VSTO アドインまたはカスタマイズの更新を確認する頻度を指定してから、 **[OK]** をクリックします。

    > [!NOTE]
    > CD またはリムーバブル ドライブを使用して配置を行う場合は、 **[更新の確認をしない]** オプション ボタンをオンにします。

     更新を発行する方法について詳しくは、「[更新プログラムの発行](#Update)」をご覧ください。

12. **[オプション]** ボタンをクリックし、 **[オプション]** ダイアログ ボックス内のオプションをレビューしてから、 **[OK]** をクリックします。

13. **[今すぐ発行]** ボタンをクリックします。

     この手順で既に指定した発行フォルダーに、Visual Studio は次のフォルダーとファイルを追加します。

    - **Application Files** フォルダー。

    - セットアップ プログラム。

    - 最新バージョンの配置マニフェストを指す配置マニフェスト。

      **Application Files** フォルダーには、発行する各バージョンに対応するサブフォルダーが含まれます。 バージョン固有の各サブフォルダーには、次のファイルが含まれます。

    - アプリケーション マニフェスト。

    - 配置マニフェスト。

    - カスタマイズ アセンブリ。

      次の図に、Outlook VSTO アドインに対応する発行フォルダーの構造を示します。

      ![発行フォルダーの構造](../vsto/media/publishfolderstructure.png "発行フォルダーの構造")

    > [!NOTE]
    > ClickOnce ではアセンブリに *.deploy* 拡張子が追加されます。これにより、セキュリティで保護されたインターネット インフォメーション サービス (IIS) がインストールされている場合でも、安全ではない拡張子を理由にファイルがブロックされることはなくなります。 ユーザーがソリューションをインストールすると、ClickOnce によって *.deploy* 拡張子が削除されます。

14. この手順で既に指定したインストール場所に、ソリューション ファイルをコピーします。

## <a name="decide-how-you-want-to-grant-trust-to-the-solution"></a><a name="Trust"></a> ソリューションに信頼を付与する方法を決定する
 ユーザーのコンピューターでソリューションを実行する前に、次のいずれかの方法で信頼を付与する必要があります。そうしない場合は、ユーザーはソリューションをインストールするときに、信頼プロンプトに応答する必要が生じます。 ソリューションに信頼を付与するには、既知の信頼される発行者を特定する証明書を使用してマニフェストに署名します。 「[アプリケーション マニフェストと配置マニフェストに署名することによってソリューションを信頼する](../vsto/granting-trust-to-office-solutions.md#Signing)」を参照してください。

 ドキュメント レベルのカスタマイズを配置し、ユーザーのコンピューター上のフォルダーにドキュメントを配置するか、または SharePoint サイトでドキュメントを使用できるようにする場合は、ドキュメントの場所が Office によって信頼されていることを確認してください。 「[ドキュメントに信頼を付与する](../vsto/granting-trust-to-documents.md)」を参照してください。

## <a name="help-users-install-the-solution"></a><a name="Helping"></a> ユーザーによるソリューションのインストールを支援する
 ユーザーは、セットアップ プログラムを実行するか、配置マニフェストを開くか、またはドキュメント レベルのカスタマイズ時にドキュメントを直接開くことで、ソリューションをインストールできます。 ベスト プラクティスとして、ユーザーはセットアップ プログラムを使用してソリューションをインストールする必要があります。 他の 2 とおりの方法では、必要なソフトウェアがインストール済みであるかどうかが確認されません。 ユーザーがインストール場所からドキュメントを開こうとする場合は、Office アプリケーションのセキュリティ センターにある信頼できる場所の一覧に、そのインストール場所を追加する必要があります。

### <a name="opening-the-document-of-a-document-level-customization"></a>ドキュメント レベルのカスタマイズに対応するドキュメントを開く
 ドキュメント レベルのカスタマイズに対応するドキュメントの場合は、ユーザーはインストール場所からそのドキュメントを直接開くか、またはドキュメントをローカル コンピューターにコピーしてからコピー先ドキュメントを開くことができます。

 ベスト プラクティスとして、ユーザーはローカル コンピューター上にあるドキュメントのコピーを開く必要があります。その結果、複数のユーザーが同じドキュメントを同時に開こうとすることはありません。 このプラクティスを強制するために、ユーザーのコンピューターにドキュメントをコピーするようにセットアップ プログラムを構成することができます。 「[ソリューションのドキュメントをエンド ユーザーのコンピューターに配置する (ドキュメント レベルのカスタマイズのみ)](#Put)」を参照してください。

### <a name="install-the-solution-by-opening-the-deployment-manifest-from-an-iis-website"></a>IIS の Web サイトから配置マニフェストを開く方法でソリューションをインストールする
 ユーザーは、Web で配置マニフェストを開くことにより、Office ソリューションをインストールできます。 ただし、セキュリティで保護されたインターネット インフォメーション サービス (IIS) がインストールされている場合は、 *.vsto* 拡張子を持つファイルがブロックされます。 IIS を使用して Office ソリューションを配置する前に、IIS に MIME の種類を定義する必要があります。

##### <a name="to-add-the-vsto-mime-type-to-iis-60"></a>IIS 6.0 に MIME の種類 (.vsto) を追加するには

1. IIS 6.0 を実行しているサーバー上で、 **[スタート]**  >  **[すべてのプログラム]**  >  **[管理ツール]**  >   **[インターネット インフォメーション サービス (IIS) マネージャー]** を選択します。

2. 構成するコンピューター名、 **[Web サイト]** フォルダー、または Web サイトを選択します。

3. メニュー バーで、 **[アクション]**  >  **[プロパティ]** を選択します。

4. **[HTTP ヘッダー]** タブの **[MIME の種類]** を選択します。

5. **[MIME の種類]** ウィンドウの **[新規作成]** をクリックします。

6. **[MIME の種類]** ウィンドウで、拡張子として「 **.vsto**」と入力し、MIME の種類として「**application/x-ms-vsto**」と入力してから、新しい設定を適用します。

    > [!NOTE]
    > 変更を有効にするために、World Wide Web 発行サービスを再起動するか、ワーカー プロセスがリサイクルされるまで待つ必要があります。 その後、ブラウザーのディスク キャッシュをフラッシュし、 *.vsto* ファイルを再度開く必要があります。

##### <a name="to-add-the-vsto-mime-type-to-iis-70"></a>IIS 7.0 に MIME の種類 (.vsto) を追加するには

1. IIS 7.0 を実行しているサーバーで、 **[スタート]**  >  **[すべてのプログラム]**  >  **[アクセサリ]** を選択します。

2. **[コマンド プロンプト]** のショートカット メニューを開き、 **[管理者として実行]** を選択します。

3. **[開く]** ボックスで次のパスを入力し、 **[OK]** をクリックします。

    ```cmd
    %windir%\system32\inetsrv
    ```

4. 次のコマンドを入力し、新しい設定を適用します。

    ```cmd
    set config /section:staticContent /+[fileExtension='.vsto',mimeType='application/x-ms-vsto']
    ```

    > [!NOTE]
    > 変更を有効にするために、World Wide Web Publishing Service を再起動するか、ワーカー プロセスがリサイクルされるまで待つ必要があります。 その後、ブラウザーのディスク キャッシュをフラッシュし、 *.vsto* ファイルを再度開く必要があります。

## <a name="put-the-document-of-a-solution-onto-the-end-users-computer-document-level-customizations-only"></a><a name="Put"></a> ソリューションのドキュメントをエンド ユーザーのコンピューターに配置する (ドキュメント レベルのカスタマイズのみ)
 配置後アクションを作成すると、エンド ユーザーのコンピューターに対して、ソリューションのドキュメントを自動的にコピーすることができます。 この方法の場合、ソリューションのインストール後に、ユーザーがインストール場所から自らのコンピューターにドキュメントを手動でコピーする必要はありません。 開発者はクラスを作成し、その中で配置後アクションを定義し、ソリューションのビルドと発行を行い、アプリケーション マニフェストを変更し、アプリケーション マニフェストと配置マニフェストに再署名する必要があります。

 次の手順では、プロジェクト名が **ExcelWorkbook** であること、およびコンピューター上に作成された **C:\publish** というフォルダーにソリューションを発行することを前提としています。

### <a name="create-a-class-that-defines-the-post-deployment-action"></a>配置後アクションを定義するクラスを作成します。

1. メニュー バーで、 **[ファイル]**  >  **[追加]**  >  **[新しいプロジェクト]** を選択します。

2. **[新しいプロジェクトの追加]** ダイアログ ボックスの **[インストールされたテンプレート]** ペインで、 **[Windows]** フォルダーを選択します。

3. **[テンプレート]** ペインで、 **[クラス ライブラリ]** テンプレートを選択します。

4. **[名前]** フィールドに「**FileCopyPDA**」と入力し、 **[OK]** をクリックします。

5. **ソリューション エクスプローラー** で、**FileCopyPDA** プロジェクトを選択します。

6. メニュー バーで、 **[プロジェクト]**  >  **[参照の追加]** の順に選択します。

7. **[.NET]** タブで、`Microsoft.VisualStudio.Tools.Applications.Runtime` および `Microsoft.VisualStudio.Tools.Applications.ServerDocument` への参照を追加します。

8. クラスの名前を `FileCopyPDA` に変更してから、ファイルの内容を次のコードに置き換えます。 このコードは、以下のタスクを実行します。

   - ドキュメントをユーザーのデスクトップにコピーします。

   - _AssemblyLocation プロパティを、相対パスから配置マニフェストの完全修飾パスに変更します。

   - ユーザーがソリューションをアンインストールする場合は、ファイルを削除します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_excelworkbookpda/filecopypda/class1.vb" id="Snippet7":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_excelworkbookpda/filecopypda/class1.cs" id="Snippet7":::

### <a name="build-and-publish-the-solution"></a>ソリューションをビルドし、発行します。

1. **ソリューション エクスプローラー** で、**FileCopyPDA** プロジェクトのショートカット メニューを開き、 **[ビルド]** を選択します。

2. **ExcelWorkbook** プロジェクトのショートカット メニューを開き、 **[ビルド]** を選択します。

3. **ExcelWorkbook** プロジェクトのショートカット メニューを開き、 **[参照の追加]** を選択します。

4. **[参照の追加]** ダイアログ ボックスで **[プロジェクト]** タブ、 **[FileCopyPDA]** 、 **[OK]** の順に選択します。

5. **ソリューション エクスプローラー** で、**ExcelWorkbook** プロジェクトを選択します。

6. メニュー バーで、 **[プロジェクト]**  >  **[新しいフォルダー]** を選択します。

7. 「**Data**」と入力し、**Enter** キーを押します。

8. **ソリューション エクスプローラー** で、**Data** フォルダーを選択します。

9. メニュー バーで、 **[プロジェクト]**  >  **[既存項目の追加]** を選択します。

10. **[既存項目の追加]** ダイアログ ボックスで、**ExcelWorkbook** プロジェクトの出力ディレクトリを参照し、**ExcelWorkbook.xlsx** ファイルを選択した後、 **[追加]** をクリックします。

11. **ソリューション エクスプローラー** で、**ExcelWorkbook.xlsx** ファイルを選択します。

12. **プロパティ** ウィンドウで、"**ビルド アクション**" プロパティを "**コンテンツ**" に変更し、"**出力ディレクトリにコピー**" プロパティを "**新しい場合はコピーする**" に変更します。

     これらの手順を完了した時点で、プロジェクトは次の図のようになります。

     ![配置後アクションのプロジェクト構造。](../vsto/media/vsto-postdeployment.png "配置後アクションのプロジェクト構造。")

13. **ExcelWorkbook** プロジェクトを発行します。

### <a name="modify-the-application-manifest"></a>アプリケーション マニフェストの変更

1. **エクスプローラー** を使用して、ソリューションディレクトリ (**c:\publish**) を開きます。

2. **Application Files** フォルダーを開き、ソリューションの最新の発行済みバージョンに対応するフォルダーを開きます。

3. メモ帳などのテキスト エディターで **ExcelWorkbook.dll.manifest** ファイルを開きます。

4. `</vstav3:update>` 要素の後に、次のコードを追加します。 `<vstav3:entryPoint>` 要素の class 属性には、次の構文を使用します: *NamespaceName.ClassName*。 次の例では、名前空間名とクラス名は同じであるため、最終的にエントリ ポイント名は `FileCopyPDA.FileCopyPDA` になります。

    ```xml
    <vstav3:postActions>
      <vstav3:postAction>
        <vstav3:entryPoint
          class="FileCopyPDA.FileCopyPDA">
          <assemblyIdentity
            name="FileCopyPDA"
            version="1.0.0.0"
            language="neutral"
            processorArchitecture="msil" />
        </vstav3:entryPoint>
        <vstav3:postActionData>
        </vstav3:postActionData>
      </vstav3:postAction>
    </vstav3:postActions>
    ```

### <a name="re-sign-the-application-and-deployment-manifests"></a>アプリケーション マニフェストと配置マニフェストへの再署名

1. **%USERPROFILE%\Documents\Visual Studio 2013\Projects\ExcelWorkbook\ExcelWorkbook** フォルダー内で、**ExcelWorkbook_TemporaryKey.pfx** 証明書ファイルをクリップボードにコピーし、そのファイルを *PublishFolder* **\Application Files\ExcelWorkbook**\__MostRecentPublishedVersion_ フォルダーに貼り付けます。

2. Visual Studio コマンド プロンプトを開き、ディレクトリを **c:\publish\Application Files\ExcelWorkbook**\__MostRecentPublishedVersion_ フォルダーに移動します (たとえば、**c:\publish\Application Files\ExcelWorkbook_1_0_0_4**)。

3. 次のコマンドを実行し、変更したアプリケーション マニフェストに署名します。

    ```cmd
    mage -sign ExcelWorkbook.dll.manifest -certfile ExcelWorkbook_TemporaryKey.pfx
    ```

     "ExcelWorkbook.dll.manifest が正常に署名されました" というメッセージが表示されます。

4. **c:\publish** フォルダーに移動した後、次のコマンドを実行することで、配置マニフェストを更新し、署名します。

    ```cmd
    mage -update ExcelWorkbook.vsto -appmanifest "Application Files\Ex
    celWorkbookMostRecentVersionNumber>\ExcelWorkbook.dll.manifest" -certfile "Application Files\ExcelWorkbookMostRecentVersionNumber>\ExcelWorkbook_TemporaryKey.pfx"
    ```

    > [!NOTE]
    > 前述の例では、MostRecentVersionNumber を、ソリューションの最新発行バージョンのバージョン番号に置き換えます (たとえば、**1_0_0_4**)。

     "ExcelWorkbook.vsto 正常に署名されました" というメッセージが表示されます。

5. *ExcelWorkbook.vsto* ファイルを **c:\publish\Application Files\ExcelWorkbook**\__MostRecentVersionNumber_ ディレクトリにコピーします。

## <a name="put-the-document-of-a-solution-onto-a-server-thats-running-sharepoint-document-level-customizations-only"></a><a name="SharePoint"></a> ソリューションのドキュメントを、SharePoint を実行しているサーバーに配置する (ドキュメント レベルのカスタマイズのみ)
 SharePoint を使用して、エンド ユーザーに対してドキュメント レベルのカスタマイズを発行できます。 ユーザーが SharePoint サイトにアクセスし、ドキュメントを開くと、ランタイムが自動的に共有ネットワーク フォルダーからユーザーのローカル コンピューターにソリューションをインストールします。 ソリューションをローカル インストールした後、ドキュメントをデスクトップなど別の場所にコピーした場合でも、カスタマイズは引き続き機能します。

#### <a name="to-put-the-document-on-a-server-thats-running-sharepoint"></a>SharePoint を実行しているサーバーにドキュメントを配置するには

1. SharePoint サイト上のドキュメント ライブラリにソリューション ドキュメントを追加します。

2. 次の方法のいずれかに対応する手順を実行します。

    - Office 構成ツールを使用し、すべてのユーザーのコンピューターで Word または Excel のセキュリティ センターに、SharePoint を実行しているサーバーを追加します。

         「[Office 2010 でのセキュリティ ポリシーと設定](/previous-versions/office/office-2010/cc178946(v=office.14))」を参照してください。

    - 各ユーザーが確実に次の手順を実行するようにします。

        1. ローカル コンピューターで Word または Excel を開き、 **[ファイル]** タブを選択して、 **[オプション]** ボタンをクリックします。

        2. **[セキュリティ センター]** ダイアログ ボックスで、 **[信頼できる場所]** ボタンをクリックします。

        3. **[プライベート ネットワーク上にある信頼できる場所を許可する (推奨しません)]** チェック ボックスをオンにし、 **[新しい場所の追加]** ボタンをクリックします。

        4. **[パス]** ボックスで、アップロードしたドキュメントを含む SharePoint ドキュメント ライブラリの URL (たとえば、 *http://SharePointServerName/TeamName/ProjectName/DocumentLibraryName* ) を入力します。

             ここで、*default.aspx* や *AllItems.aspx* など、既定の Web ページの名前を追加しないでください。

        5. **[この場所のサブフォルダーも信頼する]** チェック ボックスをオンにし、 **[OK]** をクリックします。

             ユーザーが SharePoint サイトからドキュメントを開いた時点で、そのドキュメントが開かれ、カスタマイズがインストールされます。 ユーザーは、ドキュメントを自分のデスクトップにコピーすることができます。 ドキュメント内のプロパティは、ドキュメントが存在しているネットワークの場所を指しているので、カスタマイズは引き続き実行されます。

## <a name="create-a-custom-installer"></a><a name="Custom"></a> カスタム インストーラーを作成する
 ソリューションを発行したときに自動的に作成されたセットアップ プログラムを使用する代わりに、Office ソリューション用のカスタム インストーラーを作成することもできます。 たとえば、サインイン スクリプトを使用してインストールを開始したり、バッチ ファイルを使用して、ユーザーの操作なしにソリューションをインストールすることもできます。 このようなシナリオは、エンド ユーザーのコンピューターに必須コンポーネントがインストール済みの場合に最適です。

 カスタム インストール プロセスの一環として、Office ソリューション用のインストーラー ツール (*VSTOInstaller.exe*) を呼び出します。既定では、このツールは次の場所にインストールされます。

 *%commonprogramfiles%\microsoft shared\VSTO\10.0\VSTOInstaller.exe*

 ツールがこの場所にない場合は、**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VSTO Runtime Setup\v4\InstallerPath** レジストリ キーまたは **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\VSTO Runtime Setup\v4\InstallerPath** レジストリ キーを使用して、このツールのパスを見つけることができます。

 *VSTOinstaller.exe* では次のパラメーターを使用できます。

| パラメーター | 定義 |
|------------------| - |
| /Install または /I | ソリューションをインストールします。 このオプションの後に配置マニフェストのパスを指定する必要があります。 ローカル コンピューター上のパス、汎用名前付けの規則 (UNC) のファイル共有を指定できます。 ローカル パス (*C:\FolderName\PublishFolder*)、相対パス (*Publish\\* )、または完全修飾の場所 ( *\\\ServerName\FolderName* または http://<em>ServerName/FolderName</em>) を指定できます。 |
| /Uninstall または /U | ソリューションをアンインストールします。 このオプションの後に配置マニフェストのパスを指定する必要があります。 ローカル コンピューター上のパス、UNC ファイル共有を指定できます。 ローカル パス (*c:\FolderName\PublishFolder*)、相対パス (*Publish\\* )、または完全修飾の場所 ( *\\\ServerName\FolderName* または http://<em>ServerName/FolderName</em>) を指定できます。 |
| /Silent または /S | ユーザーに入力を要求したりメッセージを表示したりすることなくソリューションをインストールまたはアンインストールします。 信頼プロンプトが必要な場合は、カスタマイズのインストールや更新は実行されません。 |
| /Help または /? | ヘルプ情報を表示します。 |

 *VSTOinstaller.exe* を実行すると、次のエラー コードが表示されることがあります。

|エラー コード|定義|
|----------------|----------------|
|0|ソリューションが正常にインストールまたはアンインストールされたか、VSTOInstaller ヘルプが表示されました。|
|-100|1 つ以上のコマンド ライン オプションが有効でないか、複数回設定されました。 詳細については、"vstoinstaller /?" と入力してください。 または、「[ClickOnce Office ソリューションのカスタムインストーラーを作成する](/previous-versions/bb772078(v=vs.110))」を参照してください。|
|-101|1 つ以上のコマンド ライン オプションが有効ではありません。 詳細については、"vstoinstaller /?" と入力してください。|
|-200|配置マニフェストの URI が有効でありません。 詳細については、"vstoinstaller /?" と入力してください。|
|-201|配置マニフェストが有効でないため、ソリューションをインストールできませんでした。 「[Office ソリューション用配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)」を参照してください。|
|-202|アプリケーション マニフェストの Visual Studio Tools for Office セクションが有効ではないため、ソリューションをインストールできませんでした。 「[Office ソリューション用アプリケーション マニフェスト](../vsto/application-manifests-for-office-solutions.md)」を参照してください。|
|-203|ダウンロード エラーが発生したため、ソリューションをインストールできませんでした。 配置マニフェストの URI またはネットワーク ファイルの位置を確認し、もう一度、実行してみてください。|
|-300|セキュリティ例外が発生したため、ソリューションをインストールできませんでした。 「[Office ソリューションをセキュリティで保護する](../vsto/securing-office-solutions.md)」を参照してください。|
|-400|ソリューションをインストールできませんでした。|
|-401|ソリューションをアンインストールできませんでした。|
|-500|ソリューションをインストールまたはアンインストールできなかったこと、または配置マニフェストをダウンロードできなかったことが原因で、操作は取り消されました。|

## <a name="publish-an-update"></a><a name="Update"></a> 更新プログラムを発行する
 ソリューションを更新するには、**プロジェクト デザイナー** または **発行ウィザード** を使用してソリューションを再度発行し、更新後のソリューションをインストール場所にコピーします。 インストール場所にファイルをコピーするときに、前のファイルを確実に上書きしてください。

 次回ソリューションで更新プログラムがチェックされたときに、自動的に新しいバージョンが検出され、読み込まれます。

## <a name="change-the-installation-location-of-a-solution"></a><a name="Location"></a> ソリューションのインストール場所を変更する
 ソリューションを発行した後、インストール パスの追加または変更を行うことができます。 次の理由の 1 つ以上により、インストール パスを変更する可能性があります:

- インストール パスが既知になる前に、セットアップ プログラムをコンパイルした。

- ソリューション ファイルは、別の場所からコピーされたものである。

- インストール ファイルをホストするサーバーの名前または場所が変更された。

  ソリューションのインストール パスを変更するには、開発者がセットアップ プログラムを更新し、その後、ユーザーがそのプログラムを実行する必要があります。 ドキュメント レベルのカスタマイズの場合、新しい場所を指すように、ユーザーがドキュメントのプロパティを更新する必要もあります。

> [!NOTE]
> ユーザーにドキュメント プロパティの更新を求めることが望ましくない場合は、更新後のドキュメントをインストール場所から取得するようにユーザーに求めることもできます。

#### <a name="to-change-the-installation-path-in-the-setup-program"></a>セットアップ プログラムのインストール パスを変更するには

1. **コマンド プロンプト** ウィンドウを開き、インストール フォルダーに移動します。

2. セットアップ プログラムを実行します。このとき、文字列として新しいインストール パスを表す `/url` パラメーターを指定します。

    次の例で、インストール パスを、Fabrikam の Web サイト上にある場所に変更する方法を示しますが、この URL は必要なパスに置き換えることができます。

   ```cmd
   setup.exe /url="http://www.fabrikam.com/newlocation"
   ```

   > [!NOTE]
   > 実行可能ファイルのシグネチャが無効化されることを示すメッセージが表示された場合は、ソリューションの署名に使用された証明書がもう有効ではなく、発行者が不明です。 その結果、ユーザーはソリューションをインストールする前に、ソリューションのソースを信頼することを示すために、メッセージを確認する必要があります。

   > [!NOTE]
   > URL の現在の値を表示するには、`setup.exe /url` を実行します。

   ドキュメント レベルのカスタマイズでは、ユーザーがドキュメントを開き、そのドキュメントの _AssemblyLocation プロパティを更新する必要があります。 次の手順では、ユーザーがこのタスクを実行する方法について説明します。

#### <a name="to-update-the-_assemblylocation-property-in-a-document"></a>ドキュメントの_AssemblyLocation プロパティを更新するには

1. 次の図に示すように、 **[ファイル]** タブの **[情報]** をクリックします。

     ![Excel の [情報] タブ](../vsto/media/vsto-infotab.png "Excel の [情報] タブ")

2. 次の図に示すように、 **[プロパティ]** の一覧で **[詳細プロパティ]** を選択します。

     ![Excel の [詳細プロパティ]。](../vsto/media/vsto-advanceddocumentproperties.png "Excel の [詳細プロパティ]。")

3. 次の図に示すように、 **[カスタム]** タブにある **[プロパティ]** の一覧で、_AssemblyLocation をクリックします。

     ![[AssemblyLocation] プロパティ。](../vsto/media/vsto-assemblylocationproperty.png "[AssemblyLocation] プロパティ。")

     **[値]** ボックスには、配置マニフェストの識別子が含まれています。

4. 識別子の前に、ドキュメントの完全修飾パスと縦棒を入力します。形式としては、"*パス*|*識別子*" となります (たとえば、*File://ServerName/FolderName/FileName|74744e4b-e4d6-41eb-84f7-ad20346fe2d9*)。

     この識別子を指定する方法について詳しくは、「[カスタム ドキュメント プロパティの概要](../vsto/custom-document-properties-overview.md)」をご覧ください。

5. **[OK]** をクリックし、ドキュメントを保存して閉じます。

6. セットアップ プログラムを実行します。このとき、指定の場所にあるソリューションをインストールするための /url パラメーターは指定しません。

## <a name="roll-back-a-solution-to-an-earlier-version"></a><a name="Roll"></a> ソリューションを以前のバージョンにロールバックする
 開発者がソリューションをロールバックすると、ユーザーはそのソリューションの以前のバージョンに戻されることになります。

#### <a name="to-roll-back-a-solution"></a>ソリューションをロールバックするには

1. ソリューションのインストール場所を開きます。

2. 最上位の発行フォルダーで、配置マニフェスト ( *.vsto* ファイル) を削除します。

3. ロールバック先のバージョンに対応するサブフォルダーを見つけます。

4. このサブフォルダー内の配置マニフェストをトップレベルの発行フォルダーにコピーします。

     たとえば、**OutlookAddIn1** という名前のソリューションをバージョン 1.0.0.1 からバージョン 1.0.0.0 にロールバックするには、**OutlookAddIn1_1_0_0_0** フォルダーから **OutlookAddIn1.vsto** ファイルをコピーします。 最上位の発行フォルダーにファイルを貼り付け、既に存在していた **OutlookAddIn1_1_0_0_1** に対応するバージョン固有の配置マニフェストを上書きします。

     次の図に、この例に対応する発行フォルダーの構造を示します。

     ![発行フォルダーの構造](../vsto/media/publishfolderstructure.png "発行フォルダーの構造")

     アプリケーションまたはカスタマイズされたドキュメントをユーザーが次回開くときに、配置マニフェストの変更が検出されます。 Office ソリューションの以前のバージョンは、ClickOnce キャッシュから実行されます。

> [!NOTE]
> ローカル データは、ソリューションの 1 つ前のバージョンについてのみ保存されます。 2 つのバージョンをロールバックした場合、ローカル データは保持されません。 ローカル データについて詳しくは、「[ClickOnce アプリケーションにおけるローカル データおよびリモート データへのアクセス](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)」をご覧ください。

## <a name="see-also"></a>関連項目

- [Office ソリューションを配置する](../vsto/deploying-an-office-solution.md)
- [Office ソリューションを発行する](../vsto/deploying-an-office-solution-by-using-clickonce.md)
- [方法: ClickOnce を使用して Office ソリューションを発行する](/previous-versions/bb386095(v=vs.110))
- [方法: ClickOnce Office ソリューションをインストールする](/previous-versions/bb608592(v=vs.110))
- [方法: ClickOnce を使用してドキュメント レベルの Office ソリューションを SharePoint Server に発行する](/previous-versions/bb608595(v=vs.110))
- [ClickOnce Office ソリューションのカスタム インストーラーを作成する](/previous-versions/bb772078(v=vs.110))