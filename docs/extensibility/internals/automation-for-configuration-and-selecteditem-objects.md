---
title: 構成および SelectedItem オブジェクトのためのオートメーション | Microsoft Docs
description: Shell Interop の構成および SelectedItem オブジェクトを使用して、Visual Studio のビルドと選択された項目の処理を自動化する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], SelectedItem object
- automation [Visual Studio SDK], builds
ms.assetid: 120377f1-51aa-4445-b2f7-06ab7fc2b47f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9f6e7f153e7d5b32e54cc51e3b7af06f14545cea
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086262"
---
# <a name="automation-for-configuration-and-selecteditem-objects"></a>構成および SelectedItem オブジェクトのためのオートメーション

Visual Studio では、ビルドと選択された項目の処理を自動化できます。

## <a name="automation-for-builds"></a>ビルドのオートメーション

ビルドまたは構成には、<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider> の実装時に提供されるオートメーション モデルがあります。 詳しくは、「[ビルド構成について](../../ide/understanding-build-configurations.md)」をご覧ください。

VSPackage を作成して構成オプションを制御する場合は、オートメーション モデルを使用する必要があります。

## <a name="automation-for-selecteditem"></a>SelectedItem のオートメーション

Visual Studio には標準の実装が含まれているため、`SelectedItem` オブジェクトの実装を行う必要はありません。 ただし、必要に応じて `SelectedItem` オブジェクトを実装することができます。 `SelectedItem` インターフェイスを含むオブジェクトを実装し、(`VSITEMID` に [__VSHPROPID.VSHPROPID_ExtSelectedItem](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_ExtSelectedItem>) を設定して) <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A> メソッドへの呼び出しに対する応答を返す必要があります。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A>
- [オートメーション モデルに貢献する](../../extensibility/internals/contributing-to-the-automation-model.md)
- [ビルド構成について](../../ide/understanding-build-configurations.md)
