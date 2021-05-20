---
title: 'チュートリアル: 従来の言語サービスの作成 | Microsoft Docs'
description: マネージド パッケージ フレームワークの言語クラスを使用して、Visual C# で言語サービスを実装する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- language services [managed package framework], creating
ms.assetid: 6a5dd2c2-261b-4efd-a3f4-8fb90b73dc82
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 42c9f2d2a91b90cab31dd225d0ace081988135fb
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106213642"
---
# <a name="walkthrough-creating-a-legacy-language-service"></a>チュートリアル: 従来の言語サービスの作成
マネージド パッケージ フレームワーク (MPF) の言語クラスを使用して、[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] で言語サービスを実装するのは簡単です。 必要となるのは、言語サービス、言語サービス自体、および言語のパーサーをホストするための VSPackage です。

## <a name="prerequisites"></a>前提条件
 このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「[Visual Studio SDK](../../extensibility/visual-studio-sdk.md)」を参照してください。

## <a name="locations-for-the-visual-studio-package-project-template"></a>Visual Studio パッケージ プロジェクト テンプレートの場所
 Visual Studio パッケージ プロジェクト テンプレートは、 **[新しいプロジェクト]** ダイアログ ボックスの、次の 3 つの場所にあります。

1. Visual Basic の機能拡張の下。 プロジェクトの既定の言語は Visual Basic です。

2. C# の機能拡張の下。 プロジェクトの既定の言語は C# です。

3. その他のプロジェクトの種類の機能拡張の下。 プロジェクトの既定の言語は C++ です。

### <a name="create-a-vspackage"></a>VSPackage を作成する

1. Visual Studio パッケージ プロジェクト テンプレートを使用して VSPackage を作成します。

    既存の VSPackage に言語サービスを追加する場合は、次の手順をスキップし、「言語サービスクラスを作成する」の手順に直接進んでください。

2. プロジェクトの名前として「MyLanguagePackage」と入力し、 **[OK]** をクリックします。

    名前には任意の文字列を使用できます。 ここで説明する手順では、MyLanguagePackage という名前にする場合を想定しています。

3. 言語として [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] を選択し、新しいキー ファイルを生成するオプションを選択します。 **[次へ]** をクリックします。

4. 適切な会社およびパッケージの情報を入力します。 **[次へ]** をクリックします。

5. **[メニュー コマンド]** を選択します。 **[次へ]** をクリックします。

    コード スニペットをサポートしない場合は、[完了] をクリックし、次の手順は無視してかまいません。

6. **[コマンド名]** として「**Insert Snippet**」と入力し、 **[コマンド ID]**  には「`cmdidInsertSnippet`」と入力します。 **[完了]** をクリックします。

    **[コマンド名]** と **[コマンド ID]** には任意の文字列を指定できます。これらは例にすぎません。

### <a name="create-the-language-service-class"></a>言語サービス クラスを作成する

1. **ソリューション エクスプローラー** で、MyLanguagePackage プロジェクトを右クリックし、 **[追加]** 、 **[参照]** の順に選択し、 **[新しい参照の追加]** ボタンをクリックします。

2. **[参照の追加]** ダイアログ ボックスで、 **[.NET]** タブの **[Microsoft.VisualStudio.Package.LanguageService]** を選択し、 **[OK]** をクリックします。

     これは、言語パッケージ プロジェクトに対して 1 回だけ実行する必要があります。

3. **ソリューション エクスプローラー** で、VSPackage プロジェクトを右クリックし、 **[追加]** 、 **[クラス]** の順に選択します。

4. テンプレートの一覧で **[クラス]** が選択されていることを確認します。

5. クラス ファイルの名前として「**MyLanguageService.cs**」と入力し、 **[追加]** をクリックします。

     名前には任意の文字列を使用できます。 ここで説明する手順では、`MyLanguageService` という名前にする場合を想定しています。

6. MyLanguageService.cs ファイルで、次の `using` ディレクティブを追加します。

     :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/cs/mylanguageservice.cs" id="Snippet1":::
     :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/vb/mylanguageservice.vb" id="Snippet1":::

7. `MyLanguageService` クラスを次のように変更して、<xref:Microsoft.VisualStudio.Package.LanguageService> クラスから派生するようにします。

     :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/cs/mylanguageservice.cs" id="Snippet2":::
     :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/vb/mylanguageservice.vb" id="Snippet2":::

8. "LanguageService" にカーソルを置き、 **[編集]** の **[IntelliSense]** メニューから **[抽象クラスの実装]** を選択します。 これにより、言語サービス クラスを実装するために必要な最低限のメソッドが追加されます。

9. 「[従来の言語サービスの実装](../../extensibility/internals/implementing-a-legacy-language-service2.md)」で説明されているように、抽象メソッドを実装します。

### <a name="register-the-language-service"></a>言語サービスを登録する

1. MyLanguagePackagePackage.cs ファイルを開き、次の `using` ディレクティブを追加します。

     :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/vb/mylanguagepackagepackage.vb" id="Snippet3":::
     :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/cs/mylanguagepackagepackage.cs" id="Snippet3":::

2. 「[従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)」で説明されているように、言語サービス クラスを登録します。 これには、ProvideXX 属性と "言語サービスの提供" セクションが含まれます。 このトピックで TestLanguageService が使用されている箇所では、MyLanguageService を使用します。

### <a name="the-parser-and-scanner"></a>パーサーとスキャナー

1. 「[従来の言語サービスのパーサーとスキャナー](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)」で説明されているように、言語のパーサーとスキャナーを実装します。

     パーサーとスキャナーを実装する方法は、完全にユーザー次第なので、このトピックでは扱いません。

## <a name="language-service-features"></a>言語サービスの機能
 言語サービスの各機能を実装するには、通常、適切な MPF 言語サービス クラスからクラスを派生させ、必要に応じて抽象メソッドを実装して、適切なメソッドをオーバーライドします。 どのクラスを作成元や派生元にするかは、サポートする機能によって変わってきます。 これらの機能については、「[従来の言語サービスの機能](../../extensibility/internals/legacy-language-service-features1.md)」で詳しく説明されています。 次の手順は、MPF クラスからクラスを派生させるための一般的な方法です。

#### <a name="deriving-from-an-mpf-class"></a>MPF クラスからの派生

1. **ソリューション エクスプローラー** で、VSPackage プロジェクトを右クリックし、 **[追加]** 、 **[クラス]** の順に選択します。

2. テンプレートの一覧で **[クラス]** が選択されていることを確認します。

     クラス ファイルの適切な名前を入力し、 **[追加]** をクリックします。

3. 新しいクラス ファイルで、次の `using` ディレクティブを追加します。

     :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/cs/mysource.cs" id="Snippet4":::
     :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/vb/mysource.vb" id="Snippet4":::

4. 目的の MPF クラスから派生するように、クラスを変更します。

5. 少なくとも基底クラスのコンストラクターと同じパラメーターを受け取り、コンストラクターのパラメーターを基底クラスのコンストラクターに渡す、クラス コンストラクターを追加します。

     たとえば、<xref:Microsoft.VisualStudio.Package.Source> クラスから派生したクラスのコンストラクターは、次のようになります。

     :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/cs/mysource.cs" id="Snippet5":::
     :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/vb/mysource.vb" id="Snippet5":::

6. 基底クラスに実装する必要がある抽象メソッドがある場合は、 **[編集]** 、 **[IntelliSense]** メニューの **[抽象クラスの実装]** を選択します。

7. それ以外の場合は、クラス内にキャレットを置き、オーバーライドするメソッドを入力します。

     たとえば、「`public override`」と入力すると、そのクラスでオーバーライド可能なすべてのメソッドの一覧が表示されます。

## <a name="see-also"></a>こちらもご覧ください
- [従来の言語サービスの実装](../../extensibility/internals/implementing-a-legacy-language-service1.md)
