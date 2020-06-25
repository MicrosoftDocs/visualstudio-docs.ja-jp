---
title: '方法: エンティティ クラスに検証を追加する'
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
ms.assetid: 61107da9-7fa3-4dba-b101-ae46536f52c4
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 5d408c67b2e54fecd6404bac93d93ecfb35de162
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282346"
---
# <a name="how-to-add-validation-to-entity-classes"></a>方法: エンティティ クラスに検証を追加する
エンティティ クラスの "*検証*" とは、データ オブジェクトに入力された値が、アプリケーションに対して設定された規則に従っていること、およびオブジェクトのスキーマ内の制約に従っていることを確認するプロセスです。 基になるデータベースに更新を送信する前にデータを検証すると、エラーを減らすことができます。 アプリケーションとデータベースの間で生じる可能性のあるラウンド トリップの回数も減ります。

[Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)には、完全なエンティティの挿入、更新、および削除中に実行されるデザイナーによって生成されたコードをユーザーが拡張できる部分メソッドと、個々の列の変更中および変更後のコードが含まれます。

> [!NOTE]
> このトピックでは、 **O/R デザイナー**を使用してエンティティクラスに検証を追加するための基本的な手順について説明します。 特定のエンティティクラスを参照することなく、これらの汎用的な手順に従うのは困難な場合があるため、実際のデータを使用するチュートリアルが用意されています。

## <a name="add-validation-for-changes-to-the-value-in-a-specific-column"></a>特定の列の値に対する変更の検証を追加する
この手順では、列の値の変更時にデータを検証する方法を示します。 検証はユーザー インターフェイスではなくクラス定義の内部で実行されるため、値によって検証が失敗する場合は例外がスローされます。 列の値を変更しようとするアプリケーションのコードには、エラー処理を実装してください。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-validate-data-during-a-columns-value-change"></a>列の値の変更時にデータを検証するには

1. **O/R デザイナー**で新しい LINQ to SQL クラスファイル (**.dbml**ファイル) を開くか、作成します。 (**ソリューション エクスプローラー**で **.dbml** ファイルをダブルクリックします。)

2. **O/R デザイナー**で、検証を追加するクラスを右クリックして、**[コードの表示]** をクリックします。

     コード エディターが開き、選択したエンティティ クラスの部分クラスが表示されます。

3. 部分クラスにカーソルを置きます。

4. Visual Basic プロジェクトの場合は、次の操作を行います。

    1. **[メソッド名]** の一覧を展開します。

    2. 検証を追加する列の **OnCOLUMNNAMEChanging** メソッドを見つけます。

    3. `OnCOLUMNNAMEChanging` メソッドが部分クラスに追加されます。

    4. 次のコードを追加して、まず値が入力されたことを確認し、次に列に入力された値がアプリケーションで許容されることを確認します。 入力された値は `value` 引数に含まれています。そこで、これが有効な値であることを確認するロジックを追加します。

        ```vb
        If value.HasValue Then
            ' Add code to ensure that the value is acceptable.
            ' If value < 1 Then
            '    Throw New Exception("Invalid data!")
            ' End If
        End If
        ```

    C# プロジェクトの場合は、次の操作を行います。

    C# プロジェクトでは自動的にイベントハンドラーが生成されないため、IntelliSense を使用して列変更部分メソッドを作成できます。 「`partial`」に続けてスペースを入力して、使用可能な部分メソッドの一覧にアクセスします。 検証を追加する列の列変更メソッドをクリックします。 次のコードは、列変更部分メソッドを選択したときに生成されるコードに似ています。

    ```csharp
    partial void OnCOLUMNNAMEChanging(COLUMNDATATYPE value)
        {
           throw new System.NotImplementedException();
        }
    ```

## <a name="add-validation-for-updates-to-an-entity-class"></a>エンティティクラスに更新の検証を追加する
変更時の値のチェックに加えて、エンティティ クラス全体の更新が試行されたときにデータを検証することもできます。 更新の試行時の検証では、ビジネス ルールにおける必要性に応じて複数の列の値を比較できます。 次の手順は、エンティティ クラス全体の更新が試行されたときに検証を行う方法を示しています。

> [!NOTE]
> エンティティ クラス全体の更新に対する検証コードは、特定のエンティティ クラスの部分クラスではなく、部分 <xref:System.Data.Linq.DataContext> クラスで実行されます。

### <a name="to-validate-data-during-an-update-to-an-entity-class"></a>エンティティ クラスの更新時にデータを検証するには

1. **O/R デザイナー**で新しい LINQ to SQL クラスファイル (**.dbml**ファイル) を開くか、作成します。 (**ソリューション エクスプローラー**で **.dbml** ファイルをダブルクリックします。)

2. **O/R デザイナー**で空の領域を右クリックし、**[コードの表示]** をクリックします。

     コード エディターが開き、`DataContext` の部分クラスが表示されます。

3. `DataContext` の部分クラスにカーソルを置きます。

4. Visual Basic プロジェクトの場合は、次の操作を行います。

    1. **[メソッド名]** の一覧を展開します。

    2. **[UpdateENTITYCLASSNAME]** をクリックします。

    3. `UpdateENTITYCLASSNAME` メソッドが部分クラスに追加されます。

    4. 次のコードに示すように、`instance` 引数を使用して個々の列の値にアクセスします。

        ```vb
        If (instance.COLUMNNAME = x) And (instance.COLUMNNAME = y) Then
            Dim ErrorMessage As String = "Invalid data!"
            Throw New Exception(ErrorMessage)
        End If
        ```

    C# プロジェクトの場合は、次の操作を行います。

    C# プロジェクトではイベントハンドラーが自動的に生成されないため、IntelliSense を使用して部分メソッドを作成でき `UpdateCLASSNAME` ます。 「`partial`」に続けてスペースを入力して、使用可能な部分メソッドの一覧にアクセスします。 検証を追加するクラスの update メソッドをクリックします。 次のコードは、部分メソッドを選択したときに生成されるコードに似てい `UpdateCLASSNAME` ます。

    ```csharp
    partial void UpdateCLASSNAME(CLASSNAME instance)
    {
        if ((instance.COLUMNNAME == x) && (instance.COLUMNNAME = y))
        {
            string ErrorMessage = "Invalid data!";
            throw new System.Exception(ErrorMessage);
        }
    }
    ```

## <a name="see-also"></a>関連項目

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [検証 (データを)](../data-tools/validate-data-in-datasets.md)
- [LINQ to SQL (.NET Framework)](/dotnet/framework/data/adonet/sql/linq/index)
