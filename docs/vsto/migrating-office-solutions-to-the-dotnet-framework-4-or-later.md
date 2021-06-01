---
title: Office ソリューションを .NET Framework 4 以降に移行する
description: プロジェクトが引き続き機能するように Office ソリューションを .NET Framework 4 以降に移行する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VST.Project.TargetFrameworkWarning
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office projects [Office development in Visual Studio], migrating to .NET Framework 4
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 8c11b2f107414ac5ffb048d7c5e49609ba0b17b1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99946138"
---
# <a name="migrate-office-solutions-to-the-net-framework-4-or-later"></a>Office ソリューションを .NET Framework 4 以降に移行する
  Office プロジェクトのターゲット フレームワークを旧バージョンの .NET Framework から [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降に変更する場合は、開発用コンピューターとエンド ユーザー コンピューターでソリューションを引き続き実行するために追加の手順が必要な場合があります。 詳細については、「[.NET Framework 4 または .NET Framework 4.5 に移行する Office プロジェクトの実行に必要な変更](../vsto/required-changes-to-run-office-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)」を参照してください。

 さらに、プロジェクトがコンパイルされなくなる場合があります。 Office プロジェクトの一部の機能は、.NET Framework のバージョンに応じてプログラミング モデルが異なっています。 Office プロジェクトのターゲット フレームワークを旧バージョンの .NET Framework から [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降に変更する場合は、プロジェクトに対して次のコード変更を加える必要があります。

- [.NET Framework 4 または .NET Framework 4.5 に移行する Excel プロジェクトと Word プロジェクトを更新する](../vsto/updating-excel-and-word-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)

- [.NET Framework 4 または .NET Framework 4.5 に移行する Office プロジェクトのリボンのカスタマイズを更新する](update-ribbon-customizations-in-office-projects-to-migrate-to-dotnet-framework-4-or-4-5.md)

- [.NET Framework 4 または .NET Framework 4.5 に移行する Outlook プロジェクトのフォーム領域を更新する](../vsto/updating-form-regions-in-outlook-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)

  Office プロジェクトのターゲット フレームワークは、そのプロジェクトを旧バージョンの Visual Studio からアップグレードすると変更されます。 詳細については、「[Office ソリューションをアップグレードして移行する](../vsto/upgrading-and-migrating-office-solutions.md)」を参照してください。

  [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降を対象とする Office プロジェクトの一部の機能でプログラミング モデルが異なる理由の詳細については、「[.NET Framework 4 または .NET Framework 4.5 を対象とする Office プロジェクトのデザインの変更](../vsto/changes-to-the-design-of-office-projects-that-target-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)」と「[Visual Studio Tools for Office Runtime の概要](../vsto/visual-studio-tools-for-office-runtime-overview.md)」をご覧ください。

## <a name="see-also"></a>関連項目
- [Office ソリューションを設計して作成する](../vsto/designing-and-creating-office-solutions.md)
- [方法: .NET Framework のバージョンをターゲットにする](../ide/visual-studio-multi-targeting-overview.md)
- [Office ソリューションのエラーをトラブルシューティングする](../vsto/troubleshooting-errors-in-office-solutions.md)
- [Office ソリューションのエラーについての追加サポート](../vsto/additional-support-for-errors-in-office-solutions.md)
