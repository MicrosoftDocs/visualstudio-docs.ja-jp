---
title: 従来の言語サービスのクイック ヒント | Microsoft Docs
description: 識別子に関する情報を表示するための IntelliSense クイック ヒント操作のサポートについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Quick Info, supporting in language services [managed package framework]
- IntelliSense, Quick Info
- language services [managed package framework], IntelliSense Quick Info
ms.assetid: 159ccb0b-f5d6-4912-b88b-e9612924ed5e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 90cab5683c7a13aec25b15d75da0117beee34721
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060888"
---
# <a name="quick-info-in-a-legacy-language-service"></a>従来の言語サービスのクイック ヒント
IntelliSense のクイック ヒントは、ユーザーが識別子にキャレットを置き、 **IntelliSense** メニューから **[クイック ヒント]** を選択するか、識別子の上にマウス カーソルを置いたときに、ソースの識別子に関する情報を表示します。 これにより、識別子に関する情報を含むツール ヒントが表示されます。 通常、この情報は識別子の型で構成されます。 デバッグ エンジンがアクティブになっている場合は、この情報に現在の値が含まれている可能性があります。 デバッグ エンジンから式の値が提供されますが、言語サービスは識別子のみを処理します。

 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能の新しい実装方法では MEF 拡張機能が使用されます。 詳細については、「[チュートリアル: クイック ツールヒントの表示](../../extensibility/walkthrough-displaying-quickinfo-tooltips.md)」を参照してください。

> [!NOTE]
> 新しいエディターの API をできるだけ早く使い始めることをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

 マネージド パッケージ フレームワーク (MPF) 言語サービス クラスにより、IntelliSense クイック ツール ヒントを表示するための完全なサポートが提供されます。 必要なのは、表示するテキストを指定して、クイック ヒント機能を有効にすることだけです。

 表示されるテキストを取得するには、解析理由の <xref:Microsoft.VisualStudio.Package.ParseReason> 値を指定して <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> メソッド パーサーを呼び出します。 この理由により、<xref:Microsoft.VisualStudio.Package.ParseRequest> オブジェクトで指定された場所にある識別子について、型情報 (またはクイック ツール ヒントに表示される適切なもの) を取得するようパーサーは指示されます。 その後、<xref:Microsoft.VisualStudio.Package.ParseRequest> オブジェクトは <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> メソッドに渡されます。

 パーサーにより、すべての識別子の型を確認するために、<xref:Microsoft.VisualStudio.Package.ParseRequest> オブジェクト内の位置まですべてが解析される必要があります。 次に、パーサーにより、解析要求の場所で識別子が取得される必要があります。 最後に、パーサーから、その識別子に関連付けられたツール ヒント データを <xref:Microsoft.VisualStudio.Package.AuthoringScope> オブジェクトに渡して、オブジェクトにより <xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDataTipText%2A> メソッドからテキストを返すことができるようにする必要があります。

## <a name="enabling-the-quick-info-feature"></a>クイック ヒント機能を有効にする
 クイック ヒント機能を有効にするには、<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> の `CodeSense` および `QuickInfo` の名前付きパラメーターを設定する必要があります。これらの属性により、<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A> と <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableQuickInfo%2A> プロパティが設定されます。

## <a name="implementing-the-quick-info-feature"></a>クイック ヒント機能を実装にする
 <xref:Microsoft.VisualStudio.Package.ViewFilter> クラスにより、IntelliSense のクイック ヒント操作が処理されます。 <xref:Microsoft.VisualStudio.Package.ViewFilter> クラスで <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> コマンドを受け取ると、クラスにより、<xref:Microsoft.VisualStudio.Package.ParseReason> の解析理由と <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> コマンドが送信されたときのキャレットの位置を使用して、<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> メソッドが呼び出されます。 次に、<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> メソッド パーサーにより、所与の場所までソースが解析され、次に所与の場所にある識別子が解析され、クイック ツール ヒントに表示する内容が決定される必要があります。

 ほとんどのパーサーでは、ソース ファイル全体が最初に解析され、結果が解析ツリーに格納されます。 <xref:Microsoft.VisualStudio.Package.ParseReason> が <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> メソッドに渡されると、完全な解析が実行されます。 その後、その他の種類の解析では、解析ツリーを使用して必要な情報を取得できます。

 たとえば、<xref:Microsoft.VisualStudio.Package.ParseReason> の解析理由値では、ソースの場所で識別子が検索され、解析ツリー内の検索によって型情報の取得が可能です。 この型情報は <xref:Microsoft.VisualStudio.Package.AuthoringScope> クラスに渡され、<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDataTipText%2A> メソッドによって返されます。
