---
title: ソース管理プラグインを検索するためのキーとして使用される文字列
description: ソース管理プラグインに関する情報を検索する場合に、レジストリにアクセスするためのキーとなる文字列について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, strings used for finding
ms.assetid: c1e31f76-42a1-4c3d-afb2-664044ef12fd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b61c13973ac6668814fbc3ba076b373d6e0b1e44
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056299"
---
# <a name="strings-used-as-keys-for-finding-a-source-control-plug-in"></a>ソース管理プラグインを検索するためのキーとして使用される文字列
次の文字列は、ソース管理プラグインに関する情報を検索する場合に、レジストリにアクセスするためのキーです。

 `STR_SCC_PROVIDER_REG_LOCATION`、`STR_PROVIDERREGKEY`、`STR_SCCPROVIDERPATH`、および `STR_SCCPROVIDERNAME` は、Visual Studio のソース管理プラグインとして DLL を登録するために使用されるレジストリ キーまたは値です。

 `SCC_PROJECTNAME_KEY`、`SCC_PROJECTAUX_KEY`、`SCC_KEY, SCC_FILE_SIGNATURE`、および `SCC_STATUS_FILE` は、MSSCCPRJ.SCC ファイルの形式を記述するために使用されます。

## <a name="string-keys-and-values"></a>文字列のキーと値

|キー|値|
|---------|-----------|
|`STR_SCC_PROVIDER_REG_LOCATION`|Software\SourceCodeControlProvider|
|`STR_PROVIDERREGKEY`|ProviderRegKey|
|`STR_SCCPROVIDERPATH`|SCCServerPath|
|`STR_SCCPROVIDERNAME`|SCCServerName|
|`STR_SCC_INI_SECTION`|ソース コード管理|
|`STR_SCC_INI_KEY`|SourceCodeControlProvider|
|`SCC_PROJECTNAME_KEY`|SCC_Project_Name|
|`SCC_PROJECTAUX_KEY`|SCC_Aux_Path|
|`SCC_STATUS_FILE`|MSSCCPRJ.SCC|
|`SCC_KEY`|SCC|
|`SCC_FILE_SIGNATURE`|ソース コード管理ファイル|
|`SCC_NSE`|名前空間拡張機能|
|`SCC_NSE_PREFIX`|プロトコルのプレフィックス|
|`SCC_NSE_DisableOpenSCC`|DisableOpenFromSourceControl|
|`STR_SCCHELPCOLLECTION`|HelpCollection|
|`STR_UI_LANGUAGE`|UILanguage|
|`STR_SRCSAFE_ROOT_KEY`|Software\Microsoft\SourceSafe|

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
- [方法: ソース管理プラグインのインストール](../extensibility/internals/how-to-install-a-source-control-plug-in.md)
- [MSSCCPRJ.SCC File](../extensibility/mssccprj-scc-file.md)
