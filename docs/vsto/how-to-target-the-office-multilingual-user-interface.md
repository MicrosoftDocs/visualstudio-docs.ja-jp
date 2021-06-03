---
title: '方法: Office 多言語ユーザー インターフェイスをターゲットとする'
description: Visual Studio を使用して、プログラムで Microsoft Office 多言語ユーザー インターフェイスをターゲットとする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- globalization [Office development in Visual Studio], user interface targeting
- MUI [Office development in Visual Studio]
- Office applications [Office development in Visual Studio], localization
- Multilingual User Interface [Office development in Visual Studio]
- localization [Office development in Visual Studio], user interface targeting
- Office applications [Office development in Visual Studio], globalization
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 3cf838b544ec78c8c7d6e9e2d6f1cb747e999ccd
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107823916"
---
# <a name="how-to-target-the-office-multilingual-user-interface"></a>方法: Office 多言語ユーザー インターフェイスをターゲットとする
  多言語ユーザー インターフェイス (MUI) は、エンド ユーザーがユーザー インターフェイス (UI) の言語を変更できるようにする Microsoft Office 機能です。 たとえば、英語の UI を操作しているエンド ユーザーが UI の言語をスペイン語に変更できます。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 アプリケーションが、Office の多くの言語を使用するユーザーによって使用される場合は、UI 文字列の言語を、そのユーザーのコンピューター上の Office によって使用されている言語に一致するように自動的に変更するコードを追加できます (ユーザーが適切なリソースをインストールしている場合)。

## <a name="to-check-the-current-office-ui-setting"></a>現在の Office UI 設定を確認するには

1. 現在のスレッドの <xref:System.Threading.Thread.CurrentUICulture%2A> プロパティを使用します。 UI 文字列の言語を、ユーザーのコンピューター上で現在実行されている Office のバージョンによって使用される言語に一致するように設定します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreCreatingExcelVB/Sheet1.vb" id="Snippet10":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreCreatingExcelCS/Sheet1.cs" id="Snippet10":::

## <a name="see-also"></a>関連項目
- [方法: プライマリ相互運用機能アセンブリを利用して Office アプリケーションを使用する](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md)
- [Office ソリューションの遅延バインディング](../vsto/late-binding-in-office-solutions.md)
