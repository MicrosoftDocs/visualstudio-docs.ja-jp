---
title: 依存関係図へのカスタム プロパティの追加
description: 依存関係図の拡張コードを記述するときに、依存関係図の任意の要素と共に値を格納する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- dependency diagrams, adding custom properties
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 70588a2d472a1170b58911eece4fa70831064f72
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112389853"
---
# <a name="add-custom-properties-to-dependency-diagrams"></a>依存関係図へのカスタム プロパティの追加

依存関係図の拡張コードを記述するときに、依存関係図の任意の要素と共に値を格納できます。 値は、図が保存され、再び開かれたときに保持されます。 これらのプロパティは、ユーザーが表示して編集できるように、 **[プロパティ]** ウィンドウに表示することもできます。 たとえば、ユーザーが各レイヤーに正規表現を指定できるようにすることや、各レイヤーのクラスの名前がユーザーが指定したパターンに準拠していることを確認するための検証コードをユーザーが記述できるようにすることができます。

## <a name="non-visible-properties"></a>表示されないプロパティ

依存関係図の任意の要素に値をアタッチするコードが必要なだけの場合、MEF コンポーネントを定義する必要はありません。 [ILayerElement](/previous-versions/ff644511(v=vs.140)) には `Properties` という名前のディクショナリがあります。 マーシャリング可能な値を任意のレイヤー要素のディクショナリに単純に追加します。 これらの値は、依存関係図の一部として保存されます。

## <a name="editable-properties"></a>編集可能なプロパティ

**最初の準備**

> [!IMPORTANT]
> プロパティが表示されるようにするには、レイヤーのプロパティを表示させたい各コンピューターで次の変更を行います。
>
> 1. **[管理者として実行]** を使用して、メモ帳を実行します。 *%ProgramFiles%\Microsoft Visual Studio [version]\Common7\IDE\Extensions\Microsoft\Architecture Tools\ExtensibilityRuntime\extension.vsixmanifest* を開きます。
> 2. **Content** 要素内で、次を追加します。
>
>     ```xml
>     <MefComponent>Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer.Provider.dll</MefComponent>
>     ```
>
> 3. Visual Studio アプリケーションの [スタート] メニューの **[Visual Studio Tools]** セクションで、 **[開発者コマンド プロンプト]** を開きます。 次を入力します。
>
>      `devenv /rootSuffix /updateConfiguration`
>
>      `devenv /rootSuffix Exp /updateConfiguration`
> 4. Visual Studio を再起動します。

**コードが VSIX プロジェクトに含まれていることを確認する**

プロパティがコマンド、ジェスチャ、または検証プロジェクトの一部である場合、何も追加する必要はありません。 カスタム プロパティのコードは、MEF コンポーネントとして定義された Visual Studio 機能拡張プロジェクトで定義する必要があります。 詳細については、「[依存関係図にコマンドおよびジェスチャを追加する](../modeling/add-commands-and-gestures-to-layer-diagrams.md)」または「[カスタム アーキテクチャ検証を依存関係図に追加する](../modeling/add-custom-architecture-validation-to-layer-diagrams.md)」を参照してください。

**カスタム プロパティを定義する**

カスタム プロパティを作成するには、次のようなクラスを定義します。

```csharp
[Export(typeof(IPropertyExtension))]
public class MyProperty : PropertyExtension<ILayerElement>
{
  // Implement the interface.
}
```

プロパティは、[ILayerElement](/previous-versions/ff644511(v=vs.140))、またはその派生クラス (以下を含む) のいずれでも定義できます。

- `ILayerModel` - モデル

- `ILayer` - 各レイヤー

- `ILayerDependencyLink` - レイヤー間のリンク

- `ILayerComment`

- `ILayerCommentLink`

## <a name="example"></a>例

次のコードは、標準的なカスタム プロパティ記述子です。 この例では、Boolean プロパティがレイヤー モデル (`ILayerModel`) で定義されており、ユーザーはこれを使用してカスタム検証メソッドに値を提供できます。

```csharp
using System;
using System.ComponentModel.Composition;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer;

namespace MyNamespace
{
  /// <summary>
  /// Custom properties are added to the Layer Designer via a custom
  /// Property Descriptor. We have to export this Property Descriptor
  /// using MEF to make it available in the Layer Designer.
  /// </summary>
  [Export(typeof(IPropertyExtension))]
  public class AllTypesMustBeReferencedProperty
      : PropertyExtension<ILayerModel>
  {
    /// <summary>
    /// Each custom property must have a unique name.
    /// Usually we use the full name of this class.
    /// </summary>
    public static readonly string FullName =
      typeof(AllTypesMustBeReferencedProperty).FullName;

    /// <summary>
    /// Construct the property. Notice the use of FullName.
    /// </summary>
    public AllTypesMustBeReferencedProperty()
            : base(FullName)
    {  }

    /// <summary>
    /// The display name is shown in the Properties window.
    /// We therefore use a localizable resource.
    /// </summary>
    public override string DisplayName
    {
      get { return Strings.AllTypesMustBeReferencedDisplayName; }
    }

    /// <summary>
    /// Description shown at the bottom of the Properties window.
    /// We use a resource string for easier localization.
    /// </summary>
    public override string Description
    {
      get { return Strings.AllTypesMustBeReferencedDescription; }
    }

    /// <summary>
    /// This is called to set a new value for this property. We must
    /// throw an exception if the value is invalid.
    /// </summary>
    /// <param name="component">The target ILayerElement</param>
    /// <param name="value">The new value</param>
    public override void SetValue(object component, object value)
    {
      ValidateValue(value);
      base.SetValue(component, value);
    }
    /// <summary>
    /// Helper to validate the value.
    /// </summary>
    /// <param name="value">The value to validate</param>
    private static void ValidateValue(object value)
    {  }

    public override Type PropertyType
    { get { return typeof(bool); } }

    /// <summary>
    /// The segment label of the properties window.
    /// </summary>
    public override string Category
    {
      get
      {
        return Strings.AllTypesMustBeReferencedCategory;
      }
    }
  }
}
```

## <a name="see-also"></a>関連項目

- [依存関係図の拡張](../modeling/extend-layer-diagrams.md)
