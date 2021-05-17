---
title: '[プログラムから開く] コマンドを使用したファイルの表示 | Microsoft Docs'
description: プロジェクトが Visual Studio 統合開発環境 (IDE) で [プログラムから開く] コマンドを呼び出してファイルを表示する方法を説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, supporting Open With command
- Open With command
- persistence, supporting Open With command
ms.assetid: 53794bc3-1b73-4d40-954e-cfade1abddcf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e45e2c601873641b5ac79c54fd6709eb3f45f95d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069817"
---
# <a name="display-files-by-using-the-open-with-command"></a>[プログラムから開く] コマンドを使用してファイルを表示する
プロジェクトは、 **[プログラムから開く]** ダイアログ ボックスを表示することを IDE に要求できます。 この要求によりユーザーは、いくつかの標準エディターでサポートされているファイルを開くように求められます。 次に、このプロセスの手順を説明します。

1. プロジェクトが、`OSE_UseOpenWithDialog` の値を `OSEOpenDocEditor` パラメーターに指定して <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> を呼び出します。

2. IDE は、ドキュメントのファイル名拡張子に基づいて、指定されたドキュメントを開くことができるのは、レジストリに含まれるどのエディターかを判断し、この情報を **[プログラムから開く]** ダイアログ ボックスに表示します。

    > [!NOTE]
    > **[プログラムから開く]** ダイアログ ボックスに含める必要がある固有のエディターを持つプロジェクトでは、そのようなエディターごとにエディター ファクトリを登録する必要があります。 固有のエディターは、特定の種類のプロジェクトと共にのみ機能します。これは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> メソッドの実装で適用されます。 IDE には、コア テキスト エディターとバイナリ エディター用の組み込みエディター ファクトリが用意されています。 IDE では、登録されている各 Windows ファイル関連付けのために、エディター ファクトリのインスタンスも作成されます。 このようなファイルの例は Microsoft Word です。

3. ユーザーが **[プログラムから開く]** ダイアログ ボックスから項目を選択するとすぐに、IDE が <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> メソッドを呼び出してドキュメントを開きます。 詳細については、「[方法: 標準エディターを開く](../../extensibility/how-to-open-standard-editors.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [プロジェクト項目を開いて保存する](../../extensibility/internals/opening-and-saving-project-items.md)
- [[プログラムから開く] コマンドを使用してファイルを表示する](../../extensibility/internals/displaying-files-by-using-the-open-file-command.md)
- [方法: 標準エディターを開く](../../extensibility/how-to-open-standard-editors.md)
