---
title: '方法: ドキュメント データをビューのアタッチ |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - attach views to document data
ms.assetid: f92c0838-45be-42b8-9c55-713e9bb8df07
caps.latest.revision: 23
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 50b9ef50e077a4e335b0c4f0718a3c51624e09c8
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60080645"
---
# <a name="how-to-attach-views-to-document-data"></a>方法: ビューをドキュメントデータに添付する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

新しいドキュメント ビューがある場合は、既存のドキュメント データ オブジェクトにアタッチすることができます。  
  
### <a name="to-determine-if-you-can-attach-a-view-to-an-existing-document-data-object"></a>既存のドキュメント データ オブジェクトにビューを割り当てることができるかどうかを判断するには  
  
1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>を実装します。  
  
2. 実装で`IVsEditorFactory::CreateEditorInstance`、呼び出す`QueryInterface`IDE を呼び出すときに既存のドキュメント データ オブジェクトに、`CreateEditorInstance`実装します。  
  
     呼び出す`QueryInterface`で指定されている、既存のドキュメント データ オブジェクトを調べることができます、`punkDocDataExisting`パラメーター。  
  
     クエリを実行する必要があります、正確なインターフェイスはただしに、ステップ 4 で説明した、ドキュメントを開いているエディターによって異なります。  
  
3. 既存のドキュメント データ オブジェクトに適切なインターフェイスが見つからない場合は、ドキュメント データ オブジェクトが、エディターで互換性がないことを示す、エディターにエラー コードを返します。  
  
     IDE の実装で<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>ドキュメントが別のエディターで開かれているし、終了するように要求するメッセージ ボックスを通知します。  
  
4. このドキュメントを閉じると場合、Visual Studio を呼び出して、エディター ファクトリ 2 回目にします。 この呼び出しで、`DocDataExisting`パラメーターが NULL です。 エディター ファクトリの実装は、独自のエディターで、ドキュメント データ オブジェクトを開くことができます。  
  
    > [!NOTE]
    >  既存のドキュメント データ オブジェクトを使用できるかどうかを確認するのに使用することもプライベート インターフェイスの実装に関する知識、実際へのポインターをキャストすることによって[!INCLUDE[vcprvc](../includes/vcprvc-md.md)]プライベートな実装のクラス。 たとえば、すべての標準エディターの実装`IVsPersistFileFormat`から継承される<xref:Microsoft.VisualStudio.OLE.Interop.IPersist>します。 そのため、呼び出すことができます`QueryInterface`の<xref:Microsoft.VisualStudio.OLE.Interop.IPersist.GetClassID%2A>、既存のドキュメント データ オブジェクトのクラス ID の実装と一致するかどうか、クラス ID、ドキュメント データ オブジェクトを使用することができます。  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  
 Visual Studio での実装を呼び出すときに、<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>メソッドに渡しますポインターで既存のドキュメント データ オブジェクトに、`punkDocDataExisting`パラメーターを 1 つが存在する場合。 返されるドキュメント データ オブジェクトを調べます`punkDocDataExisting`ドキュメント データ オブジェクトがこのトピックの手順の手順 4. でメモで説明したように、エディターの適切なかどうかを判断します。 適切な場合、エディター ファクトリで説明したように、データの 2 つ目のビューを提供する必要があります[Supporting Multiple Document Views](../extensibility/supporting-multiple-document-views.md)します。 それ以外の場合は、適切なエラー メッセージを表示する必要がありますから。  
  
## <a name="see-also"></a>関連項目  
 [複数のドキュメント ビューのサポート](../extensibility/supporting-multiple-document-views.md)   
 [カスタム エディターでのドキュメント データとドキュメント ビュー](../extensibility/document-data-and-document-view-in-custom-editors.md)
