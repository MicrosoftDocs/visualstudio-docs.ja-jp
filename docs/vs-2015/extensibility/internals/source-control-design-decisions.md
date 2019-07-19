---
title: ソース コントロールの設計上の決定 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], design decisions
ms.assetid: 5f60ec1a-5a74-4362-8293-817a4dd73872
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 89d125dc52340e8528ee9692d5de00784632e6f2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68187898"
---
# <a name="source-control-design-decisions"></a>ソース管理のデザインの方針
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ソース管理を実装する場合は、プロジェクトの次の設計に関する決定事項を検討してください。  
  
## <a name="will-information-be-shared-or-private"></a>情報は共有またはプライベートか。  
 最も重要な設計上の決定は、どのような情報が共有でき、何が私的なものであるかということです。 たとえば、プロジェクトのファイルのリストは共有されていますが、このファイルのリスト内で、一部のユーザーはプライベートファイルを使用することを希望する場合があります。 コンパイラの設定は共有されていますが、スタートアッププロジェクトは通常プライベートです。 設定では、純粋に共有、上書きと共有、または純粋にプライベートのいずれかです。 仕様では、プライベートなアイテムなど、ソリューション ユーザー オプション (.suo) ファイルはチェックされませんに[!INCLUDE[vsvss](../../includes/vsvss-md.md)]します。 .Suo ファイルなどのプライベート ファイル、または作成した特定のプライベートファイル（たとえば、Visual C＃ の場合は .csproj.user ファイル、Visual Basic の場合は .vbproj.user ファイル）にプライベートな情報を必ず格納してください。  
  
 この決定は、包括的な -アイテムごとに行んだことができます。  
  
## <a name="will-the-project-include-special-files"></a>プロジェクトで特別なファイルが含まれますか。  
 もう 1 つの重要な設計上の決定は、プロジェクトの構造が特別なファイルを使用するかどうかです。 特別なファイルは、表示されるは、ソリューション エクスプ ローラーと、チェックインとチェック アウト ダイアログ ボックスにあるファイルを基になるファイルを非表示です。 特別なファイルを使用する場合は、次のガイドラインに従います。  
  
1. プロジェクトのルート ノードを特別なファイルを関連付けないでください-これは、プロジェクト ファイル自体。 プロジェクト ファイルは、1 つのファイルである必要があります。  
  
2. 特別なファイルを追加、削除、または適切なプロジェクトで名前を変更するときに<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>ファイルは、特殊なファイルを示すフラグを設定してイベントを発生する必要があります。 これらのイベントは、応答を呼び出し、適切なプロジェクトで、環境によって呼び出される<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>メソッド。  
  
3. プロジェクトまたはエディターを呼び出すと<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>ファイルの場合、そのファイルに関連付けられている特別なファイルに自動的にチェック アウトされていません。親ファイルと共にで特別なファイルを渡します。 環境に渡されるすべてのファイル間のリレーションシップを検出し、チェック アウトの UI で、特殊なファイルを適切に非表示にします。  
  
## <a name="see-also"></a>関連項目  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>   
 [ソース管理のサポート](../../extensibility/internals/supporting-source-control.md)
