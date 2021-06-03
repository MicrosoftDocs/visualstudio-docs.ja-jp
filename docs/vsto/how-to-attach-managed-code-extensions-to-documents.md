---
title: '方法: マネージド コード拡張をドキュメントにアタッチする'
description: 既存の Microsoft Office Word 文書または Microsoft Office Excel ブックにカスタマイズ アセンブリをアタッチする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- managed code extensions [Office development in Visual Studio], attaching
- documents [Office development in Visual Studio], managed code extensions
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 60fc27345ef148fd47fdcee15924917ce63f8d68
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825499"
---
# <a name="how-to-attach-managed-code-extensions-to-documents"></a>方法: マネージド コード拡張をドキュメントにアタッチする
  既存の Microsoft Office Word 文書または Microsoft Office Excel ブックにカスタマイズ アセンブリをアタッチできます。 Visual Studio の Microsoft Office プロジェクトおよび開発ツールでサポートされている任意のファイル形式の文書またはブックを使用できます。 詳細については、「[ドキュメント レベルのカスタマイズのアーキテクチャ](../vsto/architecture-of-document-level-customizations.md)」を参照してください。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 Word または Excel ドキュメントにカスタマイズを アタッチするには、<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> クラスの <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.AddCustomization%2A> メソッドを使用します。 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> クラスは Microsoft Office がインストールされていないコンピューターで実行されるように設計されているため、このメソッドは、Microsoft Office 開発に直接関係のないソリューション (コンソール アプリケーションや Windows フォーム アプリケーションなど) で使用できます。

> [!NOTE]
> 指定したドキュメントに含まれていないコントロールがコードで想定されている場合、カスタマイズは読み込みに失敗します。

### <a name="to-attach-managed-code-extensions-to-a-document"></a>マネージド コード拡張をドキュメントにアタッチするには

1. コンソール アプリケーションや Windows フォーム プロジェクトなど、Microsoft Office を必要としないプロジェクトに、*Microsoft.VisualStudio.Tools.Applications.ServerDocument.dll* および *Microsoft.VisualStudio.Tools.Applications.Runtime.dll* アセンブリへの参照を追加します。

2. 次の **Imports** または **using** ステートメントをコード ファイルの先頭に追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDeploymentCS/Program.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDeploymentVB/Program.vb" id="Snippet4":::

3. 静的メソッド <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.AddCustomization%2A> を呼び出します。

     次のコード例では、<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.AddCustomization%2A> オーバーロードを使用します。 このオーバーロードは、ドキュメントの完全なパスと、ドキュメントにアタッチするカスタマイズの配置マニフェストの場所を指定する <xref:System.Uri> を受け取ります。 この例では、**WordDocument1.docx** という名前の Word 文書がデスクトップ上にあり、デスクトップ上にある **Publish** という名前のフォルダーに配置マニフェストが配置されていることを前提としています。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDeploymentCS/Program.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDeploymentVB/Program.vb" id="Snippet3":::

4. プロジェクトをビルドし、カスタマイズをアタッチするコンピューターでアプリケーションを実行します。 コンピューターには、Visual Studio 2010 Tools for Office ランタイムがインストールされている必要があります。

## <a name="see-also"></a>関連項目
- [ServerDocument クラスを使用してサーバー上のドキュメントを管理する](../vsto/managing-documents-on-a-server-by-using-the-serverdocument-class.md)
- [方法: マネージド コード拡張をドキュメントから削除する](../vsto/how-to-remove-managed-code-extensions-from-documents.md)
- [Office ソリューションでのアプリケーション マニフェストと配置マニフェスト](../vsto/application-and-deployment-manifests-in-office-solutions.md)
