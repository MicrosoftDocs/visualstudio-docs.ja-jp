---
title: Visual Studio での Office および SharePoint 開発
description: ユーザーが Office ストアからダウンロードする軽量なアプリやアドインを作成して、Microsoft Office および SharePoint を拡張する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office applications [Office development in Visual Studio], about developing applications
- Office development in Visual Studio
- Office projects
- Visual Studio Tools for Office, see Office development in Visual Studio
- Office applications [Office development in Visual Studio]
- Office Business Applications
- applications [Office development in Visual Studio]
- programming [Office development in Visual Studio]
- VSTO, see Office development in Visual Studio
- Office, development with Visual Studio
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: cebcb16708e42f8102e2dc235b52a81e16c588c7
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99940905"
---
# <a name="office-and-sharepoint-development-in-visual-studio"></a>Visual Studio での Office および SharePoint 開発
  ユーザーが [Office ストア](https://store.office.com/) または組織のカタログからダウンロードする軽量なアプリやアドインを作成するか、ユーザーがコンピューターにインストールする .NET Framework ベースのソリューションを作成することによって、Microsoft Office および SharePoint を拡張できます。

 このトピックの内容:

- [Office と SharePoint 用アドインの作成](#Apps)

- [VSTO アドインの作成](#Add-ins)

- [SharePoint ソリューションの作成](#Solutions)

## <a name="create-add-ins-for-office-and-sharepoint"></a><a name="Apps"></a> Office と SharePoint 用アドインの作成
 Office 2013 と SharePoint 2013 では、Office と SharePoint を拡張するためのアドインを構築、配布、収益化するために役立つ新しいアドイン モデルが導入されます。  これらのアドインは、Office Online または SharePoint Online で実行でき、ユーザーは多くのデバイスからアプリと対話できます。

 新しい [Office アドイン モデル](/office/dev/add-ins/overview/office-add-ins)を使用してユーザーの Office エクスペリエンスを拡張する方法をご確認ください。

 これらのアドインのフットプリントは、VSTO アドインやソリューションと比較して小さく、その作成には、HTML5、JavaScript、CSS3、XML など、ほぼすべての Web プログラミング テクノロジを使用できます。  作業を始めるには、Visual Studio で Office Developer Tools を使用します。これを使用すると、プロジェクトを作成し、コードを記述した後、構築したアドインをブラウザー内で実行できます。

 ![Office 用アプリと SharePoint 用アプリの概念モデル](../vsto/media/officeandsharepointapps2015.png "Office 用アプリと SharePoint 用アプリの概念モデル")

### <a name="build-an-office-add-in"></a>Office アドインをビルドする
 Office の機能を拡張するには、Office アドインを構築します。 これは基本的に、Excel、Word、Outlook、PowerPoint などの Office アプリケーションでホストされる Web ページです。 構築したアプリを使用して、ドキュメント、ワークシート、電子メール メッセージ、予定、プレゼンテーション、およびプロジェクトに機能を追加できます。

 構築したアプリは Office ストアで販売できます。  [Office ストア](https://store.office.com/) を使用すると、アドインの収益化、更新プログラムの管理、および利用統計情報の追跡が簡単になります。 また、SharePoint のアプリ カタログや Exchange Server 上で、アプリをユーザーに公開することもできます。

 Bing マップ内にワークシートのデータを表示する Office 向けアプリを次に示します。

 ![Office 用のコンテンツ アプリ](../vsto/media/appforoffice.png "Office 用のコンテンツ アプリ")

 **詳細情報**

|終了|解決方法については、|
|--------|---------|
|Office アドインの詳細を確認し、アドインを構築する。|[Office アドイン](/office/dev/add-ins/publish/publish)|
|Office のさまざまな拡張方法を比較し、アプリと Office アドインのどちらを使用する必要があるかを判断する。|[Office アドイン、VSTO、および VBA へのロードマップ](/archive/blogs/officeapps/roadmap-for-apps-for-office-vsto-and-vba)|

### <a name="build-a-sharepoint-add-in"></a>SharePoint アドインをビルドする
 ユーザー向けに SharePoint を拡張するには、SharePoint アドインを構築します。 これは基本的に、ユーザーやビジネスの要件を解決する、小さくて使いやすい、スタンドアロンのアプリケーションです。

 構築した SharePoint 用のアプリは [Office ストア](https://store.office.com/)で販売できます。 また、SharePoint のアドイン カタログを使用して、アドインをユーザーに公開することもできます。  サイト所有者は、ファーム サーバーやサイト コレクションの管理者の助けを借りることなく、アドインを SharePoint サイトにインストール、アップグレード、およびアンインストールできます。

 ユーザーが取引先担当者を管理するときに役立つ SharePoint 用アプリの例を次に示します。

 ![SharePoint 用 Business Contact Manager アプリ](../vsto/media/appforsharepoint.png "SharePoint 用 Business Contact Manager アプリ")

 **詳細情報**

|終了|解決方法については、|
|--------|---------|
|SharePoint アドインの詳細を確認し、アドインを構築する。|[SharePoint アドイン](/sharepoint/dev/sp-add-ins/sharepoint-add-ins)|
|SharePoint アドインを従来の SharePoint ソリューションと比較する。|[SharePoint アドインと SharePoint ソリューションの比較](/sharepoint/dev/general-development/sharepoint-server-application-lifecycle-management)|
|SharePoint ソリューションと SharePoint アドインのどちらを構築するかを選択する。|[SharePoint アドインと SharePoint ソリューションのどちらかに決める](/sharepoint/dev/general-development/sharepoint-server-application-lifecycle-management)|

## <a name="create-a-vsto-add-in"></a><a name="Add-ins"></a>VSTO アドインの作成
 Office 2007 または Office 2010 を対象とする VSTO アドインを作成したり、Office 2013 と Office 2016 を拡張するための VSTO アドインを作成して、Office アドインでは提供できない機能を実装したりできます。VSTO アドインはデスクトップ上でのみ動作します。 ユーザーは VSTO アドインをインストールする必要があるため、通常はアドインの配置やサポートが難しくなります。  ただし、VSTO アドインは、より密接に Office に統合できます。 たとえば、Office リボンにタブやコントロールを追加し、文書の結合やグラフの変更などの高度な自動化タスクを実行できます。 また、.NET Framework を活用し、C# および Visual Basic を使用して、Office オブジェクトと対話することもできます。

 VSTO アドインで提供できる機能の例を次に示します。 この VSTO アドインは、PowerPoint にリボン コントロール、カスタム作業ウィンドウ、およびダイアログ ボックスを追加します。

 ![PowerPoint アドイン ソリューション](../vsto/media/powerpointaddin.png "PowerPoint アドイン ソリューション")

 **詳細情報**

|ターゲット|Read|
|--------|----------|
|Office のさまざまな拡張方法を比較し、VSTO アドインと Office アドインのどちらを使用する必要があるかを判断する。|[Office アドイン、VSTO、および VBA へのロードマップ](/archive/blogs/officeapps/roadmap-for-apps-for-office-vsto-and-vba)|
|VSTO アドインを作成する。|[Visual Studio で作成した VSTO アドイン](create-vsto-add-ins-for-office-by-using-visual-studio.md)|

## <a name="create-a-sharepoint-solution"></a><a name="Solutions"></a> SharePoint ソリューションの作成
 SharePoint Foundation 2010 および SharePoint Server 2010 を対象とする SharePoint ソリューションを作成したり、SharePoint 2013 と SharePoint 2016 を拡張するための SharePoint ソリューションを作成して、SharePoint アドインでは提供できない機能を実装したりできます。

 SharePoint ソリューションには、内部設置型の SharePoint ファーム サーバーが必要です。 管理者はソリューションをインストールする必要があります。また、ソリューションは SharePoint 内で実行されるため、サーバーのパフォーマンスに影響を与える可能性があります。 ただし、ソリューションでは、より深いレベルの SharePoint オブジェクトへのアクセスが提供されます。 また、SharePoint ソリューションの構築時に、.NET Framework を活用し、C# および Visual Basic を使用して、SharePoint オブジェクトと対話できます。

 **詳細情報**

|終了|解決方法については、|
|--------|---------|
|SharePoint ソリューションを SharePoint アドインと比較する。|[SharePoint アドインと SharePoint ソリューションの比較](/sharepoint/dev/general-development/sharepoint-server-application-lifecycle-management)|
|SharePoint ソリューションを作成する。|[SharePoint ソリューションの作成](../sharepoint/create-sharepoint-solutions.md)|