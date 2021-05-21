---
title: '[.NET 型の参照と選択] ダイアログ ボックス'
description: '[.NET 型の参照と選択] ダイアログ ボックスを使用して、ワークフロー デザイナーのアセンブリおよびプロジェクトのツリー ビューから型を選択する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- TypeBrowser.UI
- ActivityTypeResolver.UI
ms.assetid: 864b60b6-a070-4e5c-aa5b-a25341b57ea6
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: f0a7ffb9e100a621019a5d0ced855575a05708ea
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99875303"
---
# <a name="browse-and-select-a-net-type-dialog-box"></a>[.NET 型の参照と選択] ダイアログ ボックス

**[プロパティ]** ウィンドウ、ダイアログ ボックス、または変数デザイナーなどのデザイナーで、データ型の一覧から **[型の参照]** を選択すると、 **[.NET 型の参照と選択]** ダイアログ ボックス (省略して "型ブラウザー" と呼ばれます) が開きます。 このダイアログ ボックスでは、アセンブリとプロジェクトのツリー表示から型を選択できます。

このダイアログ ボックスは、次のようなさまざなユーザー シナリオで使用されます。

- 変数または引数の型を設定する。

- 一般的なアクティビティの型を選択する。

- <xref:System.Activities.Statements.TryCatch> アクティビティに catch を追加する。

> [!NOTE]
> 型ブラウザーは、多次元配列型ではなく Visual Basic ジャグ配列型を表示できます。 詳細については、[ジャグ配列](/previous-versions/visualstudio/visual-studio-2008/hkhhsz9t(v=vs.90))および[多次元配列](/previous-versions/visualstudio/visual-studio-2008/d2de1t93(v=vs.90))に関する記事を参照してください。

## <a name="selecting-a-value-or-reference-type-from-the-type-browser"></a>型ブラウザーでの値型または参照型の選択

### <a name="to-select-a-value-or-reference-type-from-the-type-browser"></a>型ブラウザーで値型または参照型を選択するには

1. **[型名]** ボックスに、使用する型の名前を入力します。

2. 次のいずれかの操作を行います。

    - 使用する型の名前が **[型名]** ボックスのツリーに表示されたら、その型をダブルクリックして選択します。

    - **[型名]** ボックスに、使用する型を一意に識別できるだけの文字を入力してから、Enter キーを押して、その型を選択します

### <a name="to-select-a-generic-type-from-the-type-browser"></a>型ブラウザーでジェネリック型を選択するには

1. **[型名]** ボックスに、使用する型の名前を入力します。

2. 使用する型の名前が **[型名]** ボックスのツリーに表示されたら、その型をダブルクリックして選択します。この操作により、ドロップダウン ボックスが表示されます。

     ジェネリック型を閉じるために使用する型をドロップダウン ボックスから選択し、 **[OK]** をクリックします。

## <a name="types-displayed-in-the-type-browser"></a>型ブラウザーに表示される型

型ブラウザーに表示される型は、型ブラウザーを起動した方法に応じて変わる場合があります。 **vs2010** 内のワークフロー プロジェクトから型ブラウザーを起動した場合、既定では、参照アセンブリおよび参照プロジェクトのすべての型が表示されます。 **vs2010** プロジェクト システムの外部 (再ホストされたワークフロー アプリケーション、スタンドアロンのワークフロー ファイルなど) から型ブラウザーを起動した場合、既定では、AppDomain に読み込まれているすべてのアセンブリの型が表示されます。

アクティビティ デザイナーの開発者は、型ブラウザーの型をフィルター処理できます。 どのアクティビティでも、表示されるのは型のサブセットのみです。 たとえば、<xref:System.Activities.Statements.TryCatch> アクティビティでは、<xref:System.Exception> から派生した型のみが型ブラウザーに表示されます。

## <a name="filtering-search-results-in-the-type-browser"></a>型ブラウザーでの検索結果のフィルター処理

**[型名]** ボックスの型の一覧は、検索する文字を入力した分だけ短くなります。 フィルター処理された一覧には、入力した文字列で完全修飾名が始まる型、または、入力した文字列で始まる短い名前を持つ型のみが表示されます。

次に例を示します。

1. 「**Operation**」と入力すると、<xref:System.OperationCanceledException> とは一致しますが、<xref:System.InvalidOperationException> とは一致しません。 <xref:System.InvalidOperationException> と一致するためには、「System.I」または「Invalid」と入力します。

2. 「**Generic**」と入力すると、<xref:System.GenericUriParser> とは一致しますが、<xref:System.Collections.Generic> 名前空間の型とは一致しません。 <xref:System.Collections.Generic> 名前空間の型を検索するには、その名前空間の完全修飾名を入力します。

## <a name="selecting-a-service-contract-using-the-type-browser-dialog"></a>型ブラウザー ダイアログを使用したサービス コントラクトの選択

サービス コントラクト型を選択すると、型ブラウザーは <xref:System.ServiceModel.ServiceContractAttribute> 属性を持つ型だけを表示します。

## <a name="see-also"></a>関連項目

- [アクティビティ デザイナーの使用](control-flow-activity-designers.md)
