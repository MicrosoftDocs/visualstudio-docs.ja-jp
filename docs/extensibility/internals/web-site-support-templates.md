---
title: Web サイト サポートのテンプレート | Microsoft Docs
description: Web サイト サポートのテンプレートについて説明します。 Visual Studio Web サイトのプロジェクト テンプレートと項目テンプレートは、再利用可能で、かつカスタマイズ可能な Web サイト プロジェクトおよび項目スタブを提供します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- we site projects, templates
ms.assetid: 37173c97-486b-4b3c-8ed3-cf5890c4de23
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a1bd391d13a6d650cb4d23ce78789a66ef50c2e3
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898896"
---
# <a name="web-site-support-templates"></a>Web サイト サポートのテンプレート
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Web サイトのプロジェクト テンプレートと項目テンプレートは、新しい Web サイトのプロジェクトや項目を最初から作成しなくても済むようにして開発プロセスを加速する、再利用可能で、かつカスタマイズ可能な Web サイト プロジェクトおよび項目スタブを提供します。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] テンプレートの詳細については、[プロジェクト テンプレートと項目テンプレートの作成](../../ide/creating-project-and-item-templates.md)に関するページを参照してください。

## <a name="project-template-folder"></a>プロジェクト テンプレート フォルダー
 Web プロジェクト テンプレートは通常、[*Visual Studio インストール パス*]\Common7\IDE\ProjectTemplates\Web\\ 内の、その Web プログラミング言語に基づいて名前が付けられたサブフォルダーに各テンプレートがインストールされます。

## <a name="project-file"></a>プロジェクト ファイル
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE) には、テンプレートを正しいプロジェクトの種類にマップするための方法としてプロジェクト ファイル拡張子が必要です。 Web プロジェクトにはプロジェクト ファイルがないため、テンプレートをこのプロジェクトの種類にマップするには、ダミーのプロジェクト ファイル拡張子 .webproj が登録されます。

 必要に応じて、Web プロジェクト システムで、テンプレートに基づいて項目の **[新しい項目の追加]** ダイアログ ボックスで既定の言語を設定できるようにするために、テンプレートに言語名文字列を追加できます。 この文字列は、ファイルの最初の行である必要があります。 これは、IntelliSense エンジンの登録で AddItemLanguageName に登録されている名前と、プロジェクト サブタイプ (VsTemplate) に登録されている名前の両方に一致している必要があります。 詳細については、「[Web サイト サポートの属性](../../extensibility/internals/web-site-support-attributes.md)」を参照してください。

 この文字列が存在しない場合、Web プロジェクト システムでは、プロジェクト テンプレートによってその Web プロジェクトに追加されたページの Language 属性とファイル拡張子に基づいて既定の言語を特定しようとします。

## <a name="project-templates"></a>プロジェクト テンプレート
 Web サイト プロジェクト テンプレートは、 **[ファイル]** メニューの **[新しい Web サイト]** コマンドに応答して新しい Web サイトを構築するために使用されます。 現在、次の 3 つの Web サイト プロジェクトの種類がサポートされています。

- 空の Web サイト プロジェクト

- Web サイト プロジェクト

- Web サービス プロジェクト

### <a name="empty-web-site-projects"></a>空の Web サイト プロジェクト
 次のファイルでは、 **[ファイル]**  >  **[新しい Web サイト]** の順に選択した後に使用できる **[空の Web サイト]** コマンドに応答して新しい空の Web サイトを作成します。

- EmptyWeb.vstemplate

     新しい空の Web サイトの作成を案内するテンプレート ファイル。

- EmptyWeb.webproj

     このファイルは、プロジェクト テンプレート システムの成果物です。 これは、EmptyWeb.vstemplate ファイル内のプロジェクト ファイル参照を満たしています。

### <a name="web-site-projects"></a>Web サイト プロジェクト
 次のファイルでは、 **[ファイル]**  >  **[新しい Web サイト]** の順に選択した後に使用できる **[ASP.NET Web サイト]** コマンドに応答して新しい Web サイトを作成します。

- Default.aspx

     新しい Web サイトの既定のホーム ページ。 Language 属性は分離コード言語を指定し、CodeFile 属性は、このページに関連付けられた分離コードが含まれている依存ファイルを指定します。

- Default.aspx.*拡張子*

     既定のホーム ページの分離コードが含まれている依存ファイル。 分離コード言語によって、このファイルの "*拡張子*" が決定されます。

- web.config

     ルート web.site 構成ファイル。

- WebApplication.vstemplate

     Web サイト ソリューションの内容を決定し、App_Data フォルダーを強制的に作成するテンプレート ファイル。

- WebApplication.webproj

     このファイルは、プロジェクト テンプレート システムの成果物です。 これは、WebApplication.vstemplate ファイル内のプロジェクト ファイル参照を満たしています。

### <a name="web-service-projects"></a>Web サービス プロジェクト
 次のファイルでは、 **[ファイル]**  >  **[新しい Web サイト]** の順に選択した後に使用できる **[ASP.NET Web サービス]** コマンドに応答して新しい Web サイトを作成します。

- Service.asmx

     新しい Web サービスの HTML ページ。 Language 属性は分離コード言語を指定し、CodeBehind 属性は、このサービスに関連付けられた分離コードが含まれている依存ファイルを指定します。

- サービス。 *extension*

     サービス クラスを実装する依存ファイル。 分離コード言語によって、このファイルの "*拡張子*" が決定されます。

- web.config

- ルート web.site 構成ファイル。

- WebService.vstemplate

     Web サイト ソリューションの内容を決定し、App_Data および App_Code フォルダーを強制的に作成するテンプレート ファイル。 service.*拡張子* ファイルは、App_Code フォルダーにコピーされます。

- WebService.webproj

     このファイルは、プロジェクト テンプレート システムの成果物です。 これは、WebService.vstemplate ファイル内のプロジェクト ファイル参照を満たしています。

## <a name="project-item-template-folder"></a>プロジェクト項目テンプレート フォルダー
 Web プロジェクト項目テンプレートは通常、[*Visual Studio インストール パス*]\Common7\IDE\ItemTemplates\Web\\ 内の、その Web プログラミング言語に基づいて名前が付けられたサブフォルダーに各テンプレートがインストールされます。

## <a name="project-item-templates"></a>プロジェクト項目テンプレート
 Web サイト プロジェクト項目テンプレートは、 **[既存項目の追加]** コマンドに応答して、Web サイトに新しい Web ページを追加するために使用されます。 現在、次の種類の Web ページがサポートされています。

- 新しいクラス

- 新しい HTML ページ

- 新しい Web フォーム

- 新しいマスター ページ

### <a name="new-class"></a>新しいクラス
 このテンプレートでは、 **[新しいクラスの追加]** コマンドに応答して、空のクラスを定義する新しいソース ファイルを作成します。

- クラス。 *extension*

     空のクラスを実装するソース ファイル。 分離コード言語によって、このファイルの "*拡張子*" が決定されます。

- Class.vstemplate

     ソース ファイルを作成し、その内容を決定するテンプレート ファイル。

### <a name="new-html-page"></a>新しい HTML ページ
 このテンプレートでは、 **[新しい HTML ページの追加]** コマンドに応答して新しい Web ページを作成します。

- HTMLPage.htm

     Web ページの開始コンテンツ。 この Web ページには通常、分離コード依存ファイルが関連付けられていません。 関連付けられた分離コード ファイルを使用してスマート ページを作成するには、代わりに Web フォーム テンプレートを使用します。

- HTMLPage.vstemplate

     Web ページを作成し、その内容を決定するテンプレート ファイル。

### <a name="new-webform"></a>新しい Web フォーム
 このテンプレートでは、 **[新しい Web フォームの追加]** コマンドに応答して新しいスマート Web ページを作成します。

 依存した分離コード ソース ファイルを作成するには、 **[コードを別のファイルに配置する]** を選択します。 それ以外の場合は、空のスクリプト ブロックを含み、依存ファイルをフックするための \<% Page %> ディレクティブが存在しない 1 つの Web ページが作成されます。

 選択されたマスター ページのコンテンツ ページを作成するには、 **[マスター ページを選択する]** を選択します。

- WebForm.aspx

     Web ページの開始コンテンツ。 この Web ページには、分離コード依存ファイルが関連付けられていません。

- WebForm_cb.aspx

     Web ページの開始コンテンツ。 この Web ページには、分離コード依存ファイルが関連付けられています。

- Codebehind. *extension*

     webform クラスを実装する依存ファイル。 分離コード言語によって、このファイルの "*拡張子*" が決定されます。

- ContentPage.aspx

     コンテンツ ページとしての Web ページの開始コンテンツ。 この Web ページには、分離コード依存ファイルが関連付けられていません。

- ContentPage_cb.aspx

     コンテンツ ページとしての Web ページの開始コンテンツ。 この Web ページには、分離コード依存ファイルが関連付けられています。

- WebForm.vstemplate

     新しい Web ページとその依存ファイル (存在する場合) の内容を決定するテンプレート ファイル。

### <a name="new-master-page"></a>新しいマスター ページ
 このテンプレートでは、 **[新しいマスター ページの追加]** コマンドに応答して新しいマスター ページを作成します。

 依存した分離コード ソース ファイルを作成するには、 **[コードを別のファイルに配置する]** を選択します。 それ以外の場合は、空のスクリプト ブロックを含み、依存ファイルをフックするための \<% Page %> ディレクティブが存在しない 1 つの Web ページが作成されます。

- MasterPage.master

     マスター ページの開始コンテンツ。 このマスター ページには通常、分離コード依存ファイルが関連付けられていません。

- MasterPage_cb.master

     マスター ページの開始コンテンツ。 このマスター ページには、分離コード依存ファイルが関連付けられています。

- Codebehind.*拡張子*

     マスター ページ クラスを実装する依存ファイル。 分離コード言語によって、このファイルの "*拡張子*" が決定されます。

- MasterPage.vstemplate

     新しいマスター ページとその依存ファイル (存在する場合) の内容を決定するテンプレート ファイル。

## <a name="see-also"></a>関連項目
- [Web サイト サポート](../../extensibility/internals/web-site-support.md)
