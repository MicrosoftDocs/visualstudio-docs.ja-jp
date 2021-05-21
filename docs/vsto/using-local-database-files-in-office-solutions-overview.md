---
title: Office ソリューションにおけるローカル データベース ファイル使用の概要
description: Office ソリューションに、SQL Server Express (.mdf) ファイルや Microsoft Office Access (.mdb) ファイルなどのデータベース ファイルを含める方法を説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office applications [Office development in Visual Studio], data
- data [Office development in Visual Studio], local
- local data [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 857038700a29f423250f006e743152bceea43c14
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99838233"
---
# <a name="use-local-database-files-in-office-solutions-overview"></a>Office ソリューションにおけるローカル データベース ファイル使用の概要
  Office ソリューションには、SQL Server Express ( *.mdf*) ファイルや Microsoft Office Access ( *.mdb*) ファイルなどのデータベース ファイルを含めることができます。 これにより、エンド ユーザーは、1 台のコンピューターでのみ使用されるローカル インベントリ ソリューションなど、集中管理されたデータベースを維持する必要がない場合に、ローカル データベースを維持できます。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="import-the-database-file-into-a-project"></a>データベース ファイルをプロジェクトにインポートする
 データベース ファイルをプロジェクトにインポートするには、**データ ソース構成ウィザード** を使用して、データベース ファイルに基づいてデータ ソースを作成します。 ウィザードによって、データベース ファイルと型指定されたデータセットがプロジェクトに追加されます。

## <a name="deploy-the-database-file"></a>データベース ファイルの配置
 **データ ソース構成ウィザード** で、相対パスを使用して、ローカル データベース ファイルへの接続を作成します。 これにより、ファイルの相対位置を維持する場合に、ソリューションを、あるコンピューターから別のコンピューターにコピーすることができます。

 ソリューションをサーバーに配置してから、ドキュメントを各エンド ユーザーに配布する場合は、データベース ファイルを手動で配布し、ドキュメントに対する同じ相対位置にそれを配置する必要もあります。 つまり、エンド ユーザーは、データベース ファイルを移動しない限り、自分のコンピューター上の新しい場所にドキュメントを移動することはできません。

## <a name="local-database-files-and-caching-the-dataset"></a>ローカル データベース ファイルとデータセットのキャッシュ
 Microsoft Office Excel と Microsoft Office Word のドキュメントレベルのソリューションでは、データセット インスタンスを <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> 属性でマークすることによって、ドキュメント内のデータセットをキャッシュすることができます。 **データ ソース構成ウィザード** を使用してデータベース ファイルをプロジェクトに追加するときは、型指定されたデータセットがプロジェクトに自動的に追加されます。 データはユーザーのコンピューター上にローカルに既にあるため、このデータセットに <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> を適用する必要はほぼありません。 詳細については、「[データのキャッシュ](../vsto/caching-data.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [Office ソリューションでコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)
- [方法: データベースのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-a-database.md)
- [方法: ホスト コントロールのデータでデータ ソースを更新する](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)
- [Office ソリューションを配置する](../vsto/deploying-an-office-solution.md)
- [キャッシュ データ](../vsto/caching-data.md)
