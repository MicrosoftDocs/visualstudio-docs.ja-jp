---
title: プライバシー プロンプトを使用してカスタム ブートストラップを作成する
description: 新しいファイル バージョンとアセンブリ バージョンのアセンブリが使用可能になったときに、ClickOnce アプリケーションが自動的に更新されるように構成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, prerequisites
- dependencies [.NET Framework], custom bootstrapper package
- deploying applications [Visual Studio], custom prerequisites
- Windows Installer deployment, prerequisites
- prerequisites [.NET Framework], custom bootstrapper package
ms.assetid: 2f3edd6a-84d1-4864-a1ae-6a13c5732aae
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 96cfbf8693ce23dbc0b0584c7742607224aeab4f
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216944"
---
# <a name="walkthrough-create-a-custom-bootstrapper-with-a-privacy-prompt"></a>チュートリアル: プライバシー プロンプトを使用してカスタム ブートストラップを作成する
新しいファイル バージョンとアセンブリ バージョンのアセンブリが使用可能になったときに、ClickOnce アプリケーションが自動的に更新されるように構成することができます。 ユーザーがこの動作に同意するかどうかを確認するには、プライバシー プロンプトを表示します。 その後、ユーザーは自動更新のアクセス許可をアプリケーションに付与するかどうかを選択できます。 アプリケーションの自動更新が許可されなかった場合、インストールは実行されません。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- Visual Studio 2010。

## <a name="create-an-update-consent-dialog-box"></a>更新への同意に関するダイアログ ボックスを作成する
 プライバシー プロンプトを表示するには、アプリケーションの自動更新への同意をユーザーに求めるアプリケーションを作成します。

#### <a name="to-create-a-consent-dialog-box"></a>同意ダイアログ ボックスを作成するには

1. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

2. **[新しいプロジェクト]** ダイアログ ボックスで、 **[Windows]** をクリックし、 **[WindowsFormsApplication]** をクリックします。

3. **[名前]** に「**ConsentDialog**」と入力し、 **[OK]** をクリックします。

4. デザイナーで、フォームをクリックします。

5. **プロパティ** ウィンドウで、**Text** プロパティを「**更新への同意ダイアログ**」に変更します。

6. **ツールボックス** で、 **[すべての Windows フォーム]** を展開し、 **[Label]** コントロールをフォームにドラッグします。

7. デザイナーで、ラベル コントロールをクリックします。

8. **プロパティ** ウィンドウで、 **[表示]** の **Text** プロパティを次のように変更します。

    インストールしようとしているアプリケーションでは、Web 上の最新の更新プログラムの確認が行われます。 [同意する] をクリックすると、アプリケーションで更新プログラムを自動的にチェックし、インターネットからインストールすることを承認したことになります。

9. **ツールボックス** で、**Checkbox** コントロールをフォームの中央にドラッグします。

10. **プロパティ** ウィンドウで、 **[レイアウト]** の **Text** プロパティを「**同意する**」に変更します。

11. **ツールボックス** で、**Button** コントロールをフォームの左下にドラッグします。

12. **プロパティ** ウィンドウで、 **[レイアウト]** の **Text** プロパティを「**次へ**」に変更します。

13. **プロパティ** ウィンドウで、 **[デザイン]** の **(Name)** プロパティを「**ProceedButton**」に変更します。

14. **ツールボックス** で、**Button** コントロールをフォームの右下にドラッグします。

15. **プロパティ** ウィンドウで、 **[レイアウト]** の **Text** プロパティを「**キャンセル**」に変更します。

16. **プロパティ** ウィンドウで、 **[デザイン]** の **(Name)** プロパティを「**CancelButton**」に変更します。

17. デザイナーで、 **[同意する]** チェック ボックスをダブルクリックして、CheckedChanged イベント ハンドラーを生成します。

18. Form1 のコード ファイルで、CheckedChanged イベント ハンドラーに次のコードを追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_ProTools/consentdialog/cs/form1.cs" id="Snippet1":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_ProTools/consentdialog/vb/form1.vb" id="Snippet1":::

19. クラス コンストラクターを更新して、 **[次へ]** ボタンを既定で無効にします。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_ProTools/consentdialog/cs/form1.cs" id="Snippet6":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_ProTools/consentdialog/vb/form1.vb" id="Snippet6":::

20. Form1 のコード ファイルで、ブール変数の次のコードを追加して、エンド ユーザーがオンライン更新に同意したかどうかを追跡します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_ProTools/consentdialog/cs/form1.cs" id="Snippet3":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_ProTools/consentdialog/vb/form1.vb" id="Snippet3":::

21. デザイナーで、 **[次へ]** ボタンをダブルクリックして、Click イベント ハンドラーを生成します。

22. Form1 のコード ファイルで、 **[次へ]** ボタンの Click イベント ハンドラーに次のコードを追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_ProTools/consentdialog/cs/form1.cs" id="Snippet2":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_ProTools/consentdialog/vb/form1.vb" id="Snippet2":::


23. デザイナーで、 **[キャンセル]** ボタンをダブルクリックして、Click イベント ハンドラーを生成します。

24. Form1 のコード ファイルで、 **[キャンセル]** ボタンの Click イベント ハンドラーに次のコードを追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_ProTools/consentdialog/cs/form1.cs" id="Snippet4":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_ProTools/consentdialog/vb/form1.vb" id="Snippet4":::

25. アプリケーションを更新して、エンド ユーザーがオンライン更新に同意しなかった場合にエラーが返されるようにします。

     Visual Basic 開発者の場合のみ:

    1. **ソリューション エクスプローラー** で、**ConsentDialog** をクリックします。

    2. **[プロジェクト]** メニューで、 **[モジュールの追加]** をクリックし、 **[追加]** をクリックします。

    3. *Module1.vb* のコード ファイルで、次のコードを追加します。

       :::code language="vb" source="../snippets/visualbasic/VS_Snippets_ProTools/consentdialog/vb/module1.vb" id="Snippet7":::

    4. **[プロジェクト]** メニューで、 **[ConsentDialog のプロパティ]** をクリックし、 **[アプリケーション]** タブをクリックします。

    5. **[アプリケーション フレームワークを有効にする]** をオフにします。

    6. **[スタートアップ オブジェクト]** ドロップダウン メニューで、 **[Module1]** を選択します。

       > [!NOTE]
       > アプリケーション フレームワークを無効にすると、Windows XP のビジュアル スタイル、アプリケーション イベント、スプラッシュ スクリーン、単一インスタンス アプリケーションなどの機能が無効になります。 詳細については、「[[アプリケーション] ページ (プロジェクト デザイナー) (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md)」を参照してください。

       Visual C# 開発者の場合のみ:

       *Program.cs* のコード ファイルを開き、次のコードを追加します。

       :::code language="csharp" source="../snippets/csharp/VS_Snippets_ProTools/consentdialog/cs/program.cs" id="Snippet5":::

26. **[ビルド]** メニューで、 **[ソリューションのビルド]** をクリックします。

## <a name="create-the-custom-bootstrapper-package"></a>カスタム ブートストラップ パッケージを作成する
 エンド ユーザーにプライバシーに関する確認メッセージを表示するには、Update Consent Dialog アプリケーション用のカスタム ブートストラップ パッケージを作成し、すべての ClickOnce アプリケーションに必須コンポーネントとして含めます。

 この手順では、次のドキュメントを作成してカスタム ブートストラップ パッケージを作成する方法を示します。

- ブートストラップの内容を記述した *product.xml* マニフェスト ファイル。

- パッケージのローカライズ関連の内容物 (文字列やソフトウェア ライセンス条項など) をリストした *package.xml* マニフェスト ファイル。

- ソフトウェア ライセンス条項のドキュメント。

#### <a name="step-1-to-create-the-bootstrapper-directory"></a>手順 1: ブートストラップ ディレクトリを作成するには

1. *%PROGRAMFILES%\Microsoft SDKs\Windows\v7.0A\Bootstrapper\Packages* に、**UpdateConsentDialog** という名前のディレクトリを作成します。

    > [!NOTE]
    > このフォルダーを作成するには、管理特権が必要な場合があります。

2. *UpdateConsentDialog* ディレクトリで、*en* という名前のサブディレクトリを作成します。

    > [!NOTE]
    > ロケールごとに新しいディレクトリを作成してください。 たとえば、fr や de ロケール用のサブディレクトリを追加するなどします。 これらのディレクトリには、フランス語とドイツ語の文字列と言語パックが含められます (必要な場合)。

#### <a name="step-2-to-create-the-productxml-manifest-file"></a>手順 2: product.xml マニフェスト ファイルを作成するには

1. *product.xml* というテキスト ファイルを作成します。

2. *product.xml* ファイルで、次の XML コードを追加します。 既存の XML コードを上書きしないようにしてください。

    ```xml
    <Product
      xmlns="http://schemas.microsoft.com/developer/2004/01/bootstrapper"
      ProductCode="Microsoft.Sample.EULA">
      <!-- Defines the list of files to be copied on build. -->
      <PackageFiles CopyAllPackageFiles="false">
        <PackageFile Name="ConsentDialog.exe"/>
      </PackageFiles>

      <!-- Defines how to run the Setup package.-->
      <Commands >
        <Command PackageFile = "ConsentDialog.exe" Arguments=''>
          <ExitCodes>
            <ExitCode Value="0" Result="Success" />
            <ExitCode Value="-1" Result="Fail" String="AU_Unaccepted" />
            <DefaultExitCode Result="Fail"
              FormatMessageFromSystem="true" String="GeneralFailure" />
          </ExitCodes>
        </Command>
      </Commands>

    </Product>
    ```

3. ファイルを UpdateConsentDialog ブートストラップ ディレクトリに保存します。

#### <a name="step-3-to-create-the-packagexml-manifest-file-and-the-software-license-terms"></a>手順 3: package.xml マニフェスト ファイルとソフトウェア ライセンス条項を作成するには

1. *package.xml* というテキスト ファイルを作成します。

2. *package.xml* ファイルで、次の XML コードを追加してロケールを定義し、ソフトウェア ライセンス条項を含めます。 既存の XML コードを上書きしないようにしてください。

    ```xml
    <Package
      xmlns="http://schemas.microsoft.com/developer/2004/01/bootstrapper"
      Name="DisplayName"
      Culture="Culture"
      LicenseAgreement="eula.rtf">
      <PackageFiles>
        <PackageFile Name="eula.rtf"/>
      </PackageFiles>

      <!-- Defines a localizable string table for error messages. -->
      <Strings>
        <String Name="DisplayName">Update Consent Dialog</String>
        <String Name="Culture">en</String>
        <String Name="AU_Unaccepted">The automatic update agreement is not accepted.</String>
        <String Name="GeneralFailure">A failure occurred attempting to launch the setup.</String>
      </Strings>
    </Package>
    ```

3. ファイルを、UpdateConsentDialog ブートストラップ ディレクトリの en サブディレクトリに保存します。

4. ソフトウェア ライセンス条項用に、*eula.rtf* というドキュメントを作成します。

    > [!NOTE]
    > ソフトウェア ライセンス条項には、ライセンス、保証、責任、および現地法に関する情報を含める必要があります。 これらのファイルはロケール固有のものである必要があるため、MBCS または UNICODE 文字をサポートする形式でファイルを保存するようにしてください。 ソフトウェア ライセンス条項の内容については、法務部門に問い合わせてください。

5. ドキュメントを、*UpdateConsentDialog* ブートストラップ ディレクトリの en サブディレクトリに保存します。

6. 必要に応じて、新しい *package.xml* マニフェスト ファイルを作成し、各ロケールのソフトウェア ライセンス条項用の新しい *eula.rtf* ドキュメントを作成します。 たとえば、fr および de ロケール用のサブディレクトリを作成した場合は、それぞれ個別の package.xml マニフェスト ファイルとソフトウェア ライセンス条項を作成し、それらを fr サブディレクトリと de サブディレクトリに保存します。

## <a name="set-the-update-consent-application-as-a-prerequisite"></a>Update Consent アプリケーションを必須コンポーネントとして設定する
 Visual Studio では、Update Consent アプリケーションを必須コンポーネントとして設定できます。

#### <a name="to-set-the-update-consent-application-as-a-prerequisite"></a>Update Consent アプリケーションを必須コンポーネントとして設定するには

1. **ソリューション エクスプローラー** で、配置するアプリケーションの名前をクリックします。

2. **[プロジェクト]** メニューの *ProjectName の* **[プロパティ]** をクリックします。

3. **[発行]** ページをクリックし、 **[必須コンポーネント]** をクリックします。

4. **Update Consent Dialog** を選択します。

    > [!NOTE]
    > 場合によっては、Visual Studio を一度閉じて再度開かないと、[必須コンポーネント] ダイアログ ボックスに Update Consent Dialog が表示されない場合があります。

5. **[OK]** をクリックします。

## <a name="create-and-test-the-setup-program"></a>セットアップ プログラムを作成してテストする
 Update Consent アプリケーションを必須コンポーネントとして設定したら、アプリケーションのインストーラーとブートストラップを生成することができます。

#### <a name="to-create-and-test-the-setup-program-by-not-clicking-i-agree"></a>[同意する] をクリックせずにセットアップ プログラムを作成およびテストするには

1. **ソリューション エクスプローラー** で、配置するアプリケーションの名前をクリックします。

2. **[プロジェクト]** メニューの *ProjectName の* **[プロパティ]** をクリックします。

3. **[発行]** ページをクリックし、 **[今すぐ発行]** をクリックします。

4. 発行の出力が自動的に開かない場合は、発行の出力に移動します。

5. *Setup.exe* プログラムを実行します。

     セットアップ プログラムで、Update Consent Dialog のソフトウェア使用許諾契約書が表示されます。

6. ソフトウェア使用許諾契約書を読み、 **[同意する]** をクリックします。

     Update Consent Dialog アプリケーションが表示され、次のテキストが表示されます: インストールしようとしているアプリケーションでは、Web 上の最新の更新プログラムの確認が行われます。 [同意する] をクリックすると、アプリケーションでインターネット上の更新プログラムを自動的にチェックすることを承認したことになります。

7. アプリケーションを閉じるか、[キャンセル] をクリックします。

     アプリケーションで次のエラーが表示されます: <*アプリケーション名*> 用のシステム コンポーネントのインストール中にエラーが発生しました。 すべてのシステム コンポーネントが正常にインストールされるまで、セットアップは続行できません。

8. [詳細] をクリックすると、次のエラー メッセージが表示されます: コンポーネント Update Consent Dialog のインストールに失敗し、次のエラーがメッセージが生成されました: "The automatic update agreement is not accepted." 次のコンポーネントをインストールできませんでした: - Update Consent Dialog

9. **[閉じる]** をクリックします。

#### <a name="to-create-and-test-the-setup-program-by-clicking-i-agree"></a>[同意する] をクリックしてセットアップ プログラムを作成およびテストするには

1. **ソリューション エクスプローラー** で、配置するアプリケーションの名前をクリックします。

2. **[プロジェクト]** メニューの *ProjectName の* **[プロパティ]** をクリックします。

3. **[発行]** ページをクリックし、 **[今すぐ発行]** をクリックします。

4. 発行の出力が自動的に開かない場合は、発行の出力に移動します。

5. *Setup.exe* プログラムを実行します。

     セットアップ プログラムで、Update Consent Dialog のソフトウェア使用許諾契約書が表示されます。

6. ソフトウェア使用許諾契約書を読み、 **[同意する]** をクリックします。

     Update Consent Dialog アプリケーションが表示され、次のテキストが表示されます: インストールしようとしているアプリケーションでは、Web 上の最新の更新プログラムの確認が行われます。 [同意する] をクリックすると、アプリケーションでインターネット上の更新プログラムを自動的にチェックすることを承認したことになります。

7. **[同意する]** をクリックし、 **[次へ]** をクリックします。

     アプリケーションのインストールが開始されます。

8. [アプリケーションのインストール] ダイアログ ボックスが表示されたら、 **[インストール]** をクリックします。

## <a name="see-also"></a>こちらもご覧ください
- [アプリケーション配置の必要条件](../deployment/application-deployment-prerequisites.md)
- [ブートストラップ パッケージの作成](../deployment/creating-bootstrapper-packages.md)
- [方法: 製品マニフェストを作成する](../deployment/how-to-create-a-product-manifest.md)
- [方法: パッケージ マニフェストを作成する](../deployment/how-to-create-a-package-manifest.md)
- [製品およびパッケージ スキーマ リファレンス](../deployment/product-and-package-schema-reference.md)