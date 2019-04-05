---
title: '方法: パラメーターの型記述子の定義 |Microsoft Docs'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], type descriptor
- BDC [SharePoint development in Visual Studio], parameter types
- BDC [SharePoint development in Visual Studio], type descriptor
- Business Data Connectivity service [SharePoint development in Visual Studio], parameter types
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f28de400b417011b127b76c8813024f9721cc375
ms.sourcegitcommit: 23feea519c47e77b5685fec86c4bbd00d22054e3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/26/2019
ms.locfileid: "56843165"
---
# <a name="how-to-define-the-type-descriptor-of-a-parameter"></a>方法: パラメーターの型記述子を定義します。
  型記述子には、パラメーターのデータ型を表すプロパティが含まれています。 型記述子では、フィールド、エンティティ、またはエンティティのコレクションを定義できます。 詳細については、[TypeDescriptor](/previous-versions/office/developer/sharepoint-2007/ms543392\(v\=office.12\))を参照してください。

### <a name="to-define-the-type-descriptor-of-a-parameter"></a>パラメーターの型記述子を定義するには

1.  **BDC メソッドの詳細**ウィンドウで、パラメーターの型記述子を選択します。

2.  メニュー バーで、**ビュー**、**プロパティ ウィンドウ**します。

3.  **プロパティ**ウィンドウ、型記述子のプロパティを設定します。

     以降の手順では、型記述子をフィールド、エンティティ、またはエンティティのコレクションとして定義する方法を説明します。

### <a name="to-define-a-field"></a>フィールドを定義するには

1.  **プロパティ**ウィンドウで、設定、**名前**エンティティを表す型のフィールドの名前に、型記述子のプロパティ (例。**FirstName**)。

2.  横のリストで、 **TypeName**プロパティ、適切なデータ型を選択して (たとえば、 **Int32**)。

     その他の省略可能なパラメーターについては、[TypeDescriptor](/previous-versions/office/developer/sharepoint-2007/ms543392\(v\=office.12\))を参照してください。

### <a name="to-define-an-entity"></a>エンティティを定義するには

1.  **プロパティ**ウィンドウで、設定、**名前**プロパティをエンティティを表す名前 (例。**連絡先**)。

2.  設定、 **TypeName**プロパティをエンティティを表す型の完全修飾名。 この型は、プロジェクト内のクラスにすることも、ソリューションで参照されているアセンブリで定義されている型にすることも、BDC オブジェクト モデルで定義されている型にすることもできます。

    -   プロジェクト内のクラスに横に下向きの矢印を選択、 **TypeName**プロパティを選択、**現在のプロジェクト** ダイアログ ボックスで、プロジェクト、クラスを選択し、表示されるタブ。

         完全修飾名には、クラスの名前空間および名前と、LOB システムの名前が含まれます。 次の例の値の設定、 **TypeName**プロパティをプロジェクト内のクラスにします。

         `MyBDCNamespace.BdcModel1.Contact, BdcModel1`

    -   ソリューション内のアセンブリに配置されている型にする場合は、完全修飾名に型の名前、アセンブリの名前、バージョン番号、カルチャ、および公開キー トークンが含まれます。

         次の例の値の設定、 **TypeName**プロパティをソリューションで参照されているアセンブリで定義されている型。

         `MyNamespace.Contact, myAssemblyName, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089`

    -   BDC オブジェクト モデルで定義されている型にする場合は、完全修飾名に型の名前空間と名前が含まれます。

         次の例の値の設定、 **TypeName**プロパティを BDC オブジェクト モデル内の型。

         `Microsoft.BusinessData.Runtime.DynamicType`

3.  **BDC メソッドの詳細**ウィンドウで、型記述子のリストを開いてし、**編集**します。

     **BDC エクスプ ローラー**ウィンドウが開きます。

4.  **BDC エクスプ ローラー**、型記述子のショートカット メニューを開き、選択し、**型記述子の追加**します。

     そのエンティティ型記述子の子として新しい型記述子が追加されます。 その型記述子をフィールドとして構成します。

5.  手順 4. を繰り返して、エンティティの各フィールドに対応する子の型記述子を追加します。

### <a name="to-define-a-collection-of-entities"></a>エンティティのコレクションを定義するには

1. **BDC メソッドの詳細**ウィンドウで、使用するパラメーターの型記述子を選択します。

2. メニュー バーで、**ビュー**、**プロパティ ウィンドウ**します。

3. **プロパティ**ウィンドウで、設定、**名前**プロパティをエンティティを表す名前 (例。**連絡先**)。

4. 設定、 **IsCollection**プロパティを**True**します。 これは、この型記述子がエンティティのコレクションであることを表します。

5. 設定、 **TypeName**プロパティへの参照を含む文字列を<xref:System.Collections.Generic.IEnumerable%601>インターフェイス、およびエンティティを表す型の完全修飾名。 この型は、プロジェクト内のクラスにすることも、ソリューションで参照されているアセンブリで定義されている型にすることも、BDC オブジェクト モデルで定義されている型にすることもできます。

   - プロジェクト内のクラスに横に下向きの矢印を選択、 **TypeName**プロパティを選択、**現在のプロジェクト** ダイアログ ボックスで、プロジェクト、クラスを選択し、表示されるタブ。

      完全修飾名には、クラスの名前空間および名前と、LOB システムの名前が含まれます。

      次の例の値の設定、 **TypeName**プロパティをプロジェクト内のクラスのコレクション。

      `System.Collections.Generic.IEnumerable`1 [MyBDCNamespace.BdcModel1.Contact, BdcModel1]`

   - ソリューション内のアセンブリに配置されている型にする場合は、完全修飾名に型の名前、アセンブリの名前、バージョン番号、カルチャ、および公開キー トークンが含まれます。

      次の例の値の設定、 **TypeName**プロパティをソリューションで参照されているアセンブリ内の型のコレクション。

      `System.Collections.Generic.IEnumerable`1 [MyNamespace.Contact, myAssemblyName, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089]`

   - BDC オブジェクト モデルで定義されている型にする場合は、完全修飾名に型の名前空間と名前のみが含まれます。

      次の例の値の設定、 **TypeName**プロパティを BDC オブジェクト モデルで定義された型のコレクション。

      `System.Collections.Generic.IEnumerable`1 [Microsoft.BusinessData.Runtime.DynamicType]`

6. **BDC メソッドの詳細**ウィンドウで、型記述子のリストを開いてし、**編集**します。

    **BDC エクスプ ローラー**ウィンドウが開きます。

7. **BDC エクスプ ローラー**、型記述子のショートカット メニューを開き、選択し、**型記述子の追加**します。

    そのコレクション型記述子の子として新しい型記述子が追加されます。 その型記述子をエンティティとして構成します。

## <a name="see-also"></a>関連項目
- [BDC モデルのデザイン ツールの概要](../sharepoint/bdc-model-design-tools-overview.md)
- [方法: エンティティ モデルを追加します。](../sharepoint/how-to-add-an-entity-to-a-model.md)
- [方法: メソッドにパラメーターを追加します。](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [方法: メソッド インスタンスを定義します。](../sharepoint/how-to-define-a-method-instance.md)
- [ビジネス データ接続モデルを設計します。](../sharepoint/designing-a-business-data-connectivity-model.md)
