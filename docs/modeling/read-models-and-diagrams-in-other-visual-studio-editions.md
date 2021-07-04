---
title: Visual Studio の他のエディションでモデルおよびダイアグラムを読み取る
description: Visual Studio でのモデルと図の読み取り、およびモデルの作成をサポートしていない Visual Studio のバージョンを使用する場合の読み取り専用の動作について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- models, versions of Visual Studio
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 95fbf6451a3f07581ff2bdb098428f41904d4276
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112389905"
---
# <a name="read-models-and-diagrams-in-other-visual-studio-editions"></a>Visual Studio の他のエディションでモデルおよびダイアグラムを読み取る

モデルの作成をサポートしていないバージョンの Visual Studio でモデルを開くと、モデルは読み取り専用モードで開きます。 このモードでは、ダイアグラムのレイアウトは変更できますが、モデルは変更できません。

モデルの作成をサポートする Visual Studio のバージョンを確認するには、[アーキテクチャおよびモデリング ツールのバージョン サポートに関する記事](../modeling/analyze-and-model-your-architecture.md#VersionSupport)をご覧ください。

## <a name="obtaining-access-to-a-model-and-diagrams"></a>モデルおよび図へのアクセス

依存関係図を読み取るには、最初に Visual Studio を使用してモデリング プロジェクトを開いてから、その中で図を開く必要があります。

このため、依存関係図を読み取る場合は、その図を生成したモデリング プロジェクトにもアクセスできる必要があります。 これを行うには、ソース管理からプロジェクトにアクセスするか、プロジェクト ファイルのコピーを取得します。

> [!NOTE]
> これは、コードから生成されたコード マップおよび .NET クラス図には適用されません。 これらの図はモデリング プロジェクトとは関係なく表示できます。

依存関係図を読み取るために最低限必要なファイル セットは次のとおりです。

- 読み取る図の 2 つの図ファイル (たとえば、**MyDiagram.classdiagram と MyDiagram.classdiagram.layout**)。

    > [!NOTE]
    > 依存関係図の場合は、_Mydiagram_ **.layerdiagram.suppressions** という名前のファイルも必要です。

- モデリング プロジェクト ファイル (**Mymodel. modelproj**)

- ルート モデル ファイル (**ModelDefinition\MyModel.uml**)

- 図で参照されているすべてのパッケージのパッケージ ファイル (**ModelDefinition\MyPackage.uml**)

## <a name="changes-that-you-can-make-in-read-only-mode"></a>読み取り専用モードで行える変更

モデルの作成をサポートしていないバージョンの Visual Studio でモデルおよびその図を開く場合、モデルは変更できません。 つまり、図またはモデル エクスプローラーに表示されている要素と関係は変更できません。 ただし、図のレイアウトに次のような変更を加えることはできます:

- 図形およびコネクタを図に再配置する。

- 図形を展開および折りたたむ。

これらの変更は保存できます。 他のユーザーが変更内容を表示できるようにするには、少なくとも更新した **.layout** ファイルを送信する必要があります。

## <a name="see-also"></a>関連項目

- [依存関係図: リファレンス](../modeling/layer-diagrams-reference.md)
- [アプリのモデルを生成する](../modeling/create-models-for-your-app.md)
