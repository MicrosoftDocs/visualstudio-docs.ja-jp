---
title: .proj および .sln ファイルからソース管理情報を削除する
description: ソース管理プラグイン API では、SCC 情報はプロジェクト ファイルとソリューション ファイルではなく MSSCCPRJ.SCC ファイルに格納されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, .sln and .proj files
ms.assetid: 7b06883f-35de-41e2-9a9e-d3edba236f17
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5fd4b4f12ab819903408d4d895773664e892b3ac
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069388"
---
# <a name="removal-of-source-control-information-from-proj-and-sln-files"></a>.proj および .sln ファイルからのソース管理情報の削除

ソース管理プラグイン API のバージョン 1.2 では、SCC 情報は MSSCCPRJ.SCC ファイルに格納されます。 MSSCCPRJ.SCC ファイルの利点は、.proj ファイルや .sln ファイルと違って SCC 情報がソース管理されないことです。

## <a name="version-12-changes"></a>バージョン 1.2 の変更点

 ソース管理プラグイン API バージョン 1.1 に基づいたソース管理プラグインでは、ソース管理に関する情報はプロジェクト (.proj) ファイルとソリューション (.sln) ファイルに格納されます。 ソース管理情報のデータベースの場所は AuxPath によって指定され、データベース内の特定の場所は ProjName によって指定されます。 この動作により、分岐、フォーク、またはコピー操作の後に問題が発生する可能性があります。これは、ProjName は通常、これらの操作のいずれかを実行した後は無効になるためです。

 ソース管理プラグイン API バージョン 1.1 では、IDE で ~SAK ファイルを使用して、ソース管理情報を格納する MSSCCPRJ.SCC メソッドをプラグインがサポートしているかどうかを検出していました。 ソース管理プラグイン API バージョン 1.2 は、~SAK ファイルを使用せずに MSSCCPRJ.SCC ファイルのサポートを検出するための新しい機能を提供します。 詳細については、「[~SAK ファイルの削除](../../extensibility/internals/elimination-of-tilde-sak-files.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [ソース管理プラグイン API バージョン 1.2 の新機能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
