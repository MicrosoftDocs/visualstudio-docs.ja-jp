---
title: Office ソリューションにおけるアプリケーションと配置マニフェスト
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
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: d22d58eb8a2264d5c7765a15726db556c7d5569f
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2019
ms.locfileid: "55949565"
---
# <a name="application-and-deployment-manifests-in-office-solutions"></a>Office ソリューションにおけるアプリケーションと配置マニフェスト
  アプリケーション マニフェストは、Office ソリューションがアセンブリを特定して更新する際に使用する情報を提供する XML ファイルです。 アプリケーション マニフェストは配置マニフェストと共に使用できます。配置マニフェストは、サーバーに保存されている XML ファイルです。最新バージョンのアプリケーション マニフェストとアセンブリを特定するために必要な情報を提供します。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="manifest-structure-for-office-solutions"></a>マニフェストの Office ソリューションの構造
 Visual Studio で Office 開発ツールを使用して作成された Microsoft Office ソリューションの場合、すべてのマニフェストは、標準の ClickOnce スキーマに基づいています。 Office ソリューションを配置すると、ドキュメントレベルと VSTO アドイン プロジェクトの両方のアプリケーション マニフェストは、ClickOnce キャッシュに保存されます。 配置マニフェストは、クライアント コンピューターにコピーされません。

 アプリケーションと Office プロジェクトの配置マニフェストの内容については、[Office ソリューション用アプリケーション マニフェスト](../vsto/application-manifests-for-office-solutions.md)と[Office ソリューション用配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)を参照してください。

## <a name="create-application-and-deployment-manifests"></a>アプリケーション マニフェストと配置マニフェストを作成します。
 アプリケーション マニフェストは、ビルド プロセスの一環として自動的に作成されます。 ドキュメントレベルのプロジェクトをビルドするたびに、配置マニフェストの場所はカスタム ドキュメント プロパティとしてドキュメントに埋め込まれます。 VSTO アドインの場合、配置マニフェストの場所はレジストリに格納されます。

 詳細については、**発行ウィザード**を参照してください[ClickOnce を使用して Office ソリューションを配置](../vsto/deploying-an-office-solution-by-using-clickonce.md)します。

 詳細についてはマニフェストの Office ソリューションの機能を参照してください。 [Office ソリューションを配置](../vsto/deploying-an-office-solution.md)します。

## <a name="see-also"></a>関連項目

- [ドキュメント レベルのカスタマイズのアーキテクチャ](../vsto/architecture-of-document-level-customizations.md)
- [VSTO アドインのアーキテクチャ](../vsto/architecture-of-vsto-add-ins.md)
- [設計および Office ソリューションの作成](../vsto/designing-and-creating-office-solutions.md)
- [Office ソリューション用アプリケーション マニフェスト](../vsto/application-manifests-for-office-solutions.md)
- [Office ソリューション用配置マニフェストします。](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce アプリケーション マニフェスト](../deployment/clickonce-application-manifest.md)
- [ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)