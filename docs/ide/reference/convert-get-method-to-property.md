---
title: Get メソッドのプロパティへの変換、およびプロパティの Get メソッドへの変換
ms.date: 01/26/2018
ms.prod: visual-studio-dev15
ms.topic: reference
ms.devlang: csharp
author: gewarren
ms.author: gewarren
manager: douge
f1_keywords:
- vs.csharp.refactoring.convertmethodtoproperty
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 0af901ed6a51b962b7b2999b04909136bbb0f3e9
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2019
ms.locfileid: "53861148"
---
# <a name="convert-get-method-to-property--convert-property-to-get-method-refactorings"></a>Get メソッドのプロパティへの変換/プロパティの Get メソッドへの変換リファクタリング

これらのリファクタリングは以下に適用されます。

- C#

## <a name="convert-get-method-to-property"></a>Get メソッドのプロパティへの変換

**機能:** Get メソッド (必要に応じて Set メソッド) をプロパティに変換できます。

**条件:** ロジックを含まない Get メソッドがあるとき。

### <a name="how-to"></a>方法

1. Get メソッド名にカーソルを置きます。

1. 次に、以下のいずれかを実行します。

   - **キーボード**
      - 行の任意の場所で **Ctrl**+**.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーし、[プレビュー] ウィンドウ ポップアップから **[Replace method with property]\(メソッドをプロパティに置換\)** を選択します。
   - **マウス**
      - コードを右クリックして **[クイック アクションとリファクタリング]** メニューを選択し、[プレビュー] ウィンドウ ポップアップから **[Replace method with property]\(メソッドをプロパティに置換\)** を選択します。

1. (省略可能) Set メソッドがある場合、このときに **[Replace Get method and Set method with property]\(Get メソッドと Set メソッドをプロパティに置換\)** を選択して Set メソッドも変換できます。

1. コード プレビューで変更を確認したら、**Enter** キーを押すか、メニューから [修正] をクリックすると、変更がコミットされます。

例:

```csharp
private int MyValue;

// Before
public int GetMyValue()
{
    return MyValue;
}

// Replace 'GetMyValue' with property

// After
public int MyValue
{
    get { return MyValue; }
}
```

## <a name="convert-property-to-get-method"></a>プロパティの Get メソッドへの変換

**機能:** プロパティを Get メソッドに変換できます。

**条件:** 値の設定や取得をするだけではないプロパティがあるとき。

### <a name="how-to"></a>方法

1. Get メソッド名にカーソルを置きます。

1. 次に、以下のいずれかを実行します。

   - **キーボード**
      - 行の任意の場所で **Ctrl**+**.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーし、[プレビュー] ウィンドウ ポップアップから **[Replace property with method]\(プロパティをメソッドに置換\)** を選択します。
   - **マウス**
      - コードを右クリックして **[クイック アクションとリファクタリング]** メニューを選択し、[プレビュー] ウィンドウ ポップアップから **[Replace property with methods]\(プロパティをメソッドに置換\)** を選択します。

1. コード プレビューで変更を確認したら、**Enter** キーを押すか、メニューから [修正] をクリックすると、変更がコミットされます。

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
- [変更のプレビュー](../../ide/preview-changes.md)