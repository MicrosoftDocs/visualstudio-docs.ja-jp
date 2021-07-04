---
title: 'チュートリアル: C++ を使用して SDK を作成する | Microsoft Docs'
description: ネイティブ C++ の数値演算ライブラリ SDK を作成し、その SDK を Visual Studio 拡張機能としてパッケージ化してから、このチュートリアルを使用してアプリを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 36ea793b-3832-41a1-b906-69e680ad5e1d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6a52322e575dc201a6bf1648af93d813828e0b17
ms.sourcegitcommit: 8b75524dc544e34d09ef428c3ebbc9b09f14982d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2021
ms.locfileid: "113223008"
---
# <a name="walkthrough-create-an-sdk-using-c"></a>チュートリアル: C++ を使用して SDK を作成する
このチュートリアルでは、ネイティブ C++ 数値演算ライブラリ SDK を作成し、SDK を Visual Studio 拡張機能 (VSIX) としてパッケージ化して、それを使用してアプリを作成する方法について説明します。 このチュートリアルは、次のステップに分かれています。

- [ネイティブ ライブラリと Windows ランタイム ライブラリを作成するには](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createClassLibrary)

- [NativeMathVSIX 拡張機能プロジェクトを作成するには](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createVSIX)

- [クラス ライブラリを使用するサンプル アプリを作成するには](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createSample)

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「[Visual Studio SDK](../extensibility/visual-studio-sdk.md)」を参照してください。

## <a name="to-create-the-native-and-windows-runtime-libraries"></a><a name="createClassLibrary"></a>ネイティブ ライブラリと Windows ランタイム ライブラリを作成するには

1. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。

2. テンプレートの一覧で **[Visual C++]**  >  **[Windows ユニバーサル]** を展開し、 **[DLL (Windows ユニバーサル アプリ)]** テンプレートを選択します。 **[名前]** ボックスで「`NativeMath`」と指定してから、 **[OK]** ボタンを選択します。

3. 次のコードに一致するように *NativeMath.h* を更新します。

     :::code language="cpp" source="../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcpp/cpp/nativemath/nativemath.h" id="Snippet1":::

4. 次のコードに一致するように *NativeMath.cpp* を更新します。

     :::code language="cpp" source="../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcpp/cpp/nativemath/nativemath.cpp" id="Snippet2":::

5. **ソリューション エクスプローラー** で、 **['NativeMath' ソリューション]** のショートカット メニューを開き、 **[追加]**  >  **[新しいプロジェクト]** の順に選択します。

6. テンプレートの一覧で **[Visual C++]** を展開し、 **[Windows ランタイム コンポーネント]** テンプレートを選択します。 **[名前]** ボックスで「`NativeMathWRT`」と指定してから、 **[OK]** ボタンを選択します。

7. 次のコードに一致するように *Class1.h* を更新します。

     :::code language="cpp" source="../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcpp/cpp/nativemathwrt/class1.h" id="Snippet3":::

8. 次のコードに一致するように *Class1.cpp* を更新します。

     :::code language="cpp" source="../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcpp/cpp/nativemathwrt/class1.cpp" id="Snippet4":::

9. メニュー バーで、 **[ビルド]**  >  **[ソリューションのビルド]** の順にクリックします。

## <a name="to-create-the-nativemathvsix-extension-project"></a><a name="createVSIX"></a>NativeMathVSIX 拡張機能プロジェクトを作成するには

1. **ソリューション エクスプローラー** で、 **['NativeMath' ソリューション]** のショートカット メニューを開き、 **[追加]**  >  **[新しいプロジェクト]** の順に選択します。

2. テンプレートの一覧で、 **[Visual C#]**  >  **[機能拡張]** を展開し、 **[VSIX プロジェクト]** を選択します。 **[名前]** ボックスで「**NativeMathVSIX**」と指定してから、 **[OK]** ボタンを選択します。

3. **ソリューション エクスプローラー** で、**source.extension.vsixmanifest** ファイルのショートカット メニューを開き、 **[コードの表示]** を選択します。

4. 次の XML で既存の XML を置き換えます。

    ```xml
    <PackageManifest Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema/2011" xmlns:d="http://schemas.microsoft.com/developer/vsx-schema-design/2011">
      <Metadata>
        <Identity Id="NativeMathVSIX..c6b3cae1-e7e2-4e71-90f6-21017ea0dff7" Version="1.0" Language="en-US" Publisher="MyName" />
        <DisplayName>Native Math SDK</DisplayName>
        <Description>Native Math Library w/ Windows Runtime Additions</Description>
      </Metadata>
      <Installation Scope="Global" AllUsers="true">
        <InstallationTarget Id="Microsoft.ExtensionSDK" TargetPlatformIdentifier="Windows" TargetPlatformVersion="v8.0" SdkName="NativeMathSDK" SdkVersion="1.0" />
      </Installation>
      <Dependencies>
      </Dependencies>
      <Assets>
        <Asset Type="Microsoft.ExtensionSDK" d:Source="File" Path="SDKManifest.xml" />
      </Assets>
    </PackageManifest>
    ```

5. **ソリューション エクスプローラー** で、**NativeMathVSIX** プロジェクトのショートカット メニューを開き、 **[追加]**  >  **[新しい項目]** を選択します。

6. **Visual C# の項目** の一覧で、 **[データ]** を展開し、 **[XML ファイル]** を選択します。 **[名前]** ボックスで「`SDKManifest.xml`」と指定してから、 **[OK]** ボタンを選択します。

7. 次の XML を使用してファイルの内容を置き換えます。

    :::code language="xml" source="../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcpp/cpp/nativemathvsix/sdkmanifest.xml" id="Snippet5":::

8. **ソリューション エクスプローラー** の **NativeMathVSIX** プロジェクトで、次のフォルダー構造を作成します。

    ```xml
    \DesignTime
          \CommonConfiguration
                \Neutral
                      \Include
          \Debug
                \x86
    \Redist
          \Debug
                \x86
    \References
          \CommonConfiguration
                \Neutral
    ```

9. **ソリューション エクスプローラー** で **['NativeMath' ソリューション]** ショートカット メニューを開いてから、 **[エクスプローラーでフォルダーを開く]** を選択します。

10. **エクスプローラー** で *$SolutionRoot$\NativeMath\NativeMath.h* をコピーし、**ソリューション エクスプローラー** で、**NativeMathVSIX** プロジェクトの下の *$SolutionRoot$\NativeMathVSIX\DesignTime\CommonConfiguration\Neutral\Include\\* フォルダーに貼り付けます。

     *$SolutionRoot$\Debug\NativeMath\NativeMath.lib* をコピーし、 *$SolutionRoot$\NativeMathVSIX\DesignTime\Debug\x86\\* フォルダーに貼り付けます。

     *$SolutionRoot$\Debug\NativeMath\NativeMath.dll* をコピーし、 *$SolutionRoot$\NativeMathVSIX\Redist\Debug\x86\\* フォルダーに貼り付けます。

     *$SolutionRoot$\Debug\NativeMathWRT\NativeMathWRT.dll* をコピーし、 *$SolutionRoot$\NativeMathVSIX\Redist\Debug\x86* フォルダーに貼り付けます。
     *$SolutionRoot$\Debug\NativeMathWRT\NativeMathWRT.winmd* をコピーし、 *$SolutionRoot$\NativeMathVSIX\References\CommonConfiguration\Neutral* フォルダーに貼り付けます。

     *$SolutionRoot$\Debug\NativeMathWRT\NativeMathWRT.pri* をコピーし、 *$SolutionRoot$\NativeMathVSIX\References\CommonConfiguration\Neutral* フォルダーに貼り付けます。

11. *$SolutionRoot$\NativeMathVSIX\DesignTime\Debug\x86\\* フォルダーに、*NativeMathSDK.props* という名前のテキスト ファイルを作成し、次の内容を貼り付けます。
   
    ```xml
    <Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
      <PropertyGroup>
        <NativeMathSDKPath>$(FrameworkSDKRoot)\..\..\UAP\v0.8.0.0\ExtensionSDKs\NativeMathSDK\1.0\</NativeMathSDKPath>
        <IncludePath>$(NativeMathSDKPath)DesignTime\CommonConfiguration\Neutral\Include;$(IncludePath)</IncludePath>
        <LibraryPath>$(NativeMathSDKPath)DesignTime\Debug\x86;$(LibraryPath)</LibraryPath>
      </PropertyGroup>
      <ItemDefinitionGroup Condition="'$(Configuration)|$(Platform)'=='Debug|Win32'">
         <Link>
           <AdditionalDependencies>NativeMath.lib;%(AdditionalDependencies)</AdditionalDependencies>
         </Link>
      </ItemDefinitionGroup>
    </Project>
    ```

12. メニューバーで、 **[表示]**  >  **[他のウィンドウ]**  >  **[プロパティウィンドウ]** を選択します (キーボード: **F4** キーを押します)。

13. **ソリューション エクスプローラー** で、**NativeMathWRT.winmd** ファイルを選択します。 **[プロパティ]** ウィンドウで、 **[ビルド アクション]** プロパティを **[コンテンツ]** に変更してから、 **[VSIX に含める]** プロパティを **[True]** に変更します。

     **NativeMath.h** ファイルに対してこのプロセスを繰り返します。

     **NativeMathWRT.pri** ファイルに対してこのプロセスを繰り返します。

     **NativeMath.Lib** ファイルに対してこのプロセスを繰り返します。

     **NativeMathSDK.props** ファイルに対してこのプロセスを繰り返します。

14. **ソリューション エクスプローラー** で、**NativeMath.h** ファイルを選択します。 **[プロパティ]** ウィンドウで、 **[VSIX に含める]** プロパティを **[True]** に変更します。

     **NativeMath.dll** ファイルに対してこのプロセスを繰り返します。

     **NativeMathWRT.dll** ファイルに対してこのプロセスを繰り返します。

     **SDKManifest.xml** ファイルに対してこのプロセスを繰り返します。

15. メニュー バーで、 **[ビルド]**  >  **[ソリューションのビルド]** の順にクリックします。

16. **ソリューション エクスプローラー** で **[NativeMathVSIX]** プロジェクトのショートカット メニューを開いてから、 **[エクスプローラーでフォルダーを開く]** を選択します。

17. **エクスプローラー** で、 *$SolutionRoot$\NativeMathVSIX\bin\Debug* フォルダーに移動し、次に *NativeMathVSIX.vsix* を実行してインストールを開始します。

18. **[インストール]** ボタンをクリックし、インストールが完了するのを待ちます。次に、Visual Studio を開きます。

## <a name="to-create-a-sample-app-that-uses-the-class-library"></a><a name="createSample"></a> クラス ライブラリを使用するサンプル アプリを作成するには

1. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。

2. テンプレートの一覧で、 **[Visual C++]**  >  **[Windows ユニバーサル]** を展開し、 **[空のアプリ]** を選択します。 **[名前]** ボックスで「**NativeMathSDKSample**」と指定してから、 **[OK]** ボタンを選択します。

3. **ソリューション エクスプローラー** で、**NativeMathSDKSample** プロジェクトのショートカット メニューを開いて、 **[追加]**  >  **[参照]** を選択します。

4. **[参照の追加]** ダイアログ ボックスの [参照の種類] の一覧で、 **[ユニバーサル Windows]** を展開し、 **[拡張機能]** を選択します。 最後に、 **[Native Math SDK]** チェック ボックスをオンにし、 **[OK]** をクリックします。

5. NativeMathSDKSample のプロジェクト プロパティを表示します。

    参照を追加したときに、*NativeMathSDK.props* に定義したプロパティが適用されました。 プロジェクトの **[構成プロパティ]** の **[VC++ ディレクトリ]** プロパティを調べることで、プロパティが適用されたことを確認できます。

6. **ソリューション エクスプローラー** で **[MainPage.xaml]** を開き、次の XAML を使用して内容を置き換えます。

    :::code language="xml" source="../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcppdemoapp/cpp/mainpage.xaml" id="Snippet1":::

7. 次のコードに一致するように *Mainpage.xaml.h* を更新します。

    :::code language="cpp" source="../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcppdemoapp/cpp/mainpage.xaml.h" id="Snippet2":::

8. 次のコードに一致するように *MainPage.xaml.cpp* を更新します。

    :::code language="cpp" source="../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcppdemoapp/cpp/mainpage.xaml.cpp" id="Snippet3":::

9. **F5** キーを押してアプリを実行します。

10. アプリで、任意の 2 つの数値を入力し、操作を選択して、 **=** ボタンを選択します。

     正しい結果が表示されます。

    このチュートリアルでは、拡張 SDK を作成して使用し、[!INCLUDE[wrt](../extensibility/includes/wrt_md.md)] ライブラリと [!INCLUDE[wrt](../extensibility/includes/wrt_md.md)] 以外のライブラリを呼び出す方法について説明しました。

## <a name="next-steps"></a>次のステップ

## <a name="see-also"></a>関連項目
- [チュートリアル: C# または Visual Basic を使用して SDK を作成する](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md)
- [ソフトウェア開発キットを作成する](../extensibility/creating-a-software-development-kit.md)
