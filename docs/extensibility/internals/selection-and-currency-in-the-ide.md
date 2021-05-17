---
title: IDE での選択と通貨 | Microsoft Docs
description: VSPackage で通貨追跡を行う方法について説明します。 Visual Studio IDE では、選択コンテキストを使用して、現在選択されているオブジェクトに関する情報を保持します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- currency, Visual Studio IDE
- IDE, selection
- selection, Visual Studio IDE
- IDE, currency
ms.assetid: 2f6f18d1-acd8-454d-a856-9a4d81155052
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0fb65a63b99f625f8d32af8436db753a0f17322e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080906"
---
# <a name="selection-and-currency-in-the-ide"></a>IDE での選択と通貨
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE) では、選択 "*コンテキスト*" を使用して、ユーザーの現在選択されているオブジェクトに関する情報を保持します。 選択コンテキストを使用すると、VSPackage では次の 2 つの方法で通貨追跡を行うことができます。

- VSPackage に関する通貨情報を IDE に伝達します。

- IDE 内でユーザーの現在アクティブな選択を監視します。

## <a name="selection-context"></a>選択コンテキスト
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE では、独自のグローバル選択コンテキスト オブジェクトで IDE の通貨がグローバルに追跡されます。 次の表は、選択コンテキストを構成する要素を示しています。

|要素|説明|
|-------------|-----------------|
|現在の階層|通常は現在のプロジェクトです。現在の階層が NULL である場合は、ソリューション全体が最新であることを示します。|
|現在の ItemID|現在の階層内で選択されている項目。プロジェクト ウィンドウに複数の選択肢がある場合は、現在の項目が複数存在する可能性があります。|
|現在の `SelectionContainer`|[プロパティ] ウィンドウでプロパティを表示する必要がある 1 つ以上のオブジェクトを保持します。|

 さらに、環境では次の 2 つのグローバル リストが保持されます。

- アクティブな UI コマンド識別子のリスト

- 現在アクティブな要素の型のリスト。

### <a name="window-types-and-selection"></a>ウィンドウの種類と選択
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE では、ウィンドウは次の 2 つの一般的な種類に編成されます。

- 階層の種類ウィンドウ

- フレーム ウィンドウ (ツールおよびドキュメント ウィンドウなど)

  IDE では、これらのウィンドウの種類ごとに異なる方法で通貨を追跡します。

  最も一般的なプロジェクトの種類ウィンドウは、IDE によって制御されるソリューション エクスプローラーです。 プロジェクトの種類ウィンドウでは、グローバルな選択コンテキストのグローバル階層と ItemID を追跡し、ウィンドウでは現在の階層を決定するためにユーザーの選択に依存します。 プロジェクトの種類ウィンドウの場合、環境では、開いている要素の現在の値を VSPackage によって監視できるグローバル サービス <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> が提供されます。 環境でのプロパティの参照は、このグローバル サービスによって行われます。

  一方、フレーム ウィンドウでは、フレーム ウィンドウ内の DocObject を使用して SelectionContext 値 (hierarchy/ItemID/SelectionContainer の 3 つ) をプッシュします。 . フレーム ウィンドウでは、この目的のために <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> サービスを使用します。 DocObject では、選択コンテナーの値のみをプッシュできます。MDI 子ドキュメントでは一般的ですが、階層および ItemID のローカル値は変更されません。

### <a name="events-and-currency"></a>イベントと通貨
 環境の通貨の概念に影響する次の 2 種類のイベントが発生する可能性があります。

- グローバル レベルに反映され、ウィンドウ フレーム選択コンテキストを変更するイベント。 この種類のイベントの例としては、開いている MDI 子ウィンドウ、開いているグローバル ツール ウィンドウ、または開いているプロジェクトの種類ツール ウィンドウなどがあります。

- ウィンドウのフレーム選択コンテキスト内でトレースされた要素を変更するイベント。 例には、DocObject 内での選択の変更や、プロジェクトの種類ウィンドウでの選択の変更があります。

## <a name="see-also"></a>関連項目
- [コンテキスト オブジェクトの選択](../../extensibility/internals/selection-context-objects.md)
- [ユーザーへのフィードバック](../../extensibility/internals/feedback-to-the-user.md)
