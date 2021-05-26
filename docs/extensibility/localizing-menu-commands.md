---
title: メニュー コマンドのローカライズ | Microsoft Docs
description: VSPackage に対してローカライズされた .vsct ファイルとローカライズされた .resx ファイルを作成することによって、メニューとツールバーのコマンド用にローカライズされたテキストを提供する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 10/08/2019
ms.topic: how-to
helpviewer_keywords:
- localize
- localization
- vsct
- menu commands
- localize visual studio
- localize vsct
ms.assetid: b04ee0f6-82ea-47e6-853a-72382267d6da
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 141fb0d8ba6746e7d299984461fb3ca739d931d4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073262"
---
# <a name="localize-menu-commands"></a>メニュー コマンドをローカライズする

VSPackage に対してローカライズされた *.vsct* ファイルとローカライズされた *.resx* ファイルを作成し、プロジェクト ファイルを更新して変更内容を反映することによって、メニューとツールバーのコマンド用にローカライズされたテキストを提供することができます。

インストール エクスペリエンスをローカライズする方法の詳細については、「[VSIX パッケージをローカライズする](../extensibility/localizing-vsix-packages.md)」を参照してください。

## <a name="localize-command-names"></a>コマンド名をローカライズする

VSPackage では、メニュー コマンドとツールバー ボタンは *.vsct* ファイルで定義されています。

1. **ソリューション エクスプローラー** で、 *.vsct* ファイルの名前を *filename.vsct* から *filename.en-US.vsct* に変更します。

2. ローカライズされる言語ごとに *filename.en-US.vsct* のコピーを作成します。

    各コピーに *filename.{Locale}.vsct* という名前を指定します。ここで、 *{Locale}* は特定のカルチャ名です。 カルチャ名の値の一覧については、「[Microsoft によって割り当てられているロケール ID](/windows/uwp/publish/supported-languages)」を参照してください。

    これらの *filename.Locale.vsct* ファイルには、パッケージのローカライズされたメニュー テキストが含まれています。

3. テキストをローカライズするために、それぞれの *filename.Locale.vsct* テキストを開きます。

   1. 特定の言語に合わせて [ButtonText](../extensibility/buttontext-element.md) 要素の値を変更します。

   2. ローカライズされたアイコンを提供する場合は、ターゲット ファイルを指すように [Bitmap](../extensibility/bitmap-element.md) 値を変更します。

      次の例では、Family Tree Explorer のツール ウィンドウを開くコマンドの英語とスペイン語のボタン テキストを示しています。

      [*FamilyTree.en-US.vsct*]

   ```xml
   <Button guid="guidLocalizedPackageCmdSet" id="cmdidFamilyTree" priority="0x0100" type="Button">
     <Parent guid="guidSHLMainMenu" id="IDG_VS_WNDO_OTRWNDWS1"/>
     <Icon guid="guidImages" id="bmpPic2" />
     <Strings>
       <CommandName>cmdidFamilyTree</CommandName>
       <ButtonText>Family Tree Explorer</ButtonText>
     </Strings>
   </Button>
   ```

    [*FamilyTree.es-ES.vsct*]

   ```xml
   <Button guid="guidLocalizedPackageCmdSet" id="cmdidFamilyTree" priority="0x0100" type="Button">
     <Parent guid="guidSHLMainMenu" id="IDG_VS_WNDO_OTRWNDWS1"/>
     <Icon guid="guidImages" id="bmpPic2" />
     <Strings>
       <CommandName>cmdidFamilyTree</CommandName>
       <ButtonText>Explorar el arbol genealogico</ButtonText>
     </Strings>
   </Button>
   ```

## <a name="localize-other-text-resources"></a>その他のテキスト リソースをローカライズする

コマンド名以外のテキスト リソースは、リソース ( *.resx*) ファイルで定義されています。

1. *VSPackage.resx* の名前を *VSPackage.en-US.resx* に変更します。

2. ローカライズされる言語ごとに *VSPackage.en-US.resx* ファイルのコピーを作成します。

     各コピーに *VSPackage.{Locale}.resx* という名前を指定します。ここで、 *{Locale}* は特定のカルチャ名です。

3. *Resources.resx* の名前を *Resources.en-US.resx* に変更します。

4. ローカライズされる言語ごとに *Resources.en-US.resx* ファイルのコピーを作成します。

     各コピーに *Resources.{Locale}.resx* という名前を指定します。ここで、 *{Locale}* は特定のカルチャ名です。

5. 各 *.resx* ファイルを開き、特定の言語とカルチャに合わせて文字列値を変更します。 次の例は、ツール ウィンドウのタイトル バーのローカライズされたリソース定義を示しています。

     [*Resources.en-US.resx*]

    ```xml
    <data name="ToolWindowTitle" xml:space="preserve">
      <value>Family Tree Explorer</value>
    </data>
    ```

     [*Resources.es-ES.resx*]

    ```xml
    <data name="ToolWindowTitle" xml:space="preserve">
      <value>Explorador del arbol genealogico</value>
    </data>
    ```

## <a name="incorporate-localized-resources-into-the-project"></a>ローカライズされたリソースをプロジェクトに組み込む

ローカライズされたリソースを組み込むには、*assemblyinfo.cs* ファイルとプロジェクト ファイルを変更する必要があります。

1. **ソリューション エクスプローラー** の **[プロパティ]** ノードから、エディターで *assemblyinfo.cs* または *assemblyinfo.vb* を開きます。

2. 次のエントリを追加します。

    ```csharp
    [assembly: NeutralResourcesLanguage("en-US", UltimateResourceFallbackLocation.Satellite)]
    ```

     これにより、既定の言語として英語 (米国) が設定されます。

3. プロジェクトをアンロードします。

4. エディターでプロジェクト ファイルを開きます。

5. ルートの `Project` 要素に、既定の言語に一致する `UICulture` 要素を持つ `PropertyGroup` 要素を追加します。

    ```xml
    <PropertyGroup>
      <UICulture>en-US</UICulture>
    </PropertyGroup>
    ```

     これにより、Windows Presentation Foundation (WPF) コントロールの既定の UI カルチャとして英語 (米国) が設定されます。

6. `EmbeddedResource` 要素を含む `ItemGroup` 要素を探します。

7. *VSPackage.en-US.resx* を呼び出す `EmbeddedResource` 要素で、次のように、`ManifestResourceName` 要素を、`VSPackage.en-US.Resources` に設定された `LogicalName` 要素に置き換えます。

    ```xml
    <EmbeddedResource Include="VSPackage.en-US.resx">
      <MergeWithCTO>true</MergeWithCTO>
      <LogicalName>VSPackage.en-US.Resources</LogicalName>
    </EmbeddedResource>
    ```

8. ローカライズされる言語ごとに、`VsPackage.en-US` の `EmbeddedResource` 要素をコピーし、コピーの **Include** 属性と **LogicalName** 要素をターゲットのロケールに設定します。

9. 次の例に示すように、ローカライズされた各 `VSCTCompile` 要素に、`Menus.ctmenu` を指す `ResourceName` 要素を追加します。

    ```xml
    <ItemGroup>
      <VSCTCompile Include="LocalizedPackage.es-ES.vsct">
        <ResourceName>Menus.ctmenu</ResourceName>
      </VSCTCompile>
    </ItemGroup>
    ```

10. プロジェクト ファイルを保存してプロジェクトを再度読み込みます。

11. プロジェクトをビルドします。

     これにより、各言語のメイン アセンブリとリソース アセンブリが作成されます。 デプロイ プロセスのローカライズの詳細については、「[VSIX パッケージをローカライズする](../extensibility/localizing-vsix-packages.md)」を参照してください

## <a name="see-also"></a>関連項目

- [メニューとコマンドを拡張する](../extensibility/extending-menus-and-commands.md)
- [アプリケーションのグローバライズとローカライズ](../ide/globalizing-and-localizing-applications.md)
