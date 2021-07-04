---
title: クラス デザイナーの使用
description: Visual Studio のクラス デザイナーを使用して、コード内のクラスとその他の型をデザイン、視覚化、およびリファクターする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 05/08/2018
ms.topic: conceptual
f1_keywords:
- vs.classdesigner.diagram
- vs.classdesigner.enum
helpviewer_keywords:
- Class Designer [Visual Studio]
- Class Designer, about Class Designer
- types [Visual Studio], viewing
- classes [Visual Studio], viewing
- class designer
ms.assetid: 40ed2c9d-0ce0-4b95-ad78-5dec2065ccea
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 85921343ac52c066735d607ce32635e953cf2e6a
ms.sourcegitcommit: 4908561809ad397c99cf204f52d5e779512e502c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112254788"
---
# <a name="design-and-view-classes-and-types-with-class-designer"></a>クラス デザイナーを使用したクラスと型の設計と表示

Visual Studio の **クラス デザイナー** では、コード内のクラスとその他の型をデザイン、視覚化、およびリファクターできます。 C#、Visual Basic、または C++ プロジェクト内にあるクラスを作成および編集するには、クラス ダイアグラムを使用します。 クラス ダイアグラムを使用すると、プロジェクト構造をより深く理解したり、コードを再編成したりすることもできます。

>[!NOTE]
>クラス デザイナーは .NET Core プロジェクトで使用できません。

## <a name="what-you-can-do-with-class-diagrams"></a>クラス ダイアグラムでできること

- **デザイン**: クラス ダイアグラムを編集することによって、プロジェクトのコードを編集します。 新しい要素を追加し、不要な要素を削除します。 変更はコードに反映されます。

- **視覚化**: プロジェクト内のクラスをダイアグラムに表示して、プロジェクトの構造を理解します。 プロジェクトの中で最も重要な部分に集中できるように、ダイアグラムをカスタマイズします。 ダイアグラムを保存すると、後からデモやドキュメントに使用できます。

- **リファクター**: メソッドのオーバーライド、識別子の名前変更、パラメーターのリファクター、およびインターフェイスと抽象クラスの実装を行います。

## <a name="view-types-and-relationships"></a>型およびリレーションシップの表示

クラス ダイアグラムは、型の構成メンバーとそれらの関係など、型の詳細情報を表示します。 これらのエンティティの視覚化はコードの動的ビューです。 つまり、デザイナーで型を編集し、エンティティのソース コードで、反映された編集内容を確認できます。 同様に、クラス ダイアグラムの同期が維持され、コード ファイルに加えられた変更が反映されます。

> [!NOTE]
> プロジェクトにクラス ダイアグラムが含まれ、プロジェクトが別のプロジェクト内の型を参照している場合、その型のプロジェクトをビルドするまで、クラス ダイアグラムに参照された型は表示されません。 同様に、外部エンティティのコードに加えられた場合、そのエンティティのプロジェクトをリビルドするまで、変更内容はダイアグラムに表示されません。

## <a name="class-diagram-workflow"></a>クラス ダイアグラム ワークフロー

クラス ダイアグラムは、プロジェクトのクラス構造を解釈するのに役立ちます。 これらのプロジェクトは、他の開発者によって作成されているか、または自分で作成したプロジェクトを更新する必要があります。 クラス ダイアグラムを使用すると、プロジェクト情報をカスタマイズして、開発者間で共有および提供できます。

プロジェクト情報を提供するには、まずその情報を表示するためのクラス ダイアグラムを作成します。 詳細については、[クラス ダイアグラムの追加](how-to-add-class-diagrams-to-projects.md)に関するページを参照してください。 プロジェクトのクラス ダイアグラムを複数作成し、それらを使用して、プロジェクト自体のビュー、プロジェクトの型の特定のサブセット、または型のメンバーの特定のサブセットを表示できます。

各クラス ダイアグラムに表示する内容を定義するだけでなく、情報の提供方法を変更することもできます。詳細については、「[方法: クラス ダイアグラムをカスタマイズする](how-to-customize-class-diagrams.md)」を参照してください。

1 つまたは複数のクラス ダイアグラムを微調整した後、それらを Microsoft Office ドキュメント内にコピーして印刷したり、画像ファイルとしてエクスポートしたりできます。 詳細については、「[方法: Microsoft Office ドキュメントにクラス ダイアグラムの要素をコピーする](how-to-copy-class-diagram-elements-to-a-microsoft-office-document.md)」、「[方法: クラス ダイアグラムを印刷する](how-to-print-class-diagrams.md)」、「[方法: クラス ダイアグラムをイメージとしてエクスポートする](how-to-export-class-diagrams-as-images.md)」を参照してください。

> [!NOTE]
> クラス デザイナーはソース ファイルの場所を追跡しないので、プロジェクト構造を変更したり、プロジェクト内のソース ファイルを移動したりすると、クラス デザイナーが、特に typedef のソース型、基本クラス、またはアソシエーション型を追跡できなくなる場合があります。 **クラス デザイナーはこの型を表示できません** などのエラーが表示されることがあります。 エラーが発生した場合は、変更または再配置したソース コードをもう一度クラス ダイアグラムにドラッグして再表示します。

## <a name="see-also"></a>関連項目

- [コード エディターの機能](../writing-code-in-the-code-and-text-editor.md)
- [ソリューション間の依存関係をマップする](../../modeling/map-dependencies-across-your-solutions.md)
