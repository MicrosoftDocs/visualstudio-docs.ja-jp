---
title: ServerDocument クラスを使用してサーバー上のドキュメントを管理する
description: Visual Studio Tools for Office Runtime で ServerDocument クラスを使用して、ドキュメント レベルのカスタマイズのいくつかの側面を管理する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], managing on server
- Office documents [Office development in Visual Studio, managing on server
- ServerDocument class, managing documents on server
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 17a25ca382cfbbc762731afacaa628de616cfe1c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99879476"
---
# <a name="manage-documents-on-a-server-by-using-the-serverdocument-class"></a>ServerDocument クラスを使用してサーバー上のドキュメントを管理する
  [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] の `ServerDocument` クラスを使用すると、Microsoft Office Word と Microsoft Office Excel がインストールされていない場合でも、ドキュメント レベルのカスタマイズのさまざまな側面を管理することができます。 実行できる管理タスクは以下のとおりです。

- ドキュメントまたはブックのデータ キャッシュにあるデータへのアクセスおよびそのデータの変更。 詳細については、「[ドキュメントのキャッシュされたデータを操作する](#CachedData)」を参照してください。

- ドキュメントに関連付けられているカスタマイズ アセンブリの管理。 詳細については、「[ドキュメントのカスタマイズを管理する](#CustomizationInfo)」を参照してください。

  [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="understand-the-serverdocument-class"></a>ServerDocument クラスについて
 `ServerDocument` クラスは Office がインストールされていないコンピューターでの使用を目的としています。 したがって、このクラスは通常、Office プロジェクトではなく、コンソール プロジェクトや Windows フォーム プロジェクトなどの Office に統合されないアプリケーションで使用します。 *Microsoft.VisualStudio.Tools.Applications.ServerDocument.dll* アセンブリの <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> クラスを使用します。

 `ServerDocument` クラスは、[!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] を使用して作成されたドキュメント レベルのカスタマイズの操作に使用できます。

 Visual Studio 2010 Tools for Office Runtime および .NET Framework 用 Office 拡張機能の詳細については、「[Visual Studio Tools for Office ランタイムの概要](../vsto/visual-studio-tools-for-office-runtime-overview.md)」を参照してください。

> [!NOTE]
> `Visual Studio Tools for Office` システム (バージョン 3.0 Runtime) の `ServerDocument` クラスを使用するレガシ アプリケーションがある場合は、アプリケーションを実行するコンピューターに `Visual Studio Tools for Office` システム (バージョン 3.0 Runtime) をインストールする必要があります。 `Visual Studio 2010 Tools for Office runtime` では、これらのアプリケーションを実行できません。

## <a name="work-with-cached-data-in-the-document"></a><a name="CachedData"></a> ドキュメントのキャッシュされたデータを操作する
 `ServerDocument` クラスには、カスタマイズされたドキュメント内のデータ キャッシュの操作に使用できるメンバーが用意されています。 キャッシュされたデータの詳細については、「[キャッシュ データ](../vsto/caching-data.md)」および「[サーバー上のドキュメントのデータにアクセスする](../vsto/accessing-data-in-documents-on-the-server.md)」を参照してください。

 次の表は、キャッシュされたデータの操作に使用できるメンバーを示しています。

|タスク|使用するメンバー|
|----------|-------------------|
|ドキュメントにデータ キャッシュがあるかどうかを確認する。|<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.IsCacheEnabled%2A> メソッド。|
|ドキュメント内のキャッシュされたデータにアクセスする。<br /><br /> 詳細については、「[サーバー上のドキュメントのデータにアクセスする](../vsto/accessing-data-in-documents-on-the-server.md)」を参照してください。|<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A> プロパティ。|

## <a name="manage-the-document-customization"></a><a name="CustomizationInfo"></a> ドキュメントのカスタマイズを管理する
 `ServerDocument` クラスのメンバーを使用して、ドキュメントに関連付けられているカスタマイズ アセンブリを管理できます。 たとえば、ドキュメントのカスタマイズをプログラムによって削除し、そのドキュメントをカスタマイズから除外することもできます。

 次の表は、カスタマイズ アセンブリの管理に使用できるメンバーを示しています。

|タスク|使用するメンバー|
|----------|-------------------|
|ドキュメントがドキュメント レベルのカスタマイズの一部であるかどうかを確認する。|<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.GetCustomizationVersion%2A> メソッド。|
|プログラムによって実行時にカスタマイズをドキュメントにアタッチする。<br /><br /> 詳細については、「[方法: マネージド コード拡張をドキュメントにアタッチする](../vsto/how-to-attach-managed-code-extensions-to-documents.md)」を参照してください|<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.AddCustomization%2A> メソッドの 1 つ。|
|プログラムによって実行時にドキュメントからカスタマイズを削除する。<br /><br /> 詳細については、「[方法: マネージド コード拡張をドキュメントから削除する](../vsto/how-to-remove-managed-code-extensions-from-documents.md)」を参照してください。|<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.RemoveCustomization%2A> メソッド。|
|ドキュメントに関連付けられている配置マニフェストの URL を取得する。|<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.DeploymentManifestUrl%2A> プロパティ。|

## <a name="see-also"></a>関連項目
- [方法: マネージド コード拡張をドキュメントにアタッチする](../vsto/how-to-attach-managed-code-extensions-to-documents.md)
- [方法: マネージド コード拡張をドキュメントから削除する](../vsto/how-to-remove-managed-code-extensions-from-documents.md)
- [Visual Studio Tools for Office ランタイムの概要](../vsto/visual-studio-tools-for-office-runtime-overview.md)
- [キャッシュ データ](../vsto/caching-data.md)
