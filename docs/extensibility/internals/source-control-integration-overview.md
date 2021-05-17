---
title: ソース管理の統合の概要 | Microsoft Docs
description: ソース管理を Visual Studio に統合する 2 つの方法であるソース管理プラグインと VSPackage の違いについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], about source control
ms.assetid: 3a46e4eb-e677-49c3-8647-d927d035a19a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9feacd8e051b47b1fec6c3d3ad08e34e591fc57c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064320"
---
# <a name="source-control-integration-overview"></a>ソース管理の統合の概要
このセクションでは、ソース管理を Visual Studio に統合する 2 つの方法を比較します。1 つはソース管理プラグインです。もう 1 つは、ソース管理ソリューションを提供し、新しいソース管理機能を強調する VSPackage です。 Visual Studio では、ソース管理 VSPackage とソース管理プラグインを手動で切り替えることができ、ソリューションベースの自動切り替えも可能です。

## <a name="source-control-integration"></a>ソース管理の統合
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、2 種類のソース管理統合オプションをサポートしています。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のすべてのバージョンで、ソース管理プラグイン API (以前は MSSCCI API とも呼ばれていました) に基づいてプラグインを統合することが引き続き可能です。この API は基本的なソース管理機能を提供しますが、使用するのは Visual Studio のソース管理ユーザー インターフェイス (UI) です。 一方、ソース管理 VSPackage では、深部までの統合を実現する新しい [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] のパスが提供されます。このパスは、高いレベルの精緻化と自律性がソース管理モデルに要求されるソース管理統合に適しています。

 ![ソース管理の概要](../../extensibility/internals/media/sourcectnrloverview.gif "SourceCtnrlOverview")

## <a name="source-control-plug-in"></a>ソース管理プラグイン
 すべてのバージョンの Visual Studio で、ソース管理プラグイン API 仕様バージョン 1.2 が統合パスとしてサポートされています。 ソース管理プラグインの実装者は、[ソース管理プラグインの作成](../../extensibility/internals/creating-a-source-control-plug-in.md)に関するページで説明されているように、ソース管理の統合と登録のためのソース管理プラグイン API 関数を実装する DLL を記述します。 このアプローチでは、統合開発環境 (IDE) は、チェックイン、チェックアウト、ツール/オプションのプロパティ ページ、ツール バー、ソース管理グリフなどのダイアログ ボックスに、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の UI を使用します。 ソース管理プラグイン API に厳密に準拠することで、Visual Studio への容易な統合と、トラブルのないユーザー エクスペリエンスが保証されます。 これは、API で詳述されている関数とコールバックの大半をソース管理プラグインが実装しなければならないことを意味します。

 ソース管理プラグイン API を使用してソース管理プラグインを実装するには、次の手順を実行します。

1. [ソース管理プラグイン](../../extensibility/source-control-plug-ins.md)で指定された関数を実装する DLL を作成します。

2. 適切なレジストリ エントリを作成して DLL を登録します (「[方法: ソース管理プラグインをインストールする](../../extensibility/internals/how-to-install-a-source-control-plug-in.md)」で説明されています)。

3. ヘルパー UI を作成し、(ソース管理プラグインを介してソース管理機能を処理する Visual Studio コンポーネントである) ソース管理アダプター パッケージの要求に応じて表示します。

   ソース管理コマンドへの応答で、Visual Studio IDE は、基本操作のための標準 UI を提示した後、ソース管理プラグイン API で定義された関数を介してソース管理プラグインに情報を渡します。 高度なオプションとしては、(ソース管理対象プロジェクトのブラウズなどの) 独自 UI を提示するために、ソース管理プラグインが呼び出される場合があります。 これは、ソース管理を扱うにあたって、2 つの異なったスタイルの UI (Visual Studio が提示する UI と、ソース管理プラグインが提示する UI) がユーザーに提示される可能性があることを意味します。 これは、高度なソース管理操作で最も顕著になります。

### <a name="drawbacks-to-implementing-a-source-control-plug-in"></a>ソース管理プラグインを実装することの短所

- 高度な機能に関して、2 つの異なったスタイルのインターフェイスがユーザーに表示され、混乱を招く可能性があります。

- ソース管理プラグインは、ソース管理プラグイン API によって暗示されるソース管理モデルに限定されます。

- ソース管理プラグイン API は、一部のソース管理シナリオにとっては制限が厳しすぎる場合があります。

### <a name="advantages-to-implementing-a-source-control-plug-in"></a>ソース管理プラグインを実装することの長所

- すべての基本的なソース管理操作のための UI はすべて Visual Studio によって提供されるため、複雑になる可能性がある UI をソース管理プラグインで実装する必要はありません。

- ソース管理プラグインは、より広範な機能を提供するために、厳密な API によって外部のソース管理プログラムと容易にやり取りできます。Visual Studio では、ソース管理機能がどのように提供されるかに関しては、ソース管理プラグイン API に準拠している限り、特に細かい決まりはありません。

- ソース管理プラグインの実装は、ソース管理 VSPackage よりも容易です。

## <a name="source-control-vspackage"></a>ソース管理 VSPackage
 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] によって、Visual Studio との深部までの統合が実現します。ソース管理機能の完全な制御が可能になり、Visual Studio が提供するソース管理ユーザー インターフェイスが完全に置き換えられます。 ソース管理 VSPackage は、Visual Studio に登録され、ソース管理機能を提供します。 複数のソース管理 VSPackage を Visual Studio に登録できますが、一度にアクティブにできるのはそのうちの 1 つだけです。 ソース管理 VSPackage は、アクティブになっている間、Visual Studio のソース管理の機能と外観を完全に制御します。 システムに登録されている他のすべてのソース管理 VSPackage は非アクティブになり、UI は一切表示されません。

 ソース管理 VSPackage の実装には、"オール オア ナッシング" の戦略が要求されます。 ソース管理 VSPackage の作成者は、ソース管理機能全体をカバーするために、多数のソース管理インターフェイスと新しい UI 要素 (ダイアログ ボックス、メニュー、ツール バー) の実装に多大な労力を費やす必要があります。 詳細について は、[ソース管理 VSPackage の作成](../../extensibility/internals/creating-a-source-control-vspackage.md)に関するページを参照してください。

### <a name="drawbacks-to-implementing-a-source-control-vspackage"></a>ソース管理 VSPackage を実装することの短所

- Visual Studio と正常に統合するために、VSPackage では、多数の複雑なインターフェイスを実装する必要があります。

- ソース管理に必要なすべての UI を VSPackage で提供する必要があります。Visual Studio からはこの領域の支援は提供されません。

- ソース管理 VSPackage は Visual Studio に密接に紐付けられ、スタンドアロン プログラムとの連携はできないため、外部バージョンのソース管理プログラムと機能を簡単に共有することはできません。

### <a name="advantages-to-implementing-a-source-control-vspackage"></a>ソース管理 VSPackage を実装することの長所

- VSPackage がソース管理の UI と機能を完全に制御できるため、ユーザーにはソース管理のためのシームレスなインターフェイスが表示されます。

- VSPackage は特定のソース管理モデルに限定されません。

## <a name="see-also"></a>関連項目
- [ソース管理](../../extensibility/internals/source-control.md)
- [ソース管理プラグインの作成](../../extensibility/internals/creating-a-source-control-plug-in.md)
- [ソース管理 VSPackage の作成](../../extensibility/internals/creating-a-source-control-vspackage.md)
- [ソース管理の新機能](../../extensibility/internals/what-s-new-in-source-control.md)
