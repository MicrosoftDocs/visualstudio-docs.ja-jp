---
title: ワークフロー デザイナー - [型コレクション エディター] ダイアログ ボックス
description: '[型コレクション エディター] ダイアログ ボックスを使用して、Send および Receive アクティビティに既知の型を追加する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- TypeCollectionEditor.UI
ms.assetid: 63cdea6b-bca2-4c06-b8b4-c8faabd40726
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b8f194ee792f2a60df71a78af6f41e45aaac91da
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99875264"
---
# <a name="type-collection-editor-dialog-box"></a>[型コレクション エディター] ダイアログ ボックス

**[型コレクション エディター]** ダイアログ ボックスは、**Send** および **Receive** アクティビティに既知の型を追加するために使用します。 また、ジェネリック型の引数を **InvokeMethod** アクティビティに追加するためにも使用します。 **[型コレクション エディター]** ダイアログ ボックスを使用して、**Send** および **Receive** アクティビティに既知の型を追加する場合は、追加する型が一意であることが必要です。 重複する型を追加し、 **[OK]** をクリックして変更をコミットすると、エラー メッセージが返されます。 **[型コレクション エディター]** ダイアログ ボックスを使用して、ジェネリック型引数を **InvokeMethod** アクティビティに追加する場合は、重複する型を追加できます。

詳細については、「[既知のデータ コントラクト型](/dotnet/framework/wcf/feature-details/data-contract-known-types)」を参照してください。

**[型コレクション エディター]** ダイアログ ボックスのユーザー インターフェイス (UI) 要素を次の表に示します。

|UI 要素|説明|
|-|-----------------|
|**型リスト**|追加または削除された型のリスト。|

## <a name="to-bring-up-the-type-collection-editor-for-the-send-and-receive-activities"></a>Send アクティビティおよび Receive アクティビティの [型コレクション エディター] を表示するには

1. デザイン ビューで、**Send** または **Receive** アクティビティを選択します。

2. **F4** キーを押して、 **[プロパティ]** ウィンドウを表示します。

3. **[プロパティ]** ウィンドウで、**KnownTypes** プロパティの横にある省略記号ボタンをクリックします。

## <a name="to-bring-up-the-type-collection-editor-for-the-invokemethod-activity"></a>InvokeMethod アクティビティの [型コレクション エディター] を表示するには

1. デザイン ビューで、**InvokeMethod** アクティビティを選択します。

2. **F4** キーを押して、 **[プロパティ]** ウィンドウを表示します。

3. **[プロパティ]** ウィンドウで、**GenericTypeArguments** プロパティの横にある省略記号ボタンをクリックします。
