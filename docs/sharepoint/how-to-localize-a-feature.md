---
title: '方法: フィーチャーをローカライズする | Microsoft Docs'
description: ハードコーディングされた文字列値を、ローカライズされたリソースを参照する式に置き換えることにより、SharePoint で フィーチャーのタイトルと説明をローカライズする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- features [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, localizing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 4a3c427f207f6aac9f6a827eb6c24b799d635b46
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99913601"
---
# <a name="how-to-localize-a-feature"></a>方法: フィーチャーをローカライズする
  既定では、フィーチャーのタイトルと説明はハードコーディングされた文字列値を使用します。 フィーチャーのタイトルと説明をローカライズするには、文字列を、ローカライズされたリソースを参照する式に置き換えます。

## <a name="localize-a-feature"></a>フィーチャーをローカライズする

#### <a name="to-localize-a-feature"></a>フィーチャーをローカライズするには

1. **ソリューション エクスプローラー** で、 **[Feature1]** ノードのショートカット メニューを開き、 **[フィーチャー リソースの追加]** を選択します。

2. **[リソースの追加]** ダイアログ ボックスで、既定の言語フィーチャー リソース ファイルのカルチャとして、一覧から **[インバリアント言語]** を選択します。

3. ローカライズされた言語ごとに前の手順を繰り返して、ローカライズされたフィーチャー リソース ファイルに対して必要な言語を選択します。

     個別のフィーチャー リソース ファイルが作成されます。1 つは既定の言語用で、もう 1 つはサポートするローカライズ言語用です。

4. リソース エディターで各リソース ファイルを開き、すべての文字列 ID とその値を入力します。

     たとえば、既定のフィーチャー リソース ファイルでは、 **[Title]** の文字列 ID に「**フィーチャーのタイトル**」という値、2 番目に **[Description]** の文字列 ID に「**フィーチャーの説明**」という値を入力します。 ローカライズされたリソース ファイルごとに、既定のフィーチャー リソースで使用されているのと同じ文字列 ID を使用しますが、値にはローカライズされた文字列を入力します。

5. すべてのリソース値を入力したら、フィーチャーのショートカット メニュー (*Feature1.feature* など) を開き、 **[デザイナーの表示]** を選択してフィーチャー デザイナーでフィーチャーを開きます。

6. フィーチャーの **[タイトル]** と **[説明]** フィールドをローカライズするには、次の書式を使用してボックスに値を入力します。

     `$Resources:` *文字列 ID*

     たとえば、 **[フィーチャーのタイトル**] ボックスに「$Resources:**Title**」と入力し、 **[フィーチャーの説明]** ボックスに「$Resources:**Description**」を入力します。

     文字列 ID は、リソース ファイルで使用されているものと一致している必要があります。

7. **F5** キーを押してアプリケーションをビルドし、実行します。

8. SharePoint で、 **[サイトの操作]** メニューを開き、 **[サイトの設定]** を選択します。次に、 **[サイトの操作]** セクションで、 **[サイトのフィーチャーの管理]** リンクを選択します。

9. SharePoint で、表示言語を既定の言語から変更します。

     ローカライズされたフィーチャーのタイトルと説明がアプリケーションに表示されます。 ローカライズされたリソースを表示するには、リソース ファイルのカルチャに対応する Language Pack が SharePoint サーバーにインストールされている必要があります。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションをローカライズする](../sharepoint/localizing-sharepoint-solutions.md)
- [方法: リソース ファイルを追加する](../sharepoint/how-to-add-a-resource-file.md)
- [方法: ASPX マークアップをローカライズする](../sharepoint/how-to-localize-aspx-markup.md)
- [方法: コードをローカライズする](../sharepoint/how-to-localize-code.md)
