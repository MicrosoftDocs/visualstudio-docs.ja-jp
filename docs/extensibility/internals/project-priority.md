---
title: プロジェクトの優先順位 | Microsoft Docs
description: ある項目が複数のプロジェクトのメンバーである場合に、その項目を開くための最適なプロジェクトを特定するために Visual Studio IDE で使用する優先順位スキームについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- projects [Visual Studio SDK], opening items
ms.assetid: 9f707592-2fb6-4f75-9269-f6d4700a998e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2ac0556e63b25f0f2a0df399cb23d5e2e9473008
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899642"
---
# <a name="project-priority"></a>プロジェクトの優先順位
プロジェクト項目は通常、ソリューション内の 1 つのプロジェクトのみのメンバーです。 そのため、IDE では、その項目を開くためにどのプロジェクトが使用されるかを容易に特定できます。 ただし、ある項目が複数のプロジェクトのメンバーである場合、IDE では、その項目を開くための最適なプロジェクトを特定するために優先順位スキームを使用します。

 次の一覧は、プロジェクトの優先順位スキームを示しています。

- IDE では、ソリューション内の各プロジェクトに対して <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject2.IsDocumentInProject%2A> メソッドを呼び出して、ドキュメントがそのプロジェクトのメンバーであるかどうかを判定します。

- ドキュメントがプロジェクトのメンバーである場合、そのプロジェクトは、そのドキュメントの処理に応じてプロジェクトで割り当てる優先順位で応答します。 たとえば、言語プロジェクトは言語ソース ファイルについては高い優先順位で応答しますが、そのビルド プロセスの一部として使用されていない認識されないファイルの種類についてはより低い優先順位で応答します。

- ドキュメントにプロジェクト固有のカスタム エディターまたはデザイナーを提供するプロジェクトにも高い優先順位が与えられます。

- <xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY> 列挙型は、ドキュメントの優先順位の値を提供します。

- 最も高い優先事項を指定するプロジェクトには、ドキュメントを開くためのコンテキストが与えられます。 2 つのプロジェクトが等しい優先順位の値を返した場合は、アクティブなプロジェクトが優先されます。 ソリューション内のどのプロジェクトもドキュメントを開くことができると応答しない場合、IDE では、そのドキュメントを [その他のファイル] プロジェクトに配置します。 詳細については、「[その他のファイル プロジェクト](../../extensibility/internals/miscellaneous-files-project.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [その他のファイル プロジェクト](../../extensibility/internals/miscellaneous-files-project.md)
- [方法: 開いているドキュメントのエディターを開く](../../extensibility/how-to-open-editors-for-open-documents.md)
- [プロジェクト テンプレートとプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)
