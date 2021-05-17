---
title: ソース管理プラグインの使用開始 | Microsoft Docs
description: ソース コードのバージョン管理で使用するためにソース管理プラグイン API で定義されている関数を実装するソース管理プラグインの作成について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, getting started
- getting started, source control plug-ins
ms.assetid: 46ac1f9f-4ecc-4a72-88d3-4c7e1647e1cb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1c1279fd425e8519ede49763ee2a307778c91e9e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061256"
---
# <a name="get-started-with-source-control-plug-ins"></a>ソース管理プラグインの使用を開始する
ソース管理プラグインを作成するには、ソース管理プラグイン API で定義されている関数を実装する DLL を作成してから、ソース コードのバージョン管理で使用できるように、その DLL を [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に登録する必要があります。

 ソース管理プラグインでは、3 つのバージョン (バージョン 1.1、1.2、1.3) のソース管理プラグイン API が使用できます。ここに記載されているソース管理プラグイン API はバージョン 1.3 です。 これは、バージョン 1.1 および 1.2 をサポートするソース管理プラグインと完全に互換性があるように設計されました。 「[ソース管理プラグイン API バージョン 1.3 の新機能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-3.md)」セクションでは、最新バージョンのソース管理プラグイン API でサポートされている新機能について詳細に説明しています。

## <a name="in-this-section"></a>このセクションの内容
- [方法: ソース管理プラグインをインストールする](../../extensibility/internals/how-to-install-a-source-control-plug-in.md)

 ソース管理 DLL をプラグインするために必要なレジストリ エントリを作成する方法について説明します。

- [ソース管理プラグイン API バージョン 1.3 の新機能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-3.md)

 バージョン 1.3 でソース管理プラグイン API に加えられた変更の概要について説明します。

- [ソース管理プラグイン API バージョン 1.2 の新機能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)

 バージョン 1.2 でソース管理プラグイン API に加えられた変更の概要について説明します。

## <a name="related-sections"></a>関連項目
- [ソース管理プラグイン](../../extensibility/source-control-plug-ins.md)

 ソース管理プラグイン API のすべての要素の完全な一覧を提供します。

- [ソース管理プラグインの作成](../../extensibility/internals/creating-a-source-control-plug-in.md)

 ソース管理プラグイン SDK を定義し、含まれているリソースについて説明します。
