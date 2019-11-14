---
title: メニューコマンドのローカライズ |Microsoft Docs
ms.date: 10/08/2019
ms.topic: conceptual
helpviewer_keywords:
- localize
- localization
- vsct
- menu commands
- localize visual studio
- localize vsct
ms.assetid: b04ee0f6-82ea-47e6-853a-72382267d6da
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 94f71014440c55da0151d0ebd817aac9f5d2c7ed
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2019
ms.locfileid: "73186278"
---
# <a name="localize-menu-commands"></a>メニューコマンドのローカライズ

ローカライズさ*れた vsct*ファイルと VSPackage のローカライズさ*れた .resx*ファイルを作成し、プロジェクトファイルを更新して変更内容を反映することで、メニューとツールバーのコマンドにローカライズされたテキストを提供できます。

インストールエクスペリエンスをローカライズする方法の詳細については、「 [VSIX パッケージのローカライズ](../extensibility/localizing-vsix-packages.md)」を参照してください。

## <a name="localize-command-names"></a>コマンド名のローカライズ

Vspackage では、メニューコマンドとツールバーボタンは、 *vsct*ファイルで定義されています。

1. **ソリューションエクスプローラー**で、 *vsct*ファイルの名前を*filename. vsct*から*filename. en-us. vsct*に変更します。

2. ローカライズされた言語ごとに、*ファイル名. en-us. vsct*のコピーを作成します。

    各コピー*のファイル名を指定します。 {Locale}。 vsct。* ここで、 *{Locale}* は特定のカルチャ名です。 カルチャ名の値の一覧については、「 [Microsoft によって割り当てられたロケール id](/windows/uwp/publish/supported-languages)」を参照してください。

    これらの*ファイル名。ロケールの vsct*ファイルには、パッケージのローカライズされたメニューテキストが含まれます。

3. 各*ファイル名を開きます。* テキストをローカライズするためのロケールの vsct ファイル。

   1. [Buttontext](../extensibility/buttontext-element.md)要素の値を、特定の言語に合わせて変更します。

   2. ローカライズされたアイコンを指定する場合は、ターゲットファイルを指すように[ビットマップ](../extensibility/bitmap-element.md)値を変更します。

      次の例では、ファミリツリーエクスプローラーのツールウィンドウを開くコマンドの英語とスペイン語のボタンテキストを示しています。

      [*FamilyTree。 vsct*]

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

    [*FamilyTree.es。 vsct*]

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

## <a name="localize-other-text-resources"></a>その他のテキストリソースのローカライズ

コマンド名以外のテキストリソースは、リソース ( *.resx*) ファイルで定義されています。

1. *VSPackage*の名前を*VSPackage*に変更します。

2. ローカライズされた各言語の*VSPackage*ファイルのコピーを作成します。

     各コピー VSPackage に名前*を指定します。 {Locale} .resx。* ここで、 *{Locale}* は特定のカルチャ名です。

3. *リソース*の名前を *.resources. en-us. .resx*に変更します。

4. 各ローカライズされた言語の*リソース*のコピーを作成します。

     各コピーリソースに名前*を指定します。 {Locale} .resx。* ここで、 *{Locale}* は特定のカルチャ名です。

5. 各 *.resx*ファイルを開き、特定の言語とカルチャに合わせて文字列値を変更します。 次の例は、ツールウィンドウのタイトルバーのローカライズされたリソース定義を示しています。

     [*Resources. en-us. .resx*]

    ```xml
    <data name="ToolWindowTitle" xml:space="preserve">
      <value>Family Tree Explorer</value>
    </data>
    ```

     [*Resources.es*]

    ```xml
    <data name="ToolWindowTitle" xml:space="preserve">
      <value>Explorador del arbol genealogico</value>
    </data>
    ```

## <a name="incorporate-localized-resources-into-the-project"></a>ローカライズされたリソースをプロジェクトに組み込む

ローカライズされたリソースを組み込むには、 *assemblyinfo.cs*ファイルとプロジェクトファイルを変更する必要があります。

1. **ソリューションエクスプローラー**の **[プロパティ]** ノードで、エディターの*assemblyinfo.cs*または*assemblyinfo*を開きます。

2. 次のエントリを追加します。

    ```csharp
    [assembly: NeutralResourcesLanguage("en-US", UltimateResourceFallbackLocation.Satellite)]
    ```

     これにより、既定の言語として英語 (米国) が設定されます。

3. プロジェクトをアンロードします。

4. エディターでプロジェクトファイルを開きます。

5. ルート `Project` 要素に、既定の言語に一致する `UICulture` 要素を持つ `PropertyGroup` 要素を追加します。

    ```xml
    <PropertyGroup>
      <UICulture>en-US</UICulture>
    </PropertyGroup>
    ```

     これにより、Windows Presentation Foundation (WPF) コントロールの既定の UI カルチャとして英語 (米国) が設定されます。

6. `EmbeddedResource` 要素を含む `ItemGroup` 要素を見つけます。

7. *VSPackage*を呼び出す `EmbeddedResource` 要素で、次のように、`ManifestResourceName` 要素を `VSPackage.en-US.Resources`に設定されている `LogicalName` 要素に置き換えます。

    ```xml
    <EmbeddedResource Include="VSPackage.en-US.resx">
      <MergeWithCTO>true</MergeWithCTO>
      <LogicalName>VSPackage.en-US.Resources</LogicalName>
    </EmbeddedResource>
    ```

8. ローカライズされた言語ごとに、`VsPackage.en-US`の `EmbeddedResource` 要素をコピーし、コピーの**Include**属性と**logicalname**要素をターゲットのロケールに設定します。

9. 次の例に示すように、ローカライズされた各 `VSCTCompile` 要素に、`Menus.ctmenu`を指す `ResourceName` 要素を追加します。

    ```xml
    <ItemGroup>
      <VSCTCompile Include="LocalizedPackage.es-ES.vsct">
        <ResourceName>Menus.ctmenu</ResourceName>
      </VSCTCompile>
    </ItemGroup>
    ```

10. プロジェクトファイルを保存し、プロジェクトを再度読み込みます。

11. プロジェクトをビルドします。

     これにより、各言語のメインアセンブリとリソースアセンブリが作成されます。 デプロイプロセスのローカライズの詳細については、「 [VSIX パッケージのローカライズ](../extensibility/localizing-vsix-packages.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [メニューとコマンドを拡張する](../extensibility/extending-menus-and-commands.md)
- [アプリケーションのグローバライズとローカライズ](../ide/globalizing-and-localizing-applications.md)
