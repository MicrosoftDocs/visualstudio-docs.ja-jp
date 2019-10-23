---
title: '[ルールセットエディター] ダイアログボックス (レガシ) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Workflow.Activities.Rules.Design.RuleSetDialog.UI
helpviewer_keywords:
- Rule Set Editor dialog box
ms.assetid: 7cfd5df1-1115-4e5c-9b72-121f39419e83
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ce9e18a832ceceebc56e294023bc4ae3d06101cc
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72663336"
---
# <a name="rule-set-editor-dialog-box-legacy"></a>[ルール セット エディター] ダイアログ ボックス (レガシ)
このトピックでは、従来の [!INCLUDE[wfd1](../includes/wfd1-md.md)] の **[ルールセットエディター]** ダイアログボックスの使用方法について説明します。 [!INCLUDE[wfd2](../includes/wfd2-md.md)] または [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] を対象とする必要がある場合は、従来の[!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]を使用します。

 **[ルールセットエディター]** ダイアログボックスは、規則ファイルにシリアル化される[policyactivity](http://go.microsoft.com/fwlink?LinkID=65019)規則セットを作成および変更するために使用されます。

> [!NOTE]
> **エンコード付きの XML エディター**で. rules ファイルを開く場合は、まず、ワークフローまたはアクティビティに関連付けられているデザイナーウィンドウを閉じる必要があります。

 **[ルールセットエディター]** ダイアログボックスにアクセスする方法の詳細については、「[方法: Policyactivity ルールセットを作成する (レガシ)](../workflow-designer/how-to-create-a-policyactivity-rule-set-legacy.md)」を参照してください。

> [!WARNING]
> [!INCLUDE[wfd2](../includes/wfd2-md.md)] または [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] を対象とする場合に使用される、従来の[!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]のルール エディターは、複数バージョン対応機能をサポートしていません。

 次の表では、 **[ルールセットエディター]** ダイアログボックスのユーザーインターフェイス (UI) 要素について説明します。

|UI 要素|説明|
|----------------|-----------------|
|**ルールの追加**|新しいルール定義をルール セットに追加します。|
|**削除**|選択したルールをルール セットから削除します。|
|**継承**|ルール セットで使用するフォワード チェーンの種類を指定します。 使用可能なオプションは次のとおりです。<br /><br /> -   **完全なチェーン**では、すべてのフォワードチェーン機構 (暗黙的、メソッド属性、および**更新**関数を使用した明示) を使用することを指定します。<br />-   **シーケンシャル**。前方チェーンを使用しないことを指定します。<br />-   **明示的な更新のみ**を実行します。これは、**更新**アクションに対してのみフォワードチェーンを実行することを指定します。<br /><br /> フォワードチェーンの詳細については、「 [Policyactivity アクティビティの使用](http://go.microsoft.com/fwlink?LinkID=65004)」を参照してください。|
|**Name**|ルール セット リストの列見出しです。 ルール リストを名前で並べ替えるには、これをクリックします。|
|**的**|ルール セット リストの列見出しです。 ルール リストを優先度で並べ替えるには、これをクリックします。|
|**再**|ルール セット リストの列見出しです。 ルール リストを再評価タイプで並べ替えるには、これをクリックします。|
|**ルールのプレビュー**|ルール セット リストの列見出しです。 ルールの条件とアクションのプレビューでルール リストを並べ替えるには、これをクリックします。|
|**Name:**|ルールの名前を入力します。|
|**的**|ルールの優先度を入力します。 既定の優先順位は 0 です。|
|**再**|ルールで使用するルール再評価の種類を指定します。 使用可能なオプションは次のとおりです。<br /><br /> -   **常**に、必要に応じてルールが再評価されます。<br />-    し**ない**でください。これにより、ルールは再評価されません。 この場合、ルールは一度だけ実行されます。|
|**Active**|これをオンにすると、ルールはアクティブになります。|
|**フィルター**|ルールの条件式を入力します。 式の構文の詳細については、このページの「条件式とアクション式の入力」の項を参照してください。|
|**その後、次の操作を実行します。**|Then アクションの式を入力します。 式の構文の詳細については、このページの「条件式とアクション式の入力」の項を参照してください。|
|**Else アクション:**|Else アクションの式を入力します。 式の構文の詳細については、このページの「条件式とアクション式の入力」の項を参照してください。|
|**わかりました**|これをクリックすると、ルール セットが .rules ファイルに保存されます。|

 規則セットの詳細については、「 [Policyactivity アクティビティの使用](http://go.microsoft.com/fwlink?LinkID=65004)」を参照してください。

## <a name="entering-condition-and-action-expressions"></a>条件式とアクション式の入力
 条件の式を入力し、 **[ルールセットエディター]** ダイアログボックスの各テキストボックスにテキストとして「Then」および「Else」アクションを入力します。 これは、「」と入力することができ**ます。** エディターを使用して、ワークフローで使用されるフィールド、プロパティ、およびメソッドを、IntelliSense の種類のメニューで参照できます。 または、ワークフローのメンバ名を直接入力することもできます。 クラス名とそれに続いてメソッド名を入力することにより、参照された型で静的メソッドを呼び出すことができます。

 条件には、AND、OR、NOT といった論理演算子を追加することもできます。 述語も追加できます。 述語は、バイナリ演算子と 2 つのオペランドから成ります。 サポートされているバイナリ演算子は、= =、>、\<、> =、および < = です。 サポートされているオペランドは、定数値、算術関数、スコープ付きパブリック メンバです。

 比較の種類を指定して、 **null**または空の文字列と比較することができます。 複合型を含む変数でメンバに対する呼び出しをネストすることができます (たとえば `this.Address.State == "WA"`)。

 式では、次の演算子がサポートされます。

- 関係演算子 : ==、=、!=

- 比較演算子: <、\< =、>、> =

- 算術演算子 : +、-、*、/、MOD

- 論理演算子: AND、& &、OR &#124; &#124;、、NOT、!

- ビットごとの演算子: &、&#124;

  式演算子の優先順位は、C# 演算子の優先順位規則に従います。

  条件の詳細については、「[ワークフローでの条件の使用](https://msdn.microsoft.com/541211f5-d382-4810-894f-71f00b34fa77)」を参照してください。

### <a name="halt-and-update-functions"></a>Halt 関数と Update 関数
 **Then actions:** および**Else アクション: 式は**、 **Halt**関数と**Update**関数をサポートしています。 **Halt**関数を使用するには、「 **Halt** in a **Then action:** or **Else action:** テキストボックス」と入力します。 **Halt**アクションを実行すると、ルールセットの実行がすぐに停止し、呼び出し元のコードに制御が戻ります。 前方チェーンで**Update**関数を使用します。

 **Update**ステートメントは、次の2つの形式のいずれかでエディターで表現できます。次の例では、両方の形式を示しています。

```
Update(this.Address.State)
Update("this/Address/State")
```

 フォワードチェーンで**Update**を使用する方法の詳細については、「 [policyactivity アクティビティの使用](http://go.microsoft.com/fwlink?LinkID=65004)」を参照してください。

## <a name="see-also"></a>参照
 [Policyactivity](http://go.microsoft.com/fwlink?LinkID=65019) [[ルールセットの選択] ダイアログボックス (レガシ)](../workflow-designer/select-rule-set-dialog-box-legacy.md) [ワークフロー内の条件を使用](http://go.microsoft.com/fwlink?LinkID=65009)し[た policyactivity アクティビティの使用](http://go.microsoft.com/fwlink?LinkID=65004)