---
title: オプション ページのオートメーションのサポート | Microsoft Docs
description: VSPackage のカスタム [ツール] メニューの [オプション] ページを、Visual Studio オートメーション モデルで使用できるようにする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Tools Options pages [Visual Studio SDK], automation support
- automation [Visual Studio SDK], creating Tools Options pages
ms.assetid: 0b25b82c-7432-4e0a-9e84-350269ba8260
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b587af698cf7f044c02baab1a8207be1457d6cfd
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086223"
---
# <a name="automation-support-for-options-pages"></a>オプション ページのオートメーションのサポート
VSPackage では、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の **[ツール]** メニュー ( **[ツール] メニューの [オプション]** ページ) にカスタムの **[オプション]** ダイアログ ボックスを表示し、オートメーション モデルで使用できるようにすることができます。

## <a name="tools-options-pages"></a>[ツール] メニューの [オプション] ページ
 **[ツール] メニューの [オプション]** ページを作成するには、VSPackage で <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A> メソッドを実装して、環境に返されるユーザー コントロールの実装を提供する必要があります (または、マネージド コードの場合は <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A> メソッドです)。

 これはオプションですが、オートメーション モデルを通じてこの新しいページにアクセスできるようにすることを強くお勧めします。 次の手順で行うことができます。

1. IDispatch 派生オブジェクトの実装を通じて、<xref:EnvDTE._DTE.Properties%2A> オブジェクトを拡張します。

2. <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> メソッド (または、マネージド コードの場合は <xref:Microsoft.VisualStudio.Shell.Package.GetAutomationObject%2A> メソッド) の実装を IDispatch 派生オブジェクトに返します。

3. オートメーション コンシューマーがカスタムの **[オプション]** プロパティ ページで <xref:EnvDTE._DTE.Properties%2A> メソッドを呼び出すと、環境では <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> メソッドを使用して、カスタム **[ツール] メニューの [オプション]** ページのオートメーション実装を取得します。

4. 次に、VSPackage のオートメーション オブジェクトを使用して、<xref:EnvDTE._DTE.Properties%2A> によって返される各 <xref:EnvDTE.Property> を提供します。

   カスタム **[ツール] メニューの [オプション]** ページを実装するサンプルについては、[VSSDK のサンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples)に関するページを参照してください。

## <a name="see-also"></a>関連項目
- [プロジェクト オブジェクトの公開](../../extensibility/internals/exposing-project-objects.md)
