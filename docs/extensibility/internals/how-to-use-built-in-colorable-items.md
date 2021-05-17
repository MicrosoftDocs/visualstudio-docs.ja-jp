---
title: '方法: 組み込みの配色可能な項目の使用 | Microsoft Docs'
description: Visual Studio 統合開発環境 (IDE) で言語サービス用の組み込みの配色可能な項目を使用する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- colorable items
- language services, built-in colorable items
ms.assetid: 5e5f3436-6bad-4fd2-8823-6a30353ba648
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 253c108fe83eaf44f945f546bd64dd6529de1dd6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086080"
---
# <a name="how-to-use-built-in-colorable-items"></a>方法: 組み込みの配色可能な項目の使用
組み込みの配色可能な項目を使用する前に、まず、独自のカスタムの配色可能な項目 (この場合は <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems> オブジェクト) を提供しないことを統合開発環境 (IDE) に通知する必要があります。 これを行うには、言語サービスのレジストリ エントリを設定します。

## <a name="to-use-built-in-colorable-items"></a>組み込みの配色可能な項目を使用するには

1. **HKEY_LOCAL_MACHINE\VisualStudio\\<X.Y>\Languages\Language Services\\<Language Name\>** (ここで、\<X.Y> は [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のバージョンであり、\<Language Name> はお使いの言語の名前) に、**RequestStockColors** という DWORD レジストリ エントリの値を作成します。

2. **RequestStockColors** レジストリ エントリの値を *1* に設定します。

    レジストリ エントリを作成したら、カラーライザーの <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A> メソッドで <xref:Microsoft.VisualStudio.TextManager.Interop.DEFAULTITEMS> 列挙型のメンバーを使用して、エディターで使用する色属性の配列を入力できます。

   > [!NOTE]
   > カスタムの配色可能な項目を提供する場合は、このレジストリ エントリを設定しないでください。 詳細については、[カスタムの配色可能な項目](../../extensibility/internals/custom-colorable-items.md)に関する記事を参照してください。

## <a name="see-also"></a>関連項目
- [カスタム エディターでの構文の色分け表示](../../extensibility/syntax-coloring-in-custom-editors.md)
- [従来の言語サービスでの構文の色分け表示](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)
- [構文の色分け表示の実装](../../extensibility/internals/implementing-syntax-coloring.md)
- [カスタムの配色可能な項目](../../extensibility/internals/custom-colorable-items.md)
- [従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service2.md)
