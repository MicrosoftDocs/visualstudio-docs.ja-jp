---
title: カスタムディレクティブプロセッサをデプロイする |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- text templates, custom directive processors
ms.assetid: 80c28722-a630-47b5-923b-024dc3f2c940
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 6cce0a918b1b3e029846176832ab2feb74e3e9e4
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72669838"
---
# <a name="deploying-a-custom-directive-processor"></a>カスタム ディレクティブ プロセッサの配置
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

任意のコンピューター上の [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] でカスタム ディレクティブ プロセッサを使用するには、そのプロセッサをこのトピックで説明するいずれかの方法で登録する必要があります。

 次の方法があります。

- [Visual Studio 拡張機能 (VSIX)](https://msdn.microsoft.com/64ff1452-f7d5-42d9-98b8-76f769f76832)。 これを使用すると、ディレクティブ プロセッサを自分のコンピューターと他のコンピューターの両方でインストールおよびアンインストールできます。 通常は、他の機能も同じ VSIX にパッケージ化します。

- [VSPackage](../extensibility/internals/vspackages.md)。 ディレクティブ プロセッサ以外の機能も含む VSPackage を定義する場合は、ディレクティブ プロセッサの便利な登録方法を利用できます。

- レジストリ キーを設定する。 この方法では、ディレクティブ プロセッサのレジストリ エントリを追加します。

  これらの方法のいずれかを使用する必要があるのは、テキスト テンプレートを [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] または [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] で変換する場合だけです。 独自のアプリケーションのカスタム ホストを使用する場合は、そのカスタム ホストを通じて各ディレクティブのディレクティブ プロセッサを探します。

## <a name="deploying-a-directive-processor-in-a-vsix"></a>VSIX でのディレクティブ プロセッサの配置
 カスタムディレクティブプロセッサを[Visual Studio 拡張機能 (VSIX)](https://msdn.microsoft.com/64ff1452-f7d5-42d9-98b8-76f769f76832)に追加できます。

 .vsix ファイルに次の 2 つのアイテムが格納されていることを確認する必要があります。

- カスタム ディレクティブ プロセッサ クラスを含むアセンブリ (.dll)。

- ディレクティブ プロセッサを登録する .pkgdef ファイル。 このファイルのルート名は、アセンブリと同じにする必要があります。 たとえば、アセンブリ ファイル名が CDP.dll のときは、CDP.pkgdef にします。

  .vsix ファイルのコンテンツを確認または変更するには、そのファイル名拡張子を .zip に変更してから開きます。 コンテンツの編集が終わったら、ファイル名拡張子を .vsix に戻します。

  .vsix ファイルはいくつかの方法で作成できます。 次の手順では、そのうちの 1 つについて説明します。

#### <a name="to-develop-a-custom-directive-processor-in-a-vsix-project"></a>VSIX プロジェクトでカスタム ディレクティブ プロセッサを作成するには

1. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] で VSIX プロジェクトを作成します。

    - **[新しいプロジェクト]** ダイアログボックスで、 **[Visual Basic** ] または **[ C#ビジュアル]** を展開し、 **[拡張機能]** を展開します。 **[VSIX プロジェクト]** をクリックします。

2. **Source.extension.vsixmanifest**で、コンテンツの種類とサポートされているエディションを設定します。

    1. VSIX マニフェストエディターの **[アセット]** タブで、 **[新規作成]** をクリックし、新しい項目のプロパティを設定します。

         **コンテンツの種類** = **VSPackage**

         *現在のプロジェクト*\<**ソースプロジェクト** =  >

    2. **[選択されたエディション]** をクリックし、ディレクティブプロセッサを使用できるようにするインストールの種類を確認します。

3. .pkgdef ファイルを追加し、そのプロパティが VSIX に含まれるように設定します。

    1. テキストファイルを作成し、*assemblyName*> \< という名前を指定します。

         \<*assemblyName*> は通常、プロジェクトの名前と同じです。

    2. ソリューション エクスプローラーでこのファイルを選択し、そのプロパティを次のように設定します。

         **ビルドアクション** = **コンテンツ**

         **出力ディレクトリにコピー**  = **常にコピー**する

         **VSIX に含める** = **True**

    3. VSIX の名前を設定し、ID が一意であることを確認します。

4. 次のテキストを .pkgdef ファイルに追加します。

    ```
    [$RootKey$\TextTemplating]
    [$RootKey$\TextTemplating\DirectiveProcessors]
    [$RootKey$\TextTemplating\DirectiveProcessors\ CustomDirectiveProcessorName]
    @="Custom Directive Processor description"
    "Class"="NamespaceName.ClassName"
    "CodeBase"="$PackageFolder$\AssemblyName.dll"
    ```

     名前 (`CustomDirectiveProcessorName`、`NamespaceName`、`ClassName`、`AssemblyName`) を独自の名前に置き換えます。

5. 以下の参照をプロジェクトに追加します。

    - **VisualStudio。 \* ます。0**

    - **VisualStudio.... \*. 0**

    - **VisualStudio.... \* Vshost.exe. 0**

6. カスタム ディレクティブ プロセッサ クラスをプロジェクトに追加します。

     これは、<xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> または <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> を実装する必要のあるパブリック クラスです。

#### <a name="to-install-the-custom-directive-processor"></a>カスタム ディレクティブ プロセッサをインストールするには

1. エクスプローラーでビルド ディレクトリ (通常は bin\Debug か bin\Release) を開きます。

2. 別のコンピューターにディレクティブ プロセッサをインストールする場合は、そのコンピューターに .vsix ファイルをコピーします。

3. .vsix ファイルをダブルクリックします。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 拡張機能インストーラーが表示されます。

4. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]を再起動します。 これで、カスタム ディレクティブ プロセッサを参照するディレクティブを含むテキスト テンプレートを実行できるようになりました。 各ディレクティブの形式は次のとおりです。

     `<#@ CustomDirective Processor="CustomDirectiveProcessorName" parameter1="value1" … #>`

#### <a name="to-uninstall-or-temporarily-disable-the-custom-directive-processor"></a>カスタム ディレクティブ プロセッサをアンインストールするか、一時的に無効にするには

1. @No__t_0 **[ツール]** メニューの **[拡張機能マネージャー]** をクリックします。

2. ディレクティブプロセッサが含まれている VSIX を選択し、 **[アンインストール]** または **[無効]** をクリックします。

### <a name="troubleshooting-a-directive-processor-in-a-vsix"></a>VSIX に含まれるディレクティブ プロセッサのトラブルシューティング
 ディレクティブ プロセッサが機能しない場合は、次のヒントを参考にしてください。

- カスタム ディレクティブで指定するプロセッサ名は、.pkgdef ファイルで指定した `CustomDirectiveProcessorName` と一致している必要があります。

- `IsDirectiveSupported` メソッドは、`true` の名前が渡されたときに `CustomDirective` を返す必要があります。

- 拡張機能マネージャーで拡張機能が表示されないが、システムでインストールできない場合は、 **%localappdata%\Microsoft\VisualStudio \\ \* .0 \ Extensions \\** から拡張機能を削除します。

- .vsix ファイルを開き、そのコンテンツを調べます。 .vsix ファイルを開くには、ファイル名拡張子を .zip に変更します。 このファイルに .dll、.pkgdef、および extension.vsixmanifest の各ファイルが含まれていることを確認します。 extension.vsixmanifest ファイルでは、SupportedProducts ノードに適切なリストが含まれ、なおかつ Content ノードに VsPackage ノードが含まれている必要があります。

     `<Content>`

     `<VsPackage>CustomDirectiveProcessor.dll</VsPackage>`

     `</Content>`

## <a name="deploying-a-directive-processor-in-a-vspackage"></a>VSPackage でのディレクティブ プロセッサの配置
 ディレクティブ プロセッサが GAC にインストールされる VSPackage に含まれている場合は、システムで .pkgdef ファイルを自動的に生成できます。

 次の属性をパッケージ クラスに配置します。

```
[ProvideDirectiveProcessor(typeof(DirectiveProcessorClass), "DirectiveProcessorName", "Directive processor description.")]
```

> [!NOTE]
> この属性は、ディレクティブ プロセッサ クラスではなくパッケージ クラスに配置してください。

 .pkgdef ファイルは、プロジェクトをビルドしたときに生成されます。 VSPackage をインストールすると、.pkgdef ファイルにディレクティブ プロセッサが登録されます。

 .pkgdef ファイルがビルド フォルダー (通常は bin\Debug か bin\Release) に表示されることを確認します。 このフォルダーに表示されない場合は、テキスト エディターで .csproj ファイルを開き、`<GeneratePkgDefFile>false</GeneratePkgDefFile>` ノードを削除します。

 詳細については、「 [VSPackages](../extensibility/internals/vspackages.md)」を参照してください。

## <a name="setting-a-registry-key"></a>レジストリ キーの設定
 これは、カスタム ディレクティブ プロセッサをインストールする方法としては、最も優先順位の低い方法です。 この方法では、ディレクティブ プロセッサを簡単に有効化および無効化できないうえに、ディレクティブ プロセッサを他のユーザーに配布することもできません。

> [!CAUTION]
> レジストリを誤って編集すると、システムに重大な障害をもたらす可能性があります。 レジストリを変更する前に、コンピューター上の重要なデータはすべてバックアップしてください。

#### <a name="to-register-a-directive-processor-by-setting-a-registry-key"></a>レジストリ キーを設定してディレクティブ プロセッサを登録するには

1. `regedit` を実行します。

2. レジストリ エディターで、次のキーに移動します。

    **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio \\ \* .0 \ .0\ Texttemplating\directiveprocessors**

    [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のテスト バージョンでディレクティブ プロセッサをインストールする場合は、"11.0" の後ろに "Exp" を挿入します。

3. ディレクティブ プロセッサ クラスと同じ名前のレジストリ キーを追加します。

   - レジストリツリーで、 **[DirectiveProcessors]** ノードを右クリックし、 **[新規作成]** をポイントして、 **[キー]** をクリックします。

4. 新しいノードで、クラスとコードベース、またはクラスとアセンブリの文字列値を次の表に従って追加します。

   1. 作成したノードを右クリックして **[新規]** をポイントし、 **[文字列値]** をクリックします。

   2. 値の名前を編集します。

   3. 名前をダブルクリックし、データを編集します。

   カスタム ディレクティブ プロセッサが GAC 内にない場合は、レジストリ サブキーを次の表に従って設定します。

|名|[種類]|データ|
|----------|----------|----------|
|(既定)|REG_SZ|(値が設定されていません)|
|インスタンス|REG_SZ|**\<Namespace 名 >。\<Class 名 >**|
|CodeBase|REG_SZ|**アセンブリ名 < \\ パス > \<Your \>**|

 アセンブリが GAC に含まれている場合は、レジストリ サブキーを次の表に従って設定します。

|名|[種類]|データ|
|----------|----------|----------|
|(既定)|REG_SZ|(値が設定されていません)|
|インスタンス|REG_SZ|**完全修飾クラス名**を \< >|
|Assembly|REG_SZ|**GAC にアセンブリ名を**\< >|

## <a name="see-also"></a>参照
 [カスタム T4 テキスト テンプレート ディレクティブ プロセッサの作成](../modeling/creating-custom-t4-text-template-directive-processors.md)
