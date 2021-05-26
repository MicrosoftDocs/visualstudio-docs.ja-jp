---
title: '方法: ビューをドキュメント データに添付する | Microsoft Docs'
description: 既存のドキュメント データ オブジェクトに新しいドキュメント ビューを添付することができる可能性があります。 ビューをアタッチできるかどうかを判断するには、次の手順に従います。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], custom - attach views to document data
ms.assetid: f92c0838-45be-42b8-9c55-713e9bb8df07
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8a034fc1c7cded7de4ead38cfba5d3410341c95d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057417"
---
# <a name="how-to-attach-views-to-document-data"></a>方法: ビューをドキュメント データに添付する
新しいドキュメント ビューがある場合は、それを既存のドキュメント データ オブジェクトにアタッチすることができる可能性があります。

## <a name="to-determine-if-you-can-attach-a-view-to-an-existing-document-data-object"></a>既存のドキュメント データ オブジェクトにビューをアタッチできるかどうかを判断する方法

1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>を実装します。

2. `IVsEditorFactory::CreateEditorInstance` の実装では、IDE から `QueryInterface` の実装が呼び出されると、既存のドキュメント データ オブジェクトに対して `CreateEditorInstance` を呼び出します。

    `QueryInterface` を呼び出すと、`punkDocDataExisting` パラメーターに指定されている既存のドキュメント データ オブジェクトを調べることができます。

    ただし、クエリを実行する必要がある正確なインターフェイスは、手順 4 で説明されているように、ドキュメントを開いているエディターによって異なります。

3. 既存のドキュメント データ オブジェクトに適切なインターフェイスが見つからない場合は、ドキュメント データ オブジェクトがエディターと互換性がないことを示すエラー コードをエディターに返します。

    IDE の <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> の実装では、ドキュメントが別のエディターで開かれていることを通知するメッセージ ボックスが表示され、それを閉じるかどうかを確認するメッセージが表示されます。

4. このドキュメントを閉じると、Visual Studio では 2 回目のエディター ファクトリの呼び出しがされます。 この呼び出しでは、`DocDataExisting` パラメーターは NULL と等しくなります。 エディター ファクトリを実装により、独自のエディターでドキュメント データ オブジェクトを開くことができます。

   > [!NOTE]
   > 既存のドキュメント データ オブジェクトを使用できるかどうかを判断するために、プライベート実装の実際の [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] クラスへのポインターをキャストすることによって、インターフェイスの実装に関するプライベートの知識を使用することもできます。 たとえば、すべての標準エディターでは、<xref:Microsoft.VisualStudio.OLE.Interop.IPersist> から継承する `IVsPersistFileFormat` を実装します。 したがって、<xref:Microsoft.VisualStudio.OLE.Interop.IPersist.GetClassID%2A> に対して `QueryInterface` を呼び出すことができます。また、既存のドキュメント データ オブジェクトのクラス ID が実装のクラス ID と一致する場合は、ドキュメント データ オブジェクトを操作できます。

## <a name="robust-programming"></a>信頼性の高いプログラミング
 Visual Studio から <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> メソッドの実装が呼び出されると、`punkDocDataExisting` パラメーター内の既存のドキュメント データ オブジェクトへのポインターが渡されます (存在する場合)。 このトピックの手順 4 のメモで説明されているように、`punkDocDataExisting` で返されたドキュメント データ オブジェクトを調べて、ドキュメント データ オブジェクトがエディターに適しているかどうかを判断します。 適切な場合は、「[複数のドキュメント ビューのサポート](../extensibility/supporting-multiple-document-views.md)」で説明されているように、エディター ファクトリからデータの 2 番目のビューが提供されるはずです。 そうでない場合は、適切なエラー メッセージが表示されます。

## <a name="see-also"></a>関連項目
- [複数のドキュメント ビューのサポート](../extensibility/supporting-multiple-document-views.md)
- [カスタム エディターでのドキュメント データとドキュメント ビュー](../extensibility/document-data-and-document-view-in-custom-editors.md)
