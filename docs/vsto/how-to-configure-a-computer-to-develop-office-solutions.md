---
title: '方法: Office ソリューションを開発できるようにコンピューターを構成する'
description: Visual Studio の Microsoft Office Developer Tools を使用できるように開発コンピューターを構成する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- prerequisites [Office development in Visual Studio]
- Office development in Visual Studio, installing tools
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: eeb5deffd0d6dbfb39da22db993bdb201bac5e17
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99913480"
---
# <a name="how-to-configure-a-computer-to-develop-office-solutions"></a>方法: Office ソリューションを開発できるようにコンピューターを構成する
  Visual Studio の Microsoft Office Developer Tools を使用できるように開発コンピューターを構成するには、次のトピックの手順を実行します。 これらの手順を実行するには、開発コンピューターの管理特権を保持している必要があります。

### <a name="to-configure-the-development-computer"></a>開発コンピューターを構成するには

1. Office Developer Tools が含まれているバージョンの Visual Studio をインストールします。 Office 開発者ツールは既定でインストールされます。 インストールする機能を選択して Visual Studio のインストールをカスタマイズする場合は、セットアップ時に **[Microsoft Office Developer Tools]** を選択していることを確認してください。 Office 開発ツールが含まれているバージョンの Visual Studio の詳細については、「[Office ソリューションを開発できるようにコンピューターを構成する](../vsto/configuring-a-computer-to-develop-office-solutions.md)」を参照してください。

2. Visual Studio の Office Developer Tools によってサポートされているバージョンの Office をインストールします。 詳細については、「[Office ソリューションを開発できるようにコンピューターを構成する](../vsto/configuring-a-computer-to-develop-office-solutions.md)」を参照してください。

     インストールするバージョンの Office の PIA もインストールされることを確認してください。 PIA は、既定では Office と共にインストールされます。 Office セットアップを変更する場合は、対象とするアプリケーションに対して **.NET プログラミング サポート** 機能が選択されていることを確認します。

3. Windows の言語を英語以外に設定している状態で英語版の Visual Studio を使用する場合は、[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] の Language Pack をインストールすることにより、[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] のメッセージを Windows と同じ言語で表示できます。 英語版以外の Visual Studio では、この言語パックが自動的にインストールされます。 言語パックは「[Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=54246)」から入手できます。

## <a name="see-also"></a>関連項目

- [はじめに &#40;Visual Studio での Office 開発&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [方法: Visual Studio Tools for Office の再頒布可能なランタイムをインストールする](../vsto/how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)
- [方法: Office のプライマリ相互運用機能アセンブリをインストールする](../vsto/how-to-install-office-primary-interop-assemblies.md)
