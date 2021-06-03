---
title: Office ソリューションの構成情報を設定する
description: 構成ファイルを使用して、Microsoft Office ソリューションに固有の設定を構成する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- solutions [Office development in Visual Studio], configuration files
- configuration files [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: da3a08ad9b3f6c78a10891e7d8ef2093ab46305d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99927705"
---
# <a name="how-to-set-up-configuration-information-for-an-office-solution"></a>方法: Office ソリューションの構成情報を設定する
  構成ファイルを使用して、Office ソリューションに固有の設定を構成できます。 アセンブリ バインディング ポリシー、リモート処理オブジェクト、デバッグ、トレース設定などの設定を指定できます。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-add-a-configuration-file-to-your-office-project"></a>Office プロジェクトに構成ファイルを追加するには

1. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

2. **[カテゴリ]** ペインで **[全般]** をクリックします。

3. **[テンプレート]** ペインで **[アプリケーション構成ファイル]** を選択します。

4. **[名前]** ボックスに、アセンブリと同じ名前に拡張子 *.config* を付加して入力します。たとえば、*ExcelWorkbook1.dll* という名前の Excel プロジェクト アセンブリの構成ファイルには、*ExcelWorkbook1.dll.config* という名前を付けます。

5. **[追加]** をクリックします。

6. アプリケーション構成ファイルのスキーマに従って、構成ファイルを作成します。 詳細については、「[.NET Framework の構成ファイル スキーマ](/dotnet/framework/configure-apps/file-schema/index)」を参照してください。

   Office プロジェクトで構成ファイルを使用する場合、特別な考慮事項はありません。

## <a name="see-also"></a>関連項目
- [.NET Framework の構成ファイル スキーマ](/dotnet/framework/configure-apps/file-schema/index)
- [Office ソリューションを設計して作成する](../vsto/designing-and-creating-office-solutions.md)
- [Office ソリューションを配置する](../vsto/deploying-an-office-solution.md)
