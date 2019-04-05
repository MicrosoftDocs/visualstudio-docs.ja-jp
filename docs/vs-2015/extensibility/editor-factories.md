---
title: エディター ファクトリ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - editor factories
ms.assetid: cf4e8164-3546-441d-b465-e8a836ae7216
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fbf30d1fdb4fcce1e28a3c10c9949f1a11eae529
ms.sourcegitcommit: c496a77add807ba4a29ee6a424b44a5de89025ea
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2019
ms.locfileid: "58973901"
---
# <a name="editor-factories"></a>エディター ファクトリ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

エディター ファクトリは、エディターのオブジェクトを作成し、物理ビューと呼ばれる、ウィンドウ フレームに配置されます。 ドキュメント データとエディターとデザイナーを作成するために必要なドキュメント ビュー オブジェクトを作成します。 Visual Studio のコア エディターと任意の標準エディターを作成する、エディター ファクトリが必要です。 エディター ファクトリのカスタム エディターを作成もできます。  
  
 実装することで、エディター ファクトリを作成する、<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>インターフェイス。 次の例は、実装する方法を示しています。<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>エディター ファクトリを作成します。  
  
 [!code-csharp[VSSDKEditorFactories#1](../snippets/csharp/VS_Snippets_VSSDK/vssdkeditorfactories/cs/vssdkeditorfactoriespackage.cs#1)]
 [!code-vb[VSSDKEditorFactories#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkeditorfactories/vb/vssdkeditorfactoriespackage.vb#1)]  
  
 エディターは、そのエディターによって処理されるファイルの種類を開くことが最初に読み込まれます。 特定のエディターまたは既定のエディターを開くことができます。 既定のエディターを選択すると、統合開発環境 (IDE) は正しいエディターを開くための決定し、開かれます。 詳細については、次を参照してください。[プロジェクトでファイルを開くエディターを決定する](../extensibility/internals/determining-which-editor-opens-a-file-in-a-project.md)します。  
  
## <a name="registering-editor-factories"></a>エディター ファクトリの登録  
 作成したエディターを使用する前に処理できるファイル拡張子を含めて、についてはまず登録する必要があります。  
  
 マネージ コードで、VSPackage が書き込まれた場合は、マネージ パッケージ フレームワーク (MPF) メソッドを使用できます<xref:Microsoft.VisualStudio.Shell.Package.RegisterEditorFactory%2A>VSPackage が読み込まれた後に、エディター ファクトリを登録します。 VSPackage が、アンマネージ コードで記述されたかどうかを使用して、エディター ファクトリを登録する必要があります、<xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterEditors>サービス。  
  
### <a name="registering-an-editor-factory-by-using-managed-code"></a>マネージ コードを使用して、エディター ファクトリを登録します。  
 VSPackage ので、エディター ファクトリを登録する必要があります、`Initialize`メソッド。 まず`base.Initialize`を呼び出して<xref:Microsoft.VisualStudio.Shell.Package.RegisterEditorFactory%2A>の各エディター ファクトリ  
  
 マネージ コードで必要はありません、エディター ファクトリの登録を解除するため、VSPackage が処理されます。 また、エディター ファクトリが実装されている場合<xref:System.IDisposable>が登録解除時に自動的に破棄します。  
  
### <a name="registering-an-editor-factory-by-using-unmanaged-code"></a>アンマネージ コードを使用して、エディター ファクトリを登録します。  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>エディター パッケージ使用の実装、`QueryService`メソッドを呼び出す`SVsRegisterEditors`します。 ポインターを返しますこれを行う<xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors>します。 呼び出す、<xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors.RegisterEditor%2A>メソッドの実装を渡すことによって、<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>インターフェイス。 Mplement する必要があります<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>別のクラス。  
  
## <a name="the-editor-factory-registration-process"></a>エディター ファクトリの登録プロセス  
 次のプロセスでは、Visual Studio には、エディター ファクトリを使用して、エディターが読み込まれるときに発生します。  
  
1.  [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]プロジェクト システム コール<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>します。  
  
2.  このメソッドは、エディター ファクトリを返します。 Visual Studio の遅延がプロジェクト システムは、エディターを実際に必要になるまで、ただし、エディターのパッケージを読み込みます。  
  
3.  Visual Studio プロジェクト システムに、エディターが必要がある場合は呼び出して<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>、特殊なメソッドをドキュメントの表示と、ドキュメントの両方のデータ オブジェクトを返します。  
  
4.  場合、エディター ファクトリを使用して Visual Studio によって呼び出し<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>ドキュメント データ オブジェクトとドキュメント ビュー オブジェクトの両方を返すと、Visual Studio ドキュメント ウィンドウを作成、ドキュメント ビュー オブジェクトを配置し、実行中のドキュメントに入力ドキュメント データ オブジェクトのテーブル (RDT)。  
  
## <a name="see-also"></a>関連項目  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>   
 [ドキュメント テーブルの実行](../extensibility/internals/running-document-table.md)
