---
title: '方法: ドメイン固有言語プロジェクトを移行する'
description: ドメイン固有言語プロジェクトをより新しいバージョンの Visual Studio に移行する方法について説明します。
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: SEO-VS-2020
ms.workload:
- multiple
ms.openlocfilehash: bbefb1cd5ae546c5454660b6782f9c76f35a63f4
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99922704"
---
# <a name="how-to-migrate-a-domain-specific-language-to-a-new-version"></a>方法: ドメイン固有言語を新バージョンに移行する
ドメイン固有言語を定義して使用するプロジェクトを [!INCLUDE[vs_orcas_long](../debugger/includes/vs_orcas_long_md.md)] で配布された [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] のバージョンから [!INCLUDE[vs2010](../misc/includes/vs2010_md.md)] に移行できます。

 移行ツールは、[!INCLUDE[vssdk_current_long](../misc/includes/vssdk_current_long_md.md)] の一部として提供されています。 このツールでは、DSL ツールを使用または定義する Visual Studio プロジェクトとソリューションが変換されます。

 移行ツールは、Visual Studio でソリューションを開いたときに自動的に起動されないため、明示的に実行する必要があります。 ツールと詳細なガイダンス ドキュメントは、次のパスにあります。

 **%Program Files%\Microsoft Visual Studio 2010 SDK\VisualStudioIntegration\Tools\DSLTools\DslProjectsMigrationTool.exe**

## <a name="before-you-migrate-your-dsl-projects"></a>DSL プロジェクトを移行する前に
 移行ツールによって、Visual Studio のプロジェクト ファイル ( **.csproj**) とソリューション ファイル ( **.sln**) が変更されます。

#### <a name="to-prepare-projects-for-migration"></a>プロジェクトの移行の準備をするには以下を行います。

- **.csproj** ファイルと **.sln** ファイルに書き込むことができることを確認します。 ソース管理されている場合は、チェック アウトされていることを確認します。

- 移行するフォルダーのコピーを作成します。

## <a name="migrating-a-collection-of-projects"></a>プロジェクトのコレクションの移行

#### <a name="to-migrate-dsl-projects-and-solutions-to-visual-studio-2010"></a>DSL プロジェクトとソリューションを Visual Studio 2010 に移行するには

1. DSL 移行ツールを起動します。

   - Windows エクスプローラー (またはエクスプローラー) でツールをダブルクリックするか、コマンド プロンプトからツールを起動できます。 ツールは次の場所にあります。

        **%ProgramFiles%\Microsoft Visual Studio 2010 SDK\VisualStudioIntegration\Tools\DSLTools\DslProjectsMigrationTool.exe**

2. 変換するソリューションおよびプロジェクトが含まれているフォルダーを選択します。

   - ツールの上部にあるボックスにパスを入力するか、 **[参照]** をクリックします。

     移行ツールには、DSL を定義または使用するプロジェクトのツリーが表示されます。 ツリーには、**Microsoft.VisualStudio.Modeling.Sdk** または **TextTemplating** アセンブリを使用するすべてのプロジェクトが含まれます。

3. プロジェクトのツリーを確認し、変換しないプロジェクトをオフにします。

   - プロジェクトまたはソリューションを選択すると、ツールによって行われる変更の一覧が表示されます。

       > [!NOTE]
       > フォルダー名の横に表示されるチェックボックスは無効です。 フォルダーを展開して、プロジェクトとソリューションを検査する必要があります。

4. プロジェクトを変換します。

   1. **[変換]** をクリックします。

        各プロジェクト ファイルが変換される前に、_project_ **.csproj** のコピーが _project_ **.vs2008.csproj** として保存されます

        各 _solution_ **.sln** のコピーは _solution_ **.vs2008.sln** として保存されます

   2. 報告された失敗した変換を調査します。

        エラーはテキスト ウィンドウに報告されます。 また、ツリー ビューでは、変換に失敗した各ノードに赤いフラグが表示されます。 ノードをクリックすると、そのエラーに関する詳細情報を取得できます。

5. 正常に変換されたプロジェクトを含むソリューション内の **すべてのテンプレートを変換** します。

   1. ソリューションを開きます。

   2. ソリューション エクスプローラーのヘッダーにある **[すべてのテンプレートの変換]** ボタンをクリックします。

       > [!NOTE]
       > この手順を不要にすることができます。 詳細については、「[方法: すべてのテンプレートを自動変換する](/previous-versions/visualstudio/visual-studio-2012/ff521399\(v\=vs.110\))」を参照してください。

6. 変換されたプロジェクトのカスタム コードを更新します。

   - プロジェクトのビルドを試行し、エラーを調査します。

   - デザイナーをテストします。

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="see-also"></a>関連項目

- [関連するブログ記事](https://devblogs.microsoft.com/devops/the-visual-studio-modeling-sdk-is-now-available-with-visual-studio-2017/)