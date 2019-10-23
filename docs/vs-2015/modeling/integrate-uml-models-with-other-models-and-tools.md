---
title: UML モデルを他のモデルおよびツールと統合する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML - extending, references to models
ms.assetid: 9e75e7d1-93cf-4196-baa3-bd10b9af16d3
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 2f511a96f94ab98a93144938529a05d07bb6ed26
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72669577"
---
# <a name="integrate-uml-models-with-other-models-and-tools"></a>UML モデルを他のモデルおよびツールと統合する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

UML モデルは、他のモデルやドメイン固有の言語に統合することができます。

 さまざまな機能を実行する拡張機能のコードを記述して、次の方法でモデルを統合できます。

 任意の要素からの参照を、ファイルなどの他の項目、または他のモデル内の要素にアタッチします。
UML 要素の場合、他の UML 要素、ファイル、またはその他のオブジェクトへのリンクを格納するために、それらの身元を文字列としてエンコードすることができます。

 たとえば、UML アクション (つまり、アクティビティ図の要素) を別のアクティビティ図にリンクできる拡張機能を記述することができます。 ユーザーがアクションをダブルクリックすると、別のアクティビティ図が表示されます。 これでユーザーは、アクションに関する詳細なビューを提供できます。

 文字列やその他のデータを要素に格納するには、次の 2 つの方法があります。

- **ステレオタイプのプロパティ。** UML プロファイルを定義し、その中で定義するステレオタイプを使って、指定する種類の UML 要素にプロパティを追加できます。 たとえば、**詳細**という名前のプロパティを UML アクションに追加するプロファイルを定義できます。 ステレオタイプをアクションに適用してからリンク データをプロパティに格納することで、データをアクションに格納する拡張機能のコードを記述することができます。

   ステレオタイプとそのプロパティは、[プロパティ] ウィンドウでユーザーが表示することができます。

   この拡張機能を配置するには、プロファイル定義と拡張機能のコードを 1 つの [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 拡張機能にパッケージ化します。

   詳細については、「プロファイルを定義して[UML を拡張する](../modeling/define-a-profile-to-extend-uml.md)」を参照してください。

   メニューコマンドおよびジェスチャハンドラーと共にプロファイルが配置されるサンプルプロジェクトについては、「[サンプル: UML プロファイル](http://go.microsoft.com/fwlink/?LinkID=213811)」を参照してください。

- **形式.** 一連の文字列を任意の UML 要素にアタッチできます。 ファイル名や別の要素の GUID などの情報を格納するコードを記述することもできます。 これは、追加の定義を行わなくても行えます。 参照は、ユーザーには直接表示されません。

   詳細については、「 [UML モデル要素に参照文字列をアタッチする](../modeling/attach-reference-strings-to-uml-model-elements.md)」を参照してください。 サンプルについては、「 [UML 要素を図またはその他のファイルにリンクする](http://go.microsoft.com/fwlink/?LinkId=213813)」を参照してください。

  参照をモデル要素にエンコードするには次の 2 つの方法があります。

- ターゲットモデル要素の**GUID とファイル名**、およびターゲットモデル要素を含むモデル、またはそれを表示する特定の図。

   例については、「 [UML 要素を図またはその他のファイルにリンクする](http://go.microsoft.com/fwlink/?LinkId=213813)」を参照してください。

- **ModelBus 参照。** ModelBus は、モデル間の参照を作成および解決するためのフレームワークです。 これには、モデル内の要素をユーザーが選択できるようにする ModelBus ピッカーが含まれます。 これは、対象のモデルに変更があったために失われた参照をユーザーが解決するのにも役立ちます。

   詳細については、「 [Visual Studio Modelbus を使用](../modeling/integrating-models-by-using-visual-studio-modelbus.md)したモデルの統合」を参照してください。

  1 つのモデルから別のモデルに変更を反映します。
  たとえば、1 つの要素の名前をリンクされた図の名前と同期させると、一方がユーザーによって変更されると他方も変更されるようになります。 これを行うための次の 2 つのメカニズムがあります。

1. **Vmsdk ルール**を使用して、同じモデル内の変更を反映することができます。

    例については、「 [UML 要素を図またはその他のファイルにリンクする](http://go.microsoft.com/fwlink/?LinkId=213813)」を参照してください。

2. **Vmsdk イベント**を使用して、モデルの外部の変更を反映することができます。たとえば、リンクドキュメントのファイル名を変更したり、別のモデルの要素を変更したりできます。

   これらのメカニズムの詳細については、「[方法: UML モデルの変更に対応する](../misc/how-to-respond-to-changes-in-a-uml-model.md)」を参照してください。

   要素をドラッグして1つのモデルから別のモデルにコピーするには、ユーザーが UML 図に項目をドラッグして要素を作成できるようにします。 作成した要素は、オリジナルのコピーである必要はありません。 たとえば、ソリューション エクスプローラーからアクティビティ図を別のアクティビティ図にドラッグして新しいアクションを作成する機能をユーザーに提供することができます。

   詳細については、「[モデリング図でのジェスチャハンドラーの定義](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md)」および「[方法: ドラッグアンドドロップハンドラーを追加する](../modeling/how-to-add-a-drag-and-drop-handler.md)」を参照してください。

## <a name="samples"></a>サンプル
 [UML 要素を図またはその他のファイルにリンクする](http://go.microsoft.com/fwlink/?LinkId=213813)コードサンプルを参照してください。 このサンプルを使用すると、ユーザーは任意の UML 要素にファイルをドラッグし、後でその要素をダブルクリックしてファイルを開くことができます。 たとえば、アクティビティ図を、ユースケース要素にリンクすることができます。 リンクが設定されている要素はアイコンで示されます。

 このコード サンプルでは、以下の技法を説明します。

- [UML モデル要素に参照文字列をアタッチする](../modeling/attach-reference-strings-to-uml-model-elements.md)

   このサンプル コードは、要素に関連付けられている参照文字列にファイル パスと要素 GUID を格納します。

- UML 要素にデコレータを追加する方法。 デコレーターに関する一般的な情報については、「[テキストフィールドおよびイメージフィールドのカスタマイズ](../modeling/customizing-text-and-image-fields.md)」を参照してください。

   サンプルは、UML 図形にイメージのデコレータを追加します。

- [方法: UML モデル内で変更に応答する](../misc/how-to-respond-to-changes-in-a-uml-model.md)

   このサンプルでは、図に表示される新しい図形に応答するルールを定義する方法を示します。

- [モデリング図にメニュー コマンドを定義する](../modeling/define-a-menu-command-on-a-modeling-diagram.md)

- [モデリング図にジェスチャ ハンドラーを定義する](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md)

   このサンプルでは、Windows エクスプローラー (またはエクスプローラー)、ソリューション エクスプローラー、およびその他の UML 要素からドラッグした項目を処理する方法について説明しています。

  DSL で UML モデルを読み取る例については、「[方法: ドラッグアンドドロップハンドラーを追加する](../modeling/how-to-add-a-drag-and-drop-handler.md)」を参照してください。

## <a name="see-also"></a>参照
 [モデリング図にメニューコマンドを定義](../modeling/define-a-menu-command-on-a-modeling-diagram.md)する[モデリング図にジェスチャハンドラーを定義](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md)する[方法: ドラッグアンドドロップハンドラーを追加](../modeling/how-to-add-a-drag-and-drop-handler.md)する方法: [uml モデルの変更に応答](../misc/how-to-respond-to-changes-in-a-uml-model.md)する[例: uml プロファイル](http://go.microsoft.com/fwlink/?LinkID=213811)[を uml 要素にリンクする図またはその他のファイル](http://go.microsoft.com/fwlink/?LinkId=213813)
