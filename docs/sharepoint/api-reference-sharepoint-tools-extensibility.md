---
title: API リファレンス (SharePoint ツールの機能拡張) |Microsoft Docs
description: Visual Studio での SharePoint ツールの拡張については、API リファレンスドキュメントを参照してください。 VisualStudio など、関連する名前空間の一覧を参照してください。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, reference for project and tools extensibility
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: ec07272ede6c957afb43c29342e8479e67d1dd0e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99851723"
---
# <a name="api-reference-sharepoint-tools-extensibility"></a>API リファレンス (SharePoint ツールの機能拡張)
  このセクションでは、Visual Studio の SharePoint ツールを拡張するための API リファレンス ドキュメントを示します。

## <a name="in-this-section"></a>このセクションの内容
 <xref:Microsoft.VisualStudio.SharePoint>

 SharePoint プロジェクト システムを拡張するのに使用する型があります。 たとえば、組み込みの SharePoint プロジェクトやプロジェクト項目を拡張できるほか、独自のプロジェクト項目を作成することもできます。

 <xref:Microsoft.VisualStudio.SharePoint.Commands>

 カスタム *SharePoint コマンド* の作成に使用できる型が含まれています。 SharePoint コマンドは、SharePoint のサーバー オブジェクト モデルに対する呼び出しを SharePoint ツールの拡張機能から行うメソッドです。

 <xref:Microsoft.VisualStudio.SharePoint.Deployment>

 SharePoint プロジェクトの配置プロセスを拡張する際に使用する型があります。

 <xref:Microsoft.VisualStudio.SharePoint.Explorer>

 **サーバーエクスプローラー** で SharePoint ノードを拡張したり、独自の種類のノードを定義したりするために使用する型が含まれています。

 <xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions>

 リスト、フィールド、コンテンツタイプを表すノードなど、SharePoint サイト上の個々のコンポーネントを表す組み込み **サーバーエクスプローラー** ノードに関する情報を取得するために使用できる型が含まれています。

 <xref:Microsoft.VisualStudio.SharePoint.Features>

 SharePoint プロジェクトの機能の定義にアクセスするために使用する型があります。

 <xref:Microsoft.VisualStudio.SharePoint.Packages>

 SharePoint プロジェクトのパッケージ定義にアクセスするために使用する型があります。

 <xref:Microsoft.VisualStudio.SharePoint.Remote.Authentication>

 リモート SharePoint サイトに配置する SharePoint アプリの認証とそれらのアプリとの通信に使用する型があります。

 <xref:Microsoft.VisualStudio.SharePoint.Remote.Commands>

 リモート SharePoint サイトに配置する SharePoint アプリ用の SharePoint リモート コマンドを作成するために使用する型があります。

 <xref:Microsoft.VisualStudio.SharePoint.Tasks>

 Visual Studio で SharePoint プロジェクト、Office アプリ、SharePoint アプリのパッケージ化とデバッグ用のビルド タスクとして使用する型があります。 この API は、Office および SharePoint インフラストラクチャをサポートします。独自に作成したコードから直接使用するためのものではありません。

 <xref:Microsoft.VisualStudio.SharePoint.Validation>

 SharePoint プロジェクトの機能およびパッケージ検証動作をカスタマイズするために使用する型があります。

## <a name="see-also"></a>関連項目
- [SharePoint ツールの機能拡張&#41;のリファレンス &#40;](../sharepoint/reference-sharepoint-tools-extensibility.md)
- [SharePoint ツール拡張機能のプログラミング モデルの概要](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)
- [SharePoint プロジェクト システムを拡張する](../sharepoint/extending-the-sharepoint-project-system.md)
- [サーバー エクスプローラーで [SharePoint 接続] ノードを拡張する](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [SharePoint のパッケージ化と配置の拡張](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
- [SharePoint オブジェクトモデルの呼び出し](../sharepoint/calling-into-the-sharepoint-object-models.md)
