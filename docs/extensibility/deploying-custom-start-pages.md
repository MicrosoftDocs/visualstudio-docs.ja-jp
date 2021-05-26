---
title: カスタム スタート ページの配置 | Microsoft Docs
description: VSIX 配置を使用するか、ターゲット コンピューター上の正しい場所にファイルをコピーして、カスタム スタート ページを配置する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- package start page
- deploy start page
ms.assetid: 4a7eb360-de83-41d5-be53-3cfb160d19f9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: a356fe3dadaf0eca4f0b4d0f2a7d17f0b475acfb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061408"
---
# <a name="deploy-custom-start-pages"></a>カスタム スタート ページを配置する

カスタム スタート ページを配置するには、VSIX 配置を使用するか、ターゲット コンピューター上の正しい場所にファイルをコピーします。

## <a name="vsix-deployment-by-using-the-start-page-project-template"></a>スタート ページのプロジェクト テンプレートを使用した VSIX 配置

スタート ページのプロジェクト テンプレートを使用してスタート ページを作成してから、プロジェクトをビルドすると、配布できる *.vsix* ファイルが Visual Studio によって作成されます。 *.vsix* ファイルにスタート ページをパッケージ化すると、対象ユーザーに応じて次の配置オプションを使用できます。

- *.vsix* ファイルをネットワーク共有またはパブリック Web サイトに配置できます。 他のユーザーがファイルを開くと、スタート ページが自動的にインストールされます。

- [Visual Studio Marketplace](https://marketplace.visualstudio.com/) Web サイトに *.vsix* ファイルをアップロードすると、ユーザーは **拡張機能マネージャー** を使用してそれをインストールできます。

スタート ページのプロジェクト テンプレートでは、既定の Visual Studio のスタート ページのコピーが作成されるため、コピーを変更して元を保持できます。

スタート ページのプロジェクト テンプレートを取得するには、**拡張機能マネージャー** を使用するか、Web サイトからそれをダウンロードします。

## <a name="vsix-deployment-without-using-the-start-page-project-template"></a>スタート ページのプロジェクト テンプレートを使用しない VSIX 配置
 VSIX 配置を成功させるには、VSIX 登録プロセスと **拡張機能マネージャー** で認識されるフォルダーに拡張機能をインストールする必要があります。 スタート ページのプロジェクト テンプレートには既に正しいフォルダーが指定されているので、VSIX 配置用の拡張機能をパッケージ化する場合は、常にこれを使用することをお勧めします。 ただし、テンプレートを使用できない場合は、それを使用せずに VSIX 配置を作成できます。

 スタート ページのプロジェクト テンプレートを使用せずに VSIX 配置を作成するには、最初に次の 2 つの方法のいずれかでスタート ページの *.vsix* ファイルを作成します。

- カスタム スタート ページ ファイルを空の VSIX プロジェクトに追加する。 詳細については、「[VSIX プロジェクト テンプレート](../extensibility/vsix-project-template.md)」を参照してください。

- *.vsix* ファイルを手動で作成する。 *.vsix* ファイルを手動で作成するには:

   1. 新しいフォルダーに *extension.vsixmanifest* ファイルと *[Content_Types].xml* ファイルを作成します。 詳細については、「[VSIX パッケージの構造](../extensibility/anatomy-of-a-vsix-package.md)」を参照してください。

   2. エクスプローラーで、2 つの XML ファイルを含むフォルダーを右クリックし、 **[送る]** 、[圧縮 (zip 形式) フォルダー] の順にクリックします。 作成された *.zip* ファイルの名前を *Filename.vsix* に変更します (Filename はパッケージをインストールする再頒布可能ファイルの名前です)。

Visual Studio でスタート ページを認識するには、VSIX マニフェストの `Content Element` に、`Type` 属性が `"StartPage"` に設定された `CustomExtension Element` を含める必要があります。 VSIX 配置を使用してインストールされたスタート ページ拡張機能は、 **[スタートアップ]** オプション ページの **[スタート ページのカスタマイズ]** の一覧に **[インストールされた拡張機能]** <*拡張機能名*> として表示されます。

スタート ページ パッケージにアセンブリが含まれている場合は、Visual Studio の起動時にそれらを使用できるようにするため、バインド パスの登録を追加する必要があります。 これを行うには、次の情報を含む *.pkgdef* ファイルがパッケージに含まれていることを確認します。

```
[$RootKey$\BindingPaths\{Insert a new GUID here}]
"$PackageFolder$"=""
```

### <a name="vsix-deployment-for-all-users"></a>すべてのユーザーに対する VSIX 配置
 既定では、VSIX パッケージに配置された拡張機能は、現在のユーザーに対してのみインストールされます。 ターゲット コンピューターのすべてのユーザーに対するスタート ページ インストールを作成するには、All-Users の配置を作成します。

### <a name="to-create-an-all-users-deployment"></a>All-Users の配置を作成するには

1. コード ビューで *extension.vsixmanifest* ファイルを開きます。

2. vsix マニフェストの `Identifier` 要素に、`true` の値を持つ `AllUsers` 要素を追加します。

    ```
    <AllUsers>true</AllUsers>
    ```

     これにより、vsix インストーラーで管理者のアクセス許可が求められた後、 *\Common7\IDE\Extensions* にファイルがインストールされます。

3. *.pkgdef* ファイルを開きます。

4. [HKLM] の下に次を追加して、既定のスタート ページを設定するように *.pkgdef* を変更します。ここで、*MyStartPage.xaml* は、スタート ページを含む *.xaml* ファイルの名前です。

     [$RootKey$\StartPage\Default]

     "Uri"="$PackageFolder$\\*MyStartPage.xaml*"

     これで、Visual Studio に対して新しいスタート ページの場所を検索するように指示されます。

## <a name="file-copy-deployment"></a>ファイル コピーの配置
 カスタム スタート ページを配置するために *.vsix* ファイルを作成する必要はありません。 代わりに、マークアップとサポート ファイルをユーザーの <em>\StartPages\* フォルダーに直接コピーできます。* **[スタートアップ]** オプション ページの *[スタート ページのカスタマイズ]</em> の一覧には、そのフォルダー内のすべての *.xaml* ファイルがパスと共に表示されます (たとえば、 *%USERPROFILE%\My Documents\Visual Studio <バージョン>\StartPages\\<ファイル名>.xaml*)。 スタート ページにプライベート アセンブリへの参照が含まれている場合は、それらをコピーして、*\PrivateAssemblies\* フォルダーに貼り付ける必要があります。

 作成したスタート ページを *.vsix* ファイルにパッケージ化せずに配布するには、基本的なファイル コピー方法 (バッチ スクリプトなど)、または必要なディレクトリにファイルを配置できるその他の配置テクノロジを使用することをお勧めします。

### <a name="to-manually-install-a-custom-start-page"></a>カスタム スタート ページを手動でインストールするには

1. スタート ページのマークアップを含む *.xaml* ファイルをアセンブリ以外のサポート ファイルと共にコピーし、ユーザーの *\StartPages\* フォルダーに貼り付けます。

2. スタート ページにアセンブリが必要な場合は、それらをコピーし、 *..\\<Visual Studio インストール フォルダー>\Common7\IDE\PrivateAssemblies\\* に貼り付けます。

3. **[スタートアップ]** オプション ページの **[スタート ページのカスタマイズ]** の一覧で、新しいスタート ページを選択します。 詳細については、[スタート ページのカスタマイズ](../ide/customizing-the-start-page-for-visual-studio.md)に関する記事をご覧ください。

## <a name="see-also"></a>関連項目

- [スタート ページのカスタマイズ](../ide/customizing-the-start-page-for-visual-studio.md)
- [スタート ページにユーザー コントロールを追加する](../extensibility/adding-user-control-to-the-start-page.md)
