---
title: '方法: プライマリ相互運用機能アセンブリを利用して Office アプリケーションします。'
ms.date: 02/02/2017
ms.topic: conceptual
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
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4901a4a04a2d4702a365f9b1f65406c4537b1182
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56614325"
---
# <a name="how-to-target-office-applications-through-primary-interop-assemblies"></a>方法: プライマリ相互運用機能アセンブリを利用して Office アプリケーションします。
  新しい Office プロジェクトを作成すると、Visual Studio により、そのプロジェクトのビルドに必要な Microsoft Office プライマリ相互運用機能アセンブリ (PIA: Primary Interop Assembly) への参照が自動的に追加されます。 次の場合は、他の PIA への参照を追加する必要があります。

- プロジェクトで他の Microsoft Office アプリケーションの機能を使用する。 たとえば、Microsoft Office Word プロジェクトで Microsoft Office Excel の機能を使用することが必要になる場合があります。

- Microsoft Office Access など、Visual Studio に専用のプロジェクトがない Microsoft Office アプリケーションを自動化する。

  [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="to-add-a-reference-to-a-primary-interop-assembly"></a>プライマリ相互運用機能アセンブリに参照を追加するには

1.  Office プロジェクトを開きでプロジェクト名を選択します。**ソリューション エクスプ ローラー**します。

2.  **[プロジェクト]** メニューの **[参照の追加]** をクリックします。

3.  **Framework**タブで必要な PIA を選択、**コンポーネント名**一覧。 使用可能な Microsoft Office プライマリ相互運用機能アセンブリの詳細については、次を参照してください。 [Office プライマリ相互運用機能アセンブリ](../vsto/office-primary-interop-assemblies.md)します。

     場合、プロジェクトのターゲット、[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]またはそれ以降、 **Embed Interop Types**アセンブリ参照のプロパティに設定されて**True**既定では。 この設定を使用すると、ソリューションはエンド ユーザーのコンピューターに PIA を必要としません。 詳細については、[Office ソリューションのデザインと作成](../vsto/designing-and-creating-office-solutions.md)を参照してください。

    > [!NOTE]
    >  Office プロジェクトで使用して、常に Office Pia への参照を追加、 **.NET**のタブ、**参照の追加**ダイアログではなく、 **COM**タブ。詳細については、次を参照してください。 [Office プライマリ相互運用機能アセンブリ](../vsto/office-primary-interop-assemblies.md)します。

4.  **[OK]** をクリックします。

     アセンブリ名が表示されます、**参照**フォルダーの**ソリューション エクスプ ローラー**します。

## <a name="see-also"></a>関連項目
- [Office プライマリ相互運用機能アセンブリ](../vsto/office-primary-interop-assemblies.md)
- [Office ソリューションにおけるコードの記述](../vsto/writing-code-in-office-solutions.md)
- [Office ソリューションの開発](../vsto/developing-office-solutions.md)
- [方法: Office プライマリ相互運用機能アセンブリをインストールする方法](../vsto/how-to-install-office-primary-interop-assemblies.md)
