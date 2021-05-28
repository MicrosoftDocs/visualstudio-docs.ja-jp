---
title: Outlook オブジェクト モデルの概要
description: Microsoft Outlook 用の VSTO アドインを開発するために Outlook オブジェクト モデルによって提供されているオブジェクトを操作することができます。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VST.ProjectItem.OutlookAddin
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Outlook [Office development in Visual Studio], object model overview
- object models [Office development in Visual Studio], Office
- objects [Office development in Visual Studio], Office object models
- object models [Office development in Visual Studio], Outlook
- Office object models
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 316ead76be1f84fccc6f675b204587008e8a194a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99885301"
---
# <a name="outlook-object-model-overview"></a>Outlook オブジェクト モデルの概要
  Microsoft Office Outlook 用の VSTO アドインを開発するには、Outlook オブジェクト モデルによって提供されるオブジェクトとのやり取りが可能です。 Outlook オブジェクト モデルは、ユーザー インターフェイスで項目を表すクラスとインターフェイスを提供します。 たとえば、 <xref:Microsoft.Office.Interop.Outlook.Application> オブジェクトは、アプリケーション全体を表し、 <xref:Microsoft.Office.Interop.Outlook.Folder> オブジェクトは、電子メール メッセージや他のアイテムを含むフォルダーを表します。 <xref:Microsoft.Office.Interop.Outlook.MailItem> オブジェクトは、電子メール メッセージを表します。

 このトピックでは、Outlook オブジェクト モデルのいくつかの主要なオブジェクトの概要を簡単に説明します。 Outlook オブジェクト モデル全体の詳細に関するリソースについては、「[Outlook オブジェクト モデルに関するドキュメントを使用する](#refdoc)」を参照してください。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="access-objects-in-an-outlook-project"></a>Outlook プロジェクトでオブジェクトにアクセスする
 Outlook では、多くのオブジェクトが操作対象になります。 オブジェクト モデルを効果的に使用するには、次の最上位レベルのオブジェクトについて理解する必要があります。

- <xref:Microsoft.Office.Interop.Outlook.Application>

- <xref:Microsoft.Office.Interop.Outlook.Explorer>

- <xref:Microsoft.Office.Interop.Outlook.Inspector>

- <xref:Microsoft.Office.Interop.Outlook.Folder>

- <xref:Microsoft.Office.Interop.Outlook.MailItem>

- <xref:Microsoft.Office.Interop.Outlook.AppointmentItem>

- <xref:Microsoft.Office.Interop.Outlook.TaskItem>

- <xref:Microsoft.Office.Interop.Outlook.ContactItem>

### <a name="application-object"></a>アプリケーション オブジェクト
 <xref:Microsoft.Office.Interop.Outlook.Application> オブジェクトは Outlook のアプリケーションを表し、Outlook オブジェクト モデルで最上位レベルのオブジェクトです。 このオブジェクトの最も重要なメンバーには、次のようなものがあります。

- [CreateItem](/previous-versions/office/developer/office-2003/aa220082(v=office.11)) メソッド。これを使用して、電子メール メッセージ、タスク、予定などの新しい項目を作成できます。

- <xref:Microsoft.Office.Interop.Outlook._Application.Explorers%2A> プロパティ。これを使用して、Outlook のユーザー インターフェイス (UI) で、フォルダーの内容を表示するウィンドウにアクセスできます。

- <xref:Microsoft.Office.Interop.Outlook._Application.Inspectors%2A> プロパティ。これを使用して、電子メール メッセージや会議出席依頼などの単一の項目の内容を表示するウィンドウにアクセスできます。

  <xref:Microsoft.Office.Interop.Outlook.Application> オブジェクトのインスタンスを取得するには、プロジェクトで `ThisAddIn` クラスの Application フィールドを使用します。 詳細については、「[VSTO アドインのプログラミング](../vsto/programming-vsto-add-ins.md)」を参照してください。

> [!NOTE]
> Outlook オブジェクト モデルの保護によってブロックされているプロパティとメソッドを使用するときに、セキュリティの警告が出ないようにするには、`ThisAddIn` クラスの Application フィールドから Outlook オブジェクトを取得します。 詳細については、「[Office ソリューションに関する特定のセキュリティの考慮事項](../vsto/specific-security-considerations-for-office-solutions.md)」を参照してください。

### <a name="explorer-object"></a>Explorer オブジェクト
 <xref:Microsoft.Office.Interop.Outlook.Explorer> オブジェクトは、電子メール メッセージ、タスク、または予定などの項目を含むフォルダーの内容を表示するウィンドウを表します。 <xref:Microsoft.Office.Interop.Outlook.Explorer> オブジェクトには、ウィンドウを変更するために使用するメソッドとプロパティ、およびウィンドウが変更されたときに発生するイベントが含まれます。

 <xref:Microsoft.Office.Interop.Outlook.Explorer> オブジェクトを取得するには、以下のいずれかを実行します。

- <xref:Microsoft.Office.Interop.Outlook._Application.Explorers%2A> オブジェクトの <xref:Microsoft.Office.Interop.Outlook.Application> プロパティを使用して、Outlook 内のすべての <xref:Microsoft.Office.Interop.Outlook.Explorer> オブジェクトにアクセスします。

- <xref:Microsoft.Office.Interop.Outlook._Application.ActiveExplorer%2A> オブジェクトの <xref:Microsoft.Office.Interop.Outlook.Application> メソッドを使用して、現在フォーカスしている <xref:Microsoft.Office.Interop.Outlook.Explorer> を取得します。

- <xref:Microsoft.Office.Interop.Outlook.Folder> オブジェクトの `GetExplorer` メソッドを使用して、現在のフォルダーの <xref:Microsoft.Office.Interop.Outlook.Explorer> を取得します。

### <a name="inspector-object"></a>Inspector オブジェクト
 <xref:Microsoft.Office.Interop.Outlook.Inspector> オブジェクトは、電子メール メッセージ、タスク、または予定などの単一の項目を表示するウィンドウを表します。 <xref:Microsoft.Office.Interop.Outlook.Inspector> オブジェクトには、ウィンドウを変更するために使用するメソッドとプロパティ、およびウィンドウが変更されたときに発生するイベントが含まれます。

 <xref:Microsoft.Office.Interop.Outlook.Inspector> オブジェクトを取得するには、以下のいずれかを実行します。

- <xref:Microsoft.Office.Interop.Outlook._Application.Inspectors%2A> オブジェクトの <xref:Microsoft.Office.Interop.Outlook.Application> プロパティを使用して、Outlook 内のすべての <xref:Microsoft.Office.Interop.Outlook.Inspector> オブジェクトにアクセスします。

- <xref:Microsoft.Office.Interop.Outlook._Application.ActiveInspector%2A> オブジェクトの <xref:Microsoft.Office.Interop.Outlook.Application> メソッドを使用して、現在フォーカスしている <xref:Microsoft.Office.Interop.Outlook.Inspector> を取得します。

- 特定の項目 (<xref:Microsoft.Office.Interop.Outlook.MailItem> や <xref:Microsoft.Office.Interop.Outlook.AppointmentItem> など) の `GetInspector` メソッドを使用して、それらの項目に関連付けられているインスペクタを取得します。

### <a name="folder-object"></a>Folder オブジェクト
 <xref:Microsoft.Office.Interop.Outlook.Folder> オブジェクトは、電子メール メッセージ、連絡先、タスク、およびその他の項目が含まれているフォルダーを表します。 Outlook には 16 の既定の <xref:Microsoft.Office.Interop.Outlook.Folder> オブジェクトが用意されています。

 既定の <xref:Microsoft.Office.Interop.Outlook.Folder> オブジェクトは <xref:Microsoft.Office.Interop.Outlook.OlDefaultFolders> 列挙値により、定義されます。 たとえば、次のように入力します。

 Microsoft.Office.Interop.Outlook.OlDefaultFolders.olFolderInbox は、Outlook の **受信トレイ** フォルダーに対応します。

 既定の <xref:Microsoft.Office.Interop.Outlook.Folder> にアクセスして新しい <xref:Microsoft.Office.Interop.Outlook.Folder> を作成する方法がわかる例については、「[方法: プログラムによってカスタム フォルダーのアイテムを作成する](../vsto/how-to-programmatically-create-custom-folder-items.md)」を参照してください。

### <a name="mailitem-object"></a>MailItem オブジェクト
 <xref:Microsoft.Office.Interop.Outlook.MailItem> オブジェクトは電子メール メッセージを表します。 <xref:Microsoft.Office.Interop.Outlook.MailItem> オブジェクトは通常、「 **受信トレイ**」、「 **送信済みアイテム**」、および「 **送信トレイ**」などのフォルダーにあります。 <xref:Microsoft.Office.Interop.Outlook.MailItem> は、電子メール メッセージを作成し、送信するために使用できるプロパティとメソッドを公開します。

 メール メッセージを作成する方法がわかる例については、「[方法: プログラムによって電子メール アイテムを作成する](../vsto/how-to-programmatically-create-an-e-mail-item.md)」を参照してください。

### <a name="appointmentitem-object"></a>AppointmentItem オブジェクト
 <xref:Microsoft.Office.Interop.Outlook.AppointmentItem> オブジェクトは **カレンダー** フォルダー内の会議、1 回限りの予定、または定期的な予定や会議を表します。 <xref:Microsoft.Office.Interop.Outlook.AppointmentItem> オブジェクトには、会議出席依頼の応答や転送などのアクションを実行するメソッドと、会議の場所や時間など、会議詳細を指定するプロパティが含まれます。

 予定を作成する方法がわかる例については、「[方法: プログラムによって会議出席依頼を作成する](../vsto/how-to-programmatically-create-a-meeting-request.md)」を参照してください。

### <a name="taskitem-object"></a>TaskItem オブジェクト
 <xref:Microsoft.Office.Interop.Outlook.TaskItem> オブジェクトは、指定した期間内で実行するタスクを表します。 <xref:Microsoft.Office.Interop.Outlook.TaskItem> オブジェクトは **[タスク]** フォルダーにあります。

 タスクを作成するには、 [オブジェクトの](/previous-versions/office/developer/office-2003/aa220082(v=office.11)) CreateItem <xref:Microsoft.Office.Interop.Outlook.Application> メソッドを使用して、パラメーターの値 <xref:Microsoft.Office.Interop.Outlook.OlItemType.olTaskItem> を渡します。

### <a name="contactitem-object"></a>ContactItem オブジェクト
 <xref:Microsoft.Office.Interop.Outlook.ContactItem> オブジェクトは、**連絡先** フォルダー内の連絡先を表します。 <xref:Microsoft.Office.Interop.Outlook.ContactItem> オブジェクトには、住所、電子メール アドレス、電話番号など、そのオブジェクトが表す人のさまざまな連絡先情報が含まれます。

 新しい連絡先を作成する方法がわかる例については、「[方法: プログラムによって Outlook の連絡先にエントリを追加する](../vsto/how-to-programmatically-add-an-entry-to-outlook-contacts.md)」を参照してください。 既存の連絡先を検索する方法がわかる例については、「[方法: プログラムによって特定の連絡先を検索する](../vsto/how-to-programmatically-search-for-a-specific-contact.md)」を参照してください。

## <a name="use-the-outlook-object-model-documentation"></a><a name="refdoc"></a> Outlook オブジェクト モデルに関するドキュメントを使用する
 Outlook オブジェクト モデルに関する詳細については、Outlook プライマリ相互運用機能アセンブリ (PIA) のリファレンスと、VBA オブジェクト モデルのリファレンスを参照してください。

### <a name="primary-interop-assembly-reference"></a>プライマリ相互運用機能アセンブリのリファレンス
 Outlook の PIA リファレンスには、Outlook 2010 のプライマリ相互運用機能アセンブリの種類について記述されています。 詳細については、[Outlook 2010 プライマリ相互運用機能アセンブリ リファレンス](/previous-versions/office/developer/office-2010/bb652780(v=office.14))に関する記事を参照してください。

 この資料には、PIA の型すべての情報を提供されています。さらに、PAI の構造に関する詳細情報と、一般的な Outlook 自動化タスクのコード例も提供されています。

### <a name="vba-object-model-reference"></a>VBA オブジェクト モデルのリファレンス
 VBA オブジェクト モデルのリファレンスでは、Visual Basic for Applications (VBA) コードに公開される Outlook オブジェクト モデルについて説明しています。 詳細については、[Outlook 2010 オブジェクト モデル リファレンス](/office/vba/api/overview/Outlook/object-model)に関する記事を参照してください。

 VBA オブジェクト モデルのリファレンス内のオブジェクトとメンバーはすべて、Outlook PIA の型とメンバーに対応します。 たとえば、VBA オブジェクト モデルのリファレンスの Inspector オブジェクトは、Outlook PIA の <xref:Microsoft.Office.Interop.Outlook.Inspector> オブジェクトに対応します。 VBA オブジェクト モデルのリファレンスでは、ほとんどのプロパティ、メソッド、およびイベントのコード例を紹介しています。ただし、Visual Studio を使用して作成した Outlook VSTO アドイン プロジェクトでこのリファレンス内の VBA コードを使用するには、それらを Visual Basic または Visual C# に変換する必要があります。

### <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[連絡先アイテムを操作する](../vsto/working-with-contact-items.md)|アドレス帳を使用したさまざまなタスクを実行する方法を説明するトピックを提供します。|
|[メール アイテムを操作する](../vsto/working-with-mail-items.md)|メール アイテムを使用してタスクを実行する方法を説明するトピックを提供します。|
|[フォルダーを操作する](../vsto/working-with-folders.md)|フォルダーを使用してタスクを実行する方法を説明するトピックを提供します。|
|[予定表アイテムを操作する](../vsto/working-with-calendar-items.md)|予定表アイテムを使用してタスクを実行する方法を説明するトピックを提供します。|
|[方法: プログラムによって現在の Outlook のアイテムを確認する](../vsto/how-to-programmatically-determine-the-current-outlook-item.md)|現在のフォルダー名と、選択したアイテムに関する情報を表示する方法を示します。|
