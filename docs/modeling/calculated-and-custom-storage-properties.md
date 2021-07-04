---
title: 計算プロパティおよびカスタム格納プロパティ
description: ドメイン固有言語 (DSL) のすべてのドメイン プロパティをダイアグラム上と言語エクスプローラー内でユーザーに表示する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, programming domain properties
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f98dca6759b9e4a77e71139b6d9ec9b394d99b04
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112385423"
---
# <a name="calculated-and-custom-storage-properties"></a>計算プロパティおよびカスタム格納プロパティ
ドメイン固有言語 (DSL) のすべてのドメイン プロパティをダイアグラム上と言語エクスプローラー内でユーザーに表示して、プログラム コードでアクセスすることができます。 ただし、プロパティの値が格納される方法は異なります。

## <a name="kinds-of-domain-properties"></a>ドメイン プロパティの種類
 DSL 定義では、次の表に示すように、ドメイン プロパティの **種類** を設定できます。

|ドメイン プロパティの種類|説明|
|-|-|
|**標準** (既定)|*ストア* に保存され、ファイルにシリアル化されるドメイン プロパティ。|
|**Calculated**|ストアに保存されていないが、他の値から計算される読み取り専用のドメイン プロパティ。<br /><br /> たとえば、`Person.Age` は `Person.BirthDate` から計算できます。<br /><br /> 計算を実行するコードを指定する必要があります。 通常は、他のドメイン プロパティから値を計算します。 ただし、外部リソースを使用することもできます。|
|**カスタム ストレージ**|ストアに直接保存されるのではなく、get と set の両方にすることができるドメイン プロパティ。<br /><br /> 値を取得および設定するメソッドを指定する必要があります。<br /><br /> たとえば、`Person.FullAddress` は、`Person.StreetAddress`、`Person.City`、`Person.PostalCode` に格納できます。<br /><br /> たとえばデータベースから値を取得して設定するために、外部リソースにアクセスすることもできます。<br /><br /> `Store.InUndoRedoOrRollback` が true の場合、コードでストアの値を設定することはできません。 「[トランザクションとカスタム Setter](#setters)」を参照してください。|

## <a name="providing-the-code-for-a-calculated-or-custom-storage-property"></a>計算済みまたはカスタム ストレージのプロパティのコードを指定
 ドメイン プロパティの [種類] を [計算済み] または [カスタム ストレージ] に設定する場合は、アクセス方法を指定する必要があります。 ソリューションをビルドすると、必要なものがエラー レポートに表示されます。

#### <a name="to-define-a-calculated-or-custom-storage-property"></a>計算済みまたはカスタム ストレージのプロパティを定義するには

1. DslDefinition.dsl で、ダイアグラムまたは **DSL エクスプローラー** のいずれかでドメイン プロパティを選択します。

2. **[プロパティ]** ウィンドウで、 **[種類]** フィールドを **[計算済み]** または **[カスタム ストレージ]** に設定します。

     また、その **[タイプ]** が必要なものに設定されていることも確認します。

3. **ソリューション エクスプローラー** のツール バーで、 **[すべてのテンプレートの変換]** をクリックします。

4. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

     次のエラー メッセージが表示されます。"*YourClass* に Get *YourProperty* の定義が含まれていません。"

5. エラー メッセージをダブルクリックします。

     Dsl\GeneratedCode\DomainClasses.cs または DomainRelationships.cs が開きます。 強調表示されたメソッド呼び出しの上に、Get *YourProperty*() の実装の指定を要求するコメントが表示されます。

    > [!NOTE]
    > このファイルは、DslDefinition.dsl から生成されます。 このファイルを編集すると、次回 **[すべてのテンプレートの変換]** をクリックしたときに変更内容が失われます。 代わりに、必要なメソッドを別のファイルに追加します。

6. クラス ファイルを作成するか、別のフォルダーで開きます (たとえば、CustomCode\\*YourDomainClass*.cs)。

     名前空間が生成済みのコードと同じであることを確認します。

7. クラス ファイルで、ドメイン クラスの部分実装を記述します。 クラスに、次の例のように、見つからない `Get` メソッドの定義を記述します。

    ```
    namespace Company.FamilyTree
    {  public partial class Person
       {  int GetAgeValue()
          { return System.DateTime.Today.Year - this.BirthYear; }
    }  }
    ```

8. **[種類]** を **[カスタム ストレージ]** に設定した場合は、`Set` メソッドも指定する必要があります。 次に例を示します。

    ```
    void SetAgeValue(int value)
    { if (!Store.InUndoRedoOrRollback)
        this.BirthYear =
            System.DateTime.Today.Year - value; }
    ```

     `Store.InUndoRedoOrRollback` が true の場合、コードでストアの値を設定することはできません。 「[トランザクションとカスタム Setter](#setters)」を参照してください。

9. ソリューションをビルドして実行します。

10. プロパティをテストします。 **Undo** と **Redo** を試行するようにしてください。

## <a name="transactions-and-custom-setters"></a><a name="setters"></a> トランザクションとカスタム Setter
 メソッドは通常、アクティブなトランザクションの内部で呼び出されるので、カスタム ストレージのプロパティの Set メソッドでは、トランザクションを開く必要はありません。

 ただし、ユーザーが Undo または Redo を呼び出した場合、またはトランザクションがロールバックされている場合にも、Set メソッドを呼び出すことができます。 <xref:Microsoft.VisualStudio.Modeling.Store.InUndoRedoOrRollback%2A> が true の場合、Set メソッドは次のように動作します。

- 他のドメイン プロパティに値を割り当てるなど、ストアに変更を加えることはできません。 これらの値は、アンドゥ マネージャーによって設定されます。

- ただし、データベースやファイルの内容などの外部リソースや、ストアの外部にあるオブジェクトを更新する必要があります。 これにより、ストア内の値との同期状態が維持されます。

  次に例を示します。

```
void SetAgeValue(int value)
{
  // If we are in Undo, no changes to Store objects:
  if (!this.Store.InUndoRedoOrRollback)
  {
    this.BirthYear = System.DateTime.Today.Year - value;
  }
  // But always update external objects:
  System.IO.File.WriteAllText(AgeFile, value);
}
```

 トランザクションの詳細については、「[プログラム コードにおけるモデル内の移動およびモデルの更新](../modeling/navigating-and-updating-a-model-in-program-code.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [プログラム コードにおけるモデル内の移動およびモデルの更新](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [ドメイン プロパティのプロパティ](../modeling/properties-of-domain-properties.md)
- [方法: ドメイン固有言語を定義する](../modeling/how-to-define-a-domain-specific-language.md)
