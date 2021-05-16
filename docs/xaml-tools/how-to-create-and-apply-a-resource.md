---
title: リソースを作成して適用する方法
description: 要素のスタイルとテンプレートを保存し、再利用できるよう、XAML デザイナーでリソースを作成し、適用する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- VS.XamlDesigner.CreateResource
- VS.XamlDesigner.EditResource
ms.assetid: 3ff4006d-659d-4073-9a41-06ff85e6cfdf
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b6c6c243896370cc97b8a85d5de520c4c033d49b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99971610"
---
# <a name="how-to-create-and-apply-a-resource"></a>リソースを作成して適用する方法

XAML デザイナーで、要素のスタイルとテンプレートは "リソース" という再利用可能なエンティティに保存されます。 スタイルを使用すると、要素のプロパティを設定し、それらの設定を複数の要素で再利用することにより、一貫した外観を維持できます。 [ControlTemplate](xref:Windows.UI.Xaml.Controls.ControlTemplate) は、コントロールの外観を定義し、リソースとしての適用も可能です。 詳細については、「[XAML スタイル](/windows/uwp/design/controls-and-patterns/xaml-styles)」と「[コントロール テンプレート](/windows/uwp/design/controls-and-patterns/control-templates)」を参照してください。

既存のプロパティ、[Style](xref:Windows.UI.Xaml.Style)、または [ControlTemplate](xref:Windows.UI.Xaml.Controls.ControlTemplate) から新しいリソースを作成するたびに、**[リソースの作成]** ダイアログ ボックスで、アプリケーション レベル、ドキュメント レベル、または要素レベルでリソースを定義できます。 定義したレベルに応じて、そのリソースを使用できる場所が決まります。 たとえば、要素レベルで定義したリソースは、そのリソースの作成時に使用した要素にのみ適用できます。 リソースを[リソース ディクショナリ](/windows/uwp/design/controls-and-patterns/resourcedictionary-and-xaml-resource-references)に格納することも可能です。これは、別のプロジェクトでもう一度使用できる個別のファイルです。

## <a name="create-a-new-resource"></a>新しいリソースを作成

1. XAML ファイルを XAML デザイナーで開き、要素を作成するか、または [ドキュメント アウトライン] ウィンドウで要素を選択します。

2. **[プロパティ]** ウィンドウで、プロパティ値の右側にボックス型のシンボルとして表示されているプロパティ マーカーを選択し、**[新しいリソースに変換]** を選択します。 白色のボックス シンボルは既定値であることを示し、黒色のボックス シンボルは通常、ローカル リソースが適用されたことを示します。

     選択したオブジェクトに適したダイログ ボックスが表示されます。 ブラシからリソースを作成するときには、次のダイアログ ボックスが表示されます。

     ![[リソースの作成] ダイアログ ボックス](../designers/media/xaml_create_resource.png)

3. **[名前 (キー)]** ボックスに、キー名を入力します。 これは、他の要素からリソースを参照するときに使用できる名前です。

4. **[定義先]** で、リソースを定義する場所を指定するオプションを選択します。

    - リソースをアプリケーション内の任意のドキュメントで使用できるようにするには、**[アプリケーション]** を選択します。

    - リソースを現在のドキュメントでのみ使用できるようにするには、**[このドキュメント]** を選択します。

    - リソースを作成元の要素またはその子要素でのみ使用できるようにするには、**[このドキュメント]** を選択し、ドロップダウン リストで [**要素**: **名前**] を選択します。

    - 他のプロジェクトで再利用できる [リソース ディクショナリ](/windows/uwp/design/controls-and-patterns/resourcedictionary-and-xaml-resource-references) ファイルにリソースを定義する場合は、**[リソース ディクショナリ]** をクリックします。 その後、ドロップダウン リストで既存のリソース ディクショナリ ファイル (**StandardStyles.xaml** など) を選択します。

5. **[OK]** をクリックします。リソースが作成され、作成元の要素に適用されます。

## <a name="apply-a-resource-to-an-element-or-property"></a>要素またはプロパティにリソースを適用する

1. [ドキュメント アウトライン] ウィンドウで、リソースを適用する先の要素を選択します。

2. 次のいずれかの操作を行います。

   - リソースをプロパティに適用します。 **[プロパティ]** ウィンドウで、プロパティ値の横にあるプロパティ マーカーを選択し、 **[ローカル リソース]** または **[システム リソース]** を選択した後、表示される一覧から使用可能なリソースを選択します。

      表示されるはずのリソースが表示されない場合は、リソースの種類がプロパティの種類と一致していない可能性があります。

   - スタイルまたはコントロール テンプレート リソースをコントロールに適用します。 [ドキュメント アウトライン] ウィンドウでコントロールの右クリック メニュー (コンテキスト メニュー) を開き、**[テンプレートの編集]** または **[追加テンプレートの編集]** を選択し、**[リソースの適用]** を選択した後、表示される一覧からコントロール テンプレートの名前を選択します。

     > [!NOTE]
     > **[テンプレートの編集]** はコントロール テンプレートを適用します。 **[追加テンプレートの編集]** は、その他の種類のテンプレートを適用します。

     リソースは互換性があれば適用できます。 たとえば、ブラシ リソースは [TextBox](xref:Windows.UI.Xaml.Controls.TextBox) コントロールの **[Foreground]** プロパティに適用できます。

## <a name="edit-a-resource"></a>リソースを編集する

1. アートボードまたは [ドキュメント アウトライン] ウィンドウで要素を選択します。

2. **[プロパティ]** ウィンドウで、プロパティの右側にある既定またはローカルのプロパティ マーカーを選択し、**[リソースの編集]** を選択して **[リソースの編集]** ダイアログ ボックスを開きます。

3. リソースのオプションを変更します。

## <a name="see-also"></a>関連項目

- [XAML デザイナーを使用した UI の作成](../xaml-tools/creating-a-ui-by-using-xaml-designer-in-visual-studio.md)
