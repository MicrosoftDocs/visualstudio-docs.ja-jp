---
title: SharePoint プロジェクト システムの拡張 | Microsoft Docs
description: SharePoint プロジェクト システムを拡張します。 SharePoint プロジェクト システムを拡張する方法について説明します。 一般的な開発タスクについて説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, extending projects
- SharePoint development in Visual Studio, extending project items
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 5a81fef67cc6816f16a074494005a61d647abeab
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99889682"
---
# <a name="extend-the-sharepoint-project-system"></a>SharePoint プロジェクト システムを拡張する
  Visual Studio で一連のプロジェクト テンプレートと項目テンプレートを使用して SharePoint ソリューションを作成できます。 これらのテンプレートは、多くの開発シナリオの要件を満たしていますが、必要な機能が提供されないことが判明する場合もあります。 このような場合は、SharePoint プロジェクト システムを拡張できます。

## <a name="overview-of-the-sharepoint-project-system"></a>SharePoint プロジェクト システムの概要
 SharePoint プロジェクト システムは、"*SharePoint プロジェクト項目*" という基本コンポーネントに基づいています。 SharePoint プロジェクト項目は、リスト定義、Web パーツ、コンテンツ タイプなどの単一の SharePoint カスタマイズを表します。

 SharePoint プロジェクトは、1 つまたは複数の SharePoint プロジェクト項目を含む Visual Studio プロジェクトです。 SharePoint プロジェクトには、プロジェクト項目を配置用のフィーチャーとパッケージにグループ化する方法を定義する追加コンポーネントも含まれています。

 SharePoint プロジェクト項目の内容の詳細については、「[SharePoint プロジェクト項目の項目テンプレートとプロジェクト テンプレートを作成する](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)」を参照してください。

## <a name="how-to-extend-the-sharepoint-project-system"></a>SharePoint プロジェクト システムを拡張する方法
 SharePoint プロジェクト システムは、次の方法で拡張できます。

- Visual Studio で独自の SharePoint プロジェクト項目の種類を定義し、それらを新しい項目テンプレートまたはプロジェクト テンプレートに関連付けます。 たとえば、カスタム アクションまたはフィールドを作成するための SharePoint プロジェクト項目の種類を定義できます。 詳細については、「[カスタム SharePoint プロジェクト項目の種類を定義する](../sharepoint/defining-custom-sharepoint-project-item-types.md)」を参照してください。

- Visual Studio に既にインストールされている SharePoint プロジェクト項目の種類を拡張します。 たとえば、**ソリューション エクスプローラー** にプロジェクト項目へのショートカット メニュー項目を追加し、開発者がメニュー項目を選択したときにプロジェクト項目をカスタマイズできます。 詳細については、「[SharePoint プロジェクト項目の拡張](../sharepoint/extending-sharepoint-project-items.md)」を参照してください。

- SharePoint プロジェクトを拡張します。 たとえば、SharePoint プロジェクトで項目が追加または削除されたときに特定のタスクを実行するためのイベント ハンドラーを追加できます。 詳細については、「[SharePoint プロジェクトの拡張](../sharepoint/extending-sharepoint-projects.md)」を参照してください。

- SharePoint プロジェクト項目および SharePoint プロジェクトのパッケージ化と配置の動作を拡張します。 たとえば、プロジェクトを配置または取り消すときに実行する独自の配置手順を作成できます。また、Visual Studio で特定の配置手順を実行するときに、追加のカスタム タスクを実行することもできます。 詳細については、「[SharePoint のパッケージ化と配置の拡張](../sharepoint/extending-sharepoint-packaging-and-deployment.md)」を参照してください。

## <a name="common-development-tasks"></a>一般的な開発タスク
 SharePoint プロジェクト システムの拡張機能では、次の一般的なタスクを実行できます。

- プロジェクト項目およびさまざまな種類のプロジェクト ファイルにカスタム文字列データを保存する。 詳細については、「[SharePoint プロジェクト システムの拡張機能にデータを保存する](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)」を参照してください。

- SharePoint プロジェクト システム内のオブジェクトを Visual Studio オートメーション オブジェクト モデルまたは統合オブジェクト モデル内のオブジェクトに (またはその逆に) 変換する。 詳細については、「[SharePoint プロジェクト システムの種類とその他の Visual Studio プロジェクトの種類の変換](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [カスタムの SharePoint プロジェクト項目の種類を定義する](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [SharePoint プロジェクト項目を拡張する](../sharepoint/extending-sharepoint-project-items.md)
- [SharePoint プロジェクトを拡張する](../sharepoint/extending-sharepoint-projects.md)
- [SharePoint のパッケージ化と配置を拡張する](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
- [SharePoint プロジェクト システムの拡張機能にデータを保存する](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)
- [SharePoint プロジェクト システムの種類とその他の Visual Studio プロジェクトの種類の変換](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md)
- [Visual Studio での SharePoint ツールの拡張](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)
- [SharePoint ツール拡張機能におけるプログラミングに関する概念および特徴](../sharepoint/programming-concepts-and-features-for-sharepoint-tools-extensions.md)
