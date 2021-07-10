---
title: Visual Studio 拡張機能を更新するための ImageOptimizer サンプル
description: 例に従って、Visual Studio 2022 Preview で動作するように Visual Studio 拡張機能を更新する方法について学習します。
ms.date: 06/08/2021
ms.topic: sample
author: leslierichardson95
ms.author: lerich
manager: jmartens
monikerRange: vs-2022
ms.workload:
- vssdk
ms.openlocfilehash: 12bbc159884c16ea89849e5c97a4b87292f7089d
ms.sourcegitcommit: 674d3fafa7c9e0cb0d1338027ef419a49c028c36
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2021
ms.locfileid: "112602220"
---
# <a name="imageoptimizer---update-a-visual-studio-extension-step-by-step"></a>ImageOptimizer - Visual Studio 拡張機能をステップ バイ ステップで更新する

[!INCLUDE [preview-note](../includes/preview-note.md)]

このガイドでは、ケース スタディとして Image Optimizer 拡張機能を使用して Visual Studio 2019 のサポートを維持しながら、Visual Studio 2022 サポートを追加するために必要なすべての手順を示します。  
これは、各手順への Git コミット リンクを含む完全なガイドを意図していますが、完成した PR については、こちら ([https://github.com/madskristensen/ImageOptimizer/pull/46](https://github.com/madskristensen/ImageOptimizer/pull/46)) から自由に確認できます。

このガイドの最後には、[追加のサンプル](#other-samples)も用意されています。

## <a name="step-1---modernize-the-project"></a>手順 1 - プロジェクトを最新化する

[プロジェクトの最新化](update-visual-studio-extension.md#modernize-your-vsix-project)に関するページを参照してください。

[git コミット e052465](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/e052465f30e6bed37e6d76eac016047095e8e18b)

まず、VSIX と単体テスト プロジェクトを、プロジェクトのプロパティ ページの下の .NET 4.7.2 にバンプします。

   ![Framework バージョンのバンプ](media/samples/framework-bump.png)

Image Optimizer では、いくつかの古いカスタム 14.* および 15.* パッケージが参照されています。ここでは代わりに、必要なすべての参照を統合する [`Microsoft.VisualStudio.Sdk` NuGet パッケージ](https://www.nuget.org/packages/microsoft.visualstudio.sdk)をインストールします。

```Diff
-  <ItemGroup>
-    <PackageReference Include="Madskristensen.VisualStudio.SDK">
-      <Version>14.0.0-beta4</Version>
-    </PackageReference>
-    <PackageReference Include="Microsoft.VSSDK.BuildTools">
-      <Version>15.8.3247</Version>
-      <IncludeAssets>runtime; build; native; contentfiles; analyzers</IncludeAssets>
-      <PrivateAssets>all</PrivateAssets>
-    </PackageReference>
-  </ItemGroup>

+  <ItemGroup>
+    <PackageReference Include="Microsoft.VisualStudio.SDK">
+      <Version>16.9.31025.194</Version>
+    </PackageReference>
+  </ItemGroup>
```

プロジェクトのビルドに成功すると、スレッド化に関する警告がいくつか示されます。 これらの警告を修正するには、`ctrl` と `.` をクリックし、Intellisense を使用して欠落しているスレッド切り替え行を追加します。

## <a name="step-2---refactor-source-code-into-a-shared-project"></a>手順 2 - ソース コードを共有プロジェクトにリファクターする

[共有プロジェクト](update-visual-studio-extension.md#use-shared-projects-for-multi-targeting)に関するページを参照してください。

Visual Studio 2022 をサポートするには、Visual Studio 2019 と Visual Studio 2022 VSIX プロジェクト間で共有される拡張機能のソース コードを含む新しい共有プロジェクトを追加する必要があります。

1. ソリューションに新しい共有プロジェクトを追加する

   [Git コミット abf249d](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/abf249d5a4bed9010652f3f3fc4753c7c771c892)

   ![共有プロジェクトを追加する](media/samples/add-shared-project.png)

1. VSIX プロジェクトに共有プロジェクトへの参照を追加します。

   [Git コミット e8e941e](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/e8e941e5a5482cc15f5b9e7e4f1727f5cab5b12c)

   :::image type="content" source="media/update-visual-studio-extension/add-shared-project-reference.png" alt-text="共有プロジェクト参照を追加する" lightbox="media/update-visual-studio-extension/add-shared-project-reference.png":::

1. 次のものを **除き**、ソース コード ファイル (cs、xaml、resx) を新しい共有プロジェクトに移動します。
    - `source.extension.vsixmanifest`
    - 拡張機能メタデータ ファイル (アイコン、ライセンス、リリース ノートなど)
    - VSCT ファイル
    - リンク ファイル
    - VSIX に含める必要がある外部ツールまたはライブラリ

   [Git コミット f31f051](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/f31f0515305623988f2c355ed3bf5952fc8f1d9e)

   ![共有プロジェクトにファイルを移動する](media/samples/move-to-shared-project.png)

1. 次に、すべてのメタデータ、VSCT ファイル、リンク ファイル、および外部ツールやライブラリを共有の場所に移動し、それらをリンクされた項目として VSIX プロジェクトに追加して戻します。 `source.extension.vsixmanifest` は削除 **しない** でください。

   [Git コミット 73ba920 - ファイルの移動](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/73ba920b7db0bdb7c4d66aa9bc932c268efd49cb)

   [Git コミット d5e36b2 - 外部ツールやライブラリの追加](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/d5e36b2d047290d38ffc977511510bc03e257f13)

   1. このプロジェクトでは、拡張機能アイコン、VSCT ファイル、および外部ツールを新しいフォルダー `ImageOptimizer\Resources` に移動する必要があります。 それらを共有フォルダーにコピーし、VSIX プロジェクトから削除します。
   1. それらをリンクされた項目として追加して戻し、項目が既にリンクされている場合は、それらの項目 (ライセンスなど) をそのまま保持できます。
   1. [ビルド アクション] と他のプロパティが、追加されたリンク ファイルで正しく設定されていることを確認します。その場合、各ファイルを選択し、プロパティ ツール ウィンドウを確認します。 このプロジェクトでは、次のように設定する必要がありました。
       - `icon.png` [ビルド アクション] を `Content` に設定し、マークされた [VSIX に含める] を `true` に設定する
       - `ImageOptimizer.vsct` [ビルド アクション] を `VSCTComplile` に設定し、[VSIX に含める] を `false` に設定する
       - `Resources\Tools` の下にあるファイルのすべての [ビルド アクション] を `Content` に設定し、マークされた [VSIX に含める] を `true` に設定する

           ![VSIX プロジェクトにリンク ファイルを追加する](media/samples/add-linked-files.png)

       - さらに、`ImageOptimizer.cs` は `ImageOptimizer.vsct` の依存関係であるため、この依存関係を csproj ファイルに手動で追加する必要があります。

          ```diff  
          - <Content Include="..\SharedFiles\ImageOptimizer.vsct">
          -   <Link>ImageOptimizer.vsct</Link>
          - </Content>
          - <Compile Include="..\SharedFiles\ImageOptimizer.cs">
          -   <Link>ImageOptimizer.cs</Link>
          - </Compile>

          + <VSCTCompile Include="..\SharedFiles\ImageOptimizer.vsct">
          +   <ResourceName>Menus.ctmenu</ResourceName>
          +   <Generator>VsctGenerator</Generator>
          +   <LastGenOutput>..\SharedFiles\ImageOptimizer.cs</LastGenOutput>
          + </VSCTCompile>
          + <Compile Include="..\SharedFiles\ImageOptimizer.cs">
          +   <AutoGen>True</AutoGen>
          +   <DesignTime>True</DesignTime>
          +   <DependentUpon>..\SharedFiles\ImageOptimizer.vsct</DependentUpon>
          + </Compile>
          ```

       - プロパティ ツール ウィンドウにより特定の [ビルド アクション] の設定が妨げられる場合は、上記のように csproj を手動で変更し、必要に応じて [ビルド アクション] を設定できます。

1. プロジェクトをビルドして変更を確認し、エラーや問題を修正します。 一般的な問題については、[よく寄せられる質問](update-visual-studio-extension.md#q--a)に関するセクションを確認してください。

## <a name="step-3---add-a-visual-studio-2022-vsix-project"></a>手順 3 - Visual Studio 2022 VSIX プロジェクトを追加する

[Visual Studio 2022 のターゲットの追加](update-visual-studio-extension.md#add-a-visual-studio-2022-target)に関するページを参照してください。

1. ソリューションに新しい VSIX プロジェクトを追加します。
1. `source.extension.vsixmanifest.` を除き、新しいプロジェクト内の追加のソース コードを削除します

   ![新しい VSIX プロジェクトを作成する](media/samples/visual-studio-2022-vsix-initial.png)

1. 共有プロジェクトへの参照を追加します。

   [Git コミット dd49cb2](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/dd49cb227b52c46206bf4be5c25790ac0377568d)

   :::image type="content" source="media/update-visual-studio-extension/add-shared-project-reference.png" alt-text="共有プロジェクトへの参照を追加する" lightbox="media/update-visual-studio-extension/add-shared-project-reference.png":::

1. Visual Studio 2019 VSIX プロジェクトからリンク ファイルを追加し、[ビルド アクション] および [VSIX に含める] プロパティが一致することを確認します。 また、`source.extension.vsixmanifest` ファイルをコピーします。これは、Visual Studio 2022 をサポートするために後で変更します。

   [Git コミット 98c43ee](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/98c43ee6fbe912c38a1275542c44c65e11d7dbd9)

   ![VSIX プロジェクトにリンク ファイルを追加する](media/samples/visual-studio-2022-add-linked-files.png)

1. 試行されたビルドでは、`System.Windows.Forms` への参照が欠落していることが示されます。 それを Visual Studio 2022 プロジェクトに追加し、リビルドするだけです。

   [Git コミット de71ccd](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/de71ccd9baff703aa6679392ad41a2cfe7bd7d72)

   ```Diff
   + <Reference Include="System.Windows.Forms" />
   ```

1. `Microsoft.VisualStudio.SDK` および `Microsoft.VSSDK.BuildTools` パッケージ参照を Visual Studio 2022 バージョンにアップグレードします。

   [Git コミット d581fc3](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/d581fc3c954974124dc7e31e5ecc85f78f7828ab)

   > [!NOTE]
   > これらは、このガイドが作成された時点で使用可能な最新バージョンです。 使用可能な最新バージョンを取得することをお勧めします。
   >
   > ```diff
   > -<PackageReference Include="Microsoft.VisualStudio.SDK" Version="16.0.206" />
   > +<PackageReference Include="Microsoft.VisualStudio.SDK" Version="17.0.0-preview-1-31216-1036" />
   > -<PackageReference Include="Microsoft.VSSDK.BuildTools" Version="16.10.32" />
   > +<PackageReference Include="Microsoft.VSSDK.BuildTools" Version="17.0.63-Visual Studio 2022-g3f11f5ab" />
   > ```

1. `source.extension.vsixmanifest` ファイルを編集し、ターゲットの Visual Studio 2022 が反映されるようにします。

   [Git コミット 9d393c7](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/9d393c708c04ac4af48d1eb9ce3da4470db5d5cc)
   1. `<InstallationTarget>` タグを設定し、Visual Studio 2022 が反映され、amd64 ペイロードが示されるようにします。

      ```xml
      <InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[17.0,18.0)">
          <ProductArchitecture>amd64</ProductArchitecture>
      </InstallationTarget>
      ```

   1. 前提条件を変更し、Visual Studio 2022 以降のみが含まれるようにします。

      ```Diff
      - <Prerequisite Id="Microsoft.VisualStudio.Component.CoreEditor" Version="[15.0,)" DisplayName="Visual Studio core editor" />
      + <Prerequisite Id="Microsoft.VisualStudio.Component.CoreEditor" Version="[17.0,)" DisplayName="Visual Studio core editor" />
      ```

完了です。

これで、ビルド時に Visual Studio 2019 と Visual Studio 2022 VSIX の両方が生成されるようになりました。

## <a name="other-samples"></a>その他のサンプル

- [ProPower ツール](https://github.com/microsoft/VS-PPT/pull/244)
  - PeekF1
    - 選択されたクラスやオブジェクトに関するヘルプ情報を使用して、Web ブラウザーをピークできるようにします。
  - FixMixedTabs
    - ドキュメントをスキャンし、タブをスペース (またはその逆) に置き換えます

## <a name="next-steps"></a>次のステップ

この[開始から終了までのガイド](update-visual-studio-extension.md)を読んで、拡張機能を更新する準備を行います。
