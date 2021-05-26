---
title: '方法: 開いているドキュメントのエディターを開く | Microsoft Docs'
description: 標準またはプロジェクト固有のエディターでファイルを開く方法について説明します。 プロジェクトでドキュメント ウィンドウを開くときに、ファイルが既に開いているかどうかを確認する必要があります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], opening for open documents
ms.assetid: 1a0fa49c-efa4-4dcc-bdc0-299b7052acdc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f6dfcd44a03b110ae514c2de36092ee07fd0c35e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069921"
---
# <a name="how-to-open-editors-for-open-documents"></a>方法: 開いているドキュメントのエディターを開く
プロジェクトでドキュメント ウィンドウを開く前に、まず、そのファイルが別のエディターのドキュメント ウィンドウで既に開いているかどうかを確認する必要があります。 ファイルは、プロジェクト固有のエディターで開くことも、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] に登録されているいずれかの標準エディターで開くこともできます。

## <a name="open-a-project-specific-editor"></a>プロジェクト固有のエディターを開く
 既に開いているファイルのプロジェクト固有のエディターを開くには、次の手順に従います。

### <a name="to-open-a-project-specific-editor-for-an-open-file"></a>開いているファイルのプロジェクト固有のエディターを開くには

1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A> メソッドを呼び出します。

    この呼び出しでは、ドキュメントの階層、階層項目、およびウィンドウ フレームへのポインターを返します (該当する場合)。

2. ドキュメントが開いている場合、プロジェクトでは、ドキュメント データ オブジェクトのみが存在するのか、ドキュメント ビュー オブジェクトも存在するのかを確認する必要があります。

   - ドキュメント ビュー オブジェクトが存在し、このビューが別の階層または階層項目用である場合、プロジェクトではビューのウィンドウ フレームへのポインターを使用して、既存のウィンドウを再表示します。

   - ドキュメント ビュー オブジェクトが存在し、このビューが同じ階層および階層項目用である場合、基になるドキュメント データ オブジェクトにアタッチできるならば、プロジェクトで 2 番目のビューを開くことができます。 それ以外の場合、プロジェクトではビューのウィンドウ フレームへのポインターを使用して、既存のウィンドウを再表示する必要があります。

   - ドキュメント データ オブジェクトのみが存在する場合、プロジェクトでは、そのビューにドキュメント データ オブジェクトを使用できるかどうかを判断する必要があります。 ドキュメント データ オブジェクトに互換性がある場合は、「[プロジェクト固有のエディターを開く](../extensibility/how-to-open-project-specific-editors.md)」で説明されている手順を実行します。

     ドキュメント データ オブジェクトに互換性がない場合は、ファイルが現在使用中であることを示すエラーがユーザーに表示されます。 このエラーは、ユーザーが [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] コア テキスト エディター以外のエディターを使用してファイルを開こうとしたそのときに、ファイルがコンパイル中である場合など、一時的な場合にのみ表示されます。 コア テキスト エディターでは、ドキュメント データ オブジェクトをコンパイラと共有できます。

3. ドキュメント データ オブジェクトまたはドキュメント ビュー オブジェクトがないためにドキュメントが開いていない場合は、「[プロジェクト固有のエディターを開く](../extensibility/how-to-open-project-specific-editors.md)」の手順を実行します。

## <a name="open-a-standard-editor"></a>標準のエディターを開く
 既に開いているファイルの標準エディターを開くには、次の手順に従います。

### <a name="to-open-a-standard-editor-for-an-open-file"></a>開いているファイルの標準エディターを開くには

1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> を呼び出します。

     このメソッドは、まず、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A> を呼び出してドキュメントがまだ開かれていないことを確認します。 ドキュメントが既に開いている場合、そのエディター ウィンドウが再表示されます。

2. ドキュメントが開いていない場合は、「[方法: 標準エディターを開く](../extensibility/how-to-open-standard-editors.md)」の手順を実行します。

## <a name="see-also"></a>関連項目
- [プロジェクト項目を開いて保存する](../extensibility/internals/opening-and-saving-project-items.md)
- [方法: プロジェクト固有のエディターを開く](../extensibility/how-to-open-project-specific-editors.md)
- [方法: 標準エディターを開く](../extensibility/how-to-open-standard-editors.md)
