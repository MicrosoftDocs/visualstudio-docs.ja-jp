---
title: ソフトウェア開発キットを作成する | Microsoft Docs
description: SDK の一般的なインフラストラクチャと、プラットフォーム SDK と拡張 SDK の作成方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 8496afb4-1573-4585-ac67-c3d58b568a12
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: bc762912abdc58b33e49406dd46cadd152f732b6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089369"
---
# <a name="create-a-software-development-kit"></a>ソフトウェア開発キットを作成する

ソフトウェア開発キット (SDK) は、Visual Studio で 1 つの項目として参照できる API のコレクションです。 **[参照マネージャー]** ダイアログ ボックスでは、プロジェクトに関連するすべての SDK が一覧表示されます。 SDK をプロジェクトに追加すると、Visual Studio で API を使用できるようになります。

SDK には 2 つの種類があります。

- プラットフォーム SDK は、プラットフォーム用のアプリを開発するための必須コンポーネントです。 たとえば、[!INCLUDE[win81](../debugger/includes/win81_md.md)] SDK は [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] アプリを開発するために必要です。

- 拡張 SDK は、プラットフォームを拡張するオプションのコンポーネントですが、そのプラットフォーム用のアプリを開発するために必須ではありません。

以下のセクションでは、SDK の一般的なインフラストラクチャと、プラットフォーム SDK と拡張 SDK の作成方法について説明します。

## <a name="platform-sdks"></a>プラットフォーム SDK

プラットフォーム用のアプリを開発するには、プラットフォーム SDK が必要です。 たとえば、[!INCLUDE[win81](../debugger/includes/win81_md.md)] SDK は [!INCLUDE[win81](../debugger/includes/win81_md.md)] 用のアプリを開発するために必要です。

### <a name="installation"></a>インストール

すべてのプラットフォーム SDK は、"*HKLM\Software\Microsoft\Microsoft SDKs\\[TPI]\v[TPV]\\@InstallationFolder = [SDK ルート]* " にインストールされます。 したがって、[!INCLUDE[win81](../debugger/includes/win81_md.md)] SDK は、*HKLM\Software\Microsoft\Microsoft SDKs\Windows\v8.1* にインストールされます。

### <a name="layout"></a>Layout

プラットフォーム SDK のレイアウトは次のとおりです。

```
\[InstallationFolder root]
            SDKManifest.xml
            \References
                  \[config]
                        \[arch]
            \DesignTime
                  \[config]
                        \[arch]
```

| Node | 説明 |
|------------------------| - |
| "*参照*" フォルダー | コーディング可能な API を含むバイナリが格納されています。 これには、Windows メタデータ (WinMD) ファイルまたはアセンブリが含まれます。 |
| "*デザイン時*" フォルダー | 実行前またはデバッグ時にのみ必要なファイルが格納されています。 これには、XML ドキュメント、ライブラリ、ヘッダー、ツールボックスのデザイン時バイナリ、MSBuild 成果物などが含まれます。<br /><br /> XML ドキュメントは *\DesignTime* フォルダーに配置するのが理想的ですが、参照用の XML ドキュメントは引き続き Visual Studio の参照ファイルと共に配置されます。 たとえば、参照 <em>\References\\[config]\\[arch]\sample.dll</em> 用の XML ドキュメントは *\References\\[config]\\[arch]\sample.xml* であり、そのドキュメントのローカライズ版は *\References\\[config]\\[arch]\\[locale]\sample.xml* です。 |
| "*構成*" フォルダー | フォルダーは、*Debug*、*Retail*、*CommonConfiguration* の 3 つしかありません。 SDK の作成者は、SDK のコンシューマーが対象とする構成に関係なく同じ SDK ファイル セットを使用する必要がある場合に、それらのファイルを *CommonConfiguration* の下に配置できます。 |
| "*アーキテクチャ*" フォルダー | サポートされているすべての "*アーキテクチャ*" フォルダーが存在する可能性があります。 Visual Studio では、x86、x64、ARM、およびニュートラル アーキテクチャがサポートされています。 注: Win32 は x86 にマップされ、AnyCPU はニュートラルにマップされます。<br /><br /> MSBuild は、プラットフォーム SDK の *\CommonConfiguration\neutral* の下のみ参照します。 |
| *SDKManifest.xml* | このファイルでは、Visual Studio で SDK をどのように使用するかを記述します。 [!INCLUDE[win81](../debugger/includes/win81_md.md)] の SDK マニフェストは次のようになっています。<br /><br /> `<FileList             DisplayName = "Windows"             PlatformIdentity = "Windows, version=8.1"             TargetFramework = ".NET for Windows Store apps, version=v4.5.1; .NET Framework, version=v4.5.1"             MinVSVersion = "14.0">              <File Reference = "Windows.winmd">                <ToolboxItems VSCategory = "Toolbox.Default" />             </File> </FileList>`<br /><br /> **DisplayName:** オブジェクト ブラウザーで参照一覧に表示される値。<br /><br /> **PlatformIdentity:** この属性が存在する場合、SDK がプラットフォーム SDK であること、およびその SDK から追加された参照をローカルにコピーできないことが Visual Studio と MSBuild に通知されます。<br /><br /> **TargetFramework:** この属性は、この属性の値に指定されているものと同じフレームワークを対象とするプロジェクトだけが SDK を使用できるようにするために、Visual Studio によって使用されます。<br /><br /> **MinVSVersion:** この属性は、適用される SDK のみを使用するために Visual Studio によって使用されます。<br /><br /> **Reference:** この属性は、コントロールを含む参照に対してのみ指定する必要があります。 参照にコントロールが含まれているかどうかを指定する方法については、以下を参照してください。 |

## <a name="extension-sdks"></a>拡張 SDK

以下のセクションでは、拡張 SDK をデプロイするために必要な作業について説明します。

### <a name="installation"></a>インストール

拡張 SDK は、レジストリ キーを指定せずに、特定のユーザーまたはすべてのユーザーに対してインストールできます。 すべてのユーザーに対して SDK をインストールするには、次のパスを使用します。

*%Program Files%\Microsoft SDKs\<target platform\>\v<プラットフォームのバージョン番号\>\ExtensionSDKs*

ユーザー固有のインストールの場合は、次のパスを使用します。

*%USERPROFILE%\AppData\Local\Microsoft SDKs\<target platform\>\v<プラットフォームのバージョン番号\>\ExtensionSDKs*

別の場所を使用する場合は、次の 2 つのいずれかを実行する必要があります。

1. レジストリ キーで指定します。

     **HKLM\Software\Microsoft\Microsoft SDKs\<target platform>\v<プラットフォームのバージョン番号\>\ExtensionSDKs\<SDKName>\<SDKVersion>** \

     `<path to SDK><SDKName><SDKVersion>` の値を持つ (既定の) サブキーを追加します。

2. MSBuild プロパティ `SDKReferenceDirectoryRoot` をプロジェクト ファイルに追加します。 このプロパティの値は、参照する拡張 SDK が存在するディレクトリのセミコロン区切りの一覧です。

### <a name="installation-layout"></a>インストール レイアウト

拡張 SDK のインストール レイアウトは次のとおりです。

```
\<ExtensionSDKs root>
           \<SDKName>
                 \<SDKVersion>
                        SDKManifest.xml
                        \References
                              \<config>
                                    \<arch>
                        \Redist
                              \<config>
                                    \<arch>
                        \DesignTime
                               \<config>
                                     \<arch>

```

1. \\<SDKName\>\\<SDKVersion\>: 拡張 SDK の名前とバージョンは、SDK ルートのパス内の対応するフォルダー名から導かれます。 MSBuild ではこの ID を使用してディスク上の SDK が検索され、Visual Studio では **[プロパティ]** ウィンドウと **[参照マネージャー]** ダイアログにこの ID が表示されます。

2. "*参照*" フォルダー: API を含むバイナリ。 これには、Windows メタデータ (WinMD) ファイルまたはアセンブリが含まれます。

3. "*再頒布*" フォルダー: ランタイム/デバッグに必要であり、ユーザーのアプリケーションの一部としてパッケージ化する必要があるファイル。 すべてのバイナリは、 *\redist\\<config\>\\<arch\>* の下に配置する必要があります。また、バイナリ名は、一意性を確保するために *]* \<company>.\<product>.\<purpose>.\<extension> <em>の形式にする必要があります。たとえば、*Microsoft.Cpp.Build.dll</em> のようになります。 他の SDK のファイル名と競合する可能性のある名前を持つすべてのファイル (javascript、css、pri、xaml、png、jpg ファイルなど) は、<em>\redist\\<config\>\\<arch\>\\<sdkname\>\* の下に配置する必要があります。ただし、XAML コントロールに関連付けられているファイルを除きます。これらのファイルは、*\redist\\<config\>\\<arch\>\\<componentname\>\\</em> の下に配置する必要があります。

4. "*デザイン時*" フォルダー: 実行前またはデバッグ時にのみ必要であり、ユーザーのアプリケーションの一部としてパッケージ化することができないファイル。 これには、XML ドキュメント、ライブラリ、ヘッダー、ツールボックスのデザイン時バイナリ、MSBuild 成果物などが含まれます。 ネイティブ プロジェクトでの使用を目的とした SDK には、*SDKName.props* ファイルが含まれている必要があります。 この種類のファイルの例を次に示します。

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
     <PropertyGroup>
       <ExecutablePath>C:\Temp\ExecutablePath;$(ExecutablePath)</ExecutablePath>
       <IncludePath>$(FrameworkSDKRoot)\..\v8.1\ExtensionSDKs\cppimagingsdk\1.0\DesignTime\CommonConfiguration\Neutral\include;$(IncludePath)</IncludePath>
       <AssemblyReferencePath>C:\Temp\AssemblyReferencePath;(AssemblyReferencePath)</AssemblyReferencePath>
       <LibraryPath>$(FrameworkSDKRoot)\..\v8.1\ExtensionSDKs\cppimagingsdk\1.0\DesignTime\Debug\ARM;$(LibraryPath)</LibraryPath>
       <SourcePath>C:\Temp\SourcePath\X64;$(SourcePath)</SourcePath>
       <ExcludePath>C:\Temp\ExcludePath\X64;$(ExcludePath)</ExcludePath>
       <_PropertySheetDisplayName>DevILSDK, 1.0</_PropertySheetDisplayName>
     </PropertyGroup>
   </Project>

   ```

    XML 参照ドキュメントは、参照ファイルと共に配置されます。 たとえば、 *\References\\<config\>\\<arch\>\sample.dll* アセンブリの XML 参照ドキュメントは *\References\\<config\>\\<arch\>\sample.xml* であり、そのドキュメントのローカライズ版は *\References\\<config\>\\<arch\>\\<locale\>\sample.xml* です。

5. "*構成*" フォルダー: *Debug*、*Retail*、*CommonConfiguration* の 3 つのサブフォルダー。 SDK の作成者は、SDK のコンシューマーの対象となる構成に関係なく同じ SDK ファイル セットを使用する必要がある場合に、それらのファイルを *CommonConfiguration* の下に配置できます。

6. "*アーキテクチャ*" フォルダー: x86、x64、ARM、ニュートラルの各アーキテクチャがサポートされています。 Win32 は x86 にマップされ、AnyCPU はニュートラルにマップされます。

### <a name="sdkmanifestxml"></a>SDKManifest.xml

*SDKManifest.xml* ファイルでは、Visual Studio で SDK をどのように使用するかを記述します。 次に例を示します。

```
<FileList>
DisplayName = "My SDK"
ProductFamilyName = "My SDKs"
TargetFramework = ".NETCore, version=v4.5.1; .NETFramework, version=v4.5.1"
MinVSVersion = "14.0"
MaxPlatformVersion = "8.1"
AppliesTo = "WindowsAppContainer + WindowsXAML"
SupportPrefer32Bit = "True"
SupportedArchitectures = "x86;x64;ARM"
SupportsMultipleVersions = "Error"
CopyRedistToSubDirectory = "."
DependsOn = "SDKB, version=2.0"
MoreInfo = "https://msdn.microsoft.com/MySDK">
<File Reference = "MySDK.Sprint.winmd" Implementation = "XNASprintImpl.dll">
<Registration Type = "Flipper" Implementation = "XNASprintFlipperImpl.dll" />
<Registration Type = "Flexer" Implementation = "XNASprintFlexerImpl.dll" />
<ToolboxItems VSCategory = "Toolbox.Default" />
</File>
</FileList>
```

ファイルの要素を次の一覧に示します。

1. DisplayName: 参照マネージャー、ソリューション エクスプローラー、オブジェクト ブラウザー、および Visual Studio のユーザー インターフェイスのその他の場所に表示される値。

2. ProductFamilyName: SDK 製品全体の名前。 たとえば、[!INCLUDE[winjs_long](../debugger/includes/winjs_long_md.md)] SDK には、"Microsoft.WinJS.1.0" と "Microsoft.WinJS.2.0" という名前が付けられています。これらは、SDK 製品ファミリの同じファミリ "Microsoft.WinJS" に属しています。 この属性によって、Visual Studio と MSBuild でその接続を行うことが許可されます。 この属性が存在しない場合は、SDK 名が製品ファミリ名として使用されます。

3. FrameworkIdentity: 1 つ以上の Windows コンポーネント ライブラリに対する依存関係を指定します。 この属性の値は、使用アプリのマニフェストに格納されます。 この属性は、Windows コンポーネント ライブラリにのみ適用できます。

4. TargetFramework: 参照マネージャーとツールボックスで使用できる SDK を指定します。 これは、ターゲット フレームワーク モニカーのセミコロン区切りの一覧です。たとえば、".NET Framework, version=v2.0; .NET Framework, version=v4.5.1" のようになります。 同じターゲット フレームワークの複数のバージョンが指定されている場合、参照マネージャーのフィルター処理では、指定された最も低いバージョンが使用されます。 たとえば、".NET Framework, version=v2.0; .NET Framework, version=v4.5.1" が指定されている場合、参照マネージャーでは ".NET Framework, version=v2.0" が使用されます。 特定のターゲット フレームワーク プロファイルが指定されている場合、参照マネージャーではそのプロファイルだけがフィルター処理に使用されます。 たとえば、"Silverlight, version=v4.0, profile=WindowsPhone" を指定した場合、参照マネージャーでは Windows Phone プロファイルのみがフィルター処理されます。完全な Silverlight 4.0 フレームワークを対象とするプロジェクトでは、参照マネージャーで SDK が表示されません。

5. MinVSVersion: Visual Studio の最小バージョン。

6. MaxPlatformVerson: 拡張 SDK が動作しないプラットフォームのバージョンを指定するには、ターゲット プラットフォームの最大バージョンを使用する必要があります。 たとえば、Microsoft Visual C++ ランタイム パッケージ v11.0 は、Windows 8 プロジェクトでのみ参照する必要があります。 このため、Windows 8 プロジェクトの MaxPlatformVersion は 8.0 です。 これは、参照マネージャーのフィルター処理で Windows 8.1 プロジェクトの Microsoft Visual C++ ランタイム パッケージが除外され、MSBuild では [!INCLUDE[win81](../debugger/includes/win81_md.md)] プロジェクトが参照したときにエラーがスローされることを意味します。 注: この要素は [!INCLUDE[vs_dev12](../extensibility/includes/vs_dev12_md.md)] 以降でサポートされています。

7. AppliesTo: 適用可能な Visual Studio プロジェクト タイプを指定して、参照マネージャーで使用できる SDK を指定します。 WindowsAppContainer、VisualC、VB、CSharp、WindowsXAML、JavaScript、Managed、Native の 9 つの値が認識されます。 SDK の作成者は、SDK に適用されるプロジェクト タイプのスコープを厳密に指定するために、and ("+")、or ("&#124;")、not ("!") の演算子を使用できます。

    WindowsAppContainer は、[!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] アプリのプロジェクトを識別します。

8. SupportPrefer32Bit: サポートされている値は "True" と "False" です。 既定値は "True" です。 値が "False" に設定されている場合、SDK を参照しているプロジェクトで Prefer32Bit が有効になっていると、MSBuild は [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] プロジェクトに対してエラー (または、デスクトップ プロジェクトの場合は警告) を返します。 Prefer32Bit の詳細については、「[[ビルド] ページ (プロジェクト デザイナー) (C#)](../ide/reference/build-page-project-designer-csharp.md)」または「[[コンパイル] ページ、プロジェクト デザイナー (Visual Basic)](../ide/reference/compile-page-project-designer-visual-basic.md)」を参照してください。

9. SupportedArchitectures: SDK でサポートされている、セミコロンで区切られたアーキテクチャの一覧。 使用中のプロジェクトで対象の SDK アーキテクチャがサポートされていない場合、MSBuild では警告が表示されます。 この属性が指定されていない場合、MSBuild ではこの種類の警告は表示されません。

10. SupportsMultipleVersions: この属性が **Error** または **Warning** に設定されている場合、MSBuild は同じプロジェクトが同じ SDK ファミリの複数のバージョンを参照できないことを示します。 この属性が存在しない場合、または **Allow** に設定されている場合、MSBuild ではこの種類のエラーまたは警告は表示されません。

11. AppX: ディスク上の Windows コンポーネント ライブラリのアプリ パッケージのパスを指定します。 この値は、ローカル デバッグ中に Windows コンポーネント ライブラリの登録コンポーネントに渡されます。 ファイル名の名前付け規則は、 *\<Company>.\<Product>.\<Architecture>.\<Configuration>.\<Version>.appx* です。 Windows コンポーネント ライブラリに適用されない場合、属性名と属性値の構成とアーキテクチャは省略可能です。 この値は、Windows コンポーネント ライブラリにのみ適用できます。

12. CopyRedistToSubDirectory: アプリ パッケージ ルート (つまり、**アプリ パッケージの作成** ウィザードで選択した **[パッケージの場所]** ) およびランタイム レイアウト ルートを基準として、 *\redist* フォルダーの下にあるファイルをコピーする場所を指定します。 既定の場所は、アプリ パッケージと **F5** レイアウトのルートです。

13. DependsOn: この SDK が依存する SDK を定義する SDK ID の一覧。 この属性は、参照マネージャーの詳細ペインに表示されます。

14. MoreInfo: ヘルプと詳細情報を提供する Web ページの URL。 この値は、参照マネージャーの右ペインにある [詳細情報] リンクで使用されます。

15. Registration Type: アプリ マニフェストの WinMD 登録を指定します。これは、対応する実装 DLL を持つネイティブ WinMD に必要です。

16. File Reference: コントロールが含まれているかネイティブ WinMD である参照のみに対して指定されています。 参照にコントロールが含まれているかどうかを指定する方法については、以下の「[ツールボックス項目の場所を指定する](#ToolboxItems)」を参照してください。

## <a name="specify-the-location-of-toolbox-items"></a><a name="ToolboxItems"></a> ツールボックス項目の場所を指定する

*SDKManifest.xml* スキーマの **ToolBoxItems** 要素では、プラットフォーム SDK と拡張 SDK の両方で、ツールボックス項目のカテゴリと場所を指定します。 異なる場所を指定する例を次に示します。 これは、WinMD 参照または DLL 参照に適用されます。

1. ツールボックスの既定のカテゴリにコントロールを配置します。

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Toolbox.Default"/>
    </File>
    ```

2. 特定のカテゴリ名の下にコントロールを配置します。

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory= "MyCategoryName"/>
    </File>
    ```

3. 特定のカテゴリ名の下にコントロールを配置します。

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Graph">
        <ToolboxItems/>
        <ToolboxItems VSCategory = "Data">
        <ToolboxItems />
    </File>
    ```

4. Blend と Visual Studio で、異なるカテゴリ名の下にコントロールを配置します。

    ```xml
    // Blend accepts a slightly different structure for the category name because it allows a path rather than a single category.
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Graph" BlendCategory = "Controls/sample/Graph">
        <ToolboxItems />
    </File>
    ```

5. Blend と Visual Studio で特定のコントロールを別々に列挙します。

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Graph">
        <ToolboxItems/>
        <ToolboxItems BlendCategory = "Controls/sample/Graph">
        <ToolboxItems/>
    </File>
    ```

6. 特定のコントロールを列挙し、Visual Studio の共通パスの下に配置するか、[すべてのコントロール] グループだけに配置します。

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Toolbox.Common">
        <ToolboxItems />
        <ToolboxItems VSCategory = "Toolbox.All">
        <ToolboxItems />
    </File>
    ```

7. 特定のコントロールを列挙し、ツールボックスに表示せずに選択された項目の特定のセットのみを表示します。

    ```xml
    <File Reference = "sample.winmd">
        <ToolboxItems VSCategory = "Toolbox.ChooseItemsOnly">
        <ToolboxItems />
    </File>
    ```

## <a name="see-also"></a>関連項目

- [チュートリアル: C++ を使用して SDK を作成する](../extensibility/walkthrough-creating-an-sdk-using-cpp.md)
- [チュートリアル: C# または Visual Basic を使用して SDK を作成する](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md)
- [プロジェクト内の参照の管理](../ide/managing-references-in-a-project.md)
