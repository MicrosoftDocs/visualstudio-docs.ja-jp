---
title: サンドボックス ソリューションに関する考慮事項 |Microsoft Docs
description: サンドボックス ソリューションについて説明します。これは、サイト コレクション ユーザーが独自のカスタム コード ソリューションをアップロードできるようにする Microsoft SharePoint の機能です。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.Project.SandboxedSolutions
- VS.SharePointTools.Security.SandboxedSolutions
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, sandboxed solutions
- sandboxed solutions [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, farm solutions
- farm solutions [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 23424c1681a9967d9d50df47f9e67ec895a308a1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99881608"
---
# <a name="sandboxed-solution-considerations"></a>サンドボックス ソリューションの考慮事項
  "*サンドボックス ソリューション*" は、サイト コレクション ユーザーが独自のカスタム コード ソリューションをアップロードできるようにする Microsoft SharePoint 2010 の機能です。 一般的なサンドボックス ソリューションでは、ユーザーが独自の Web パーツをアップロードします。

 サンドボックス化された SharePoint アプリケーションは、Web ファームの限られた部分にアクセスできる、セキュリティで保護された監視対象のプロセスで実行されます。 Microsoft SharePoint 2010 では、機能、ソリューション ギャラリー、ソリューションの監視、検証フレームワークの組み合わせを使用して、サンドボックス ソリューションを有効にします。

## <a name="specify-project-trust-level"></a>プロジェクトの信頼レベルを指定する
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] では、"*サンドボックス ソリューション*" と呼ばれるブール型のプロジェクト プロパティを使用して、サンドボックス ソリューションをサポートします。 このプロパティは、プロジェクトでいつでも設定できます。また、**SharePoint カスタマイズ ウィザード** でプロジェクトを作成するときに指定することもできます。

> [!NOTE]
> プロジェクトの作成後に、その "*サンドボックス ソリューション*" プロパティを変更すると、検証エラーが発生する可能性があります。

 "*サンドボックス ソリューション*" プロパティが **false** に設定されている場合、または **[ファーム ソリューションとして配置する]** オプションを選択した場合、このソリューションはファーム スコープのソリューションと見なされます。 しかし、"*サンドボックス ソリューション*" プロパティが **true** に設定されている場合、またはウィザードで **[サンドボックス ソリューションとして配置する]** オプションを選択した場合、このソリューションはファーム ソリューションとは異なる方法で処理されます。

## <a name="sharepoint-site-hierarchy"></a>SharePoint サイト階層
 サンドボックス ソリューションのしくみを理解するには、SharePoint サイトがスコープ内に階層化されていることを知っておくと役に立ちます。 最上位の要素は Web ファームと呼ばれ、他の要素はその下位にあります。

 Web ファーム

 Web アプリケーション A

 サイト コレクション A1

 サイト A1a

 Web アプリケーション B

 サイト コレクション B1

 サイト B1a

 サイト B1b

 サイト コレクション B2

 サイト B2a

 ご覧のように、Web ファームに 1 つ以上の Web アプリケーションが含まれ、そこに 1 つ以上のサイト コレクションが含まれ、そこにサブサイトが含まれます (以下同様)。 1 つのサイト コレクションに加えられた変更は、そのサイト コレクションにのみ影響し、それ以外には影響しません。 しかし、Web ファーム レベルで行われた変更は、ファーム上のすべてのサイト コレクションに影響します。

 Windows SharePoint Services (WSS) 3.0 では、ソリューションをファーム レベルにのみ配置できますが、[!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] では、ファーム レベル (ファーム ソリューション) またはサイト コレクション レベル (サンドボックス ソリューション) のいずれかに配置できます。

## <a name="why-sandboxed-solutions"></a>サンドボックス ソリューションを使用する理由
 WSS 3.0 では、ソリューションをファーム レベルにのみ配置できました。 これは、潜在的に有害または不安定なソリューションを配置すると、Web ファーム全体とその下で実行される他のすべてのサイト コレクションおよびアプリケーションに影響する可能性があることを意味していました。 しかし、サンドボックス ソリューションを使用すると、ファームのサブエリアである特定のサイト コレクションにソリューションを配置できます。 追加の保護を提供するため、ソリューションのアセンブリはメイン [!INCLUDE[TLA2#tla_iis5](../sharepoint/includes/tla2sharptla-iis5-md.md)] プロセス (*w3wp.exe*) に読み込まれません。 代わりに、別のプロセス (*SPUCWorkerProcess.exe*) に読み込まれます。 このプロセスは監視され、これによって実装されたクォータとスロットルにより、CPU サイクルを消費する短いループの実行など、有害なアクティビティを実行するサンドボックス ソリューションからファームが保護されます。

## <a name="site-collection-solution-gallery"></a>サイト コレクション ソリューション ギャラリー
 [!INCLUDE[sharepointShort](../sharepoint/includes/sharepointshort-md.md)] 2010 には、"サイト コレクション ソリューション ギャラリー" と呼ばれる機能があります。 この機能にアクセスするには、SharePoint 2010 サーバーの全体管理ページを開くか、SharePoint サイトで **[サイトの操作]** メニューを開いて **[サイトの設定]** を選択してから、 **[ギャラリー]** の下にある **[ソリューション]** リンクを選択します。 ソリューション ギャラリーは、サイト コレクションの管理者がサイト コレクション内のソリューションを管理できるようにするソリューションのリポジトリです。

 ソリューション ギャラリーは、SharePoint サイトのルート Web に格納されているドキュメント ライブラリです。 ソリューション ギャラリーによって、サイト テンプレートが置き換えられ、ソリューション パッケージがサポートされます。 SharePoint ソリューション パッケージ ( *.wsp*) ファイルがアップロードされると、それはサンドボックス ソリューションとして処理されます。

## <a name="sandboxed-solution-limitations"></a>サンドボックス ソリューションの制限事項
 サンドボックス ソリューションが配置されている場合は、そこで使用できる一連の SharePoint 機能が制限されているため、そこで発生するセキュリティの脆弱性を減らすことができます。 これらの制限事項には、次のようなものがあります。

- サンドボックス ソリューションでは、使用できる配置可能なソリューション要素がサブセットに制限されます。 サイト定義やワークフローなど、脆弱である可能性がある SharePoint プロジェクト テンプレートは使用できません。

- SharePoint では、メイン [!INCLUDE[TLA2#tla_iis5](../sharepoint/includes/tla2sharptla-iis5-md.md)] アプリケーション プール (*w3wp.exe*) プロセスとは別のプロセス (*SPUCWorkerProcess.exe*) で、サンドボックス ソリューションのコードを実行します。

- マップされたフォルダーをプロジェクトに追加することはできません。

- サンドボックス ソリューションでは、[!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] のアセンブリ Microsoft.Office.Server 内の型を使用できません。 また、サンドボックス ソリューションでは [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] のアセンブリ Microsoft.SharePoint 内の型のみを使用できます。

  SharePoint ソリューションをサンドボックス ソリューションとして指定しても、SharePoint サーバーには影響しないことにご注意ください。SharePoint プロジェクトを [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] から SharePoint に配置する方法とバインド先のアセンブリが決定されるだけです。 生成された *.wsp* ファイルには影響しません。また、 *.wsp* ファイルには、"*サンドボックス ソリューション*" プロパティに直接関連付けられるデータはありません。

## <a name="capabilities-and-elements-in-sandboxed-solutions"></a>サンドボックス ソリューションの機能と要素
 サンドボックス ソリューションでは、次の機能と要素がサポートされます。

- コンテンツの種類/フィールド

- カスタム アクション

- 宣言型ワークフロー

- イベント レシーバー

- 機能のコールアウト

- List Definitions

- リスト インスタンス

- モジュール/ファイル

- ナビゲーション

- *Onet.xml*

- SPItemEventReceiver

- SPListEventReceiver

- SPWebEventReceiver

- `System.Web.UI.WebControls.WebParts.WebPart` から派生するすべての Web パーツのサポート

- Web パーツ

- WebTemplate 機能要素 (*Webtemp.xml* ではなく)

- 視覚的 Web パーツ

  サンドボックス ソリューションでは、次の機能と要素はサポートされません。

- アプリケーション ページ

- カスタム アクション グループ

- ファーム スコープの機能

- `HideCustomAction` 要素

- Web アプリケーション スコープの機能

- コードを含むワークフロー

## <a name="see-also"></a>関連項目
- [サンドボックス ソリューションとファーム ソリューションの違い](../sharepoint/differences-between-sandboxed-and-farm-solutions.md)
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
