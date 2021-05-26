---
title: エディター内の Managed Extensibility Framework | Microsoft Docs
description: Visual Studio SDK のエディターを拡張するための独自のコンポーネントを作成できる、Managed Extensibility Framework について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - using MEF for extensions
ms.assetid: 3f59a285-6c33-4ae3-a4fb-ec1f5aa21bd1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 881b0f4d112b7739ff33099b26a30ab073f55924
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073171"
---
# <a name="managed-extensibility-framework-in-the-editor"></a>エディター内の Managed Extensibility Framework
エディターは、Managed Extensibility Framework (MEF) コンポーネントを使用して作成されます。 エディターを拡張するために独自の MEF コンポーネントを構築することができ、コードでエディター コンポーネントを使用することもできます。

## <a name="overview-of-the-managed-extensibility-framework"></a>Managed Extensibility Framework の概要
 MEF は、MEF プログラミング モデルに準拠するアプリケーションまたはコンポーネントの機能を追加および変更できる .NET ライブラリです。 Visual Studio エディターでは、MEF コンポーネント パーツの提供および使用の両方が可能です。

 MEF は .NET Framework バージョン 4 の *System.ComponentModel.Composition.dll* アセンブリに含まれています。

 MEF の詳細については、「[Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index)」を参照してださい。

### <a name="component-parts-and-composition-containers"></a>コンポーネント パーツと合成コンテナー
 コンポーネント パーツは、次のいずれかまたは両方の操作を実行できるクラスまたはクラスのメンバーです。

- 別のコンポーネントを使用する

- 別のコンポーネントによって使用される

  たとえば、倉庫の在庫コンポーネントによって提供される製品の購入可能性データに依存する注文入力コンポーネントを持つショッピング アプリケーションを考えてみます。 MEF 用語では、在庫部分で製品の購入可能性データを "*エクスポート*" でき、注文入力部分でデータを "*インポート*" できます。 注文入力部分と在庫部分は、相互に認識する必要がなく、(ホスト アプリケーションによって提供される) "*合成コンテナー*" によって一連のエクスポートを維持し、エクスポートとインポートを解決します。

  通常、合成コンテナー <xref:System.ComponentModel.Composition.Hosting.CompositionContainer> はホストによって所有されます。 合成コンテナーは、エクスポートされたコンポーネント パーツの "*カタログ*" を保持します。

### <a name="export-and-import-component-parts"></a>コンポーネント パーツのエクスポートとインポート
 パブリック クラスまたはクラスのパブリック メンバー (プロパティまたはメソッド) として実装されている限り、任意の機能をエクスポートできます。 コンポーネント パーツを <xref:System.ComponentModel.Composition.Primitives.ComposablePart> から派生させる必要はありません。 代わりに、エクスポートするクラスまたはクラス メンバーに <xref:System.ComponentModel.Composition.ExportAttribute> 属性を追加する必要があります。 この属性では、別のコンポーネント パーツが機能をインポートする際に使用する "*コントラクト*" を指定します。

### <a name="the-export-contract"></a>エクスポート コントラクト
 <xref:System.ComponentModel.Composition.ExportAttribute> では、エクスポートされるエンティティ (クラス、インターフェイス、または構造体) を定義します。 通常、エクスポート属性は、エクスポートの型を指定するパラメーターを受け取ります。

```
[Export(typeof(ContentTypeDefinition))]
class TestContentTypeDefinition : ContentTypeDefinition {   }
```

 既定では、<xref:System.ComponentModel.Composition.ExportAttribute> 属性ではエクスポートするクラスの型であるコントラクトを定義します。

```
[Export]
[Name("Structure")]
[Order(After = "Selection", Before = "Text")]
class TestAdornmentLayerDefinition : AdornmentLayerDefinition {   }
```

 この例では、既定の `[Export]` 属性は `[Export(typeof(TestAdornmentLayerDefinition))]` と同じです。

 次の例に示すように、プロパティまたはメソッドをエクスポートすることもできます。

```
[Export]
[Name("Scarlet")]
[Order(After = "Selection", Before = "Text")]
public AdornmentLayerDefinition scarletLayerDefinition;
```

### <a name="import-a-mef-export"></a>MEF エクスポートをインポートする
 MEF エクスポートを使用する場合は、エクスポートに使用したコントラクト (通常は型) を把握し、その値を持つ <xref:System.ComponentModel.Composition.ImportAttribute> 属性を追加する必要があります。 既定では、インポート属性は、変更するクラスの型である 1 つのパラメーターを受け取ります。 次のコード行では、<xref:Microsoft.VisualStudio.Text.Classification.IClassificationTypeRegistryService> 型をインポートします。

```
[Import]
internal IClassificationTypeRegistryService ClassificationRegistry;
```

## <a name="get-editor-functionality-from-a-mef-component-part"></a>MEF コンポーネント パーツからエディター機能を取得する
 既存のコードが MEF コンポーネント パーツである場合、MEF メタデータを使用してエディター コンポーネント パーツを使用できます。

#### <a name="to-consume-editor-functionality-from-a-mef-component-part"></a>MEF コンポーネント パーツからエディター機能を取得するには

1. グローバル アセンブリ キャッシュ (GAC) にある *System.Composition.ComponentModel.dll* およびエディター アセンブリへの参照を追加します。

2. 関連する using ディレクティブを追加します。

    ```
    using System.ComponentModel.Composition;
    using Microsoft.VisualStudio.Text;
    ```

3. 次のように、サービス インターフェイスに `[Import]` 属性を追加します。

    ```
    [Import]
    ITextBufferFactoryService textBufferService;
    ```

4. サービスを取得したら、そのコンポーネントのいずれかを使用できます。

5. アセンブリをコンパイルしたら、Visual Studio のインストールの *..\Common7\IDE\Components\* フォルダーにこれを配置します。

## <a name="see-also"></a>関連項目
- [言語サービスとエディターの拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)
