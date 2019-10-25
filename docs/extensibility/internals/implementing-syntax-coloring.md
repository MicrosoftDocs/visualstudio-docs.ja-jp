---
title: 構文の色分けを実装する |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- syntax coloring, implementing
- editors [Visual Studio SDK], colorizing text
- text, colorizing in editors
ms.assetid: 96e762ca-efd0-41e7-8958-fda4897c8c7a
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cab338e253cca8c7f8457752980e7f3624317d9c
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72727037"
---
# <a name="implementing-syntax-coloring"></a>構文の色分け表示の実装
言語サービスが構文の色付けを提供すると、パーサーはテキスト行を装飾 items の配列に変換し、これらの装飾 items に対応するトークンの種類を返します。 パーサーは、装飾 items のリストに属するトークン型を返す必要があります。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] は、colorizer オブジェクトによって割り当てられた属性に従って、コードウィンドウ内の各項目を適切なトークンの種類に表示します。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] はパーサーインターフェイスを指定せず、パーサーの実装は完全に行われます。 ただし、Visual Studio 言語パッケージプロジェクトでは、既定のパーサー実装が用意されています。 マネージコードの場合、managed package framework (MPF) は、色分けテキストを完全にサポートします。

 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能を実装するための新しい方法として、MEF 拡張機能を使用することをお勧めします。 新しい構文の色分けを実装する方法の詳細については、「[チュートリアル: テキストの強調](../../extensibility/walkthrough-highlighting-text.md)表示」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、エディターの新機能を利用できるようになります。

## <a name="steps-followed-by-an-editor-to-colorize-text"></a>テキストを色分けするためのエディターの後続の手順

1. このエディターでは、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo> オブジェクトの <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A> メソッドを呼び出すことによって、色の値を取得します。

2. このエディターは、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.GetStateMaintenanceFlag%2A> メソッドを呼び出して、colorizer、色計の外にある各行の状態を確認する必要があるかどうかを判断します。

3. Colorizer、色計の外に状態を維持する必要がある場合、エディターは <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.GetStartState%2A> メソッドを呼び出して、最初の行の状態を取得します。

4. エディターは、バッファー内の各行に対して、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> メソッドを呼び出します。このメソッドは、次の手順を実行します。

    1. テキスト行は、テキストをトークンに変換するためにスキャナーに渡されます。 各トークンは、トークンテキストとトークンの種類を指定します。

    2. トークン型は、装飾 items リストにインデックスに変換されます。

    3. トークン情報は、配列の各要素が行内の文字に対応するように配列に格納するために使用されます。 配列に格納されている値は、装飾 items リスト内のインデックスです。

    4. 行の最後の状態が各行に対して返されます。

5. 色計で状態を維持する必要がある場合は、エディターによってその行の状態がキャッシュされます。

6. エディターでは、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> メソッドから返された情報を使用して、テキスト行がレンダリングされます。 この場合、次の手順が必要です。

    1. 行の各文字について、装飾 item インデックスを取得します。

    2. 既定の装飾項目を使用する場合は、エディターの装飾 items リストにアクセスします。

    3. それ以外の場合は、言語サービスの <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A> メソッドを呼び出して、装飾項目を取得します。

    4. 装飾項目の情報を使用して、テキストを画面に表示します。

## <a name="managed-package-framework-colorizer"></a>マネージパッケージフレームワークの色計
 Managed package framework (MPF) には、colorizer 実装するために必要なすべてのクラスが用意されています。 言語サービスクラスは <xref:Microsoft.VisualStudio.Package.LanguageService> クラスを継承し、必要なメソッドを実装する必要があります。 @No__t_0 インターフェイスを実装し、そのインターフェイスのインスタンスを <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> メソッド (<xref:Microsoft.VisualStudio.Package.LanguageService> クラスで実装する必要があるメソッドの1つ) から返すことによって、スキャナーとパーサーを提供する必要があります。 詳細については、「[従来の言語サービスの構文色分け](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: ビルトインの配色可能な項目の使用](../../extensibility/internals/how-to-use-built-in-colorable-items.md)
- [カスタムの配色可能な項目](../../extensibility/internals/custom-colorable-items.md)
- [従来の言語サービスの開発](../../extensibility/internals/developing-a-legacy-language-service.md)
- [従来の言語サービスでの構文の配色変更](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)