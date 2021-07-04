---
title: アイコンまたはデコレーターの可視性の制御
description: モデルのプロパティの状態に応じて、アイコンまたはデコレーターの表示を制御する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9c60d66188364ddd18be1d60a92b51ee5d7a9fc8
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112389619"
---
# <a name="controlling-the-visibility-of-an-icon-or-decorator"></a>アイコンまたはデコレーターの可視性の制御
"*デコレーター*" は、ドメイン固有言語 (DSL) の図形に表示されるアイコンまたはテキスト行です。 モデルのプロパティの状態に応じて、デコレーターを表示したり、非表示にしたりすることができます。 たとえば、人物を表す図形に対して、その人物の性別や子の数などに応じて異なるアイコンを表示できます。

## <a name="controlling-the-visibility-of-an-icon-or-decorator"></a>アイコンまたはデコレーターの表示の制御
 次の手順では、図形とドメイン クラスへのマッピングが既に定義されていることを前提としています。 詳細については、「[方法: ドメイン固有言語を定義する](../modeling/how-to-define-a-domain-specific-language.md)」を参照してください。

#### <a name="to-control-the-visibility-of-an-icon-or-text-decorator"></a>アイコンまたはテキスト デコレーターの表示を制御するには

1. DSL 定義図で、表示するアイコンまたはテキスト デコレーターを図形クラスに追加します。

   1. 図形クラスを右クリックし、 **[追加]** をポイントし、目的のデコレーターの種類をクリックします。

   2. デコレーターの **[位置]** プロパティを設定します。 複数のデコレーターを同じ位置に設定できます。 たとえば、男性と女性のアイコンを同じ位置で共有できます。

   3. アイコン デコレーターの **[既定のアイコン]** プロパティを設定します。

2. DSL 定義図で、ダイアグラム要素マップ (図形クラスとドメイン クラスの間に表示される灰色の線) を選択します。

3. [DSL の詳細] ウィンドウの **[デコレーター マップ]** タブで、デコレーターを選択します (例: MaleDecorator)。

4. **[表示フィルター]** ボックスをオンにします。

5. 表示を制御するドメイン プロパティがイミディエイト ドメイン クラスにある場合は、 **[Path To Filter]\(フィルターへのパス\)** プロパティを空白のままにします。

    それ以外の場合は、ドロップダウン メニューをクリックし、リレーションシップまたはプロパティが配置されているクラスに移動します。

   - エラー レポートを回避するため、ナビゲーション ツールで "*" とマークされているリレーションシップに移動しないでください。

6. ドメイン プロパティに **フィルター プロパティ** を設定します (例: Gender)。

7. **[表示エントリ]** の一覧で、デコレーターが表示されるこのドメイン プロパティの値を追加します (例: Male)。

8. この手順をアイコンごとに繰り返します。

9. **すべてのテンプレートを変換** し、ビルドして実行し、テスト ダイアグラムを開きます。

10. 制御プロパティの値を変更すると、デコレーターの表示/非表示が切り替わります。

    多くの場合、単純な値のセットよりも複雑な数式によって、表示を制御する必要があります。 たとえば、特定の種類のリンクの数に応じてアイコンを使用する場合や、数値が特定の範囲内にあるかどうかに依存させる場合などです。 その場合は、次の手順を使用します。

#### <a name="to-control-the-visibility-of-a-decorator-based-on-a-formula"></a>数式に基づいてデコレーターの表示を制御するには

1. ドメイン クラスに、計算されるドメイン プロパティを追加します。 **[プロパティ]** ウィンドウで、次の値を設定します。

     **IsBrowsable =** `False`  **- これにより、ユーザーに対してプロパティが非表示になります**

     **Kind =** `Calculated`  **- これは、値を計算するコードを自分で指定することを意味します**

     **Name** - たとえば **DecoratorControl** です

     **Type** = `Boolean`

     詳細については、「[Calculated および Custom Storage プロパティ](../modeling/calculated-and-custom-storage-properties.md)」を参照してください。

2. 新しいプロパティによってデコレーターの表示を制御するようにします。

    1. ダイアグラム要素マップ (ドメイン クラスから図形に伸びている灰色の線) を選択します。 **[DSL の詳細]** ウィンドウで、 **[DecoratorMap]** タブを開きます。

    2. **[表示フィルター]** ボックスをオンにします。

    3. **[フィルター]** プロパティで、 **[DecoratorControl]** 制御プロパティを選択します。

    4. **[表示エントリ]** に「`True`」と入力します。

3. **ソリューション エクスプローラー** のツールバーで **[すべてのテンプレートの変換]** をクリックします。

4. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

5. 表示されたエラー レポートの "*YourClass* には GetDecoratorControlValue の定義が含まれていません ..." をダブルクリックします。

     テキスト エディターが開いて、Dsl\GeneratedCode\DomainClasses.cs が表示されます。 強調表示されたエラーの上にあるのは、メソッドの追加を要求するコメントです。

6. 名前空間、クラス、およびメソッドが不足していることに注意してください。  たとえば Company.FamilyTree.Person.GetDecoratorControlValue() です。

7. 別のコード ファイルで、不足しているメソッドを含む部分クラス定義を記述します。 次に例を示します。

    ```
    namespace Company.FamilyTree
    { partial class Person
      { bool GetDecoratorControlValue()
        {
          return this.Children.Count > 0;
    } } }
    ```

     プログラム コードを使用したモデルのカスタマイズの詳細については、「[プログラム コードでのモデルのナビゲーションと更新](../modeling/navigating-and-updating-a-model-in-program-code.md)」を参照してください。

8. ソリューションをリビルドして実行します。

## <a name="see-also"></a>こちらもご覧ください

- [シェイプとコネクタの定義](../modeling/defining-shapes-and-connectors.md)
- [ダイアグラムへの背景イメージの設定](../modeling/setting-a-background-image-on-a-diagram.md)
- [プログラム コードにおけるモデル内の移動およびモデルの更新](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [ドメイン固有言語をカスタマイズするコードの記述](../modeling/writing-code-to-customise-a-domain-specific-language.md)