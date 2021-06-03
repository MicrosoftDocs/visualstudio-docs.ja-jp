---
title: カスタム ドキュメント プロパティの概要
description: ドキュメント レベルのプロジェクトをビルドしたときに Visual Studio によって 2 つのカスタム プロパティがプロジェクト内のドキュメントに追加されることについて説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], custom properties
- custom document properties
- document-level customizations [Office development in Visual Studio], custom properties
- Office documents [Office development in Visual Studio], custom properties
- _AssemblyLocation property
- _AssemblyName property
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 51039c71c97614cb9e43df263b3d7155c9cb86f6
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99947802"
---
# <a name="custom-document-properties-overview"></a>カスタム ドキュメント プロパティの概要

ドキュメントレベルのプロジェクトをビルドすると、Visual Studio によって \_AssemblyLocation と \_AssemblyName という 2 つのカスタム プロパティがプロジェクト内のドキュメントに追加されます。 ユーザーがドキュメントを開くと、Microsoft Office アプリケーションによって、これらのカスタム ドキュメント プロパティがチェックされます。 それらがドキュメント内に存在する場合は、アプリケーションによって [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]が読み込まれ、カスタマイズが開始されます。 詳細については、「[Visual Studio での Office ソリューションのアーキテクチャ](../vsto/architecture-of-office-solutions-in-visual-studio.md)」を参照してください。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="_assemblyname"></a>\_AssemblyName

このプロパティには、[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]の Office ソリューション ローダー コンポーネント内のインターフェイスの CLSID が含まれています。 CLSID 値は、4E3C66D5-58D4-491E-A7D4-64AF99AF6E8B です。 この値は変更しないでください。

## <a name="_assemblylocation"></a>\_AssemblyLocation

このプロパティには、カスタマイズ用の配置マニフェストに関する詳細を示す文字列が含まれています。 マニフェストの詳細については、「[Office ソリューションでのアプリケーション マニフェストと配置マニフェスト](../vsto/application-and-deployment-manifests-in-office-solutions.md)」を参照してください。

 \_Assemblylocation プロパティ値の形式は、ソリューションの配置方法によって異なります。

- ソリューションが Web サイト、UNC パス、あるいは CD または USB ドライブからインストールされるように発行されている場合、_AssemblyLocation プロパティの形式は *DeploymentManifestPath*|*SolutionID* になります。 次の文字列は一例です。

     file://deployserver/MyShare/ExcelWorkbook1.vsto|74744e4b-e4d6-41eb-84f7-ad20346fe2d9

- ソリューションを Visual Studio から実行またはデバッグしている場合、_AssemblyLocation プロパティの形式は *DeploymentManifestName*|*SolutionID*|vstolocal になります。 次の文字列は一例です。

     ExcelWorkbook1.vsto|74744e4b-e4d6-41eb-84f7-ad20346fe2d9|vstolocal

  *SolutionID* は、[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]でソリューションを識別するために使用される GUID です。 *SolutionID* は、プロジェクトをビルドしたときに自動的に生成されます。 **vstolocal** の項は、ドキュメントと同じフォルダーからアセンブリが読み込まれることを [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]に知らせるものです。

## <a name="see-also"></a>関連項目

- [Visual Studio での Office ソリューションのアーキテクチャ](../vsto/architecture-of-office-solutions-in-visual-studio.md)
- [ドキュメント レベルのカスタマイズのアーキテクチャ](../vsto/architecture-of-document-level-customizations.md)
- [Office ソリューションでのアプリケーション マニフェストと配置マニフェスト](../vsto/application-and-deployment-manifests-in-office-solutions.md)
- [方法: ClickOnce を使用して Office ソリューションを発行する](/previous-versions/bb386095(v=vs.110))
- [方法: カスタム ドキュメント プロパティを作成および変更する](../vsto/how-to-create-and-modify-custom-document-properties.md)