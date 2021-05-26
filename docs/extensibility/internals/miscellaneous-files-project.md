---
title: その他のファイル プロジェクト | Microsoft Docs
description: Visual Studio プロジェクトでファイルを開くために使用できる 2 種類のエディターと、使用するエディターを決定するプロジェクトのロールについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- files, adding existing files to solutions
- Miscellaneous Files project
- Solution Items folder
- files, opening with Miscellaneous Files project
ms.assetid: 93a278a8-d4f4-400b-8945-4f1b0a2b5bac
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b79eaaeaf94954e2d3dc1bd855b56bee5b8bdae4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063280"
---
# <a name="miscellaneous-files-project"></a>その他のファイル プロジェクト
ユーザーがプロジェクト項目を開くと、IDE はソリューション内のプロジェクトのメンバーではないすべての項目をその他のファイル プロジェクトに割り当てます。

 プロジェクトは、ユーザーがプロジェクト項目を開いたときにどのエディターが使用されるかを決定するうえで重要な役割を果たします。 プロジェクトは、プロジェクト固有のエディターまたは標準エディターを使用して、特定のファイルを開くように設計できます。

 プロジェクト固有のエディターを使用する場合、通常、ユーザーが特別な知識を持っているか、またはプロジェクトから特殊なインターフェイスを使用している必要があります。 詳細については、「[方法: プロジェクト固有エディターを開く](../../extensibility/how-to-open-project-specific-editors.md)」を参照してください。

 標準エディターでは、任意のプロジェクトで特定の拡張機能の任意のファイルを開くことができます。 ユーザーは、プロジェクト用に、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] テキスト エディターなどの一部の標準エディターをカスタマイズできますが、パブリック文字は引き続き保持されます。 標準エディターは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> メソッドを使用して作成されます。

 応答としてプロジェクト項目を開けるプロジェクトがソリューション内にない場合に、任意のファイルを開く、その他のファイル プロジェクトと呼ばれる特別なプロジェクトが IDE に用意されています。

 この特別なプロジェクトでは、プロジェクトのコンテキストの外部でファイルを開くことができます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenDocumentViaProject%2A> メソッドの処理中、その他のファイル プロジェクトは常に低優先度で応答します。 そのため、ファイルを開くことができる高優先度のプロジェクトがあれば、その他のファイル プロジェクトは常に処理を譲ります。

 その他のファイル プロジェクトでは、 **[新しいプロジェクト]** ダイアログ ボックスを使用して明示的に作成する必要はありません。 また、その他のファイル プロジェクトでは、プロジェクト メンバーの一覧は永続的には管理されません。 オプションの機能を使用して、各ユーザーが最近使用したファイルの一覧を記録します。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument>
- <xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY>
- [方法: プロジェクト固有のエディターを開く](../../extensibility/how-to-open-project-specific-editors.md)
- [方法: 標準のエディターを開く](../../extensibility/how-to-open-standard-editors.md)
- [プロジェクト テンプレートとプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)
- [プロジェクト テンプレートとプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)
