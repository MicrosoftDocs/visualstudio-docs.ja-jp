---
title: プライマリ相互運用機能アセンブリを使用して Office アプリを対象にする
description: Visual Studio を使用して、プログラムでプライマリ相互運用機能アセンブリを使用して Microsoft Office アプリケーションを対象にする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- assemblies [Office development in Visual Studio], PIA references
- primary interop assemblies [Office development in Visual Studio], adding references to
- Office primary interop assemblies in Visual Studio, adding references to
- Office applications [Office development in Visual Studio], automating
- application development [Office development in Visual Studio], automating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 11a0db0e23cf5512a6568ba5b66e0c18e563bd12
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99962380"
---
# <a name="how-to-target-office-applications-through-primary-interop-assemblies"></a>方法: プライマリ相互運用機能アセンブリを使用して Office アプリケーションを対象にする
  新しい Office プロジェクトを作成すると、Visual Studio により、そのプロジェクトのビルドに必要な Microsoft Office プライマリ相互運用機能アセンブリ (PIA: Primary Interop Assembly) への参照が自動的に追加されます。 次の場合は、他の PIA への参照を追加する必要があります。

- プロジェクトで他の Microsoft Office アプリケーションの機能を使用する。 たとえば、Microsoft Office Word プロジェクトで Microsoft Office Excel の機能を使用することが必要になる場合があります。

- Microsoft Office Access など、Visual Studio に専用のプロジェクトがない Microsoft Office アプリケーションを自動化する。

  [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="to-add-a-reference-to-a-primary-interop-assembly"></a>プライマリ相互運用機能アセンブリに参照を追加するには

1. Office プロジェクトを開き、**ソリューション エクスプローラー** でプロジェクト名を選択します。

2. **[プロジェクト]** メニューの **[参照の追加]** をクリックします。

3. **[Framework]** タブの **[コンポーネント名]** ボックスの一覧で、使用する PIA を選択します。 用意されている Microsoft Office プライマリ相互運用機能アセンブリの詳細については、「[Office プライマリ相互運用機能アセンブリ](../vsto/office-primary-interop-assemblies.md)」を参照してください。

     プロジェクトが [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降を対象としている場合は、アセンブリ参照の **[相互運用型の埋め込み]** プロパティが既定で **[True]** に設定されます。 この設定を使用すると、ソリューションはエンド ユーザーのコンピューターに PIA を必要としません。 詳細については、「[Office ソリューションの設計と作成](../vsto/designing-and-creating-office-solutions.md)」を参照してください。

    > [!NOTE]
    > Office プロジェクトでは、 **[COM]** タブではなく **[参照の追加]** ダイアログの **[.NET]** タブを使用して、常に Office PIA への参照を追加してください。詳細については、「[Office プライマリ相互運用機能アセンブリ](../vsto/office-primary-interop-assemblies.md)」を参照してください。

4. **[OK]** をクリックします。

     アセンブリ名が **ソリューション エクスプローラー** の **[参照設定]** フォルダーに表示されます。

## <a name="see-also"></a>関連項目
- [Office プライマリ相互運用機能アセンブリ](../vsto/office-primary-interop-assemblies.md)
- [Office ソリューションでコードを書く](../vsto/writing-code-in-office-solutions.md)
- [Office ソリューションを開発する](../vsto/developing-office-solutions.md)
- [方法: Office のプライマリ相互運用機能アセンブリをインストールする](../vsto/how-to-install-office-primary-interop-assemblies.md)
