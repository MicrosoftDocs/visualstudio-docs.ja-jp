---
title: Visual Studio Tools for Office ランタイムのインストール シナリオ
description: Visual Studio 2010 Tools for Office ランタイムをインストールする方法について説明します。 この記事では、3 つのインストール シナリオについて説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visual Studio Tools for Office runtime, installation scenarios
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 10b747602a1c5af9f63c567103a80405341019af
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99921802"
---
# <a name="visual-studio-tools-for-office-runtime-installation-scenarios"></a>Visual Studio Tools for Office ランタイムのインストール シナリオ
  Visual Studio 2010 Tools for Office ランタイムは、次の 3 つの方法でインストールできます。

- Visual Studio のインストール時。

- Microsoft Office のインストール時。

- Visual Studio 2010 Tools for Office ランタイムの再頒布可能パッケージのインストール時。

  インストールされるランタイム コンポーネントは、コンピューターの構成およびインストール シナリオによって異なります。

## <a name="runtime-components-that-are-installed-in-each-installation-scenario"></a>各インストール シナリオでインストールされるランタイム コンポーネント
 Visual Studio 2010 Tools for Office ランタイムには、Office ソリューション ローダー、.NET Framework 3.5 用の Office 拡張機能、および [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降用の Office 拡張機能の 3 つのコンポーネントがあります。 ランタイムをインストールすると、常に Office ソリューション ローダーがインストールされます。 .NET Framework 用の Office 拡張機能のインストールは、コンピューターの構成およびインストール シナリオによって異なります。 最初にランタイムをインストールするときにどちらかの Office 拡張機能をインストールできない場合、後で特定の要件を満たすと、インストールされていない Office 拡張機能がランタイムによって自動的にインストールされます。 ランタイムのこの機能は、"*オンデマンド インストール*" と呼ばれます。

 各ランタイム インストールのシナリオで、既定でインストールされるランタイム コンポーネントを次の表に示します。 各シナリオの詳細については、後で説明します。

|ランタイムのインストール シナリオ|Office ソリューション ローダー|.NET Framework 3.5 用の Office 拡張機能|[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] の Office 拡張機能|[!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] の Office 拡張機能|
|-----------------------------------|----------------------------|--------------------------------------------------| - |---------------------------------------------------------------------------|
|[!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] 以降を使用する場合|はい|○ (.NET Framework Version 3.5 がインストール済みの場合)|はい|はい|
|[!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] あり|はい|○ (.NET Framework Version 3.5 がインストール済みの場合)|いいえ|いいえ|
|Office 2010 Service Pack 1 (SP1) 以降を使用する場合|はい|○ (.NET Framework Version 3.5 がインストール済みの場合)|○ ([!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] がインストール済みの場合)|No|
|ランタイムの再頒布可能パッケージのインストール時|はい|○ (.NET Framework Version 3.5 がインストール済みの場合)|○ ([!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] がインストール済みの場合)|○ ([!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] がインストール済みの場合)|

### <a name="install-the-runtime-with-visual-studio-or-the-microsoft-office-developer-tools-for-visual-studio"></a>Visual Studio または Microsoft Office Developer Tools for Visual Studio でランタイムをインストールする
 Visual Studio の Office Developer Tools をインストールすると、開発用コンピューターに [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] および [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 用の Office 拡張機能が常にインストールされます。 また、.NET Framework 3.5 用の Office 拡張機能は、開発用コンピューターに .NET Framework 3.5 が既に存在している場合にのみインストールされます。 [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] をインストールした後で .NET Framework 3.5 をインストールすると、初めて .NET Framework 3.5 を対象とする Office プロジェクトを作成するときに、.NET Framework 3.5 用の Office 拡張機能がランタイムによって自動的にインストールされます。

> [!WARNING]
> [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] 以降を使用して .NET Framework 3.5 を対象とする Office プロジェクトを作成することはできません。

 Office Developer Tools をインストールする方法の詳細については、「[方法: Office ソリューションを開発できるようにコンピューターを構成する](../vsto/how-to-configure-a-computer-to-develop-office-solutions.md)」を参照してください。

### <a name="install-the-runtime-with-office"></a>Office でランタイムをインストールする
 コンピューターに .NET Framework 3.5 が既に存在している場合、Office をインストールすると、.NET Framework 3.5 用の Office 拡張機能がインストールされます。 Office の後で .NET Framework 3.5 をインストールすると、初めて Office アプリケーションが .NET Framework 3.5 を対象とするソリューションを読み込むときに、.NET Framework 3.5 用の Office 拡張機能がランタイムによって自動的にインストールされます。

 Office のインストール時に [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降が既に存在している場合でも、[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降用の Office 拡張機能は Office と共にインストールされません。

 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 用の Office 拡張機能は、Office と共にインストールされます。 エンド ユーザーは、Windows Update をインストールすることで [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] 用の Office 拡張機能を取得できます。

 アプリケーションを使用するために必要な拡張機能をユーザーがインストールした状態にするには、ソリューションの必須コンポーネントとして Visual Studio 2010 Tools for Office ランタイムの再頒布可能パッケージの最新バージョンを含めます。 必須コンポーネントの詳細については、「[Office ソリューションを配置するための必須コンポーネント](/previous-versions/bb608617(v=vs.110))」を参照してください。

### <a name="install-the-runtime-by-using-the-runtime-redistributable"></a>ランタイムの再頒布可能パッケージを使用してランタイムをインストールする
 ランタイムをインストールするには、Visual Studio 2010 Tools for Office ランタイムの再頒布可能パッケージを手動で実行するか、Office ソリューションの配置時に必須コンポーネントとして再頒布可能パッケージを含めます。

 Visual Studio 2010 Tools for Office ランタイムの再頒布可能パッケージを使用してランタイムをインストールするときに、対応するバージョンの .NET Framework がコンピューターに既に存在している場合は、.NET Framework 3.5 用の Office 拡張機能と [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降用の Office 拡張機能がインストールされます。 ランタイムをインストールするときにこれらのバージョンの .NET Framework の 1 つがコンピューターに存在しない場合、その時点では、存在しないバージョンの .NET Framework 用の Office 拡張機能はインストールされません。 存在しないバージョンの .NET Framework を後でインストールすると、次回、対応する Office 拡張機能を必要とするソリューションがインストールされたとき (ClickOnce を使用して配置されたソリューションと共にランタイムがインストールされた場合) または読み込まれたときに (Windows インストーラーを使用して配置されたソリューションと共にランタイムがインストールされた場合)、その拡張機能がランタイムによって自動的にインストールされます。

 ClickOnce ソリューションの必須コンポーネントを含む詳細については、「[方法: Office ソリューションを実行するための必須コンポーネントをエンド ユーザーのコンピューターにインストールする](/previous-versions/bb608608(v=vs.110))」を参照してください。 再頒布可能パッケージからランタイムを手動でインストールする方法の詳細については、「[方法: Visual Studio Tools for Office ランタイム再頒布可能パッケージをインストールする](../vsto/how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [Visual Studio Tools for Office ランタイムの概要](../vsto/visual-studio-tools-for-office-runtime-overview.md)
- [Visual Studio Tools for Office ランタイムのアセンブリ](../vsto/assemblies-in-the-visual-studio-tools-for-office-runtime.md)