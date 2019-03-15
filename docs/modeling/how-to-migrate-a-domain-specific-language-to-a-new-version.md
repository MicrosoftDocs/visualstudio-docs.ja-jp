---
title: '方法: ドメイン固有言語を新バージョンに移行する'
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: dae9c7728de35c92c973c9fca097595b56aabaf5
ms.sourcegitcommit: f7c401a376ce410336846835332a693e6159c551
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/14/2019
ms.locfileid: "57869245"
---
# <a name="how-to-migrate-a-domain-specific-language-to-a-new-version"></a>方法: ドメイン固有言語を新バージョンに移行する
ドメイン固有言語を使って定義するプロジェクトを移行する[!INCLUDE[vs2010](../misc/includes/vs2010_md.md)]のバージョンから[!INCLUDE[dsl](../modeling/includes/dsl_md.md)]を使用して配布されて[!INCLUDE[vs_orcas_long](../debugger/includes/vs_orcas_long_md.md)]します。

 一部として移行ツールが提供される[!INCLUDE[vssdk_current_long](../misc/includes/vssdk_current_long_md.md)]します。 このツールでは、Visual Studio プロジェクトとソリューションを使用して、またはツールを DSL 定義に変換します。

 移行ツールを明示的に実行する必要があります: が起動しない自動的に Visual Studio でソリューションを開くときにします。 ツールおよび詳細なガイダンスのドキュメントは、このパスで見つかんだことができます。

 **%Program Files%\Microsoft Visual Studio 2010 SDK\VisualStudioIntegration\Tools\DSLTools\DslProjectsMigrationTool.exe**

## <a name="before-you-migrate-your-dsl-projects"></a>DSL プロジェクトを移行する前に
 移行ツールは Visual Studio プロジェクト ファイルを変更します (**.csproj**) とソリューション ファイル (**.sln**)。

#### <a name="to-prepare-projects-for-migration"></a>移行するには、プロジェクトを準備します。

-   必ず、 **.csproj**と **.sln**ファイルを書き込むことができます。 ソース管理下にある場合は、チェック アウトすることを確認します。

-   移行するフォルダーのコピーを作成します。

## <a name="migrating-a-collection-of-projects"></a>プロジェクトのコレクションを移行します。

#### <a name="to-migrate-dsl-projects-and-solutions-to-visual-studio-2010"></a>DSL プロジェクトおよびソリューションを Visual Studio 2010 に移行するには

1. DSL の移行ツールを起動します。

   -   Windows エクスプ ローラー (またはファイル エクスプ ローラー) ツールをダブルクリックします。 または、コマンド プロンプトからツールを起動できます。 このツールは、この場所には。

        **%ProgramFiles%\Microsoft Visual Studio 2010 SDK\VisualStudioIntegration\Tools\DSLTools\DslProjectsMigrationTool.exe**

2. ソリューションおよび変換するプロジェクトを含むフォルダーを選択します。

   - ツールの上部にあるボックスにパスを入力またはクリックして**参照**します。

     移行ツールには、定義または Dsl を使用するプロジェクトのツリーが表示されます。 ツリーには使用するすべてのプロジェクトが含まれています、 **Microsoft.VisualStudio.Modeling.Sdk**または**TextTemplating**アセンブリ。

3. プロジェクトのツリーを確認し、変換したくないプロジェクトをオフにします。

   -   プロジェクトまたはツールによって、変更の一覧を表示するソリューションを選択します。

       > [!NOTE]
       >  フォルダー名の横に表示されるチェック ボックスは、影響を与えるありません。 プロジェクトおよびソリューションを検査するフォルダーを展開する必要があります。

4. プロジェクトに変換します。

   1.  クリックして**変換**します。

        各プロジェクト ファイルが変換される前のコピーを_プロジェクト_**.csproj**として保存されます_プロジェクト_**vs2008.csproj。**

        各コピー_ソリューション_**.sln**として保存されます_ソリューション_**vs2008.sln。**

   2.  報告されるすべての失敗した変換を調査します。

        テキスト ウィンドウにエラーが報告されます。 さらに、ツリー ビューでは、変換に失敗した各ノードに赤いフラグを示しています。 そのエラーの詳細を取得するノードをクリックすることができます。

5. **すべてのテンプレートの変換**ソリューションで正常に格納しているプロジェクトを変換します。

   1.  ソリューションを開きます。

   2.  をクリックして、**すべてのテンプレートの変換**ソリューション エクスプ ローラーのヘッダーにボタンをクリックします。

       > [!NOTE]
       >  この手順を不要なことできます。 詳細については、次を参照してください。[すべてのテンプレートの変換を自動化する方法](/previous-versions/visualstudio/visual-studio-2012/ff521399\(v\=vs.110\))します。

6. 変換後のプロジェクトでのカスタム コードを更新します。

   -   プロジェクトをビルドし、すべてのエラーを調査しようとします。

   -   デザイナーをテストします。


[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="see-also"></a>関連項目

- [関連するブログの投稿](https://devblogs.microsoft.com/devops/the-visual-studio-modeling-sdk-is-now-available-with-visual-studio-2017/)