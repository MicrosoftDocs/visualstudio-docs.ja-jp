---
title: プロファイルとステレオタイプを使用してモデルをカスタマイズする |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML model, profiles
- UML model, stereotypes
- UML model, customizing
ms.assetid: fd607157-0d3a-4583-a84e-427a4b2a5acb
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4f83fcf3ea500e0640a226b80d3d3c0e2c7ed869
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72655098"
---
# <a name="customize-your-model-with-profiles-and-stereotypes"></a>プロファイルとステレオタイプを使用したモデルのカスタマイズ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio では、クラスやコンポーネントなどの標準の UML モデル要素を特定の目的に合わせてカスタマイズできます。 要素のプロパティリストを変更できるモデル要素に*ステレオタイプ*を適用できます。 ステレオタイプは、*プロファイル*と呼ばれるコレクション内で定義されます。

 この機能をサポートする Visual Studio のバージョンを確認するには、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

 ステレオタイプを使用するには、パッケージをプロファイルにリンクします。 これにより、プロファイルで定義されているステレオタイプをパッケージ内の要素に適用できます。 Visual Studio をインストールするときに、いくつかのプロファイルもインストールされます。 また、独自のプロファイルを定義できます。

 ステレオタイプは、要素のプロパティ リストで設定できます。 次の例に示すように、図のシェイプの主な種類については、適用されたステレオタイプもシェイプに表示されます。

 ![ステレオタイプを持つ UML クラス。](../modeling/media/uml-class-stereotype.png "UML_class_stereotype")

> [!NOTE]
> プロファイルを使用してモデルを生成し、そのモデルを他のユーザーと共有する場合、それぞれのコンピューターに同じプロファイルをインストールしなければ、ステレオタイプを表示できません。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[UML モデル要素にステレオタイプを追加する](../modeling/add-stereotypes-to-uml-model-elements.md)|モデル要素をパッケージ内に配置して、パッケージをプロファイルにリンクし、ステレオタイプを要素に適用します。|
|[UML モデルの標準ステレオタイプ](../modeling/standard-stereotypes-for-uml-models.md)|Visual Studio をインストールするときに、UML 標準プロファイル L2 および L3 がインストールされます。既定では、すべてのモデルがこれらのプロファイルにリンクされます。 これらのプロファイルによって、モデルに注釈を付けるために使用できるステレオタイプが提供されます。<br /><br /> たとえば、«specification» ステレオタイプをクラスに適用して、クラスの使用目的が、そのインスタンスの外部から見える動作の定義のみであることを示すことができます。|
|[プロファイルを定義して UML を拡張する](../modeling/define-a-profile-to-extend-uml.md)|独自のアプリケーション領域に適合した独自のステレオタイプとツールを定義できます。<br /><br /> たとえば、銀行業務ソフトウェアを開発する場合、クラスに適用できる «Account» ステレオタイプを定義できます。 これにより、クラス図を使用して複数の異なる種類の口座および口座間のリレーションシップを記述できます。|
|[UML プロファイルのインストール](../modeling/install-a-uml-profile.md)|他のユーザーから UML プロファイルを受け取った場合、それを自分のコンピューターにインストールできます。|
|[カスタム モデリング ツールボックス アイテムを定義する](../modeling/define-a-custom-modeling-toolbox-item.md)|カスタム ツールボックス項目を使用すると、新しい要素にステレオタイプを繰り返し設定する手間を省くことができます。|
|[ステレオタイプによる UML クラスの色の設定](http://code.msdn.microsoft.com/UML-Color-Classes-by-07de2b70)|このサンプル コードは、UML 図を拡張します。 要素のステレオタイプに従って、UML シェイプの色を自動的に設定します。|
