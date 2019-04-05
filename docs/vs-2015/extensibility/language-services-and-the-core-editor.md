---
title: 言語サービスとコア エディター |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - language services
ms.assetid: e03199a6-ad5f-4075-bfba-8d36865112b7
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1e708ffe796bfc9342bc20c3e7f20d5cf0d05058
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58963068"
---
# <a name="language-services-and-the-core-editor"></a>言語サービスとコア エディター
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio のエディターは、言語サービスに頻繁に関連付けられます。 その他のものは、言語サービスは、構文の色分け表示、ステートメント入力候補、IntelliSense、およびテキストの書式設定を提供します。  
  
## <a name="core-editors-and-document-data-objects"></a>コア エディターやドキュメント データ オブジェクト  
 コア エディターにアクセスする場合は、ドキュメント データとドキュメント ビュー オブジェクトは作成しません。 作成され、これら 2 つのオブジェクトを制御し、エディター ファクトリの実装で適切な呼び出しを作成してそれらへのハンドルを取得します。  
  
 詳細については、次を参照してください。[プロジェクトでファイルを開くエディターを決定する](../extensibility/internals/determining-which-editor-opens-a-file-in-a-project.md)します。  
  
## <a name="language-services-and-the-core-editor"></a>言語サービスとコア エディター  
 言語サービスを実装すると、ドキュメント ビューでデータを表示する方法を制御できます。 言語サービスは、情報とは、Visual C などの特定の言語に固有の動作を提供します。 テキスト バッファーが HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Editors のレジストリ キーからこのファイル名拡張子に関連付けられた言語サービスを決定するテキスト バッファーを作成して開いているドキュメントのファイル名拡張子を確認します。\\YourLanguageService {GUID} \Extensions します。 プロシージャを読み込み、標準の VSPackage は、VSPackage を読み込むし、言語サービスのインスタンスが作成されます。  
  
 基本的な言語サービスは、次の図に表示されます。  
  
 ![言語サービス モデル グラフィック](../extensibility/media/vslanguageservicemodel.gif "vsLanguageServiceModel")  
コア エディターと言語サービスのオブジェクト  
  
 コア エディター ドキュメント データ オブジェクトを選択してテキスト バッファーを呼びますで表される、<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>オブジェクト。 ドキュメント ビュー オブジェクトを選択してテキスト ビューを呼びますで表される、<xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow>オブジェクト。 これら 2 つのオブジェクトは、コア エディターの統合ビューを提供する言語サービスを介して連携します。 テキスト バッファーと、ドキュメント ウィンドウにテキスト ビューに表示される情報には、コード ウィンドウが呼び出されます。 コード ウィンドウのドキュメントは、コード ウィンドウ マネージャーによって管理されます。  
  
## <a name="see-also"></a>関連項目  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow>   
 [レガシ API を使用して、言語サービスのコンテキストを提供します。](../extensibility/providing-a-language-service-context-by-using-the-legacy-api.md)   
 [IntelliSense をホストしています。](../extensibility/intellisense-hosting.md)   
 [含まれている言語](../extensibility/contained-languages.md)   
 [従来の言語サービスの開発](../extensibility/internals/developing-a-legacy-language-service.md)
