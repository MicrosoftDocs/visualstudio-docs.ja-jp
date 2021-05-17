---
title: '[ファイルを開く] コマンドを使用したファイルの表示 | Microsoft Docs'
description: Visual Studio 統合開発環境 (IDE) で [ファイル] メニューの [ファイルを開く] コマンドを処理してファイルを表示する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, supporting Open File command
- Open File command
- persistence, supporting Open File command
ms.assetid: 4fff0576-b2f3-4f17-9769-930f926f273c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b2617050ff26536df5a94d0cb51fe74d37a55725
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061343"
---
# <a name="display-files-by-using-the-open-file-command"></a>[ファイルを開く] コマンドを使用してファイルを表示する
次の手順では、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の **[ファイル]** メニューで使用できる **[ファイルを開く]** コマンドを IDE で処理する方法について説明します。 手順では、このコマンドから行われた呼び出しに対するプロジェクトの応答についても説明します。

 ユーザーが **[ファイル]** メニューの **[ファイルを開く]** コマンドをクリックし、 **[ファイルを開く]** ダイアログ ボックスでファイルを選択すると、次の処理が行われます。

1. IDE では、実行中のドキュメント テーブルを使用して、ファイルが既にプロジェクトで開かれているかどうかを判断します。

    - ファイルが開いている場合は、IDE によってウィンドウの表示が更新されます。

    - ファイルが開いていない場合、IDE は <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A> を呼び出して各プロジェクトに対してクエリを実行し、ファイルを開くことができるプロジェクトを判別します。

        > [!NOTE]
        > <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A> のプロジェクト実装で、プロジェクトがファイルを開くレベルを示す優先度値を指定します。 優先度値は、<xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY> 列挙で指定されます。

2. それぞれのプロジェクトでは、ファイルを開くプロジェクトであることの重要性を示す優先度レベルが返されます。

3. IDE では、次の基準を使用して、ファイルを開くプロジェクトを決定します。

    - 最高の優先度 (`DP_Intrinsic`) を返すプロジェクトがファイルを開きます。 複数のプロジェクトがこの優先度を返した場合、最初に応答したプロジェクトがファイルを開きます。

    - 最高の優先度 (`DP_Intrinsic`) を返すプロジェクトはないが、すべてのプロジェクトで同じ低い優先度が返される場合、アクティブなプロジェクトがファイルを開きます。 アクティブなプロジェクトがない場合は、最初に応答したプロジェクトがファイルを開きます。

    - ファイル (`DP_Unsupported`) の所有権を要求するプロジェクトがない場合、[その他のファイル] プロジェクトがファイルを開きます。

         [その他のファイル] プロジェクトのインスタンスが作成された場合、プロジェクトは常に `DP_CanAddAsExternal` の値を返します。 この値は、このプロジェクトでファイルを開くことができることを示します。 このプロジェクトは、他のプロジェクトに含まれていない開いているファイルを格納するために使用されます。 このプロジェクト内の項目の一覧は永続化されません。このプロジェクトは、ファイルを開くために使用された場合にのみ **ソリューション エクスプローラー** に表示されます。

         [その他のファイル] プロジェクトでファイルを開くことができないことが示されていない場合は、プロジェクトのインスタンスが作成されていません。 この場合、IDE では [その他のファイル] プロジェクトのインスタンスを作成し、ファイルを開くようにプロジェクトに指示します。

4. IDE では、ファイルを開くプロジェクトが決定されるとすぐに、そのプロジェクトで <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A> メソッドが呼び出されます。

5. この場合、プロジェクトでは、プロジェクト固有のエディターまたは標準エディターを使用してファイルを開くこともできます。 詳細については、「[方法: プロジェクト固有のエディターを開く](../../extensibility/how-to-open-project-specific-editors.md)」および「[方法: 標準のエディターを開く](../../extensibility/how-to-open-standard-editors.md)」をそれぞれ参照してください。

## <a name="see-also"></a>関連項目
- [[プログラムから開く] コマンドを使用してファイルを表示する](../../extensibility/internals/displaying-files-by-using-the-open-with-command.md)
- [プロジェクト項目を開いて保存する](../../extensibility/internals/opening-and-saving-project-items.md)
- [方法: プロジェクト固有のエディターを開く](../../extensibility/how-to-open-project-specific-editors.md)
- [方法: 標準エディターを開く](../../extensibility/how-to-open-standard-editors.md)
