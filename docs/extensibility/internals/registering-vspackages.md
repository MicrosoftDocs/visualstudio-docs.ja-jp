---
title: VSPackage の登録 | Microsoft Docs
description: .pkgdef ファイルには、本来ならばシステム レジストリに追加される情報が含まれています。 Visual Studio で .pkgdef ファイルを使用して VSPackage を記述または検索する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- managed VSPackages, registering
- registration, managed VSPackages
ms.assetid: 79b9424e-7e9b-4fc8-9b9f-00212674573c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9e2ed8d7c376f7d9f23e06786fefc1a955ebea3a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069466"
---
# <a name="registering-vspackages"></a>VSPackage の登録
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] は、VSPackage を記述および検索するときに .pkgdef ファイルに依存します。 .pkgdef ファイルには、本来ならばシステム レジストリに追加されるすべての登録情報が含まれています。 マネージド VSPackage は、ソース コードに属性を追加してから、生成されるアセンブリで [CreatePkgDef ユーティリティ](../../extensibility/internals/createpkgdef-utility.md)を実行して、.pkgdef ファイルを生成することによって登録されます。

## <a name="in-this-section"></a>このセクションの内容
- [VSPackage ファイルの場所を VS Shell に指定する](../../extensibility/internals/specifying-vspackage-file-location-to-the-vs-shell.md)

 VSPackage の読み込みパスについて説明します。

- [VSPackage の登録と登録解除](../../extensibility/registering-and-unregistering-vspackages.md)

 VSPackage の登録方法について説明します。
