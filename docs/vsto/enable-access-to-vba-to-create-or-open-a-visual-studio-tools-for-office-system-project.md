---
title: VSTO システム プロジェクトを作成または開くための VBA へのアクセス
titleSuffix: ''
description: Visual Studio Tools for Office システム プロジェクトを作成または開く前に、Office VBA プロジェクト システムへのアクセスを明示的に有効にする必要があることについて説明します。
ms.custom: seodec18, SEO-VS-2020
ms.date: 08/14/2019
ms.topic: conceptual
f1_keywords:
- vst.project.vbawrongversion
- VST.Project.VBASecurityGenericError
- VST.Project.VBASecurityPermissions
- VST.SelectDocWizard.MissingCOM
- VST.Project.VBASecurityNotSet
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: ef68ffccd7a048cd0591ee0bf1aa511fe0489c92
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99910517"
---
# <a name="enable-access-to-vba-to-create-or-open-a-visual-studio-tools-for-the-microsoft-office-system-project"></a>Visual Studio Tools for the Microsoft Office システム プロジェクトを作成するか開くために VBA へのアクセスを有効にする

Visual Studio Tools for the Microsoft Office システム プロジェクトを作成または開く前に、Microsoft Office の Visual Basic for Applications (VBA) プロジェクト システムへのアクセスを明示的に有効にする必要があります。

 Office 開発プロジェクトでは、プロジェクトで Visual Basic for Applications を使用しない場合でも、Microsoft Office Word と Microsoft Office Excel の Visual Basic for Applications (VBA) プロジェクト システムにアクセスする必要があります。 Visual Basic プロジェクトと C# プロジェクトでは、デザイン時にコントロールをサポートするために Visual Basic for Applications プロジェクト システムを使用します。

 一部の Microsoft Office マクロ ウイルスは、ウイルス感染を広げる手段として Visual Basic for Applications プロジェクト システムを自動化しようとします。 Visual Basic for Applications プロジェクト システムへのアクセスを許可すると、マクロ ウイルスの感染防止に有効な保護手段が削除されます。 ただし、通常のマクロ セキュリティは有効なままであるため、コンピューターでマクロを実行するかどうかは、Office アプリケーションで保持されているマクロ セキュリティ レベルおよび信頼される発行者のリストによって決まります。

> [!NOTE]
> これは開発用のコンピューターにのみ適用されます。 エンド ユーザーのコンピューターでは、Office ソリューションを実行するためにこのオプションを有効にする必要はありません。

 Visual Basic for Applications プロジェクト システムへのアクセスを禁止してもウイルスから保護されないことに注意してください。コンピューターがそれ以前に一部のマクロ ウイルスに感染していた場合にも、他の文書へのウイルス感染の防止に役立つだけです。 コンピューターに保護層を追加するこのオプションは、既定では無効になっていますが、セキュリティに関する以下のベスト プラクティスに従えば、このオプションを有効にしてもコンピューターがウイルスに感染しやすくなることはありません。

 Office のマクロ ウイルスに対する最善の保護対策は、セキュリティ レベルを [高] または [最高] に設定して Office を実行し、検証済みの既知のソースのマクロのみを信頼し、常にセキュリティ パッチとウイルス検出プログラムを最新にしておくことです。

 **[Visual Basic プロジェクトへのアクセスを信頼する]** オプションは手動で有効または無効にできます。

 VBA エラーまたは COM エラーが表示される場合、Office のインストールを修復できます。

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="to-enable-or-disable-access-to-visual-basic-projects"></a>Visual Basic プロジェクトへのアクセスを有効または無効にするには

1. **[ファイル]** タブをクリックします。

2. **[オプション]** をクリックします。

3. **[トラスト センター]** をクリックし、 **[トラスト センターの設定]** をクリックします。

4. **トラスト センター** で、 **[マクロの設定]** をクリックします。

5. **[VBA プロジェクト オブジェクト モデルへのアクセスを信頼する]** をオンまたはオフにして、Visual Basic プロジェクトへのアクセスを有効または無効にします。

6. **[OK]** をクリックします。

### <a name="to-enable-or-disable-access-to-visual-basic-projects-with-the-2007-microsoft-office-system"></a>2007 Microsoft Office システムで Visual Basic プロジェクトへのアクセスを有効または無効にするには

1. Word または Excel の **[ツール]** メニューで **[マクロ]** をポイントし、 **[セキュリティ]** をクリックします。

2. **[セキュリティ]** ダイアログ ボックスで **[信頼できる発行元]** タブをクリックします。

3. **[Visual Basic プロジェクトへのアクセスを信頼する]** を有効にするにはオンにし、無効にするにはオフにします。

4. **[OK]** をクリックします。

## <a name="to-set-your-office-macro-security-level"></a>Office マクロのセキュリティ レベルを設定するには

1. **[ファイル]** タブをクリックします。

2. **[オプション]** をクリックします。

3. **[トラスト センター]** をクリックし、 **[トラスト センターの設定]** をクリックします。

4. **トラスト センター** で、 **[マクロの設定]** をクリックします。

5. **[マクロの設定]** セクションで、目的の設定を選択します。

6. **[OK]** をクリックします。

### <a name="to-set-your-office-macro-security-level-with-the-2007-microsoft-office-system"></a>2007 Microsoft Office システムで Office マクロのセキュリティ レベルを設定するには

1. Word または Excel の **[ツール]** メニューで **[マクロ]** をポイントし、 **[セキュリティ]** をクリックします。

2. **[セキュリティ レベル]** タブで、必要な設定を選択します。

    **[セキュリティ レベル]** タブには、各レベルの詳細な設定が含まれています。 詳細については、Office ヘルプの「マクロのセキュリティ レベル」を参照してください。

### <a name="to-install-vba-with-the-2007-microsoft-office-system"></a>2007 Microsoft Office システムとともに VBA をインストールするには

1. コントロール パネルで、 **[プログラムの追加と削除]** または **[プログラムと機能]** を実行します。

2. **[現在インストールされているプログラム]** リストで [Office] を選択します。

3. **[変更]** をクリックします。

4. **[機能の追加または削除]** を選択して **[続行]** をクリックします。

5. **[アプリケーションごとにオプションを指定してインストール]** を選択し、 **[次へ]** をクリックします。

6. **[アプリケーションおよびツールの更新オプションの選択]** リストの **[Office 共有機能]** を展開します。

7. **[Visual Basic for Applications]** の横にあるドロップダウン メニューを開き、 **[マイ コンピューターから実行]** をクリックします。

8. **[Continue]** をクリックします。

9. **[閉じる]** をクリックします。

## <a name="to-repair-your-installation-of-office"></a>Office のインストールを修復するには

1. コントロール パネルで、 **[プログラムの追加と削除]** または **[プログラムと機能]** を実行します。

2. **[現在インストールされているプログラム]** リストで、Office の使用しているバージョンを選択します。

3. **[変更]** をクリックします。

4. **[再インストール/修復]** を選択し、 **[次へ]** をクリックします。

5. **[Office のインストールで発生したエラーを検出して修復する]** を選択して **[インストール]** をクリックします。

## <a name="see-also"></a>こちらもご覧ください
- [Office ソリューションをセキュリティで保護する](../vsto/securing-office-solutions.md)
