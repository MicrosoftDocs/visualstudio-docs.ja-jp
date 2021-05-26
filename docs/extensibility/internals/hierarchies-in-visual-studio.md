---
title: Visual Studio における階層 | Microsoft Docs
description: プロジェクト項目とそれらに関連付けられたプロパティを含む、Visual Studio 統合開発環境 (IDE) のプロジェクト階層について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- hierarchies, Visual Studio IDE
- IDE, hierarchies
ms.assetid: 0a029a7c-79fd-4b54-bd63-bd0f21aa8d30
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d3fe1487e082907958c1cf8a36f1653efb97c9de
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056624"
---
# <a name="hierarchies-in-visual-studio"></a>Visual Studio での階層
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE) では、プロジェクトが *階層* として表示されます。 IDE では、階層はノードのツリーで、各ノードには関連付けられたプロパティのセットがあります。 *プロジェクト階層* は、プロジェクトの項目、項目のリレーションシップ、項目に関連付けられているプロパティとコマンドを保持するコンテナーです。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 階層インターフェイスを使用してプロジェクト階層を管理します。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> インターフェイスにより、プロジェクト項目から呼び出したコマンドを、標準コマンド ハンドラーではなく、適切な階層ウィンドウにリダイレクトされます。

## <a name="project-hierarchies"></a>プロジェクト階層
 各プロジェクト階層には、表示および編集できるアイテムが含まれています。 これらの項目は、プロジェクト タイプによって異なります。 たとえば、データベース プロジェクトには、ストアド プロシージャ、データベース ビュー、データベース テーブルが含まれる場合があります。 一方、プログラミング言語プロジェクトには、ビットマップおよびダイアログ ボックスのソース ファイルとリソース ファイルが含まれている可能性が高いです。 階層を入れ子にすることができます。これにより、プロジェクト階層を作成するときに柔軟性を高めることができます。

 新しいプロジェクト タイプを作成すると、プロジェクト タイプによって、編集可能な項目の完全なセットが制御されます。 ただし、プロジェクトには、編集がサポートされていない項目を含めることができます。 Visual C++ では HTML ファイル種類のカスタマイズされたエディターが用意されていませんが、Visual C++ プロジェクトに HTML ファイルを含めることができます。

 階層は、含まれている項目の永続性を管理します。 階層の実装では、階層内のアイテムの永続性に影響する特別なプロパティを制御する必要があります。 たとえば、項目がファイルではなくリポジトリ内のオブジェクトを表す場合、階層の実装では、それらのオブジェクトの永続性を制御する必要があります。 IDE 自体により、ユーザー入力に準拠して項目を保存するように階層への指示が行われますが、IDE ではこれらの項目を保存するために必要な操作は制御されません。 代わりに、プロジェクトにより制御されています。

 ユーザーがエディターで項目を開くと、その項目を制御する階層が選択され、アクティブな階層になります。 選択した階層によって、その項目に対して操作できるコマンドのセットが決まります。 この方法でユーザー フォーカスを追跡することで、階層にユーザーの現在のコンテキストを反映させることができます。

## <a name="see-also"></a>関連項目
- [プロジェクト タイプ](../../extensibility/internals/project-types.md)
- [IDE での選択と通貨](../../extensibility/internals/selection-and-currency-in-the-ide.md)
- [VSSDK のサンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples)
