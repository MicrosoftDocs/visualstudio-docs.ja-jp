---
title: '方法: 開いているドキュメントのエディターを開く |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], opening for open documents
ms.assetid: 1a0fa49c-efa4-4dcc-bdc0-299b7052acdc
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c8342947681bcd8f698c2a646e917b353ec6c9dd
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66319321"
---
# <a name="how-to-open-editors-for-open-documents"></a>方法: 開いているドキュメントのエディターを開く
プロジェクトでは、ドキュメント ウィンドウが開いたら、プロジェクト最初判断しなければなりませんかどうか、ファイルが既に開いている別のエディターのドキュメント ウィンドウ。 ファイルがプロジェクトに固有のエディターで開くかを指定できますに登録されている標準のエディターのいずれかまたは[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]します。

## <a name="open-a-project-specific-editor"></a>プロジェクト固有のエディターを開く
 次の手順を使用して、既に開いているファイルをプロジェクトに固有のエディターを開きます。

### <a name="to-open-a-project-specific-editor-for-an-open-file"></a>開いているファイルのプロジェクトに固有のエディターを開く

1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A> メソッドを呼び出します。

    この呼び出しは、該当する場合に、ドキュメントの階層、階層のアイテムと、ウィンドウ フレームにポインターを返します。

2. ドキュメントが開いている場合は、プロジェクトは、またはドキュメント ビュー オブジェクトが存在することも、ドキュメント データ オブジェクトのみが存在するかどうかを確認する必要があります。

   - ドキュメント ビューのオブジェクトが存在する、このビューは、別の階層または階層アイテムの場合は、プロジェクトは、既存のウィンドウを再び表面化するビューのウィンドウ フレームへのポインターを使用します。

   - ドキュメント ビュー オブジェクトが存在し、このビューは、同じ階層および階層アイテムの場合、プロジェクトは、基になるドキュメント データ オブジェクトにアタッチできますが場合 2 つ目のビューを開くことができます。 それ以外の場合、プロジェクトでは、既存のウィンドウを再び表面化するビューのウィンドウ フレームへのポインターを使用する必要があります。

   - ドキュメントのデータ オブジェクトが存在する場合のみ、プロジェクトがそのビューに、ドキュメント データ オブジェクトを使用できるかどうかを決定する必要があります。 ドキュメント データ オブジェクトが互換性のある場合は、完全な手順で説明した[プロジェクト固有のエディターを開く](../extensibility/how-to-open-project-specific-editors.md)します。

     ドキュメント データ オブジェクトに互換性がない場合は、ファイルが現在使用中であることを示します。 ユーザーにエラーが表示されます。 など、ユーザーが以外のエディターを使用してファイルを開こうとしてファイルが同時にコンパイルされるときに、このエラーを一時的な場合は、表示のみか、 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] core テキスト エディター。 コアのテキスト エディターでは、コンパイラとドキュメント データ オブジェクトを共有できます。

3. ドキュメント データ オブジェクトまたはドキュメント ビュー オブジェクトがないため、ドキュメントが開いていない場合は、手順を完了[プロジェクト固有のエディターを開く](../extensibility/how-to-open-project-specific-editors.md)します。

## <a name="open-a-standard-editor"></a>標準のエディターを開く
 使用になっているファイルの標準のエディターを開くには、次の手順を開きます。

### <a name="to-open-a-standard-editor-for-an-open-file"></a>開いているファイルの標準のエディターを開く

1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> を呼び出す。

     このメソッドが最初に、ドキュメントがまだ開いていない呼び出してを検証します<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A>します。 ドキュメントが既に開いている場合、エディター ウィンドウが示されます。

2. ドキュメントが開いていない場合、その後の手順を完了[方法。標準のエディターを開く](../extensibility/how-to-open-standard-editors.md)します。

## <a name="see-also"></a>関連項目
- [開き、プロジェクト項目の保存](../extensibility/internals/opening-and-saving-project-items.md)
- [方法: 開いているプロジェクト固有のエディター](../extensibility/how-to-open-project-specific-editors.md)
- [方法: 標準のエディターを開く](../extensibility/how-to-open-standard-editors.md)
