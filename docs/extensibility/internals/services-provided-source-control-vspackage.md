---
title: 提供されるサービス (ソース管理 VSPackage) | Microsoft Docs
description: VSPackage ではサービスを通じてどのように機能を共有するかを説明します。これには、Visual Studio IDE とその VSPackage との対話が含まれます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- services, source control packages
- source control packages, services
ms.assetid: 9db07d70-87d2-4401-bc88-e3a49d81e9a2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fe1d9ee9805e6e86595f3f7f3cf640114c7030b9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080815"
---
# <a name="services-provided-source-control-vspackage"></a>提供されるサービス (ソース管理 VSPackage)
サービスは、VSPackage 間、および Visual Studio 統合開発環境 (IDE) とインストールされている VSPackage の間で機能を共有するための主要なメカニズムです。 Visual Studio IDE におけるサービスとその重要度の詳細については、「[サービスの使用と提供](../../extensibility/using-and-providing-services.md)」を参照してください。

## <a name="the-source-control-service"></a>ソース管理サービス
 Visual Studio には、IDE レベルのサービスとパッケージ レベルのサービスの 2 つのレイヤーが用意されています。 IDE レベルのサービスは、Visual Studio IDE によってネイティブに提供されます。 ソース管理パッケージでは、これらのサービスの一部を使用します。 VSPackage としてのソース管理パッケージでは、独自のプライベート ソース管理サービスを提供することによって、ソース管理機能を共有します。 ソース管理パッケージでは、これによって実装されたソース管理関連のインターフェイスのセットが、Visual Studio IDE で使用できるコントラクトの形式でカプセル化されます。

## <a name="see-also"></a>関連項目
- [デザイン要素](../../extensibility/internals/source-control-vspackage-design-elements.md)
