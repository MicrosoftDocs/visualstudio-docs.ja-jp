---
title: ソース管理 VSPackage を実装するタイミング
description: Visual Studio ソース管理ソリューションの拡張に使用できるソース管理プラグインとソース管理 VSPackage の選択肢について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control packages, about source control packages
ms.assetid: 60b3326e-e7e2-4729-95fc-b682e7ad5c99
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 89e2ea0db7f162c70261ab2ba9aab187f9c11bd0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090890"
---
# <a name="determine-whether-to-implement-a-source-control-vspackage"></a>ソース管理 VSPackage を実装するかどうかの判断

このセクションでは、ソース管理ソリューションを拡張するためのソース管理プラグインとソース管理 VSPackage の選択肢について詳しく説明し、適切な統合パスの選択に関する幅広いガイドラインを示します。

## <a name="small-source-control-solution-with-limited-resources"></a>リソースが限られた小規模なソース管理ソリューション

 リソースが限られていて、ソース管理パッケージの作成に伴うオーバーヘッドを負担できない場合は、ソース管理プラグイン API ベースのプラグインを作成できます。これにより、ソース管理パッケージと並行して作業できるようになり、ソース管理プラグインとパッケージを必要に応じて切り替えることができます。 詳細については、[登録と選択](../../extensibility/internals/registration-and-selection-source-control-vspackage.md)に関するページを参照してください。

## <a name="large-source-control-solution-with-a-rich-feature-set"></a>豊富な機能セットを備えた大規模なソース管理ソリューション

 ソース管理プラグイン API を使用して適切にキャプチャされていない、豊富なソース管理モデルを提供するソース管理ソリューションを実装する場合は、統合パスとしてソース管理パッケージを使用することを検討できます。 これは特に、ソース管理アダプター パッケージ (ソース管理プラグインと通信し、基本的なソース管理 UI を提供する) を独自のものに置き換えて、カスタムの方法でソース管理イベントを処理できるようにする場合に当てはまります。 十分なソース管理 UI が既にあり、そのエクスペリエンスを [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] で保持したい場合は、ソース管理パッケージ オプションを使用してそれを実行できます。 ソース管理パッケージは汎用ではなく、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE で使用するためだけに設計されています。

 ソース管理のロジックと UI を柔軟かつ高度に制御できるソース管理ソリューションを実装する場合は、ソース管理パッケージの統合ルートをお勧めします。 次のようにすることができます。

1. 独自のソース管理 VSPackage を登録します ([登録と選択](../../extensibility/internals/registration-and-selection-source-control-vspackage.md)に関するページを参照してください)。

2. 既定のソース管理 UI をカスタム UI に置き換えます ([カスタム ユーザー インターフェイス](../../extensibility/internals/custom-user-interface-source-control-vspackage.md)に関するページを参照してください)。

3. 使用するグリフを指定し、ソリューション エクスプローラーのグリフ イベントを処理します ([グリフ管理](../../extensibility/internals/glyph-control-source-control-vspackage.md)に関するページを参照してください)。

4. クエリの編集とクエリの保存イベントを処理します ([クエリの編集とクエリの保存](../../extensibility/internals/query-edit-query-save-source-control-vspackage.md)に関するページを参照してください)。

## <a name="see-also"></a>関連項目

- [ソース管理プラグインの作成](../../extensibility/internals/creating-a-source-control-plug-in.md)
