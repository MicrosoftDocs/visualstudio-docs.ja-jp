---
title: '方法: Visual Studio で Office プロジェクトを作成する'
description: Visual Studio を使用して、Microsoft Office アプリケーション向けに、VSTO アドインの作成やドキュメント レベルのカスタマイズを行う方法について説明します。
titleSuffix: ''
ms.custom: seodec18, SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VST.SelectDocWizard.Page1
- VST.SelectDocWizard.Http
- VST.SelectDocWizard.Extension
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- add-ins [Office development in Visual Studio], creating projects
- Office applications [Office development in Visual Studio], creating
- Office projects [Office development in Visual Studio]
- projects [Office development in Visual Studio], creating
- document-level customizations [Office development in Visual Studio], creating
- application-level add-ins [Office development in Visual Studio], creating projects
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 1d0bd242f3a57031442cb0b39e62a28c01ad1a6b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99962393"
---
# <a name="how-to-create-office-projects-in-visual-studio"></a>方法: Visual Studio で Office プロジェクトを作成する
  [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] を使用すると、Microsoft Office アプリケーション向けに、VSTO アドインの作成やドキュメント レベルのカスタマイズができます。 これらの種類のプロジェクトの詳細については、「[Office ソリューションの開発の概要 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)」を参照してください。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-create-a-vsto-add-in-project"></a>VSTO アドイン プロジェクトを作成するには

1. **[ファイル]** メニューで、 **[新規]**  >  **[プロジェクト]** の順にクリックします。 統合開発環境 (IDE) が [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] 開発設定を使用するように設定されている場合は、 **[ファイル]** メニューの **[新規作成]**  >  **[プロジェクト]** の順に選択します。

    **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

   > [!NOTE]
   > 既定では、Office プロジェクトは [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] を対象とします。 詳細については、「[.NET Framework Client Profile](/dotnet/framework/deployment/client-profile)」を参照してください。

2. [テンプレート] ウィンドウで、使用する言語のノードの下にある **[Office/SharePoint]** を展開します。

3. **[Office アドイン]** ノードを選択します。

4. プロジェクト テンプレートの一覧で、VSTO アドイン プロジェクト テンプレートを選択します。 使用できる VSTO アドイン プロジェクト テンプレートの一覧については、[Office プロジェクト テンプレートの概要](../vsto/office-project-templates-overview.md)に関するページを参照してください。

   > [!NOTE]
   > **[Office アドイン]** ノードを選択してもプロジェクト テンプレートが表示されない場合、ダイアログ ボックス上部のコンボ ボックスで **[.NET Framework 4]** またはそれ以降が選択されていることを確認してください。 Office プロジェクト テンプレートは、.NET Framework の両方のバージョンで表示されます。

5. **[名前]** ボックスにプロジェクト名を入力します。 既定では、このプロジェクト名がソリューション名としても使用されます。

6. **[場所]** ボックスに、プロジェクトを作成する場所を表すパスを入力します。 絶対パスと UNC (Universal Naming Convention) パスを使用できます。 HTTP、FTP、またはその他のプロトコル パスは使用しないでください。

    場所は、次の形式で指定します。

   * [*ドライブ*\]\:

   * \\\\*サーバー*\\*共有*

     次の文字は使用しないでください。

   * アスタリスク (*)

   * 縦棒 (|)

   * コロン (:) (ドライブ文字の後に使用する場合は除く)

   * 二重引用符 (") (スペースを含むパスには引用符は不要)

   * より小さい (\<)

   * より大きい (>)

   * 疑問符 (?)

   * パーセント記号 (%)

7. **[OK]** を選択します。

   ::: moniker range="vs-2017"

   > [!NOTE]
   > アドイン プロジェクトを作成すると、必ず保存されます。 アドイン プロジェクトを一時プロジェクトとして作成することはできません。 一時プロジェクトの詳細については、「[一時プロジェクト](../ide/creating-solutions-and-projects.md#create-a-temporary-project)」を参照してください。

   ::: moniker-end

### <a name="to-create-a-document-level-customization-project"></a>ドキュメント レベルのカスタマイズ プロジェクトを作成するには

1. **[ファイル]** メニューで、 **[新規]**  >  **[プロジェクト]** の順にクリックします。 IDE が Visual Basic 開発設定を使用するように設定されている場合は、 **[ファイル]** メニューの **[新規作成]**  >  **[プロジェクト]** の順に選択します。

    **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

2. [テンプレート] ウィンドウで、使用する言語のノードの下にある **[Office/SharePoint]** を展開します。

3. **[Office アドイン]** ノードを選択します。

4. プロジェクト テンプレートの一覧で、ドキュメント レベルのプロジェクト テンプレートを選択します。 使用できるドキュメント レベルのプロジェクト テンプレートの一覧については、[Office プロジェクト テンプレートの概要](../vsto/office-project-templates-overview.md)に関するページを参照してください。

   > [!NOTE]
   > **[Office アドイン]** ノードを選択してもプロジェクト テンプレートが表示されない場合、 **[.NET Framework 4]** またはそれ以降が選択されていることを確認してください。

5. **[名前]** ボックスにプロジェクト名を入力します。 既定では、この名前がドキュメントにも使用されます。 IDE が Visual C# 開発設定または一般的な開発設定を使用するように設定されている場合は、場所とソリューション名も入力します。

   > [!NOTE]
   > プロジェクトの場所へのパス、またはプロジェクト名には、サロゲート文字を使用できません。 また、オフラインで使用するソリューションを配置する場合は、プロジェクト名に HTTP プロトコルの仕様に準拠した文字を使用する必要があります。

6. **[OK]** を選択します。

    **Visual Studio Tools for Office プロジェクト ウィザード** が開きます。

7. ソリューションのドキュメントを新規に作成する場合は、 **[新規ドキュメントの作成]** を選択します。既存のドキュメントをカスタマイズする場合は、 **[既存のドキュメントをコピーする]** を選択します。

    新しいドキュメントを作成する場合は、 **[名前]** ボックスに名前を指定し、 **[形式]** ボックスを使用してドキュメントの形式を選択します。 使用できる形式の詳細については、[ドキュメント レベルのカスタマイズのアーキテクチャ](../vsto/architecture-of-document-level-customizations.md)に関するページを参照してください。

    既存のドキュメントを使用する場合は、 **[既存のドキュメントの完全パス]** ボックスでドキュメントの場所を指定します。 使用できるパスは、絶対パスと UNC パスです。 ドキュメントへの HTTP パス、FTP パス、または他のプロトコル パスは使用しないでください。

    場所は、次の形式で指定します。

   - [*ドライブ*\]\:

   - \\\\*サーバー*\\*共有*

     次の文字は使用しないでください。

   - アスタリスク (*)

   - 縦棒 (|)

   - コロン (:) (ドライブ文字の後に使用する場合は除く)

   - 二重引用符 (") (スペースを含むパスには引用符は不要)

   - より小さい (\<)

   - より大きい (>)

   - 疑問符 (?)

   - パーセント記号 (%)

   > [!NOTE]
   > [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] プロジェクトで既存のドキュメントを使用する場合は、[!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] で作成したドキュメントか、この形式に変換したドキュメントだけを使用してください。 同様に、Word 2010 プロジェクトで既存のドキュメントを使用する場合は、Word 2010 で作成したドキュメントか、Word 2010 に変換したドキュメントだけを使用してください。 以前のバージョンの Word で作成した文書を使用すると、文書の一部の機能が使用できなくなります。 このような機能を使用するコードを記述しようとすると、プロジェクトでエラーが発生する可能性があります。 ドキュメントを変換するには、[!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] または Word 2010 でドキュメントを開き、リボンの **[ファイル]** タブで、 **[情報]**  >  **[変換]** の順に選択します。

8. **[完了]** を選択します。

9. 次の場合、Word のセキュリティ センターにある信頼できる場所の一覧に、プロジェクト フォルダーとそのサブフォルダーを追加します。

   - *.docm* ファイルに基づく Word ドキュメントを作成する、および Windows フォーム コントロールをホストする VBA プロジェクトを含むドキュメントを作成する。 プロジェクト フォルダーを信頼できる場所の一覧に追加すると、デザイン時に文書が期待どおりに動作するか確認するのに役立ちます。

   - *.dotx* ファイルに基づく Word テンプレート プロジェクトを作成する。 プロジェクトを実行およびデバッグできるようにするために、プロジェクト フォルダーを信頼できる場所の一覧に追加する必要があります。

     ドキュメントを信頼できる場所の一覧に追加する方法の詳細については、Microsoft Office Online Web サイトの「[ファイルに対して信頼できる場所を作成、削除、変更する](https://support.office.com/article/Create-remove-or-change-a-trusted-location-for-your-files-f5151879-25ea-4998-80a5-4208b3540a62)」を参照してください。

## <a name="see-also"></a>関連項目
- [Office プロジェクト テンプレートの概要](../vsto/office-project-templates-overview.md)
- [Office ソリューションの共同開発](../vsto/collaborative-development-of-office-solutions.md)
- [Office ソリューションを設計して作成する](../vsto/designing-and-creating-office-solutions.md)
- [VSTO アドインのプログラミングの概要](../vsto/getting-started-programming-vsto-add-ins.md)
