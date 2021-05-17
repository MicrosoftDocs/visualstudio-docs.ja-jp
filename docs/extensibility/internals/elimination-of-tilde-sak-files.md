---
title: ~SAK ファイルの削除 | Microsoft Docs
description: ソース管理プラグイン API 1.2 からの ~SAK ファイルの削除と、このファイルが機能フラグと新しい関数にどのように置き換えられているかについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- temporary files
- ~sak files
- source control plug-ins, ~SAK files
ms.assetid: 5277b5fa-073b-4bd1-8ba1-9dc913aa3c50
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: cf0f8bc567a097d4bb7d400f829489c517e9a68f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061239"
---
# <a name="elimination-of-sak-files"></a>~SAK ファイルの削除
ソース管理プラグイン API 1.2 では、 *~SAK* ファイルは、ソース管理プラグインが *MSSCCPRJ* ファイルと共有チェックアウトをサポートしているかどうかを検出する機能フラグと新しい関数に置き換えられています。

## <a name="sak-files"></a>~SAK ファイル
Visual Studio .NET 2003 では、 *~SAK* というプレフィックスが付いた一時ファイルが作成されました。 これらのファイルは、ソース管理プラグインが次のものをサポートしているかどうかを判定するために使用されます。

- *MSSCCPRJ.SCC* ファイル。

- 複数の (共有) チェックアウト。

ソース管理プラグイン API 1.2 で提供されている高度な関数をサポートするプラグインの場合、IDE では、以降のセクションで詳細に説明する新しい機能、フラグ、関数を使用して、一時ファイルを作成しなくてもこれらの機能を検出できます。

## <a name="new-capability-flags"></a>新しい機能フラグ
 `SCC_CAP_SCCFILE`

 `SCC_CAP_MULTICHECKOUT`

## <a name="new-functions"></a>新しい関数
- [SccWillCreateSccFile](../../extensibility/sccwillcreatesccfile-function.md)

- [SccIsMultiCheckoutEnabled](../../extensibility/sccismulticheckoutenabled-function.md)

 ソース管理プラグインでは、複数の (共有) チェックアウトをサポートしている場合は `SCC_CAP_MULTICHECKOUT` 機能を宣言し、`SccIsMultiCheckOutEnabled` 関数を実装します。 この関数は、ソース管理されているいずれかのプロジェクトでチェックアウト操作が実行されるたびに呼び出されます。

 ソース管理プラグインでは、*MSSCCPRJ.SCC* ファイルの作成および使用をサポートしている場合は `SCC_CAP_SCCFILE` 機能を宣言し、[SccWillCreateSccFile](../../extensibility/sccwillcreatesccfile-function.md) を実装します。 この関数は、ファイルの一覧と共に呼び出されます。 この関数は、各ファイルに対して `TRUE' or 'FALSE` を返すことにより、Visual Studio がそのファイルのために *MSSCCPRJ.SCC* ファイルを使用する必要があるかどうかを示します。 ソース管理プラグインがこれらの新機能と機能をサポートしないことを選択した場合、次のレジストリキーを使用してこれらのファイルの作成を無効にすることができます。

 **[HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl]DoNotCreateTemporaryFilesInSourceControl** = *dword:00000001*

> [!NOTE]
> このレジストリ キーが *dword:00000000* に設定されている場合は、このキーが存在しないことに相当するため、Visual Studio では引き続きこの一時ファイルを作成しようとします。 ただし、このレジストリ キーが *dword:00000001* に設定されている場合、Visual Studio では、この一時ファイルを作成しようとしません。 代わりに、ソース管理プラグインが *MSSCCPRJ.SCC* ファイルをサポートしていないと見なし、共有チェックアウトをサポートしません。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API バージョン 1.2 の新機能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
