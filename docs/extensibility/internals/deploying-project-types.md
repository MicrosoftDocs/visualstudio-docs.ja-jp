---
title: プロジェクト タイプのデプロイ | Microsoft Docs
description: Visual Studio SDK で、新しいプロジェクト タイプ アグリゲーターと再配布用の Windows インストーラー パッケージを使用して、マネージド コード プロジェクト タイプをデプロイする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], managed-code
- projects [Visual Studio SDK], aggregator
ms.assetid: 7f132f67-8589-464c-90dc-0d57ae02aa8f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 121dda58b8e01c5b0029d8b3c93ef66d2657446e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090994"
---
# <a name="deploy-project-types"></a>プロジェクト タイプのデプロイ
[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] では、新しいプロジェクト タイプ アグリゲーター (*ProjectAggregator2.dll*) と、再配布用の Windows インストーラー パッケージ (*ProjectAggregator2.msi*) をインストールします。 マネージド コード プロジェクト タイプには、新しいアグリゲーターを使用する必要があります。 ProjectAggregator2 では、マネージド コード プロジェクト タイプが正しく動作しなくなる [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] プロジェクト アグリゲーターの制限に対処します。 次の手順では、新しいアグリゲーターを使用するように VSPackage を変更する方法について説明します。

1. ソリューションから NativeHierarchyWrapper プロジェクトを削除します。

2. セットアップから NativeHierarchyWrapper バイナリを削除します。

3. セットアップに *ProjectAggregator2.msi* を追加します。
