---
title: ブックに読み込むことができない ActiveX コントロールが含まれている
description: ブックに読み込むことができない ActiveX コントロールが含まれている場合に発生するエラーを解決する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: error-reference
f1_keywords:
- VST.SelectDocWizard.ContainsActiveXControls
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 4c8039fc2a5df197446873f0b2efef82d9a5f662
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99940788"
---
# <a name="the-workbook-contains-activex-controls-that-cannot-be-loaded"></a>ブックに読み込むことができない ActiveX コントロールが含まれている

  Word 文書または Excel ワークシートにコントロールをプログラムを使用して追加し、そのドキュメントまたはブックを保存して、そのドキュメントまたはブックに基づいて新しいドキュメントレベルのソリューションを作成すると、"このプロジェクトの作成に使用されるブックには、デザイナーで読み込めない ActiveX コントロールが含まれています" というエラーが表示されます。

 コントロールのマネージド型を記述した情報は、文書またはブックと共に保存されません。 このような文書またはブックに基づいて新しいソリューションを作成すると、コントロールをホスト項目デザイナーに読み込むのに必要な情報が Visual Studio に提供されません。

## <a name="to-correct-this-error"></a>このエラーを解決するには

1. 文書またはブックを開きます。

2. 実行時に追加されたコントロールを削除します。 この操作は、文書またはブックでそれらを選択し、**Delete** キーを押すことで実行できます。

3. 文書またはブックに基づいたドキュメント レベルのソリューションを作成します。

## <a name="see-also"></a>関連項目
- [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)
