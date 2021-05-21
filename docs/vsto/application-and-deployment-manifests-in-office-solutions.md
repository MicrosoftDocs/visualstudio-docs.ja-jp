---
title: Office ソリューションでのアプリケーション マニフェストと配置マニフェスト
description: アプリケーション マニフェストが、Office ソリューションがアセンブリを特定して更新する際に使用する情報を提供する XML ファイルであることを説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- manifests [Office development in Visual Studio]
- deployment manifests [Office development in Visual Studio]
- application manifests [Office development in Visual Studio]
- assemblies [Office development in Visual Studio], updating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 584d2414235ca70bd8a8fbcb6d2b4e2a31a1828b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99965747"
---
# <a name="application-and-deployment-manifests-in-office-solutions"></a>Office ソリューションでのアプリケーション マニフェストと配置マニフェスト
  アプリケーション マニフェストは、Office ソリューションがアセンブリを特定して更新する際に使用する情報を提供する XML ファイルです。 アプリケーション マニフェストは配置マニフェストと共に使用できます。配置マニフェストは、サーバーに保存されている XML ファイルです。最新バージョンのアプリケーション マニフェストとアセンブリを特定するために必要な情報を提供します。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="manifest-structure-for-office-solutions"></a>Office ソリューションのマニフェストの構造
 Visual Studio で Office 開発ツールを使用して作成された Microsoft Office ソリューションの場合、すべてのマニフェストは、標準の ClickOnce スキーマに基づいています。 Office ソリューションを配置すると、ドキュメントレベルと VSTO アドイン プロジェクトの両方のアプリケーション マニフェストは、ClickOnce キャッシュに保存されます。 配置マニフェストは、クライアント コンピューターにコピーされません。

 Office プロジェクトのアプリケーション マニフェストと配置マニフェストの詳しい内容については、「[Office ソリューション用アプリケーション マニフェスト](../vsto/application-manifests-for-office-solutions.md)」、および「[Office ソリューションの配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)」を参照してください。

## <a name="create-application-and-deployment-manifests"></a>アプリケーションと配置マニフェストを作成する
 アプリケーション マニフェストは、ビルド プロセスの一環として自動的に作成されます。 ドキュメントレベルのプロジェクトをビルドするたびに、配置マニフェストの場所はカスタム ドキュメント プロパティとしてドキュメントに埋め込まれます。 VSTO アドインの場合、配置マニフェストの場所はレジストリに格納されます。

 **発行ウィザード** の詳細については、「[ClickOnce を使用して Office ソリューションを配置する](../vsto/deploying-an-office-solution-by-using-clickonce.md)」を参照してください。

 Office ソリューションでのマニフェストの機能に関する詳細については、「[Office ソリューションを配置する](../vsto/deploying-an-office-solution.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [ドキュメント レベルのカスタマイズのアーキテクチャ](../vsto/architecture-of-document-level-customizations.md)
- [Architecture of VSTO Add-Ins](../vsto/architecture-of-vsto-add-ins.md)
- [Office ソリューションを設計して作成する](../vsto/designing-and-creating-office-solutions.md)
- [Office ソリューション用アプリケーション マニフェスト](../vsto/application-manifests-for-office-solutions.md)
- [Office ソリューション用配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce アプリケーション マニフェスト](../deployment/clickonce-application-manifest.md)
- [ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)