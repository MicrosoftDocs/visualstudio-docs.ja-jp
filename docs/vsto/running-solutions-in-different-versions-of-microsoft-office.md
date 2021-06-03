---
title: 異なるバージョンの Microsoft Office でソリューションを実行する
description: Visual Studio 2010 以降を使用して作成された Microsoft Office ソリューションのバージョンを実行する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- solutions [Office development in Visual Studio], multiple Office versions
- Office applications [Office development in Visual Studio], multiple Office versions
- Office development in Visual Studio, multiple Office versions
- Office solutions [Office development in Visual Studio]
- multiple Office versions
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f9083a92482a99d7ec7ecce144ece2806e9889e9
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99961392"
---
# <a name="run-solutions-in-different-versions-of-microsoft-office"></a>異なるバージョンの Microsoft Office でソリューションを実行する

## <a name="run-office-solutions-created-by-using-visual-studio-2010-and-above"></a>Visual Studio 2010 以降を使用して作成された Office ソリューションを実行する

|プロジェクト テンプレートが対象とする Office のバージョン|プロジェクトの対象とする .NET Framework<sup>1</sup>|ソリューションを実行できる Office のバージョン|エンド ユーザーのコンピューターに必要なランタイム|
|--------------------------------------------------------|------------------------------------------------------|--------------------------------------------------|-------------------------------------------|
|Office 2016 と [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)]|[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降|Office 2016<br /><br /> [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)]<br /><br /> [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]<br /><br /> 2007 Microsoft Office システム<sup>2</sup>|Visual Studio 2010 Tools for Office Runtime|
|[!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]|[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降|Office 2016<br /><br /> [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)]<br /><br /> [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]<br /><br /> 2007 Microsoft Office システム<sup>2</sup>|Visual Studio 2010 Tools for Office Runtime|
|[!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]|.NET Framework 3.5|Office 2016<br /><br /> [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)]<br /><br /> [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]|Visual Studio 2010 Tools for Office Runtime|
|2007 Microsoft Office system|[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降<br /><br /> or<br /><br /> .NET Framework 3.5|Office 2016<br /><br /> [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)]<br /><br /> [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]<br /><br /> 2007 Microsoft Office system|Visual Studio 2010 Tools for Office Runtime|

 1. ソリューションを実行するエンド ユーザーのコンピューターには、プロジェクトが対象とする .NET Framework のバージョンが必要です。 たとえば、プロジェクトが .NET Framework 3.5 を対象としている場合、エンド ユーザーのコンピューターには .NET Framework 3.5 が必要です。 この例では、エンド ユーザーのコンピューターに [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] しかインストールされていない場合、ソリューションは実行されません。

 2. このシナリオでは、ソリューションが [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] の新機能を使用しない場合にのみ、エラーが発生することなく 2007 Microsoft Office system で実行されます。

## <a name="run-office-solutions-created-by-using-versions-of-visual-studio-prior-to-visual-studio-2010"></a>Visual Studio 2010 以前のバージョンの Visual Studio を使用して作成された Office ソリューションを実行する
 Microsoft Office アプリケーションは、Visual Studio 2010 以前のバージョンの Visual Studio を使用して作成されたソリューションを実行できます。 これらのソリューションは、異なるバージョンの [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] を必要とする場合があります。 異なるバージョンの [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] を同じコンピューターに同時にインストールできます。

 次の表は、以前のバージョンの Visual Studio を使用して作成されたソリューションを実行できる Microsoft Office のバージョン、および各ソリューションに必要な [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] および .NET Framework のバージョンを示しています。

|ソリューションの作成に使用される Visual Studio のエディション|プロジェクト テンプレートが対象とする Office のバージョン|ソリューションを実行できる Office のバージョン|エンド ユーザーのコンピューターに必要なランタイム|エンド ユーザーのコンピューターに必要な .NET Framework のバージョン|
|----------------------------------------------------------|--------------------------------------------------------|--------------------------------------------------|-------------------------------------------|----------------------------------------------------------|
|Visual Studio 2008 Professional<br /><br /> or<br /><br /> Visual Studio Team System 2008|2007 Microsoft Office system|[!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] および [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]<sup>1</sup><br /><br /> 2007 Microsoft Office system|Visual Studio 2010 Tools for Office Runtime<sup>1</sup><br /><br /> or<br /><br /> Visual Studio Tools for the Microsoft Office System (Version 3.0 Runtime)|.NET Framework 3.5|
|VSTO 2005 SE<sup>2</sup> がインストールされた、次のいずれかのエディションの Visual Studio 2005:<br /><br /> -   Visual Studio 2005 Tools for Office<br />-   Visual Studio Team System 2005<br />-   Visual Studio 2005 Professional|2007 Microsoft Office system|[!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] および [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] (32 ビットのみ<sup>3</sup>)<br /><br /> 2007 Microsoft Office system|Visual Studio 2005 Tools for Office Second Edition Runtime|.NET Framework 2.0、.NET Framework 3.0、または .NET Framework 3.5|
|次のいずれかのエディションの Visual Studio<br /><br /> -   Visual Studio 2008 Professional<br />-   Visual Studio Team System 2008<br />-   Visual Studio 2005 Tools for Office (VSTO 2005 SE<sup>2</sup> のインストールの有無は問わない)<br />-   Visual Studio Team System 2005 (VSTO 2005 SE<sup>2</sup> のインストールの有無は問わない)<br />-   VSTO 2005 SE<sup>2</sup> がインストールされた Visual Studio 2005 Professional|Microsoft Office 2003|[!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] および [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] (32 ビットのみ<sup>3</sup>)<br /><br /> 2007 Microsoft Office system<br /><br /> Microsoft Office 2003|Visual Studio 2005 Tools for Office Second Edition Runtime|.NET Framework 2.0、.NET Framework 3.0、または .NET Framework 3.5|

 1. [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] および [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] アプリケーションには、Visual Studio 2010 Tools for Office ランタイムが含まれます。 そのため、このシナリオの場合、これらのアプリケーションでは、Visual Studio Tools for the Microsoft Office システム (Version 3.0 Runtime) ではなく、Visual Studio 2010 Tools for Office ランタイムを常に使用します。 2007 Microsoft Office system のアプリケーションでは、Visual Studio 2010 Tools for Office Runtime または Visual Studio Tools for the Microsoft Office system (Version 3.0 Runtime) を使用できます。

 2. VSTO 2005 SE は、Microsoft Office 2003 および 2007 Microsoft Office system 用の VSTO アドイン プロジェクト テンプレートを提供する無料の Visual Studio アドオンです。 Visual Studio 2005 Professional、Visual Studio 2005 Tools for Office、または Visual Studio Team System 2005 のエディションと共にインストールできます。 詳細については、「[Visual Studio 2005 Tools for Office Second Edition](https://developer.microsoft.com/office/docs)」を参照してください。

 3. Visual Studio 2005 Tools for Office Second Edition Runtime を必要とする Office ソリューションは、[!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] および [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] の 64 ビット バージョンと互換性がありません。 [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] または [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] の 64 ビット エディションでこれらのソリューションを実行するには、プロジェクトを [!INCLUDE[vs_dev10_long](../sharepoint/includes/vs-dev10-long-md.md)] または 2007 Microsoft Office system を対象とする Visual Studio 2008 プロジェクトにアップグレードする必要があります。

## <a name="see-also"></a>関連項目
- [Office ソリューションを設計して作成する](../vsto/designing-and-creating-office-solutions.md)
- [Visual Studio Tools for Office ランタイムの概要](../vsto/visual-studio-tools-for-office-runtime-overview.md)
- [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [Visual Studio Tools for Office ランタイムのインストール シナリオ](../vsto/visual-studio-tools-for-office-runtime-installation-scenarios.md)
- [Office ソリューションを開発できるようにコンピューターを構成する](../vsto/running-solutions-in-different-versions-of-microsoft-office.md)
