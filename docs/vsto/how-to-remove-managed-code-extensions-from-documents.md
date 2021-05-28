---
title: '方法: マネージド コード拡張をドキュメントから削除する'
description: Microsoft Word または Excel 用のドキュメント レベルのカスタマイズの一部であるドキュメントやブックから、カスタマイズ アセンブリをプログラムによって削除します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- managed code extensions [Office development in Visual Studio], removing
- documents [Office development in Visual Studio], managed code extensions
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 129b1bda44abf7283efe1996f1898491025ee9d9
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825447"
---
# <a name="how-to-remove-managed-code-extensions-from-documents"></a>方法: マネージド コード拡張をドキュメントから削除する
  Microsoft Office Word または Microsoft Office Excel 用のドキュメント レベルのカスタマイズの一部であるドキュメントやブックから、カスタマイズ アセンブリをプログラムによって削除できます。 その後、ユーザーはドキュメントを開いて内容を表示することはできますが、ドキュメントに追加されたカスタム ユーザー インターフェイス (UI) は表示されなくなり、コードは実行されなくなります。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 カスタマイズ アセンブリは、[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] によって提供される `RemoveCustomization` メソッドのいずれかを使用して削除できます。 どのメソッドを使用するかは、カスタマイズを実行時に削除する (つまり、Word 文書または Excel ブックが開いているときにカスタマイズ内でコードを実行する) のか、閉じたドキュメントや Microsoft Office がインストールされていないサーバー上のドキュメントからカスタマイズを削除するのかによって決まります。

## <a name="to-remove-the-customization-assembly-at-run-time"></a>カスタマイズ アセンブリを実行時に削除するには

1. カスタマイズ コードで、<xref:Microsoft.Office.Tools.Word.Document.RemoveCustomization%2A> メソッド (Word の場合) または <xref:Microsoft.Office.Tools.Excel.Workbook.RemoveCustomization%2A> メソッド (Excel の場合) を呼び出します。 このメソッドは、カスタマイズが不要になった後で呼び出すようにしてください。

     コード内のどこでこのメソッドを呼び出すかは、カスタマイズの使用方法によって異なります。 たとえば、(カスタマイズではなく) ドキュメントそのものだけを必要とするクライアントにドキュメントを送信するユーザーが、その準備を終えた後にカスタマイズの機能を使用する場合は、何らかの UI を提供して、ユーザーがそれをクリックしたときに `RemoveCustomization` が呼び出されるようにすることができます。 また、ドキュメントが最初に開かれたときにデータを入力するカスタマイズで、ユーザーが直接アクセスする機能が他に提供されない場合は、カスタマイズによってドキュメントの初期化が完了した直後に RemoveCustomization を呼び出すことができます。

## <a name="to-remove-the-customization-assembly-from-a-closed-document-or-a-document-on-a-server"></a>閉じているドキュメントやサーバー上のドキュメントからカスタマイズ アセンブリを削除するには

1. コンソール アプリケーションや Windows フォーム プロジェクトなど、Microsoft Office を必要としないプロジェクトでは、*Microsoft.VisualStudio.Tools.Applications.ServerDocument.dll* アセンブリへの参照を追加します。

2. 次の **Imports** または **using** ステートメントをコード ファイルの先頭に追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDeploymentCS/Program.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDeploymentVB/Program.vb" id="Snippet1":::

3. <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> クラスの静的 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.RemoveCustomization%2A> メソッドを呼び出し、パラメーターのソリューション ドキュメント パスを指定します。

     次のコード例では、デスクトップ上にある *WordDocument1.docx* というドキュメントからカスタマイズを削除する場合を想定しています。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDeploymentCS/Program.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDeploymentVB/Program.vb" id="Snippet2":::

4. プロジェクトをビルドし、カスタマイズを削除するコンピューターでアプリケーションを実行します。 コンピューターには、Visual Studio 2010 Tools for Office ランタイムがインストールされている必要があります。

## <a name="see-also"></a>関連項目
- [ServerDocument クラスを使用してサーバー上のドキュメントを管理する](../vsto/managing-documents-on-a-server-by-using-the-serverdocument-class.md)
- [方法: マネージド コード拡張機能をドキュメントにアタッチする](../vsto/how-to-attach-managed-code-extensions-to-documents.md)
