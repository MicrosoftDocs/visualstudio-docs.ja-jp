---
title: Windows Vista の ClickOnce 配置 | Microsoft Docs
description: Visual Studio での外部マニフェストを必要とする ClickOnce および Registration-Free COM アプリケーション用の外部 UAC マニフェストの生成方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- UAC manifest generation
- ClickOnce deployment, Windows
- manifest generation
- Windows, ClickOnce deployment
ms.assetid: b21a0ebc-0ff6-4f49-8993-7d1ad3f8cac2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ccac1cd234a0f83810ff2596e1763209d95a8325
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99918453"
---
# <a name="clickonce-deployment-on-windows-vista"></a>Windows Vista の ClickOnce 配置

Windows Vista でのユーザーアカウント制御 (UAC) 用に Visual Studio でアプリケーションをビルドすると、通常、埋め込みマニフェストが生成され、アプリケーションの実行可能ファイルにバイナリ XML データとしてエンコードされます。  ClickOnce および Registration-Free COM アプリケーションでは外部マニフェストが必要であるため、Visual Studio では、埋め込みマニフェストではなく、UAC データを含むこれらのプロジェクト用のファイルが生成されます。 ClickOnce および Registration-Free COM 配置の場合、Visual Studio では、*app.manifest* と呼ばれるファイルからの情報を使用して外部の UAC マニフェスト情報を生成します。 それ以外の場合は、Visual Studio によって UAC データがアプリケーションの実行可能ファイルに埋め込まれます。

Visual Studio には、マニフェスト生成のための次のオプションが用意されています。

- 埋め込みマニフェストを使用します。 UAC データをアプリケーションの実行可能ファイルに埋め込み、通常のユーザーとして実行します。

   これは既定の設定です (ClickOnce を使用する場合を除く)。 この設定は、`AsInvoker` を使用して内部と外部の両方のマニフェストを生成する、Windows Vista での Visual Studio の通常の動作方法をサポートします。

- 外部マニフェストを使用します。 *app.manifest* を使用して外部マニフェストを生成します。

   これにより、*app.manifest* の情報を使用して、外部マニフェストのみが生成されます。 ClickOnce または Registration-Free COM を使用してアプリケーションを発行すると、Visual Studio によってプロジェクトに *app.manifest* が追加され、このオプションが追加されます。

- マニフェストを使用しません。 マニフェストなしでアプリケーションを作成します。

   このような方法を *仮想化* といいます。 以前のバージョンの Visual Studio からの既存のアプリケーションとの互換性を確保するには、このオプションを使用します。

  新しいプロパティは、プロジェクト デザイナーの **[アプリケーション]** ページ (Visual C# プロジェクトの場合のみ) および MSBuild プロジェクト ファイル形式で使用できます。

  Visual Studio IDE で UAC マニフェストの生成を構成する方法は、プロジェクトの種類 (Visual C# または Visual Basic) によって異なります。

  * マニフェスト生成のための Visual C# プロジェクトの構成の詳細については、「[[アプリケーション] ページ (プロジェクト デザイナー) (C#)](../ide/reference/application-page-project-designer-csharp.md)」を参照してください。

  * マニフェスト生成のための Visual Basic プロジェクトの構成の詳細については、「[[アプリケーション] ページ (プロジェクト デザイナー) (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [ClickOnce のセキュリティと配置](../deployment/clickonce-security-and-deployment.md)
- [ユーザー アクセス許可と Visual Studio](/previous-versions/ms165100(v=vs.100))
- [[アプリケーション] ページ (プロジェクト デザイナー) (C#)](../ide/reference/application-page-project-designer-csharp.md)
- [[アプリケーション] ページ (プロジェクト デザイナー)](../ide/reference/application-page-project-designer-visual-basic.md)