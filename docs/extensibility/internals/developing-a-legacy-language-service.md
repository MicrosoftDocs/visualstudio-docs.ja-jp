---
title: 従来の言語サービスの開発 | Microsoft Docs
description: VSPackage の一部として、または Managed Extensibility Framework (MEF) 拡張機能を使用して、従来の言語サービスを実装する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.vsip.LangServWiz.langtoks
- vs.vsip.LangServWiz.welcome
- vs.vsip.LangServWiz.langSpec
- vs.vsip.LangServWiz.langInfo
- vs.vsip.LangServWiz.langServOpts
helpviewer_keywords:
- language services, developing
ms.assetid: 6151ba88-c1c3-41de-a1cc-668f494d48d1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 59c06c96d2a0263c9e76ed4359e0fac93ab2ab25
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056728"
---
# <a name="develop-a-legacy-language-service"></a>従来の言語サービスを開発する
このセクションでは、従来の言語サービスの作成に役立つトピックへのリンクを示します。

 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能の新しい実装方法では MEF 拡張機能が使用されます。 言語サービスの新しい実装方法の詳細については、「[エディターと言語サービスの拡張機能](../../extensibility/editor-and-language-service-extensions.md)」を参照してください。

> [!NOTE]
> 新しいエディターの API をできるだけ早く使い始めることをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

## <a name="in-this-section"></a>このセクションの内容
- [従来の言語サービスのモデル](../../extensibility/internals/model-of-a-legacy-language-service.md)

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] コア エディターの最小言語サービスのモデルを示します。 このモデルは、独自の言語サービスを作成するためのガイドとして使用できます。

- [従来の言語サービスのインターフェイス](../../extensibility/internals/legacy-language-service-interfaces.md)

 言語サービスを実装するために必要なオブジェクトについて説明し、構文の強調表示、メソッドのデータ、その他の機能を提供するために使用できる追加のオブジェクトの一覧を示します。

- [従来の言語サービスのコマンドをインターセプトする](../../extensibility/internals/intercepting-legacy-language-service-commands.md)

 言語サービスにコマンド フィルターを挿入して、テキスト ビューで処理されるコマンドをインターセプトする方法について説明します。

- [従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service2.md)

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] を使用して言語サービスを登録する方法について説明します。

- [デバッグのための言語サービスのサポート](../../extensibility/internals/language-service-support-for-debugging.md)

 言語サービスでデバッガーをサポートする機能を提供する方法について説明します。

- [チェック リスト: 従来の言語サービスを作成する](../../extensibility/internals/checklist-creating-a-legacy-language-service.md)

 コア エディターの言語サービスを作成して統合するための詳しい手順について説明します。

## <a name="related-sections"></a>関連項目
- [従来の言語サービスでの構文の色分け表示](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)

 言語サービスで構文の強調表示を実装する方法について説明します。

- [従来の言語サービスのステートメント入力候補](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md)

 ステートメント入力候補について説明します。これは、ユーザーが言語サービスを使用して、入力を開始した言語キーワードまたは要素を完成させるプロセスです。

- [従来の言語サービスのパラメーター ヒント](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md)

 オーバーロードされた関数やメソッドに対してメソッドのヒントを示す方法について説明します。

- [方法: 従来の言語サービスでの隠し文字サポートの提供](../../extensibility/internals/how-to-provide-hidden-text-support-in-a-legacy-language-service.md)

 非表示テキスト領域の目的について説明し、非表示テキスト領域を実装する手順について説明します。

- [方法: 従来の言語サービスでのアウトラインの拡張サポートの提供](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md)

 *[定義に縮小]* コマンドのサポートにとどまらず、言語のアウトラインのサポートを拡張する 2 つのオプションについて説明します。
