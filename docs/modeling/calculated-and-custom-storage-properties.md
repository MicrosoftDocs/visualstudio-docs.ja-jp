---
title: 計算プロパティおよびカスタム格納プロパティ
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, programming domain properties
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: def432c5c2861716b4b3fb6e2f93f20a93a54a28
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72748540"
---
# <a name="calculated-and-custom-storage-properties"></a>計算プロパティおよびカスタム格納プロパティ
ドメイン固有言語 (DSL) 内のすべてのドメインプロパティは、図および言語エクスプローラーでユーザーに表示できます。また、プログラムコードからアクセスすることもできます。 ただし、プロパティの値が格納される方法は異なります。

## <a name="kinds-of-domain-properties"></a>ドメインプロパティの種類
 DSL 定義では、次の表に示すように、ドメインプロパティの**種類**を設定できます。

|ドメインプロパティの種類|説明|
|-|-|
|**Standard** (既定値)|*ストア*に保存され、ファイルにシリアル化されるドメインプロパティ。|
|**計算**|ストアに保存されていないが、他の値から計算される読み取り専用のドメインプロパティ。<br /><br /> たとえば、`Person.Age` は `Person.BirthDate` から計算できます。<br /><br /> 計算を実行するコードを指定する必要があります。 通常は、他のドメインプロパティから値を計算します。 ただし、外部リソースを使用することもできます。|
|**カスタムストレージ**|ストアに直接保存されるのではなく、get と set の両方が可能なドメインプロパティ。<br /><br /> 値を取得および設定するメソッドを指定する必要があります。<br /><br /> たとえば、`Person.FullAddress` は `Person.StreetAddress`、`Person.City`、および `Person.PostalCode` に格納できます。<br /><br /> 外部リソースにアクセスすることもできます。たとえば、データベースから値を取得して設定することができます。<br /><br /> @No__t_0 が true の場合、コードでストアに値を設定することはできません。 「[トランザクションとカスタム setter」を](#setters)参照してください。|

## <a name="providing-the-code-for-a-calculated-or-custom-storage-property"></a>計算またはカスタムストレージプロパティのコードを提供する
 ドメインプロパティの種類を [計算済み] または [カスタムストレージ] に設定する場合は、アクセス方法を指定する必要があります。 ソリューションをビルドすると、必要なものがエラーレポートに表示されます。

#### <a name="to-define-a-calculated-or-custom-storage-property"></a>計算またはカスタムのストレージプロパティを定義するには

1. [DslDefinition. dsl] で、図または**Dsl エクスプローラー**でドメインプロパティを選択します。

2. **[プロパティ]** ウィンドウで、 **[種類]** フィールドを **[計算]** 済み または **[カスタムストレージ]** に設定します。

     また、その**型**が必要なものにも設定されていることを確認します。

3. **ソリューションエクスプローラー**のツールバーで **[すべてのテンプレートの変換]** をクリックします。

4. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

     次のエラーメッセージが表示されます。 "*クラス*に Get*プロパティ*の定義が含まれていません。"

5. エラーメッセージをダブルクリックします。

     DomainRelationships.cs またはが表示されます。 強調表示されたメソッド呼び出しの上に、*プロパティ*を取得するための実装を提供するようにというコメントが表示されます ()。

    > [!NOTE]
    > このファイルは、DslDefinition. dsl から生成されます。 このファイルを編集すると、次回 **[すべてのテンプレートの変換]** をクリックしたときに変更内容が失われます。 代わりに、必要なメソッドを別のファイルに追加します。

6. クラスファイルを作成するか、別のフォルダーに開きます。たとえば、CustomCode \\*domainclass*.cs にします。

     名前空間が生成されたコードと同じであることを確認します。

7. クラスファイルで、ドメインクラスの部分実装を記述します。 クラスで、次の例のように、missing `Get` メソッドの定義を記述します。

    ```
    namespace Company.FamilyTree
    {  public partial class Person
       {  int GetAgeValue()
          { return System.DateTime.Today.Year - this.BirthYear; }
    }  }
    ```

8. **[種類]** を **[カスタムストレージ]** に設定した場合は、`Set` メソッドも指定する必要があります。 (例:

    ```
    void SetAgeValue(int value)
    { if (!Store.InUndoRedoOrRollback)
        this.BirthYear =
            System.DateTime.Today.Year - value; }
    ```

     @No__t_0 が true の場合、コードでストアに値を設定することはできません。 「[トランザクションとカスタム setter」を](#setters)参照してください。

9. ソリューションをビルドして実行します。

10. プロパティをテストします。 **元に戻す**と**やり直し**を実行していることを確認してください。

## <a name="setters"></a>トランザクションとカスタム Setter
 メソッドは通常、アクティブなトランザクションの内部で呼び出されるので、[カスタムストレージの設定方法] プロパティでは、トランザクションを開く必要はありません。

 ただし、ユーザーが Undo または Redo を呼び出した場合、またはトランザクションがロールバックされている場合にも、Set メソッドを呼び出すことができます。 @No__t_0 が true の場合、Set メソッドは次のように動作します。

- 他のドメインプロパティに値を割り当てるなど、ストアに変更を加えることはできません。 これらの値は、元に戻すマネージャーによって設定されます。

- ただし、データベースやファイルの内容などの外部リソースや、ストアの外部にあるオブジェクトを更新する必要があります。 これにより、ストア内の値と共に synchronism に保持されます。

  (例:

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

 トランザクションの詳細については、「[プログラムコードでのモデルの移動と更新](../modeling/navigating-and-updating-a-model-in-program-code.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [プログラム コードにおけるモデル内の移動およびモデルの更新](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [ドメイン プロパティのプロパティ](../modeling/properties-of-domain-properties.md)
- [方法: ドメイン固有言語を定義する](../modeling/how-to-define-a-domain-specific-language.md)