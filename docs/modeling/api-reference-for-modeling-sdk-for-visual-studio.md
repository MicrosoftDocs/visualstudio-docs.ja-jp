---
title: モデリング SDK の API リファレンス
ms.date: 11/04/2016
ms.topic: reference
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3915dc0ee7359c8fb0093f397542afb557d0796a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72654332"
---
# <a name="api-reference-for-modeling-sdk-for-visual-studio"></a>Modeling SDK for Visual Studio の API リファレンス

Visual Studio の視覚化およびモデリング SDK には、ドメイン固有言語 (DSL) ツールがビルドされるプラットフォームが用意されています。

このセクションには、名前が "VisualStudio" で始まる名前空間の参照資料が含まれています。

|Namespace|Content|
|-|-|
|<xref:Microsoft.VisualStudio.Modeling?displayProperty=fullName>|ModelElement などのクラス。 DSL で定義するすべてのドメインクラスの基本クラスです。|
|<xref:Microsoft.VisualStudio.Modeling.Design?displayProperty=fullName>|DSL 定義の一部を形成するクラス。|
|<xref:Microsoft.VisualStudio.Modeling.Diagnostics?displayProperty=fullName>|モデルストアビューアーとパフォーマンス測定ツール。|
|<xref:Microsoft.VisualStudio.Modeling.Diagrams?displayProperty=fullName>|[図形] 要素などのクラスは、DSL で定義したすべての図形の基本クラスです。|
|<xref:Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement?displayProperty=fullName>|ジェスチャと選択のメソッド。|
|<xref:Microsoft.VisualStudio.Modeling.DslDefinition?displayProperty=fullName>|DSL 定義デザイナーの API。|
|<xref:Microsoft.VisualStudio.Modeling.DslDefinition.Design?displayProperty=fullName>|DSL 定義デザイナーの内部クラス。|
|<xref:Microsoft.VisualStudio.Modeling.DslDefinition.ExtensionEnablement?displayProperty=fullName>|コマンド、ジェスチャ、および検証を使用して DSL デザイナーを拡張できる属性。|
|<xref:Microsoft.VisualStudio.Modeling.Extensibility?displayProperty=fullName>|DSL 拡張を実装する ModelElement の拡張メソッド。|
|<xref:Microsoft.VisualStudio.Modeling.ExtensionEnablement?displayProperty=fullName>|拡張属性|
|<xref:Microsoft.VisualStudio.Modeling.Immutability?displayProperty=fullName>|モデルの一部を読み取り専用にすることができます。|
|[VisualStudio の統合](/previous-versions/ee904412(v=vs.140))|Modelbus API。さまざまなモデルを統合するのに役立ちます。|
|[VisualStudio を選択します。](/previous-versions/ee904394(v=vs.140))|ユーザーがモデルおよび要素に移動して Modelbus 参照を作成できるダイアログボックス。|
|`Microsoft.VisualStudio.Modeling.Integration.Picker.Hosting`|ピッカーサービス。|
|[VisualStudio を作成します。](/previous-versions/ee869435(v=vs.140))|Visual Studio の modelbus アダプターフレームワーク。|
|[VisualStudio を選択してください。](/previous-versions/ee886769(v=vs.140))|ユーザーがモデルと要素に移動して Modelbus 参照を作成できるようにする [ピッカー] ダイアログボックス。|
|<xref:Microsoft.VisualStudio.Modeling.Shell?displayProperty=fullName>|Dsl と Visual Studio の間のインターフェイス。|
|<xref:Microsoft.VisualStudio.Modeling.Shell.ExtensionEnablement?displayProperty=fullName>|ショートカット (コンテキスト) メニューコマンドを定義できます。|
|<xref:Microsoft.VisualStudio.Modeling.Validation?displayProperty=fullName>|検証制約を定義できます。|

## <a name="see-also"></a>参照

- [T4 テキスト変換のカスタマイズ](../modeling/customizing-t4-text-transformation.md)
