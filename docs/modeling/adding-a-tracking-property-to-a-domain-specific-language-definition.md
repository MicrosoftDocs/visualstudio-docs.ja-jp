---
title: DSL 定義への追跡プロパティの追加
description: 追跡ドメイン プロパティについてと、追跡プロパティをドメイン モデルに追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- tracking properties [Domain-Specific Language Tools], walkthrough
- Domain-Specific Language Tools, walkthroughs
- walkthroughs [Domain-Specific Language Tools]
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 546636ec3de4656bf0f6480dfaa5141d38e963d6
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112384916"
---
# <a name="add-a-tracking-property-to-a-domain-specific-language-definition"></a>ドメイン固有言語の定義に追跡プロパティを追加する

このチュートリアルでは、ドメイン モデルに追跡プロパティを追加する方法について説明します。

*追跡ドメイン* プロパティは、ユーザーが更新できるが、他のドメイン プロパティまたは要素の値を使用して計算される既定値を持つプロパティです。

たとえば、ドメイン固有言語ツール (DSL ツール) では、ドメイン クラスの [表示名] プロパティには、ドメイン クラスの名前を使用して計算される既定値がありますが、ユーザーはデザイン時に値を変更するか、集計値にリセットすることができます。

このチュートリアルでは、モデルの [既定の名前空間] プロパティに基づく既定値が設定された Namespace 追跡プロパティを持つ、ドメイン固有言語 (DSL) を作成します。 追跡プロパティの詳細については、[追跡プロパティの定義](/previous-versions/cc825929(v=vs.100))に関するページを参照してください。

- DSL ツールでは、追跡プロパティ記述子をサポートしています。 ただし、DSL デザイナーを使用して、追跡プロパティを言語に追加することはできません。 したがって、追跡プロパティを定義および実装するには、カスタム コードを追加する必要があります。

  追跡プロパティには、追跡とユーザーによって更新済みの 2 つの状態があります。 追跡プロパティには、次の特徴があります。

- 追跡状態のときは、追跡プロパティの値が計算され、モデルの他のプロパティが変更されると値が更新されます。

- ユーザーによって更新済み状態のときは、追跡プロパティの値には、ユーザーが最後にプロパティを設定した値が保持されます。

- **[プロパティ]** ウィンドウでは、プロパティがユーザーによって更新済み状態のときにのみ、追跡プロパティの **Reset** コマンドが有効になります。 **Reset** コマンドは、追跡プロパティの状態を tracking に設定します。

- **[プロパティ]** ウィンドウでは、追跡プロパティが追跡状態のとき、その値は通常のフォントで表示されます。

- **[プロパティ]** ウィンドウでは、追跡プロパティがユーザーによって更新済み状態のとき、その値は太字フォントで表示されます。

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルを開始するには、まず次のコンポーネントをインストールする必要があります。

| コンポーネント | リンク |
|-|-|
| Visual Studio | [http://go.microsoft.com/fwlink/?LinkID=185579](https://visualstudio.microsoft.com/) |
| [!INCLUDE[vssdk_current_short](../modeling/includes/vssdk_current_short_md.md)] | [http://go.microsoft.com/fwlink/?LinkID=185580](/azure/devops/integrate/index?view=azure-devops&viewFallbackFrom=vsts&preserve-view=true) |
| [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] | [http://go.microsoft.com/fwlink/?LinkID=185581](https://code.msdn.microsoft.com/site/search?query=%22Modeling%20SDK%22&f%5B0%5D.Value=%22Modeling%20SDK%22&f%5B0%5D.Type=SearchText&ac=5) |

## <a name="create-the-project"></a>プロジェクトを作成する

1. ドメイン固有言語デザイナー プロジェクトを作成します。 これに `TrackingPropertyDSL` という名前をつけます。

2. **ドメイン固有言語デザイナー ウィザード** で、次のオプションを設定します。

    1. **MinimalLanguage** テンプレートを選択します。

    2. ドメイン固有言語の既定の名前 `TrackingPropertyDSL` を使用します。

    3. モデル ファイルの拡張子を `trackingPropertyDsl` に設定します。

    4. モデル ファイルの既定のテンプレート アイコンを使用します。

    5. 製品の名前を `Product Name` に設定します。

    6. 会社の名前を `Company Name` に設定します。

    7. ソリューション内のプロジェクトのルート名前空間には、既定値 `CompanyName.ProductName.TrackingPropertyDSL` を使用します。

    8. アセンブリの厳密な名前のキー ファイルをウィザードで作成できるようにします。

    9. ソリューションの詳細を確認し、 **[完了]** をクリックして DSL 定義プロジェクトを作成します。

## <a name="customize-the-default-dsl-definition"></a>既定の DSL 定義をカスタマイズする
 このセクションでは、次の項目を含むように DSL 定義をカスタマイズします。

- モデルのすべての要素の Namespace 追跡プロパティ。

- モデルのすべての要素のブール値 の IsNamespaceTracking プロパティ。 このプロパティは、追跡プロパティが追跡状態であるか、またはユーザーによって更新済み状態であるかを示します。

- モデルの既定の Namespace プロパティ。 このプロパティは、Namespace 追跡プロパティの既定値を計算するために使用されます。

- モデルの CustomElements 集計プロパティ。 このプロパティは、カスタム名前空間を持つ要素の比率を示します。

### <a name="to-add-the-domain-properties"></a>ドメイン プロパティを追加するには

1. DSL デザイナーで、**ExampleModel** ドメイン クラスを右クリックし、 **[追加]** をポイントして、**DomainProperty** をクリックします。

    1. 新しいプロパティに `DefaultNamespace` という名前を付けます。

    2. 新しいプロパティの **[プロパティ]** ウィンドウで、 **[既定値]** を `DefaultNamespace` に設定し、 **[種類]** を **[文字列]** に設定します。

2. **ExampleModel** ドメイン クラスに、`CustomElements` という名前のドメイン プロパティを追加します。

     新しいプロパティの **[プロパティ]** ウィンドウで、 **[Kind]** を **[Calculated]** に設定します。

3. **ExampleElement** ドメイン クラスに、`Namespace` という名前のドメイン プロパティを追加します。

     新しいプロパティの **[プロパティ]** ウィンドウで、 **[Is Browsable]** を **[False]** に設定し、 **[Kind]** を **[CustomStorage]** に設定します。

4. **ExampleElement** ドメイン クラスに、`IsNamespaceTracking` という名前のドメイン プロパティを追加します。

     新しいプロパティの **[プロパティ]** ウィンドウで、 **[Is Browsable]** を **[False]** に設定し、 **[Default Value]** を `true` に設定し、 **[Type]** を **[Boolean]** に設定します。

### <a name="to-update-the-diagram-elements-and-dsl-details"></a>ダイアグラムの要素と DSL の詳細を更新するには

1. DSL デザイナーで、**ExampleShape** ジオメトリ シェイプを右クリックし、 **[追加]** をポイントして、 **[テキスト デコレーター]** をクリックします。

    1. 新しいテキスト デコレーターに `NamespaceDecorator` という名前を付けます。

    2. テキスト デコレーターの **[プロパティ]** ウィンドウで、 **[Position]** を **[InnerBottomLeft]** に設定します。

2. DSL デザイナーで、**ExampleElement** クラスを **ExampleShape** シェイプに接続する線を選択します。

    1. **[DSL の詳細]** ウィンドウで **[デコレーター マップ]** タブを選択します。

    2. **[デコレーター]** 一覧で **[NamespaceDecorator]** を選択し、そのチェック ボックスをオンにして、 **[表示プロパティ]** 一覧で **[名前空間]** を選択します。

3. **DSL エクスプローラー** で、 **[ドメイン クラス]** フォルダーを展開し、 **[ExampleElement]** ノードを右クリックしてから、 **[新しいドメイン型記述子の追加]** をクリックします。

    1. **[ExampleElement]** ノードを展開し、 **[カスタム型記述子 (ドメイン型記述子)]** ノードを選択します。

    2. ドメイン型記述子の **[プロパティ]** ウィンドウで、 **[Custom Coded]** を **[True]** に設定します。

4. **DSL エクスプローラー** で、 **[Xml シリアル化の動作]** ノードを選択します。

    1. **[プロパティ]** ウィンドウで、 **[Custom Post Load]** を **[True]** に設定します。

## <a name="transform-templates"></a>テンプレートを変換する

DSL のドメイン クラスとプロパティを定義したので、DSL 定義を正しく変換してプロジェクトのコードを再生成できることを確認できます。

1. **[ソリューション エクスプローラー]** ツール バーで、 **[すべてのテンプレートの変換]** をクリックします。

2. システムによってソリューションのコードが再生成され、DslDefinition.dsl が保存されます。 定義ファイルの XML 形式の詳細については、「[DslDefinition.dsl ファイル](../modeling/the-dsldefinition-dsl-file.md)」を参照してください。

## <a name="create-files-for-custom-code"></a>カスタム コード用のファイルを作成する

すべてのテンプレートを変換すると、Dsl および DslPackage プロジェクトでドメイン固有言語を定義するソース コードがシステムによって生成されます。 生成されたテキストに干渉しないようにするために、生成されたコード ファイルとは別のファイルにカスタム コードを記述します。

追跡プロパティの値と状態を維持するためのコードを指定する必要があります。 生成されたコードとカスタム コードを区別し、ファイル名の競合を回避するために、カスタム コード ファイルを別のサブフォルダーに配置します。

1. **ソリューション エクスプローラー** で **DSL** プロジェクトを右クリックし、 **[追加]** をポイントして **[新しいフォルダー]** をクリックします。 新しいフォルダーに `CustomCode` という名前を付けます。

2. 新しい **CustomCode** フォルダーを右クリックし、 **[追加]** をポイントして **[新しい項目]** をクリックします。

3. **[コード ファイル]** テンプレートを選択し、 **[名前]** を `NamespaceTrackingProperty.cs` に設定して、 **[OK]** をクリックします。

     NamespaceTrackingProperty.cs ファイルが作成され、編集用に開かれます。

4. このフォルダーで、`ExampleModel.cs,``HelperClasses.cs`、`Serialization.cs`、`TypeDescriptor.cs` の各コード ファイルを作成します。

5. **DslPackage** プロジェクトでは、さらに `CustomCode` フォルダーを作成して、それに `Package.cs` コード ファイルを追加します。

## <a name="add-helper-classes-to-support-tracking-properties"></a>追跡プロパティをサポートするヘルパー クラスを追加する

次のように、HelperClasses.cs ファイルに `TrackingHelper` および `CriticalException` クラスを追加します。 これらのクラスは、このチュートリアルの後半で参照します。

1. HelperClasses.cs ファイルに次のコードを追加します。

    ```csharp
    using System;
    using System.Collections;
    using System.Diagnostics;
    using Microsoft.VisualStudio.Modeling;

    namespace CompanyName.ProductName.TrackingPropertyDSL
    {
        internal static class TrackingHelper
        {
            /// <summary>Notify each model element in a collection that a tracked
            /// property has changed.</summary>
            /// <param name="store">The store for the model.</param>
            /// <param name="collection">The collection of model elements that
            /// contain the tracking property.</param>
            /// <param name="propertyId">The ID of the tracking property.</param>
            /// <param name="trackingPropertyId">The ID of the property that
            /// indicates whether the tracking property is tracking.</param>
            internal static void UpdateTrackingCollectionProperty(
                Store store,
                IEnumerable collection,
                Guid propertyId,
                Guid trackingPropertyId)
            {
                DomainPropertyInfo propInfo =
                    store.DomainDataDirectory.GetDomainProperty(propertyId);

                DomainPropertyInfo trackingPropInfo =
                    store.DomainDataDirectory.GetDomainProperty(trackingPropertyId);

                Debug.Assert(propInfo != null);
                Debug.Assert(trackingPropInfo != null);
                Debug.Assert(trackingPropInfo.PropertyType.Equals(typeof(bool)),
                    "Tracking property not specified as a boolean");

                foreach (ModelElement element in collection)
                {
                    // If the tracking property is currently tracking, then notify
                    // it that the tracked property has changed.
                    bool isTracking = (bool)trackingPropInfo.GetValue(element);
                    if (isTracking)
                    {
                        propInfo.NotifyValueChange(element);
                    }
                }
            }
        }

        /// <summary>Helper class to flag critical exceptions from ones that are
        /// safe to ignore.</summary>
        internal static class CriticalException
        {
            /// <summary>Gets whether an exception is critical and can not be
            /// ignored.</summary>
            /// <param name="ex">The exception to check.</param>
            /// <returns>True if the exception is critical.</returns>
            internal static bool IsCriticalException(Exception ex)
            {
                if (ex is NullReferenceException
                    || ex is StackOverflowException
                    || ex is OutOfMemoryException
                    || ex is System.Threading.ThreadAbortException)
                    return true;

                if (ex.InnerException != null)
                    return IsCriticalException(ex.InnerException);

                return false;
            }
        }
    }
    ```

## <a name="add-custom-code-for-the-custom-type-descriptor"></a>カスタム型記述子のカスタム コードを追加する

`ExampleModel` ドメイン クラスの型記述子に対して `GetCustomProperties` メソッドを実装します。

> [!NOTE]
> DSL ツールで `ExampleModel` 呼び出し `GetCustomProperties` のカスタム型記述子用に生成するコード。ただし、DSL ツールでは、メソッドを実装するコードを生成しません。

このメソッドを定義すると、Namespace 追跡プロパティの追跡プロパティ記述子が作成されます。 また、追跡プロパティの属性を指定すると、 **[プロパティ]** ウィンドウでプロパティを正しく表示できます。

### <a name="to-modify-the-type-descriptor-for-the-examplemodel-domain-class"></a>ExampleModel ドメイン クラスの型記述子を変更するには

1. TypeDescriptor.cs ファイルに次のコードを追加します。

    ```csharp
    using System;
    using System.ComponentModel;
    using Microsoft.VisualStudio.Modeling;
    using Microsoft.VisualStudio.Modeling.Design;

    namespace CompanyName.ProductName.TrackingPropertyDSL
    {
        // To the custom type descriptor for the ExampleElement domain class, add
        // the GetCustomProperties method.
        public partial class ExampleElementTypeDescriptor
        {
            /// <summary>Returns the property descriptors for the described
            /// ExampleElement domain class.</summary>
            /// <remarks>This method adds the tracking property descriptor.
            /// </remarks>
            private PropertyDescriptorCollection GetCustomProperties(
                Attribute[] attributes)
            {
                // Get the default property descriptors from the base class
                PropertyDescriptorCollection propertyDescriptors =
                    base.GetProperties(attributes);

                // Get a reference to the model element that is being described.
                ExampleElement source = this.ModelElement as ExampleElement;

                //Add the descriptor for the tracking property.
                if (source != null)
                {
                    DomainPropertyInfo domainProperty =
                        source.Store.DomainDataDirectory.GetDomainProperty(
                            ExampleElement.NamespaceDomainPropertyId);

                    DomainPropertyInfo trackingProperty =
                        source.Store.DomainDataDirectory.GetDomainProperty(
                            ExampleElement.IsNamespaceTrackingDomainPropertyId);

                    // Define attributes for the tracking property so that the
                    // Properties window displays the property correctly.
                    Attribute[] attr = new Attribute[] {
                        new DisplayNameAttribute("Element Namespace"),
                        new DescriptionAttribute("The namespace of the element."),
                        new CategoryAttribute("Tracking Properties"),
                    };

                    propertyDescriptors.Add(new TrackingPropertyDescriptor(
                        source, domainProperty, trackingProperty, attr));
                }

                // Return the property descriptors for this element
                return propertyDescriptors;
            }
        }
    }
    ```

## <a name="adding-custom-code-for-the-package"></a>パッケージのカスタム コードの追加

生成されたコードでは、ExampleElement ドメイン クラスの型説明プロバイダーを定義します。ただし、この型説明プロバイダーを使用するように DSL に指示するコードを追加する必要があります。

1. Package.cs ファイルに次のコードを追加します。

    ```csharp
    using System.ComponentModel;

    namespace CompanyName.ProductName.TrackingPropertyDSL
    {
        // Override the default Initialize method.
        internal sealed partial class TrackingPropertyDSLPackage
        {
            protected override void Initialize()
            {
                // Add the custom type descriptor for the ExampleElement type.
                TypeDescriptor.AddProvider(
                    new ExampleElementTypeDescriptionProvider(),
                    typeof(ExampleElement));

                base.Initialize();
            }
        }
    }
    ```

## <a name="add-custom-code-for-the-model"></a>モデルのカスタム コードを追加する

`ExampleModel` ドメイン クラスの `GetCustomElementsValue` メソッドを実装します。

> [!NOTE]
> DSL ツールで `ExampleModel` 呼び出し `GetCustomElementsValue` 用に生成するコード。ただし、DSL ツールでは、メソッドを実装するコードを生成しません。

`GetCustomElementsValue` メソッドを定義すると、`ExampleModel` の CustomElements 集計プロパティのロジックが提供されます。 このメソッドでは、ユーザーが更新した値が設定された Namespace 追跡プロパティを持つ `ExampleElement` ドメイン クラスの数をカウントし、モデル内の要素の総数の割合として、このカウントを表す文字列を返します。

さらに、`OnDefaultNamespaceChanged` メソッドを `ExampleModel` に追加し、`ExampleModel` の入れ子になった `DefaultNamespacePropertyHandler` クラスの `OnValueChanged` メソッドをオーバーライドして `OnDefaultNamespaceChanged` を呼び出します。

DefaultNamespace プロパティは Namespace 追跡プロパティの計算に使用されるため、`ExampleModel` では、DefaultNamespace の値が変更されたことをすべての `ExampleElement` ドメイン クラスに通知する必要があります。

### <a name="to-modify-the-property-handler-for-the-tracked-property"></a>追跡対象プロパティのプロパティ ハンドラーを変更するには

1. ExampleModel.cs ファイルに次のコードを追加します。

    ```csharp
    using System.Linq;

    namespace CompanyName.ProductName.TrackingPropertyDSL
    {
        public partial class ExampleModel
        {
            public string GetCustomElementsValue()
            {
                if (this.Elements.Count == 0) return "0/0";

                int number = this.Elements.Count(e => !e.IsNamespaceTracking);
                return string.Format("{0}/{1}", number, this.Elements.Count);
            }

            #region Value changed handler for the tracked property

            // When a tracked property changes, it needs to notify all of the properties
            // that track it.

            /// <summary>Called by the DefaultNamespace property value handler when the
            /// DefaultNamespace property changes.</summary>
            /// <param name="oldValue">The previous value of the property.</param>
            /// <param name="newValue">The new value of the property.</param>
            protected virtual void OnDefaultNamespaceChanged(
                string oldValue, string newValue)
            {
                // Use the helper class to notify all of the elements in the model
                // that the default namespace has changed.
                TrackingHelper.UpdateTrackingCollectionProperty(
                    this.Store,
                    this.Elements,
                    ExampleElement.NamespaceDomainPropertyId,
                    ExampleElement.IsNamespaceTrackingDomainPropertyId);
            }

            // Update the change handler for the DefaultNamespace property.
            internal sealed partial class DefaultNamespacePropertyHandler
            {
                /// <summary>Called when the DefaultNamespace property changes.</summary>
                /// <param name="element">The model element that has the property that
                /// changed.</param>
                /// <param name="oldValue">The previous value of the property.</param>
                /// <param name="newValue">The new value of the property.</param>
                protected override void OnValueChanged(
                    ExampleModel element, string oldValue, string newValue)
                {
                    base.OnValueChanged(element, oldValue, newValue);

                    if (!element.Store.InUndoRedoOrRollback)
                    {
                        element.OnDefaultNamespaceChanged(oldValue, newValue);
                    }
                }
            }

            #endregion
        }
    }
    ```

## <a name="add-custom-code-for-the-tracking-property"></a>追跡プロパティのカスタム コードを追加する

`ExampleElement` ドメイン クラスに `CalculateNamespace` メソッドを追加する。

このメソッドを定義すると、`ExampleModel` の CustomElements 集計プロパティのロジックが提供されます。 このメソッドでは、ユーザーによって更新済み状態の Namespace 追跡プロパティを持つ `ExampleElement` ドメイン クラスの数をカウントし、モデル内の要素の総数の割合として、このカウントを表す文字列を返します。

また、`ExampleElement` ドメイン クラスの Namespace カスタム ストレージ プロパティのストレージを追加して、取得して設定するためのメソッドを追加します。

> [!NOTE]
> DSL ツールで `ExampleModel` 呼び出し用に生成するコードによって get および set メソッドが呼び出されますが、DSL ツールではメソッドを実装するコードを生成しません。

### <a name="to-add-the-method-for-the-custom-type-descriptor"></a>カスタム型記述子のメソッドを追加するには

1. NamespaceTrackingProperty.cs ファイルに次のコードを追加します。

    ```csharp
    using System;
    using Microsoft.VisualStudio.Modeling;

    namespace CompanyName.ProductName.TrackingPropertyDSL
    {
        // To the domain class that has the tracking property, add the caluclation
        // for when the property is tracking.
        public partial class ExampleElement
        {
            /// <summary>Calculates the actual value of the property when it is
            /// tracking.</summary>
            /// <returns>The value of the tracking property when it is
            /// tracking.</returns>
            /// <remarks>Making this method virtual allows child classes to modify
            /// the calculation. This method does not need to perform validation, as
            /// its caller handles validation prior to calling this method.
            /// <para>In this case, the tracking value depends on the default namespace
            /// property of the parent model.</para></remarks>
            protected virtual string CalculateNamespace()
            {
                return this.ExampleModel.DefaultNamespace;
            }

            #region Tracking property implementation

            // Implement the Namespace domain property of the ExampleElement domain class,
            // and update the IsNamespaceTracking domain property value handler.

            /// <summary>Storage for the Namespace property.</summary>
            private string namespaceStorage;

            /// <summary>Gets the value of the Namespace property.</summary>
            /// <returns>The value of the Namespace property.</returns>
            private string GetNamespaceValue()
            {
                // Only retrieve the tracked value if the store is not in the
                // middle of a serialization transaction.
                bool loading = this.Store.TransactionManager.InTransaction
                    && this.Store.TransactionManager.CurrentTransaction.IsSerializing;

                if (!loading && this.IsNamespaceTracking)
                {
                    try
                    {
                        return this.CalculateNamespace();
                    }
                    catch (NullReferenceException)
                    {
                        return default(string);
                    }
                    catch (Exception e)
                    {
                        if (CriticalException.IsCriticalException(e))
                        {
                            throw;
                        }
                        else
                        {
                            return default(string);
                        }
                    }
                }

                return namespaceStorage;
            }

            /// <summary>Sets the value of the Namespace property.</summary>
            /// <param name="value">The new value for the property.</param>
            private void SetNamespaceValue(string value)
            {
                namespaceStorage = value;

                // Only update the state of the tracking property if the store is
                // not in the middle of a serialization transaction.
                bool loading = this.Store.TransactionManager.InTransaction
                    && this.Store.TransactionManager.CurrentTransaction.IsSerializing;

                if (!this.Store.InUndoRedoOrRollback && !loading)
                {
                    this.IsNamespaceTracking = false;
                }
            }

            // Update the default behavior of the ExampleElement.IsNamespaceTracking
            // domain property value handler.
            internal sealed partial class IsNamespaceTrackingPropertyHandler
            {
                /// <summary>Called after the IsNamespaceTracking property changes.
                /// </summary>
                /// <param name="element">The model element that has the property
                /// that changed.</param>
                /// <param name="oldValue">The previous value of the property.
                /// </param>
                /// <param name="newValue">The new value of the property.</param>
                protected override void OnValueChanged(
                    ExampleElement element, Boolean oldValue, Boolean newValue)
                {
                    base.OnValueChanged(element, oldValue, newValue);
                    if (!element.Store.InUndoRedoOrRollback && newValue)
                    {
                        DomainPropertyInfo propInfo =
                            element.Store.DomainDataDirectory.GetDomainProperty(
                                ExampleElement.NamespaceDomainPropertyId);
                        propInfo.NotifyValueChange(element);
                    }
                }

                /// <summary>Performs the reset operation for the IsNamespaceTracking
                /// property for a model element.</summary>
                /// <param name="element">The model element that has the property
                /// to reset.</param>
                internal void ResetValue(ExampleElement element)
                {
                    object calculatedValue = null;

                    try
                    {
                        calculatedValue = element.CalculateNamespace();
                    }
                    catch (NullReferenceException)
                    {
                    }
                    catch (System.Exception e)
                    {
                        if (CriticalException.IsCriticalException(e))
                        {
                            throw;
                        }
                    }

                    if ((calculatedValue != null
                        && object.Equals(element.Namespace, calculatedValue)))
                    {
                        element.isNamespaceTrackingPropertyStorage = true;
                    }
                }

                /// <summary>Method to set IsNamespaceTracking to false so that this
                /// instance of this tracking property is not storage-based.
                /// </summary>
                /// <param name="element">The element on which to reset the property
                /// value.</param>
                internal void PreResetValue(ExampleElement element)
                {
                    // Force the IsNamespaceTracking property to false so that the value
                    // of the Namespace property is retrieved from storage.
                    element.isNamespaceTrackingPropertyStorage = false;
                }
            }

            #endregion
        }
    }
    ```

## <a name="add-custom-code-to-support-serialization"></a>シリアル化をサポートするカスタム コードを追加する

XML シリアル化のカスタムの読み込み後動作をサポートするコードを追加します。

> [!NOTE]
> DSL ツールで生成されるコードによって `OnPostLoadModel` および `OnPostLoadModelAndDiagram` メソッドが呼び出されますが DSL ツールでは、これらのメソッドを実装するコードを生成しません。

### <a name="to-add-code-to-support-the-custom-post-load-behavior"></a>カスタムの読み込み後の動作をサポートするコードを追加するには

1. Serialization.cs ファイルに次のコードを追加します。

    ```csharp
    using System;
    using System.Diagnostics;
    using Microsoft.VisualStudio.Modeling;

    namespace CompanyName.ProductName.TrackingPropertyDSL
    {
        #region Helper classes for maintaining state while the store is serializing.

        public abstract partial class TrackingPropertyDSLSerializationHelperBase
        {
            /// <summary>Reset the tracking state properties to their natural values
            /// based on comparing storage with calculation.</summary>
            /// <param name="store">The store that contains this model.</param>
            internal static void ResetTrackingProperties(Store store)
            {
                // Two passes required - one to set all elements to storage-based
                // then another to set some back to being tracking.
                foreach (ModelElement element in store.ElementDirectory.AllElements)
                {
                    ExampleElement myElementInstance = element as ExampleElement;
                    if (myElementInstance != null)
                    {
                        myElementInstance.PreResetIsTrackingProperties();
                        continue;
                    }
                }
                foreach (ModelElement element in store.ElementDirectory.AllElements)
                {
                    ExampleElement myElementInstance = element as ExampleElement;
                    if (myElementInstance != null)
                    {
                        myElementInstance.ResetIsTrackingProperties();
                        continue;
                    }
                }
            }
        }

        // Add the pre-reset and reset methods for the model element.
        public partial class ExampleElement
        {
            /// <summary>Calls the pre-reset method on the associated property value
            /// handler for each tracking property of this model element.</summary>
            internal virtual void PreResetIsTrackingProperties()
            {
                ExampleElement.IsNamespaceTrackingPropertyHandler.Instance.PreResetValue(this);
            }

            /// <summary>Calls the reset method on the associated property value
            /// handler for each tracking property of this model element.</summary>
            internal virtual void ResetIsTrackingProperties()
            {
                ExampleElement.IsNamespaceTrackingPropertyHandler.Instance.ResetValue(this);
            }
        }

        #endregion

        #region Custom serialization code

        // To the serialization helper for the TrackingPropertyDSL class, add post
        // load handlers to bind the tracking property to the serialization process.
        // These handlers manage the tracking states and property values when the
        // model is serialized and deserialized.
        public partial class TrackingPropertyDSLSerializationHelperBase
        {
            /// <summary>Customize model loading.</summary>
            /// <param name="serializationResult">The serialization result from the
            /// load operation.</param>
            /// <param name="partition">The partition in which the new
            /// instance was created.</param>
            /// <param name="fileName">The name of the file from which the
            /// instance was deserialized.</param>
            /// <param name="modelRoot">The root of the file that was loaded.
            /// </param>
            private void OnPostLoadModel(
                SerializationResult serializationResult,
                Partition partition,
                string fileName,
                ExampleModel modelRoot)
            {
            }

            /// <summary>Customize model and diagram loading.</summary>
            /// <param name="serializationResult">Stores serialization result from
            /// the load operation.</param>
            /// <param name="modelPartition">Partition in which the new
            /// instance will be created.</param>
            /// <param name="modelFileName">Name of the file from which the
            /// instance will be deserialized.</param>
            /// <param name="diagramPartition">Partition in which the new
            /// diagram instance will be created.</param>
            /// <param name="diagramFileName">Name of the file from which the
            /// diagram instance will be deserialized.</param>
            /// <param name="modelRoot">The root of the file that was loaded.</param>
            /// <param name="diagram">The diagram matching the modelRoot.</param>
            private void OnPostLoadModelAndDiagram(
                SerializationResult serializationResult,
                Partition modelPartition,
                string modelFileName,
                Partition diagramPartition,
                string diagramFileName,
                ExampleModel modelRoot,
                TrackingPropertyDSLDiagram diagram)
            {
                Debug.Assert(modelPartition != null);
                Debug.Assert(modelPartition.Store != null);

                // Tracking properties need to be set up according to whether the
                // serialization matches the calculated values.
                TrackingPropertyDSLSerializationHelperBase.ResetTrackingProperties(
                    modelPartition.Store);
            }
        }

        #endregion
    }
    ```

## <a name="test-the-language"></a>言語をテストする

次の手順では、追跡プロパティが正常に機能していることを確認できるように、[!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] の新しいインスタンスで DSL デザイナーをビルドして実行します。

1. **[ビルド]** メニューで、 **[ソリューションのリビルド]** をクリックします。

2. **[デバッグ]** メニューの **[デバッグの開始]** をクリックします。

    [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] の試験的ビルドでは、空のテスト ファイルを含む **デバッグ** ソリューションが開きます。

3. **ソリューション エクスプローラー** で、Test.trackingPropertyDsl ファイルをダブルクリックしてデザイナーで開き、デザイン サーフェイスをクリックします。

    ダイアグラムの **[プロパティ]** ウィンドウでは、 **[既定の名前空間]** プロパティは **[DefaultNamespace]** であり、 **[カスタム要素]** プロパティは **[0/0]** であることに注目してください。

4. **[ツールボックス]** から **ExampleElement** 要素をダイアグラム サーフェイスにドラッグします。

5. 要素の **[プロパティ]** ウィンドウで、 **[要素の名前空間]** プロパティを選択し、値を **[DefaultNamespace]** から **[OtherNamespace]** に変更します。

    **[要素の名前空間]** の値が太字で表示されるようになったことに注目してください。

6. **[プロパティ]** ウィンドウで、 **[要素の名前空間]** を右クリックし、 **[リセット]** をクリックします。

    プロパティの値が **[DefaultNamespace]** に変更され、値が通常のフォントで表示されます。

    **[要素の名前空間]** をもう一度右クリックします。 プロパティは現在追跡状態であるため、**Reset** コマンドは無効になりました。

7. 別の **ExampleElement** を **[ツールボックス]** からダイアグラム サーフェイスにドラッグし、その **[要素の名前空間]** を **[OtherNamespace]** に変更します。

8. デザイン サーフェイスをクリックします。

    ダイアグラムの **[プロパティ]** ウィンドウで、 **[カスタム要素]** の値が **[1/2]** になりました。

9. ダイアグラムの **[既定の名前空間]** を **[DefaultNamespace]** から **[NewNamespace]** に変更します。

     最初の要素の **[名前空間]** では、 **[既定の名前空間]** プロパティを追跡します。一方、2 番目の要素の **[名前空間]** では、 **[OtherNamespace]** のユーザーが更新した値が保持されます。

10. ソリューションを保存し、試験的ビルドを閉じます。

## <a name="next-steps"></a>次のステップ

複数の追跡プロパティを使用する場合、または複数の DSL で追跡プロパティを実装する場合は、各追跡プロパティをサポートするための共通コードを生成するテキスト テンプレートを作成できます。 テキスト テンプレートの詳細については、「[コード生成と T4 テキスト テンプレート](../modeling/code-generation-and-t4-text-templates.md)」を参照してください。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Modeling.Design.TrackingPropertyDescriptor>
- <xref:Microsoft.VisualStudio.Modeling.Design.ElementTypeDescriptor>
- [方法: ドメイン固有言語を定義する](../modeling/how-to-define-a-domain-specific-language.md)
- [方法: ドメイン固有言語ソリューションを作成する](../modeling/how-to-create-a-domain-specific-language-solution.md)