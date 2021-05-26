---
title: 構文の色分け表示の実装 | Microsoft Docs
description: Managed Package Framework (MPF) の言語サービス機能を使用して、Visual Studio で構文の色分け表示を実装する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- syntax coloring, implementing
- editors [Visual Studio SDK], colorizing text
- text, colorizing in editors
ms.assetid: 96e762ca-efd0-41e7-8958-fda4897c8c7a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2c46cea481eceadef5118388633f84402870a209
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069609"
---
# <a name="implementing-syntax-coloring"></a>構文の色分け表示の実装
言語サービスで構文の色分け表示を提供すると、パーサーではテキスト行を配色可能な項目の配列に変換し、これらの配色可能な項目に対応するトークンの種類を返します。 パーサーからは、配色可能な項目の一覧に属するトークンの種類を返す必要があります。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] には、カラーライザー オブジェクトによって適切なトークンの種類に割り当てられた属性に従って、コード ウィンドウ内にそれぞれの配色可能な項目が表示されます。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ではパーサー インターフェイスを指定しないため、パーサーの実装は完全にユーザーによって決まります。 ただし、Visual Studio 言語パッケージ プロジェクトでは、既定のパーサー実装が用意されています。 マネージド コードの場合、Managed Package Framework (MPF) では、テキストの色分け表示を完全にサポートします。

 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能の新しい実装方法では MEF 拡張機能が使用されます。 構文の色分け表示を実装する新しい方法の詳細については、「[チュートリアル: テキストの強調表示](../../extensibility/walkthrough-highlighting-text.md)」を参照してください。

> [!NOTE]
> 新しいエディターの API をできるだけ早く使い始めることをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

## <a name="steps-followed-by-an-editor-to-colorize-text"></a>テキストを色分け表示するためにエディターで従う手順

1. エディターでは、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> オブジェクトに対して <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A> メソッドを呼び出すことによって、カラーライザーを取得します。

2. エディターでは <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.GetStateMaintenanceFlag%2A> メソッドを呼び出して、各行の状態がカラーライザー外部で維持されることがカラーライザーで必要かどうかを判断します。

3. 状態がカラーライザー外部で維持されることがカラーライザーで要求される場合、エディターでは <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.GetStartState%2A> メソッドを呼び出して、最初の行の状態を取得します。

4. バッファー内の行ごとに、エディターでは <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> メソッドを呼び出して次の手順を実行します。

    1. テキスト行はスキャナーに渡されて、テキストがトークンに変換されます。 各トークンでは、トークン テキストとトークンの種類を指定します。

    2. トークンの種類は、配色可能な項目の一覧のインデックスに変換されます。

    3. トークン情報は、配列の各要素が行内の文字に対応するように、配列に格納するために使用されます。 配列に格納される値は、配色可能な項目の一覧のインデックスです。

    4. 行ごとに、行の最後の状態が返されます。

5. 状態が維持されることがカラーライザーで要求される場合は、エディターによってその行の状態がキャッシュされます。

6. エディターでは、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> メソッドから返された情報を使用して、テキストの行を表示します。 この場合、次の手順が必要です。

    1. 行の文字ごとに、配色可能な項目のインデックスを取得します。

    2. 既定の配色可能な項目を使用する場合は、エディターの配色可能な項目の一覧にアクセスします。

    3. それ以外の場合は、言語サービスの <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A> メソッドを呼び出して、配色可能な項目を取得します。

    4. 配色可能な項目の情報を使用して、テキストを画面に表示します。

## <a name="managed-package-framework-colorizer"></a>Managed Package Framework カラーライザー
 Managed Package Framework (MPF) には、カラーライザーを実装するために必要なすべてのクラスが用意されています。 言語サービス クラスでは、<xref:Microsoft.VisualStudio.Package.LanguageService> クラスを継承し、必要なメソッドを実装する必要があります。 <xref:Microsoft.VisualStudio.Package.IScanner> インターフェイスを実装してスキャナーとパーサーを提供し、 <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> メソッド (<xref:Microsoft.VisualStudio.Package.LanguageService> クラスに実装する必要があるメソッドの 1 つ) からそのインターフェイスのインスタンスを返す必要があります。 詳細については、[従来の言語サービスでの構文の配色変更](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)に関するページを参照してください。

## <a name="see-also"></a>関連項目
- [方法: ビルトインの配色可能な項目の使用](../../extensibility/internals/how-to-use-built-in-colorable-items.md)
- [カスタムの配色可能な項目](../../extensibility/internals/custom-colorable-items.md)
- [従来の言語サービスの開発](../../extensibility/internals/developing-a-legacy-language-service.md)
- [従来の言語サービスでの構文の配色変更](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)
