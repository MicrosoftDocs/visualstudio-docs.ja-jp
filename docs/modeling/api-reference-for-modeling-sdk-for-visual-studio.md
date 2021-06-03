---
title: Modeling SDK の API リファレンス
description: Visual Studio Visualization and Modeling SDK によって、ドメイン固有言語 (DSL) ツールがビルドされるプラットフォームがどのように提供されるかについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b9393c8e01cb304b6a89ac9b400f3efc29d8c056
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99861914"
---
# <a name="api-reference-for-modeling-sdk-for-visual-studio"></a>Modeling SDK for Visual Studio の API リファレンス

Visual Studio Visualization and Modeling SDK によって、ドメイン固有言語 (DSL) ツールがビルドされるプラットフォームが提供されます。

このセクションには、名前が "Microsoft.VisualStudio.Modeling" で始まる名前空間の参照資料が含まれています。

|名前空間|Content|
|-|-|
|<xref:Microsoft.VisualStudio.Modeling?displayProperty=fullName>|ModelElement などのクラス。DSL で定義するすべてのドメイン クラスの基本クラスです。|
|<xref:Microsoft.VisualStudio.Modeling.Design?displayProperty=fullName>|DSL 定義の一部を形成するクラス。|
|<xref:Microsoft.VisualStudio.Modeling.Diagnostics?displayProperty=fullName>|モデル ストア ビューアーとパフォーマンス測定ツール。|
|<xref:Microsoft.VisualStudio.Modeling.Diagrams?displayProperty=fullName>|ShapeElement などのクラス。DSL で定義するすべてのシェイプの基本クラスです。|
|<xref:Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement?displayProperty=fullName>|ジェスチャと選択のメソッド。|
|<xref:Microsoft.VisualStudio.Modeling.DslDefinition?displayProperty=fullName>|DSL 定義デザイナーの API。|
|<xref:Microsoft.VisualStudio.Modeling.DslDefinition.Design?displayProperty=fullName>|DSL 定義デザイナーの内部クラス。|
|<xref:Microsoft.VisualStudio.Modeling.DslDefinition.ExtensionEnablement?displayProperty=fullName>|コマンド、ジェスチャ、検証を使用して DSL デザイナーを拡張できる属性。|
|<xref:Microsoft.VisualStudio.Modeling.Extensibility?displayProperty=fullName>|DSL 拡張性を実装する ModelElement の拡張メソッド。|
|<xref:Microsoft.VisualStudio.Modeling.ExtensionEnablement?displayProperty=fullName>|拡張性属性|
|<xref:Microsoft.VisualStudio.Modeling.Immutability?displayProperty=fullName>|モデルの一部を読み取り専用にすることができます。|
|[Microsoft.VisualStudio.Modeling.Integration](/previous-versions/ee904412(v=vs.140))|Modelbus API。さまざまなモデルを統合するのに役立ちます。|
|[Microsoft.VisualStudio.Modeling.Integration.Picker](/previous-versions/ee904394(v=vs.140))|ユーザーがモデルおよび要素に移動して Modelbus 参照を作成できるダイアログ ボックス。|
|`Microsoft.VisualStudio.Modeling.Integration.Picker.Hosting`|ピッカー サービス。|
|[Microsoft.VisualStudio.Modeling.Integration.Shell](/previous-versions/ee869435(v=vs.140))|Visual Studio の Modelbus アダプター フレームワーク。|
|[Microsoft.VisualStudio.Modeling.Integration.Shell.Picker](/previous-versions/ee886769(v=vs.140))|ユーザーがモデルおよび要素に移動して Modelbus 参照を作成できるピッカー ダイアログ ボックス。|
|<xref:Microsoft.VisualStudio.Modeling.Shell?displayProperty=fullName>|DSL と Visual Studio の間のインターフェイス。|
|<xref:Microsoft.VisualStudio.Modeling.Shell.ExtensionEnablement?displayProperty=fullName>|ショートカット (コンテキスト) メニュー コマンドを定義できます。|
|<xref:Microsoft.VisualStudio.Modeling.Validation?displayProperty=fullName>|検証制約を定義できます。|

## <a name="see-also"></a>関連項目

- [T4 テキスト変換のカスタマイズ](../modeling/customizing-t4-text-transformation.md)
