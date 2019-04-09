---
title: 'チュートリアル: プライバシーのプロンプトを表示するカスタム ブートス トラップの作成 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
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
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c71a23fc79b0d80c55418a9c7d78a48ebc76000e
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58975150"
---
# <a name="walkthrough-creating-a-custom-bootstrapper-to-show-a-privacy-prompt"></a>チュートリアル: プライバシー プロンプトを表示するカスタム ブートス トラップの作成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

新しいファイルのバージョンとアセンブリのバージョンのアセンブリが使用可能になると自動的に更新する ClickOnce アプリケーションを構成できます。 お客様がこの動作に同意することを確認するにプライバシー プロンプトを表示できます。 次に、アプリケーションが自動的に更新するアクセス許可を付与するかどうかを選択できます。 アプリケーションが自動的に更新する許可されていない場合はインストールされません。  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>必須コンポーネント  
 このチュートリアルを実行するには、次のコンポーネントが必要です。  
  
-   Visual Studio 2010。  
  
## <a name="creating-an-update-consent-dialog-box"></a>更新の同意 ダイアログ ボックスを作成します。  
 プライバシー プロンプトを表示するには、アプリケーションの自動更新に同意するリーダーを要求しているアプリケーションを作成します。  
  
#### <a name="to-create-a-consent-dialog-box"></a>同意ダイアログ ボックスを作成するには  
  
1. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。  
  
2. **新しいプロジェクト**ダイアログ ボックスで、をクリックして**Windows**、 をクリックし、 **WindowsFormsApplication**。  
  
3. **名前**、型**ConsentDialog**、順にクリックします**OK**します。  
  
4. デザイナーでフォームをクリックします。  
  
5. **プロパティ**ウィンドウで、変更、**テキスト**プロパティを**更新同意ダイアログ**します。  
  
6. **ツールボックス**、展開**すべての Windows フォーム**、ドラッグ、**ラベル**コントロールをフォームにします。  
  
7. デザイナーで、ラベル コントロールをクリックします。  
  
8. **プロパティ**ウィンドウで、変更、**テキスト**のプロパティの **外観**次。  
  
    Web 上の最新の更新プログラムをインストールしようとしているアプリケーションを確認します。 "I Agree"でクリックすると、確認し、インターネットから自動的に更新プログラムをインストールするアプリケーションを承認します。  
  
9. **ツールボックス**、ドラッグ、**チェック ボックスをオン**フォームの中央にコントロール。  
  
10. **プロパティ**ウィンドウで、変更、**テキスト**のプロパティの **レイアウト**に**同意**します。  
  
11. **ツールボックス**、ドラッグ、**ボタン**コントロールをフォームの左下にあります。  
  
12. **プロパティ**ウィンドウで、変更、**テキスト**のプロパティの **レイアウト**に**続行**します。  
  
13. **プロパティ**ウィンドウで、変更、 **(名)** のプロパティの **デザイン**に**ProceedButton**します。  
  
14. **ツールボックス**、ドラッグ、**ボタン**コントロールをフォームの右下にします。  
  
15. **プロパティ**ウィンドウで、変更、**テキスト**のプロパティの **レイアウト**に**キャンセル**します。  
  
16. **プロパティ**ウィンドウで、変更、 **(名)** のプロパティの **デザイン**に**CancelButton**します。  
  
17. デザイナーで、ダブルクリック、**同意**CheckedChanged イベント ハンドラーを生成するチェック ボックスをオンします。  
  
18. Form1 コード ファイルでは、CheckedChanged イベント ハンドラーに次のコードを追加します。  
  
     [!code-csharp[ConsentDialog#1](../snippets/csharp/VS_Snippets_ProTools/consentdialog/cs/form1.cs#1)]
     [!code-vb[ConsentDialog#1](../snippets/visualbasic/VS_Snippets_ProTools/consentdialog/vb/form1.vb#1)]  
  
19. 更新を無効にするクラスのコンス トラクター、**続行**既定ではボタンをクリックします。  
  
     [!code-csharp[ConsentDialog#6](../snippets/csharp/VS_Snippets_ProTools/consentdialog/cs/form1.cs#6)]
     [!code-vb[ConsentDialog#6](../snippets/visualbasic/VS_Snippets_ProTools/consentdialog/vb/form1.vb#6)]  
  
20. Form1 コード ファイルでは、エンド ユーザーがオンライン更新に同意した場合に追跡するためにブール値変数に次のコードを追加します。  
  
     [!code-csharp[ConsentDialog#3](../snippets/csharp/VS_Snippets_ProTools/consentdialog/cs/form1.cs#3)]
     [!code-vb[ConsentDialog#3](../snippets/visualbasic/VS_Snippets_ProTools/consentdialog/vb/form1.vb#3)]  
  
21. デザイナーで、ダブルクリック、**続行**ボタン クリック イベント ハンドラーを生成します。  
  
22. Form1 コード ファイルでのクリック イベント ハンドラーに次のコードを追加、**続行**ボタンをクリックします。  
  
     [!code-csharp[ConsentDialog#2](../snippets/csharp/VS_Snippets_ProTools/consentdialog/cs/form1.cs#2)]
     [!code-vb[ConsentDialog#2](../snippets/visualbasic/VS_Snippets_ProTools/consentdialog/vb/form1.vb#2)]  
  
23. デザイナーで、ダブルクリック、**キャンセル**ボタン クリック イベント ハンドラーを生成します。  
  
24. Form1 コード ファイルでのクリック イベント ハンドラーに次のコードを追加、**キャンセル**ボタンをクリックします。  
  
     [!code-csharp[ConsentDialog#4](../snippets/csharp/VS_Snippets_ProTools/consentdialog/cs/form1.cs#4)]
     [!code-vb[ConsentDialog#4](../snippets/visualbasic/VS_Snippets_ProTools/consentdialog/vb/form1.vb#4)]  
  
25. オンライン更新プログラムに、エンドユーザーが同意しない場合は、エラーを返すようアプリケーションを更新します。  
  
     Visual Basic 開発者の場合のみ。  
  
    1. **ソリューション エクスプ ローラー**、 をクリックして**ConsentDialog**します。  
  
    2. **プロジェクト** メニューのをクリックして**モジュールの追加**、 をクリックし、**追加**します。  
  
    3. Module1.vb コード ファイルでは、次のコードを追加します。  
  
        [!code-vb[ConsentDialog#7](../snippets/visualbasic/VS_Snippets_ProTools/consentdialog/vb/module1.vb#7)]  
  
    4. **プロジェクト** メニューのをクリックして**ConsentDialog プロパティ**、 をクリックし、**アプリケーション**タブ。  
  
    5. オフに**有効にするアプリケーション フレームワーク**します。  
  
    6. **スタートアップ オブジェクト**ドロップダウン メニューで、 **Module1**します。  
  
       > [!NOTE]
       >  アプリケーション フレームワークを無効にするには、Windows XP ビジュアル スタイルのアプリケーション イベント、スプラッシュ スクリーン、単一インスタンス アプリケーションなどの機能が無効にします。 詳細については、「[[アプリケーション] ページ (プロジェクト デザイナー) (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md)」を参照してください。  
  
       Visual C# 開発者の場合のみ。  
  
       Program.cs コード ファイルを開き、次のコードを追加します。  
  
       [!code-csharp[ConsentDialog#5](../snippets/csharp/VS_Snippets_ProTools/consentdialog/cs/program.cs#5)]  
  
26. **ビルド** メニューのをクリックして**BuildSolution**します。  
  
## <a name="creating-the-custom-bootstrapper-package"></a>カスタム ブートス トラップ パッケージを作成します。  
 プライバシー プロンプトをエンドユーザーに表示するには、更新プログラムの同意ダイアログ アプリケーション用のカスタム ブートス トラップ パッケージを作成し、ClickOnce アプリケーションのすべての前提条件として含めます。  
  
 この手順では、次のドキュメントを作成してカスタム ブートス トラップ パッケージを作成する方法を示します。  
  
-   Product.xml はマニフェスト ブートス トラップの内容を記述するファイルです。  
  
-   文字列や、ソフトウェア ライセンス条項など、パッケージのローカライズに固有の要素の一覧を package.xml マニフェスト ファイル。  
  
-   ソフトウェアのライセンス条項のドキュメントです。  
  
#### <a name="step-1-to-create-the-bootstrapper-directory"></a>手順 1: ブートス トラップ ディレクトリを作成するには  
  
1.  という名前のディレクトリを作成する**UpdateConsentDialog** %PROGRAMFILES%\Microsoft SDKs\Windows\v7.0A\Bootstrapper\Packages にあります。  
  
    > [!NOTE]
    >  このフォルダーを作成する管理者特権を必要があります。  
  
2.  UpdateConsentDialog ディレクトリでは、en という名前のサブディレクトリを作成します。  
  
    > [!NOTE]
    >  ロケールごとに新しいディレクトリを作成します。 たとえば、フランス、ドイツのロケールのサブディレクトリを追加できます。 必要に応じて、フランス語、ドイツ語の文字列と言語パック、これらのディレクトリが含まれます。  
  
#### <a name="step-2-to-create-the-productxml-manifest-file"></a>手順 2: Product.xml マニフェスト ファイルを作成するには  
  
1.  という名前のテキスト ファイルを作成する`product.xml`します。  
  
2.  Product.xml ファイルでは、次の XML コードを追加します。 既存の XML コードを上書きしないことを確認します。  
  
    ```  
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
  
3.  UpdateConsentDialog ブートス トラップ ディレクトリに保存します。  
  
#### <a name="step-3-to-create-the-packagexml-manifest-file-and-the-software-license-terms"></a>手順 3: Package.xml のマニフェスト ファイルと、ソフトウェア ライセンス条項を作成するには  
  
1.  という名前のテキスト ファイルを作成する`package.xml`します。  
  
2.  Package.xml ファイルでは、ロケールを定義し、ソフトウェア ライセンス条項を含めるには、次の XML コードを追加します。 既存の XML コードを上書きしないことを確認します。  
  
    ```  
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
  
3.  UpdateConsentDialog ブートス トラップ ディレクトリに en サブディレクトリに保存します。  
  
4.  ソフトウェアのライセンス条項 eula.rtf というドキュメントを作成します。  
  
    > [!NOTE]
    >  ソフトウェアのライセンス条項は、ライセンス、保証、負債、および現地の法律に関する情報を含める必要があります。 これらのファイルは、ロケール固有のもの、MBCS または UNICODE 文字をサポートする形式でファイルを保存するようにする必要があります。 ソフトウェアのライセンス条項のコンテンツについて、法務部門を参照してください。  
  
5.  UpdateConsentDialog ブートス トラップ ディレクトリに en サブディレクトリに、ドキュメントを保存します。  
  
6.  必要に応じて、各ロケールのソフトウェア ライセンス条項の新しい package.xml マニフェスト ファイルと新しい eula.rtf ドキュメントを作成します。 たとえば、fr および de ロケールのサブディレクトリを作成した場合は、package.xml 個別マニフェスト ファイルおよびソフトウェア ライセンス条項を作成し、fr および de サブディレクトリに保存します。  
  
## <a name="setting-the-update-consent-application-as-a-prerequisite"></a>前提条件として同意アプリケーションの更新の設定  
 Visual Studio で、前提条件として、更新プログラムの同意を求めるアプリケーションを設定できます。  
  
#### <a name="to-set-the-update-consent-application-as-a-prerequisite"></a>前提条件として更新プログラムの同意を求めるアプリケーションを設定するには  
  
1.  **ソリューション エクスプ ローラー**、展開するアプリケーションの名前をクリックします。  
  
2.  **[プロジェクト]** メニューの *ProjectName* の **[プロパティ]** をクリックします。  
  
3.  をクリックして、**発行**] ページの [クリックして**の前提条件**します。  
  
4.  選択**同意ダイアログを更新**します。  
  
    > [!NOTE]
    >  前提条件 ダイアログ ボックスで更新プログラムの同意ダイアログを表示する Visual Studio を閉じて再度開くことがあります。  
  
5.  **[OK]** をクリックします。  
  
## <a name="creating-and-testing-the-setup-program"></a>作成して、セットアップ プログラムをテスト  
 前提条件として、更新プログラムの同意を求めるアプリケーションを設定した後、アプリケーションのインストーラーとブートス トラップを生成できます。  
  
#### <a name="to-create-and-test-the-setup-program-by-not-clicking-i-agree"></a>同意を作成していないをクリックしてセットアップ プログラムをテストするには  
  
1.  **ソリューション エクスプ ローラー**、展開するアプリケーションの名前をクリックします。  
  
2.  **[プロジェクト]** メニューの *ProjectName* の **[プロパティ]** をクリックします。  
  
3.  をクリックして、**発行**] ページの [クリックして**今すぐ発行**します。  
  
4.  発行の出力が自動的に開かない場合は、発行の出力に移動します。  
  
5.  Setup.exe プログラムを実行します。  
  
     セットアップ プログラムは、同意ダイアログの更新プログラムのソフトウェア使用許諾契約書を示しています。  
  
6.  ソフトウェア ライセンス条項を読み、クリックして**Accept**します。  
  
     更新プログラムの同意ダイアログ アプリケーションの表示および次のテキストが表示されます。Web 上の最新の更新プログラムをインストールしようとしているアプリケーションを確認します。 同意でクリックするは、インターネット上に自動的に更新プログラムを確認するアプリケーションを承認します。  
  
7.  アプリケーションを閉じるか、[キャンセル] をクリックします。  
  
     アプリケーションは、エラーを示しています。システム コンポーネントのインストール中にエラーが発生しました。 *ApplicationName*します。 すべてのシステム コンポーネントが正常にインストールされるまで、セットアップを続行できません。  
  
8.  次のエラー メッセージを表示する詳細をクリックします。コンポーネント更新プログラムの同意 ダイアログ ボックスは、次のエラー メッセージでのインストールに失敗しました。「自動更新の契約に同意がありません」。 次のコンポーネントがインストールに失敗しました-更新プログラムの同意 ダイアログ。  
  
9. **[閉じる]** をクリックします。  
  
#### <a name="to-create-and-test-the-setup-program-by-clicking-i-agree"></a>同意を作成してクリックして、セットアップ プログラムをテスト、するには  
  
1.  **ソリューション エクスプ ローラー**、展開するアプリケーションの名前をクリックします。  
  
2.  **[プロジェクト]** メニューの *ProjectName* の **[プロパティ]** をクリックします。  
  
3.  をクリックして、**発行**] ページの [クリックして**今すぐ発行**します。  
  
4.  発行の出力が自動的に開かない場合は、発行の出力に移動します。  
  
5.  Setup.exe プログラムを実行します。  
  
     セットアップ プログラムは、同意ダイアログの更新プログラムのソフトウェア使用許諾契約書を示しています。  
  
6.  ソフトウェア ライセンス条項を読み、クリックして**Accept**します。  
  
     更新プログラムの同意ダイアログ アプリケーションの表示および次のテキストが表示されます。Web 上の最新の更新プログラムをインストールしようとしているアプリケーションを確認します。 同意でクリックするは、インターネット上に自動的に更新プログラムを確認するアプリケーションを承認します。  
  
7.  をクリックして**同意**、 をクリックし、**続行**します。  
  
     アプリケーションは、インストールを開始します。  
  
8.  アプリケーションのインストール ダイアログ ボックスが表示されたら、クリックして**インストール**します。  
  
## <a name="see-also"></a>関連項目  
 [アプリケーション配置の必要条件](../deployment/application-deployment-prerequisites.md)   
 [ブートストラップ パッケージの作成](../deployment/creating-bootstrapper-packages.md)   
 [方法: 製品マニフェストを作成します。](../deployment/how-to-create-a-product-manifest.md)   
 [方法: パッケージ マニフェストを作成します。](../deployment/how-to-create-a-package-manifest.md)   
 [製品およびパッケージ スキーマ リファレンス](../deployment/product-and-package-schema-reference.md)
