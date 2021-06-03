---
title: SharePoint オブジェクト モデルの呼び出し | Microsoft Docs
description: SharePoint ツールの拡張機能で使用できる 2 つの異なるオブジェクト モデルを呼び出す方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, client object model
- SharePoint development in Visual Studio, server object model
- SharePoint commands [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, extensibility features
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 14358b5cc84f63227fd5001731c261002a324492
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99928940"
---
# <a name="call-into-the-sharepoint-object-models"></a>SharePoint オブジェクト モデルの呼び出し
  Visual Studio で SharePoint ツールの拡張機能を作成するときに、特定のタスクを実行するために SharePoint API を呼び出すことが必要になる場合があります。 たとえば、SharePoint プロジェクトのカスタム配置手順を作成する場合、ソリューションを配置するためのタスクをいくつか実行するために、SharePoint API を呼び出す必要がある場合があります。

 [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] と [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] には、SharePoint ツールの拡張機能で使用できる 2 つの異なるオブジェクト モデル (サーバー オブジェクト モデルとクライアント オブジェクト モデル) が用意されています。 各オブジェクト モデルには、SharePoint ツールの拡張機能のコンテキストにおける利点と欠点があります。

 SharePoint オブジェクト モデルの概要については、「[SharePoint ツール拡張機能のプログラミング モデルの概要](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)」を参照してください。

## <a name="use-the-client-object-model-in-extension-projects"></a>拡張機能プロジェクトでクライアント オブジェクト モデルを使用する
 SharePoint ツールの拡張機能を開発する場合は、他のマネージド API セットと同様に、プロジェクトでクライアント オブジェクト モデルを使用できます。 クライアント オブジェクト モデルのアセンブリへの参照をプロジェクトに追加できます。また、コードから直接、クライアント オブジェクト モデルの API を呼び出すことができます。

 ただし、クライアント オブジェクト モデルには、SharePoint ツールの拡張機能のコンテキストにおける欠点が 2 つあります。

- クライアント オブジェクト モデルでは、サーバー オブジェクト モデルのサブセットのみを提供します。 クライアント オブジェクト モデルで公開されていない SharePoint 機能を使用する必要がある場合は、サーバー オブジェクト モデルを使用する必要があります。

- SharePoint ツールの拡張機能でクライアント オブジェクト モデルを使用すると、ほとんどの場合は機能しますが、クライアント オブジェクト モデルの呼び出しが想定どおりに動作しない場合があります。 クライアント オブジェクト モデルは、リモート サーバーまたはファーム上の SharePoint サイトを呼び出すためにクライアント アプリケーションで使用されるように設計されています。 Visual Studio の SharePoint ツールは、開発用コンピューター上の SharePoint のローカル インストールでのみ動作します。 そのため、SharePoint ツールの拡張機能でクライアント オブジェクト モデルを使用する場合は、ローカル コンピューター上の SharePoint サイトを呼び出すことになります。これは、クライアント オブジェクト モデルを使用するように設計された方法ではありません。

  Visual Studio の SharePoint ツールの拡張機能でクライアント オブジェクト モデルを使用する方法を示すチュートリアルについては、「[チュートリアル: サーバー エクスプローラー拡張機能で SharePoint クライアント オブジェクト モデルを呼び出す](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md)」を参照してください。

## <a name="use-the-server-object-model-in-extension-projects"></a>拡張機能プロジェクトでサーバー オブジェクト モデルを使用する
 サーバー オブジェクト モデルは、クライアント オブジェクト モデルのスーパーセットです。 サーバー オブジェクト モデルを使用すると、[!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] および[!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] によって公開されるすべての機能をプログラムによって使用できます。

 SharePoint ツールの拡張機能では、サーバー オブジェクト モデルの API を使用できますが、API を直接呼び出すことはできません。 サーバー オブジェクト モデルは、.NET Framework 3.5 を対象とする 64 ビット プロセスからのみ呼び出すことができます。 ただし、SharePoint ツールの拡張機能では、[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] が必要です。これらは、32 ビットの Visual Studio プロセスで実行されます。 これにより、SharePoint ツールの拡張機能は、SharePoint サーバー オブジェクト モデル内のアセンブリを直接参照できなくなります。

 SharePoint ツール拡張機能でサーバー オブジェクト モデルを使用する場合は、その API を呼び出すためのカスタム "*SharePoint コマンド*" を作成する必要があります。 セカンダリ アセンブリで、サーバー オブジェクト モデルを直接呼び出すことができる SharePoint コマンドを定義します。 拡張機能プロジェクトでは、<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> オブジェクトの ExecuteCommand メソッドを使用して、SharePoint コマンドを間接的に呼び出します。

 SharePoint コマンドの作成と使用の詳細については、「[方法: SharePoint コマンドを作成する](../sharepoint/how-to-create-a-sharepoint-command.md)」および「[方法: SharePoint コマンドを実行する](../sharepoint/how-to-execute-a-sharepoint-command.md)」を参照してください。 SharePoint コマンドを配置する方法の詳細については、「[Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

 SharePoint コマンドを作成して使用する方法を示すチュートリアルについては、「[チュートリアル: SharePoint プロジェクトのカスタム配置手順を作成する](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)」および「[チュートリアル: サーバー エクスプローラーを拡張して Web パーツを表示する](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)」を参照してください。

### <a name="understand-how-sharepoint-commands-are-executed"></a>SharePoint コマンドの実行方法について理解する
 SharePoint コマンドを定義するアセンブリは、*vssphost4.exe* という名前の 64 ビット ホスト プロセスに読み込まれます。 SharePoint ツールの拡張機能で SharePoint コマンドを呼び出すと、32 ビットの Visual Studio プロセス (*devenv.exe*) ではなく、*vssphost4.exe* によってコマンドが実行されます。 レジストリで値を設定することにより、SharePoint コマンドの実行方法のいくつかの側面を制御できます。 詳しくは、「[Visual Studio での SharePoint ツールの拡張機能のデバッグ](../sharepoint/debugging-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: SharePoint コマンドを作成する](../sharepoint/how-to-create-a-sharepoint-command.md)
- [方法: SharePoint コマンドを実行する](../sharepoint/how-to-execute-a-sharepoint-command.md)
- [SharePoint ツール拡張機能のプログラミング モデルの概要](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)
