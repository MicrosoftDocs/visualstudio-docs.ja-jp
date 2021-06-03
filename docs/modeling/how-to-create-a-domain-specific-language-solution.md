---
title: '方法: ドメイン固有言語ソリューションを作成する'
description: 特殊な Visual Studio ソリューションを使用して、ドメイン固有言語 (DSL) を作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.dsltools.designerwizard
helpviewer_keywords:
- Domain-Specific Language Tools, walkthroughs
- walkthroughs [Domain-Specific Language Tools], creating domain-specific language
- Domain-Specific Language Tools, creating solutions
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 5d04366c908494386edc9921129db27df0ead4f7
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99941412"
---
# <a name="how-to-create-a-domain-specific-language-solution"></a>方法: ドメイン固有言語ソリューションを作成する
ドメイン固有言語 (DSL) は、特殊な Visual Studio ソリューションを使用して作成されます。

## <a name="prerequisites"></a>必須コンポーネント

この手順を開始する前に、以下のコンポーネントをインストールしてください。

- Visual Studio
- Visual Studio SDK (**Visual Studio 拡張機能の開発** ワークロードの一部としてインストールされます)
- Modeling SDK (Visual Studio コンポーネントとしてインストールされます)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="creating-a-domain-specific-language-solution"></a>ドメイン固有言語ソリューションの作成

1. 新しい **ドメイン固有言語デザイナー** プロジェクトを作成して、DSL ウィザードを起動します。

   > [!NOTE]
   > そのプロジェクトに対して選択する名前は、コードの生成に使用される可能性があるため、できれば有効な Visual C# 識別子にしてください。

   ::: moniker range="vs-2017"

   ![DSL ダイアログの作成](../modeling/media/create_dsldialog.png)

   ::: moniker-end

2. DSL テンプレートを選択します。

    **[ドメイン固有言語オプションの選択]** ページで、いずれかのソリューション テンプレート ( **[最小言語]** など) を選択します。 作成する DSL と類似したテンプレートを選択します。

    ソリューション テンプレートの詳細については、「[ドメイン固有言語ソリューション テンプレートの選択](../modeling/choosing-a-domain-specific-language-solution-template.md)」を参照してください。

3. **[ファイル拡張子]** ページでファイル名拡張子を入力します。 これは、お使いのコンピューターと、DSL をインストールするすべてのコンピューターで一意でなければなりません。 "**この拡張子を使用しているアプリケーションまたは Visual Studio エディターはありません**" というメッセージが表示されるはずです。

   - 完全にインストールされていない以前の実験用 DSL でそのファイル名拡張子を使用していた場合は、Visual Studio SDK のメニューにある **[実験用インスタンスのリセット]** ツールを使用してクリアできます。

   - このファイル拡張子を使用する別の Visual Studio 拡張機能がコンピューターに完全にインストールされている場合は、そのアンインストールをご検討ください。 **[ツール]** メニューの **[拡張機能マネージャー]** をクリックします。

4. ウィザードの残りのページにあるフィールドを検査し、必要に応じて調整します。 設定に問題がなければ、 **[完了]** をクリックします。 設定の詳細については、「[DSL デザイナー ウィザードのページ](#settings)」を参照してください。

    ウィザードにより、**Dsl** および **DslPackage** という名前の 2 つのプロジェクトを含むソリューションが作成されます。

   > [!NOTE]
   > 信頼されていないソースからのテキスト テンプレートを実行しないよう警告するメッセージが表示された場合は、 **[OK]** をクリックします。 このメッセージが再度表示されないように設定できます。

## <a name="the-dsl-designer-wizard-pages"></a><a name="settings"></a>DSL デザイナー ウィザードのページ
 一部のフィールドは、既定値のままにしておくことができます。 ただし、[ファイル拡張子] フィールドは必ず設定してください。

### <a name="solution-settings-page"></a>[ソリューションの設定] ページ
 **[ドメイン固有言語の基礎にするテンプレート]**
作成する DSL と類似したテンプレートを選択します。 さまざまなテンプレートが便利な出発点となります。 ソリューション テンプレートを選択すると、ウィザードに説明が表示されます。 ソリューション テンプレートの詳細については、「[ドメイン固有言語ソリューション テンプレートの選択](../modeling/choosing-a-domain-specific-language-solution-template.md)」を参照してください。

 **[ドメイン固有言語に指定する名前]**
既定値はソリューション名です。 この値からコードが生成されます。 これは、C# クラス名として有効である必要があります。

### <a name="file-extension-page"></a>[ファイル拡張子] ページ
 **[モデル ファイルが使用する必要がある拡張子]**
新しいファイル拡張子を入力します。

 次のようにして、このファイル拡張子がこのコンピューター用にまだ登録されていないことを確認します。

 **[この拡張子を処理するために登録されている他のツールとアプリケーション]** を確認します。 "**この拡張子を使用しているアプリケーションまたは Visual Studio エディターはありません**" というメッセージが表示された場合は、このファイル拡張子を使用できます。

 ツールまたはパッケージの一覧が表示された場合は、次のいずれかを行う必要があります。

- 別のファイル拡張子を入力します。

     \- または

- Visual Studio の実験用インスタンスをリセットします。 これにより、以前に作成したすべての DSL の登録が解除されます。 **[スタート]** メニューで、 **[すべてのプログラム]** 、 **[Microsoft Visual Studio 2010 SDK]** 、 **[ツール]** 、 **[Microsoft Visual Studio 2010 実験用インスタンスのリセット]** の順にクリックします。 もう一度使用したい他の DSL はすべてリビルドできます。

     \- または

- このファイル拡張子を使用する Visual Studio 拡張機能がコンピューターに完全にインストールされている場合は、それをアンインストールします。 **[ツール]** メニューの **[拡張機能マネージャー]** をクリックします。

### <a name="product-settings-page"></a>[製品の設定] ページ
 **[新しいドメイン固有言語が属する製品の名前]**
既定値は DSL 名です。

 この値は、Windows エクスプローラー (またはファイル エクスプローラー) で、このファイル拡張子を持つファイルを記述するために使用されます。

 **[本製品が属する会社の名前]**
お客様の会社名。

 この値は、DSL パッケージの AssemblyInfo プロパティに組み込まれます。

 **[ソリューションのプロジェクトに関するルート名前空間]**
既定値は、会社名と製品名で構成される名前です。

### <a name="signing-page"></a>[署名] ページ
 **[厳密な名前のキー ファイルの作成]** 既定のオプションでは、DSL アセンブリに署名するための新しいキーが作成されます。

 **[厳密な名前の既存キーを使用]** DSL を別のアセンブリと統合する場合は、このオプションを使用します。

 厳密な名前付けの詳細については、「[厳密な名前付きアセンブリの作成と使用](/dotnet/standard/assembly/create-use-strong-named)」を参照してください。

## <a name="see-also"></a>関連項目

- [方法: ドメイン固有言語を定義する](../modeling/how-to-define-a-domain-specific-language.md)
- [ドメイン固有言語ツールの用語集](/previous-versions/bb126564(v=vs.100))