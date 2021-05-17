---
title: テンプレート ポリシーとプロパティ ウィンドウ | Microsoft Docs
description: テンプレート ポリシーを使用してプロパティの既定値を設定する方法、プロパティを非表示にする方法、およびプロパティ ウィンドウにプロパティを追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Properties window, template policy
ms.assetid: 1d8019d3-5e57-47ba-b358-526b0796a63b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b415054f65c41f03556f7d87be5b12d92ced399c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105078670"
---
# <a name="template-policy-and-the-properties-window"></a>テンプレート ポリシーとプロパティ ウィンドウ
エンタープライズ テンプレート プロジェクト内にプロジェクトが含まれている場合、そのエンタープライズ テンプレートプロジェクトでポリシーを適用できます。 テンプレート ポリシーは、プロパティの既定値を設定したり、プロパティを非表示にしたり、プロパティを追加したりするために使用できる制約システムになります。

 テンプレート ポリシーを使用して、**プロパティ** ウィンドウでの情報の表示を制御することは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing> の実装とは異なります。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing> では、コンポーネント レベルでオブジェクトのプロパティを処理しますが、テンプレートポリシーを使用すると、ソリューションまたはプロジェクト レベルでオブジェクトのプロパティを制約できます。 つまり、次のようになります。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing> にメソッドを実装して、特定のオブジェクトの **プロパティ** ウィンドウに表示される内容を決定します。

- ソリューションおよびプロジェクト レベルでテンプレート ポリシーを使用して、以前に指定したオブジェクトの **プロパティ** ウィンドウに表示される内容を決定します。

  指定された種類のプロジェクト項目が **ソリューション エクスプローラー** で選択されている場合にテンプレート ポリシーを使用して **プロパティ** ウィンドウで特定のプロパティを選択的に制限することは、プロジェクトで作業している開発チームのすべてのメンバーに役立ちます。 たとえば、テンプレート ポリシーを使用すると、開発者に用にデータベースですべての接続文字列情報を設定し、接続文字列を読み取り専用にすることができます。 このようにすると、各開発者がデータ アクセスに適切なパスを確実に使用する簡単な方法を提供できます。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing>
- [プロパティの拡張](../../extensibility/internals/extending-properties.md)
