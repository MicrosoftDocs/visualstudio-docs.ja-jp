---
title: DSL ライブラリによる DSL 間でのクラスの共有
description: Visual Studio Visualization and Modeling SDK で、別の DSL にインポートできる不完全な DSL 定義を作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 61e4785ab99ecccc61a097dd27140e250f103de2
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99899813"
---
# <a name="sharing-classes-between-dsls-by-using-a-dsl-library"></a>DSL ライブラリによる DSL 間でのクラスの共有
Visual Studio Visualization and Modeling SDK では、別の DSL にインポートできる不完全な DSL 定義を作成できます。 これにより、類似するモデルの共通部分を考慮することができます。

## <a name="creating-and-using-dsl-libraries"></a>DSL ライブラリの作成と使用

#### <a name="to-create-a-dsl-library"></a>DSL ライブラリを作成するには

1. 新しい DSL プロジェクトを作成し、DSL ライブラリ ソリューション テンプレートを選択します。

     空のモデルを使用して、単一の DSL プロジェクトが作成されます。

2. ドメイン クラス、リレーションシップ、シェイプなどを追加できます。

     ライブラリ内の要素は、1 つの埋め込みツリーを形成している必要はありません。

     インポートするときに使用できるリレーションシップを定義するには、2 つのドメイン クラスを作成し、それらの間にリレーションシップを作成します。

     ドメイン クラスの **継承修飾子** を `Abstract` に設定することを検討します。

3. DSL エクスプローラーで定義した要素 (接続ビルダーなど) を追加できます。

4. 検証制約など、追加のコードを必要とするカスタマイズを追加することができます。

5. **[すべてのテンプレートの変換]** をクリックします。

6. プロジェクトをビルドします。

7. 他のユーザーが使用できるように DSL を配布するときは、コンパイル済みのアセンブリ (DLL) と `DslDefinition.dsl` ファイルの両方を提供する必要があります。 コンパイル済みのアセンブリは、`Dsl\bin\*` の下のフォルダーにあります

#### <a name="to-import-a-dsl-library"></a>DSL ライブラリをインポートするには

1. 別の DSL 定義の **DSL エクスプローラー** で、DSL のルート クラスを右クリックし、 **[Add New DslLibrary Import]\(新しい Dsllibrary インポートの追加\)** をクリックします。

2. プロパティ ウィンドウで、ライブラリの **[ファイル パス]** を設定します。 相対パスと絶対パスのどちらかを使用することができます。

    インポートしたライブラリは、DSL エクスプローラーに読み取り専用モードで表示されます。

3. インポートしたクラスを基底クラスとして使用できます。 インポートする DSL でドメイン クラスを作成し、プロパティ ウィンドウで、 **[基底クラス]** をインポートしたクラスに設定します。

4. [すべてのテンプレートの変換] をクリックします。

5. DSL ライブラリ プロジェクトによってビルドされたアセンブリ (DLL) への参照を、DSL プロジェクトに追加します。

6. ソリューションをビルドします。

   DSL ライブラリで、他のライブラリをインポートすることができます。 ライブラリをインポートすると、そのインポートも DSL エクスプローラーに自動的に表示されます。

## <a name="see-also"></a>こちらもご覧ください

- [方法: ドメイン固有言語を定義する](../modeling/how-to-define-a-domain-specific-language.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
