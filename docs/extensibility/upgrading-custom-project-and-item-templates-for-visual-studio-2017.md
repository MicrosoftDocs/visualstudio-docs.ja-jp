---
title: Visual Studio 2017 用のカスタム プロジェクトと項目テンプレートの更新
titleSuffix: ''
description: Visual Studio 2017 以降のバージョンで使用するために、Visual Studio SDK の以前のバージョンからカスタム プロジェクトと項目テンプレートを更新する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: ad02477b-e101-4f32-aeb7-292bf95d5c2f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 8442e24bf971b8a2a0bcf5baeeb397e4646ba766
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060277"
---
# <a name="upgrade-custom-project-and-item-templates-for-visual-studio-2017"></a>Visual Studio 2017 用のカスタム プロジェクトと項目テンプレートの更新

Visual studio 2017 以降、Visual Studio では、以前のバージョンの Visual Studio とは異なる方法で、.vsix または .msi によってインストールされたプロジェクトおよび項目テンプレートが検出されます。 カスタム プロジェクトまたは項目テンプレートを使用する拡張機能を所有している場合は、拡張機能を更新する必要があります。 この記事では、必要な作業について説明します。

この変更は、Visual Studio 2017 のみに影響します。 以前のバージョンの Visual Studio には影響しません。

VSIX 拡張機能の一部としてプロジェクトまたは項目テンプレートを作成する場合は、「[カスタム プロジェクトおよび項目テンプレートの作成](../extensibility/creating-custom-project-and-item-templates.md)」を参照してください。

## <a name="template-scanning"></a>テンプレートのスキャン

以前のバージョンの Visual Studio では、**devenv/setup** または **devenv/installvstemplates** によりローカル ディスクがスキャンされ、プロジェクトと項目テンプレートが検索されていました。 Visual Studio 2017 以降では、スキャンはユーザー レベルの場所に対してのみ実行されます。 既定の場所は、 **%USERPROFILE%\Documents\\<Visual Studio バージョン\>\Templates\\** です。 この場所は、ウィザードで **[テンプレートを Visual Studio に自動的にインポートする]** オプションが選択されている場合に、 **[プロジェクト]**  >  **[テンプレートのエクスポート...]** コマンドによって生成されるテンプレートに使用されます。

他の (ユーザー以外の) 場所については、テンプレートの場所とその他の特性を指定するマニフェスト (.vstman) ファイルを含める必要があります。 .vstman ファイルは、テンプレートに使用される .vstemplate ファイルと共に生成されます。 .vsix を使用して拡張機能をインストールした場合は、Visual Studio 2017 で拡張機能を再コンパイルすることによってこれを実現できます。 ただし、.msi を使用する場合は、変更を手動で行う必要があります。 これらの変更を行うために必要な操作の一覧については、このページの後半にある「 **.MSI でインストールされた拡張機能の更新**」を参照してください。

## <a name="how-to-update-a-vsix-extension-with-project-or-item-templates"></a>プロジェクト テンプレートまたは項目テンプレートを使用して VSIX 拡張機能を更新する方法

1. Visual Studio 2017 でソリューションを開きます。 コードをアップグレードするように求められます。 **[OK]** をクリックします。

2. アップグレードが完了したら、インストール先のバージョンを変更することが必要になる場合があります。 VSIX プロジェクトで、source.extension.vsixmanifest ファイルを開き、 **[インストールするターゲット]** タブを選択します。 **[バージョン範囲]** フィールドが **[14.0]** の場合は、 **[編集]** をクリックし、Visual Studio 2017 を含むように変更します。 たとえば、Visual Studio 2015 または Visual Studio 2017 に拡張機能をインストールする場合は **[14.0, 15.0]** に設定し、Visual Studio 2017 だけにインストールする場合は **[15.0]** に設定できます。

3. コードを再コンパイルします。

4. Visual Studio を閉じます。

5. VSIX をインストールします。

6. 更新をテストするには、次の手順を実行します。

    1. ファイル スキャンの変更は、次のレジストリ キーによってアクティブ化されます。

         **reg add hklm\software\microsoft\visualstudio\15.0\VSTemplate /v DisableTemplateScanning /t REG_DWORD /d 1 /reg:32**

    2. キーを追加したら、 **devenv/installvstemplates** を実行します。

    3. Visual Studio を再度開きます。 予想される場所にテンプレートがあることが確認できるはずです。

    > [!NOTE]
    > Visual Studio 機能拡張プロジェクト テンプレートは、レジストリ キーが存在する場合は使用できません。 使用するには、レジストリ キーを削除し、**devenv/installvstemplates** を再実行する必要があります。

## <a name="other-recommendations-for-deploying-project-and-item-templates"></a>プロジェクト テンプレートと項目テンプレートを配置するためのその他の推奨事項

- zip 形式のテンプレート ファイルは使用しないでください。 zip 形式のテンプレート ファイルは、リソースとコンテンツを取得するために圧縮解除する必要があるため、使用すると負担が大きくなります。 代わりに、テンプレートの初期化を高速化するために、プロジェクトと項目テンプレートを個別のディレクトリに個別のファイルとして配置する必要があります。 VSIX 拡張機能の場合、VSIX ファイルの作成中に、SDK のビルド タスクによって、zip 形式のテンプレートが自動的に解凍されます。

- テンプレートの検出中に不要なリソース アセンブリが読み込まれないようにするために、テンプレート名、説明、アイコン、またはプレビューにはパッケージ/リソース ID のエントリを使用しないでください。 代わりに、ローカライズされたマニフェストを使用して、ローカライズされた名前またはプロパティを使用するロケールごとにテンプレート エントリを作成できます。

- テンプレートをファイル項目として含める場合は、マニフェストの生成によって期待どおりの結果が得られないことがあります。 その場合は、手動で生成されたマニフェストを VSIX プロジェクトに追加する必要があります。

## <a name="file-changes-in-project-and-item-templates"></a>プロジェクト テンプレートと項目テンプレートでのファイルの変更
新しいファイルを正しく作成できるように、Visual Studio 2015 と Visual Studio 2017 バージョンのテンプレート ファイルの相違点を示します。

 Visual Studio 2015 で作成された既定のプロジェクト .vstemplate ファイルを次に示します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<VSTemplate Version="3.0.0" Type="Project" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" xmlns:sdk="http://schemas.microsoft.com/developer/vstemplate-sdkextension/2010">
  <TemplateData>
    <Name>ProjectTemplate1</Name>
    <Description>ProjectTemplate1</Description>
    <Icon>ProjectTemplate1.ico</Icon>
    <ProjectType>CSharp</ProjectType>
    <RequiredFrameworkVersion>2.0</RequiredFrameworkVersion>
    <SortOrder>1000</SortOrder>
    <TemplateID>05b79cc9-2146-4716-a8e5-7e085cdd2221</TemplateID>
    <CreateNewFolder>true</CreateNewFolder>
    <DefaultName>ProjectTemplate1</DefaultName>
    <ProvideDefaultName>true</ProvideDefaultName>
  </TemplateData>
  <TemplateContent>
    <Project File="ProjectTemplate.csproj" ReplaceParameters="true">
      <ProjectItem ReplaceParameters="true" TargetFileName="Properties\AssemblyInfo.cs">AssemblyInfo.cs</ProjectItem>
      <ProjectItem ReplaceParameters="true" OpenInEditor="true">Class1.cs</ProjectItem>
    </Project>
  </TemplateContent>
</VSTemplate>

```

 次に示すのは、VSIX プロジェクトのリビルドに起因する .vstman ファイル (VSIX プロジェクトのマニフェスト ディレクトリにあります) です。

```xml
<VSTemplateManifest Version="1.0" Locale="1033" xmlns="http://schemas.microsoft.com/developer/vstemplatemanifest/2015">
  <VSTemplateContainer TemplateType="Project">
    <RelativePathOnDisk>CSharp\1033\ProjectTemplate1</RelativePathOnDisk>
    <TemplateFileName>ProjectTemplate1.vstemplate</TemplateFileName>
    <VSTemplateHeader>
      <TemplateData xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
        <Name>ProjectTemplate1</Name>
        <Description>ProjectTemplate1</Description>
        <Icon>ProjectTemplate1.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <RequiredFrameworkVersion>2.0</RequiredFrameworkVersion>
        <SortOrder>1000</SortOrder>
        <TemplateID>05b79cc9-2146-4716-a8e5-7e085cdd2221</TemplateID>
        <CreateNewFolder>true</CreateNewFolder>
        <DefaultName>ProjectTemplate1</DefaultName>
        <ProvideDefaultName>true</ProvideDefaultName>
      </TemplateData>
    </VSTemplateHeader>
  </VSTemplateContainer>
</VSTemplateManifest>

```

 [TemplateData](../extensibility/templatedata-element-visual-studio-templates.md) 要素によって提供される情報は変わりません。 **\<VSTemplateContainer>** 要素は、関連付けられているテンプレートの .vstemplate ファイルをポイントします。

 Visual Studio 2015 によって作成される既定の .vstemplate ファイルを次に示します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<VSTemplate Version="3.0.0" Type="Item" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" xmlns:sdk="http://schemas.microsoft.com/developer/vstemplate-sdkextension/2010">
  <TemplateData>
    <Name>ItemTemplate1</Name>
    <Description>ItemTemplate1</Description>
    <Icon>ItemTemplate1.ico</Icon>
    <TemplateID>bfeadf8e-a251-4109-b605-516b88e38c8d</TemplateID>
    <ProjectType>CSharp</ProjectType>
    <RequiredFrameworkVersion>2.0</RequiredFrameworkVersion>
    <NumberOfParentCategoriesToRollUp>1</NumberOfParentCategoriesToRollUp>
    <DefaultName>Class.cs</DefaultName>
  </TemplateData>
  <TemplateContent>
    <References>
      <Reference>
        <Assembly>System</Assembly>
      </Reference>
    </References>
    <ProjectItem ReplaceParameters="true">Class.cs</ProjectItem>
  </TemplateContent>
</VSTemplate>

```

 次に示すのは、VSIX プロジェクトのリビルドに起因する .vstman ファイル (VSIX プロジェクトのマニフェスト ディレクトリにあります) です。

```xml
<VSTemplateManifest Version="1.0" Locale="1033" xmlns="http://schemas.microsoft.com/developer/vstemplatemanifest/2015">
  <VSTemplateContainer TemplateType="Item">
    <RelativePathOnDisk>CSharp\1033\ItemTemplate1</RelativePathOnDisk>
    <TemplateFileName>ItemTemplate1.vstemplate</TemplateFileName>
    <VSTemplateHeader>
      <TemplateData xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
        <Name>ItemTemplate1</Name>
        <Description>ItemTemplate1</Description>
        <Icon>ItemTemplate1.ico</Icon>
        <TemplateID>bfeadf8e-a251-4109-b605-516b88e38c8d</TemplateID>
        <ProjectType>CSharp</ProjectType>
        <RequiredFrameworkVersion>2.0</RequiredFrameworkVersion>
        <NumberOfParentCategoriesToRollUp>1</NumberOfParentCategoriesToRollUp>
        <DefaultName>Class.cs</DefaultName>
      </TemplateData>
    </VSTemplateHeader>
  </VSTemplateContainer>
</VSTemplateManifest>
```

 **\<TemplateData>** 要素によって提供される情報は変わりません。 **\<VSTemplateContainer>** 要素は、関連付けられているテンプレートの .vstemplate ファイルをポイントします

 .vstman ファイルのさまざまな要素の詳細については、「[Visual Studio テンプレート マニフェスト スキーマ参照](../extensibility/visual-studio-template-manifest-schema-reference.md)」を参照してください。

## <a name="upgrades-for-extensions-installed-with-an-msi"></a>.MSI でインストールされる拡張機能のアップグレード

MSI ベースの拡張機能によっては、次のディレクトリのような一般的なテンプレートの場所にテンプレートが展開されます。

- **\<Visual Studio installation directory>\Common7\IDE\\<ProjectTemplates/ItemTemplates\>**

- **\<Visual Studio installation directory>\Common7\IDE\Extensions\\<ExtensionName\>\\<Project/ItemTemplates\>**

拡張機能で MSI ベースの配置を実行する場合は、手動でテンプレート マニフェストを生成し、拡張機能のセットアップに含まれていることを確認する必要があります。 上に示した .vstman の例と、[Visual Studio テンプレート マニフェスト スキーマ参照](../extensibility/visual-studio-template-manifest-schema-reference.md)を比較します。

プロジェクト テンプレートと項目テンプレートに個別のマニフェストを作成し、上記のようにルート テンプレート ディレクトリをポイントする必要があります。 拡張機能とロケールごとに 1 つのマニフェストを作成します。

## <a name="see-also"></a>関連項目

- [テンプレートの検出のトラブルシューティング](troubleshooting-template-discovery.md)
- [カスタム プロジェクト テンプレートと項目テンプレートの作成](creating-custom-project-and-item-templates.md)
