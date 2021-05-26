---
title: シンボル参照ツールのサポート | Microsoft Docs
description: Visual Studio には、Visual Studio でシンボルを参照する機能が用意されています。 コンポーネント内のシンボル用のライブラリを使用してこれらの機能を拡張する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- symbols, symbol-browsing tools
- browsers, symbol browsers
- symbol-browsing tools
- libraries
- IVsLibrary2 interface, symbol-browsing tools
- IVsSimpleLibrary2 interface, symbol-browsing tools
- symbol-browsing tools, library manager
- symbols
- libraries, symbol-browsing tools
ms.assetid: 70d8c9e5-4b0b-4a69-b3b3-90f36debe880
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d54f56ae3bc5fd5956f67400d84edfd4c8c9e55c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080568"
---
# <a name="supporting-symbol-browsing-tools"></a>シンボル参照ツールのサポート
**オブジェクト ブラウザー**、**クラス ビュー**、**呼び出しブラウザー**、および **シンボルの検索結果** の各ツールは、Visual Studio でのシンボル参照機能を提供します。 これらのツールには、シンボルの階層ツリー ビューが表示され、ツリー内のシンボル間の関係が表示されます。 シンボルは、さまざまなコンポーネントに含まれる名前空間、オブジェクト、クラス、クラス メンバー、およびその他の言語要素を表します。 コンポーネントには、Visual Studio プロジェクト、外部 .NET Framework コンポーネント、およびタイプ ライブラリ (.tlb) があります。 詳細については、「[コードの構造の表示](../../ide/viewing-the-structure-of-code.md)」を参照してください。

## <a name="symbol-browsing-libraries"></a>シンボル参照ライブラリ
 言語の実装者は、コンポーネント内のシンボルを追跡するライブラリを作成し、一連のインターフェイスを使用して Visual Studio オブジェクト マネージャーにシンボルのリストを提供することにより、Visual Studio のシンボル参照機能を拡張できます。 ライブラリは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2> インターフェイスによって記述されます。 Visual Studio オブジェクト マネージャーでは、シンボル参照ツールからの新しいデータの要求に対し、ライブラリからデータを取得して整理することによって応答します。 その後、要求されたデータを使用してツールを設定または更新します。 Visual Studio オブジェクト マネージャー (<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2>) への参照を取得するには、<xref:Microsoft.VisualStudio.Shell.Interop.SVsObjectManager> のサービス ID を `GetService` メソッドに渡します。

 各ライブラリは、すべてのライブラリの情報を収集する Visual Studio オブジェクト マネージャーに登録する必要があります。 ライブラリを登録するには、<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterSimpleLibrary%2A> メソッドを呼び出します。 Visual Studio オブジェクト マネージャーでは、要求を開始したツールに応じて適切なライブラリを検索し、データを要求します。 データは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2> インターフェイスによって記述されるシンボルのリストとして、ライブラリと [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] オブジェクト マネージャーの間でやり取りされます。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] オブジェクト マネージャーは、ライブラリに格納されている最新のデータを反映するために、シンボル参照ツールを定期的に更新する役割を担います。

 次の図には、ライブラリと Visual Studio オブジェクト マネージャーの間における要求/データ交換プロセスの主要要素のサンプルが含まれています。 図のインターフェイスは、マネージド コード アプリケーションの一部です。

 ![ライブラリとオブジェクト マネージャー間のデータ フロー](../../extensibility/internals/media/callbrowserdiagram.gif "CallBrowserDiagram")

 Visual Studio オブジェクト マネージャーにシンボルのリストを提供するには、最初に <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterSimpleLibrary%2A> メソッドを呼び出して、Visual Studio オブジェクト マネージャーにライブラリを登録する必要があります。 ライブラリが登録されると、Visual Studio オブジェクト マネージャーは、ライブラリの機能に関する特定の情報を要求します。 たとえば、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2.GetLibFlags2%2A> メソッドと <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2.GetSupportedCategoryFields2%2A> メソッドを呼び出して、ライブラリ フラグとサポートされるカテゴリを要求します。 ある時点で、いずれかのツールからこのライブラリのデータが要求されると、オブジェクト マネージャーは <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2.GetList2%2A> メソッドを呼び出して、最上位のシンボル リストを要求します。 応答として、ライブラリはシンボルのリストを作成し、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2> インターフェイスを通じて Visual Studio オブジェクト マネージャーに公開します。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] オブジェクト マネージャーは <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetItemCount%2A> メソッドを呼び出して、リスト内の項目数を特定します。 以降の要求はすべて、リスト内の特定の項目に関連するものであり、各要求にはその項目のインデックス番号が指定されます。 Visual Studio オブジェクト マネージャーは <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetCategoryField2%2A> メソッドを呼び出して、項目の型、アクセシビリティ、およびその他のプロパティに関する情報を収集します。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetTextWithOwnership%2A> メソッドを呼び出して項目の名前を特定し、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetDisplayData%2A> メソッドを呼び出してアイコン情報を要求します。 項目名の左側にアイコンが表示され、項目の型、アクセシビリティ、およびその他のプロパティが示されます。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] オブジェクト マネージャーは <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetExpandable3%2A> メソッドを呼び出して、特定のリスト項目が展開可能で子項目を持っているかどうかを確認します。 要素を展開する要求が UI から送信された場合、オブジェクト マネージャーは <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetList2%2A> メソッドを呼び出して、シンボルの子リストを要求します。 このプロセスがツリーのさまざまな部分で続行され、ツリーがオンデマンドで構築されていきます。

> [!NOTE]
> ネイティブ コード シンボル プロバイダーを実装するには、<xref:Microsoft.VisualStudio.Shell.Interop.IVsLibrary2> インターフェイスと <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectList2> インターフェイスを使用します。

## <a name="see-also"></a>関連項目
- [方法: オブジェクト マネージャーを使用したライブラリの登録](../../extensibility/internals/how-to-register-a-library-with-the-object-manager.md)
- [方法: ライブラリによって提供されるシンボルのリストをオブジェクト マネージャーに公開する](../../extensibility/internals/how-to-expose-lists-of-symbols-provided-by-the-library-to-the-object-manager.md)
- [方法: ライブラリでのシンボルの識別](../../extensibility/internals/how-to-identify-symbols-in-a-library.md)
