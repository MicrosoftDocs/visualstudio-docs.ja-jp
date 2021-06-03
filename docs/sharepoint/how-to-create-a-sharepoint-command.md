---
title: '方法: SharePoint コマンドを作成する | Microsoft Docs'
description: SharePoint ツール拡張機能でサーバー オブジェクト モデルの API を呼び出すためのカスタム SharePoint コマンドを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint commands [SharePoint development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 7cc3d29d4991b6cfb712e4754f066edbb66f0b71
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216684"
---
# <a name="how-to-create-a-sharepoint-command"></a>方法: SharePoint コマンドを作成する
  SharePoint ツール拡張機能でサーバー オブジェクト モデルを使用する場合は、その API を呼び出すためのカスタム "*SharePoint コマンド*" を作成する必要があります。 SharePoint コマンドは、サーバー オブジェクト モデルを直接呼び出すことができるアセンブリで定義します。

 SharePoint コマンドの目的の詳細については、「[SharePoint オブジェクト モデルの呼び出し](../sharepoint/calling-into-the-sharepoint-object-models.md)」を参照してください。

### <a name="to-create-a-sharepoint-command"></a>SharePoint コマンドを作成するには

1. 次の構成を備えたクラス ライブラリ プロジェクトを作成します。

    - .NET Framework 3.5 をターゲットとする。 ターゲット フレームワークの選択の詳細については、[方法: .NET Framework のターゲット バージョンの選択](../ide/visual-studio-multi-targeting-overview.md)に関するページを参照してください。

    - AnyCPU または x64 プラットフォームをターゲットとする。 既定では、クラス ライブラリ プロジェクトのターゲット プラットフォームは AnyCPU です。 ターゲット プラットフォームの選択の詳細については、「[方法: プロジェクトを構成して対象プラットフォームを設定する](../ide/how-to-configure-projects-to-target-platforms.md)」を参照してください。

    > [!NOTE]
    > SharePoint コマンドは .NET Framework 3.5 をターゲットとし、SharePoint ツール拡張機能は [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] をターゲットとしているため、SharePoint ツール拡張機能を定義するのと同じプロジェクトで SharePoint コマンドを実装することはできません。 拡張機能によって使用される SharePoint コマンドはすべて、個別のプロジェクトで定義する必要があります。 詳細については、「[Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

2. 次のアセンブリへの参照を追加します。

    - Microsoft.VisualStudio.SharePoint.Commands

    - Microsoft.SharePoint

3. プロジェクト内のクラスで、SharePoint コマンドを定義するメソッドを作成します。 このメソッドは、次のガイドラインに従う必要があります。

    - 1 つまたは 2 つのパラメーターを持つことができます。

         最初のパラメーターは <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> オブジェクトである必要があります。 このオブジェクトは、コマンドが実行される Microsoft.SharePoint.SPSite または Microsoft.SharePoint.SPWeb を提供します。 また、Visual Studio の **[出力]** ウィンドウまたは **[エラー一覧]** ウィンドウにメッセージを書き込むために使用できる <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandLogger> オブジェクトも提供します。

         2 番目のパラメーターは任意の型にすることができますが、このパラメーターは省略可能です。 SharePoint ツール拡張機能から SharePoint コマンドにデータを渡す必要がある場合は、このパラメーターをそのコマンドに追加できます。

    - 戻り値を持つことができますが、これは省略可能です。

    - 2 番目のパラメーターと戻り値は、Windows Communication Foundation (WCF) でシリアル化できる型である必要があります。 詳細については、「[データ コントラクト シリアライザーでサポートされる型](/dotnet/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer)」および「[XmlSerializer クラスの使用](/dotnet/framework/wcf/feature-details/using-the-xmlserializer-class)」を参照してください。

    - このメソッドは、どの可視性 (**パブリック**、**内部**、または **プライベート**) も持つことができ、静的でも非静的でもかまいません。

4. メソッドに <xref:Microsoft.VisualStudio.SharePoint.Commands.SharePointCommandAttribute> を適用します。 この属性では、コマンドの一意識別子を指定します。この識別子がメソッド名に一致している必要はありません。

     このコマンドを SharePoint ツール拡張機能から呼び出すときは、同じ一意識別子を指定する必要があります。 詳細については、「[方法: SharePoint コマンドを実行する](../sharepoint/how-to-execute-a-sharepoint-command.md)」を参照してください。

## <a name="example"></a>例
 次のコード例は、識別子 `Contoso.Commands.UpgradeSolution` を持つ SharePoint コマンドを示しています。 このコマンドでは、サーバー オブジェクト モデルの API を使用して、配置されたソリューションにアップグレードします。

 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/SharePointCommands/Commands.cs" id="Snippet5":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/sharepointcommands/commands.vb" id="Snippet5":::

 暗黙的な最初の <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> パラメーターに加えて、このコマンドには、SharePoint サイトにアップグレードされる .wsp ファイルの完全なパスを含むカスタム文字列パラメーターもあります。 このコードをより大きな例のコンテキストで確認するには、「[チュートリアル: SharePoint プロジェクトのカスタム配置手順を作成する](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)」を参照してください。

## <a name="compiling-the-code"></a>コードのコンパイル
 この例には、次のアセンブリへの参照が必要です。

- Microsoft.VisualStudio.SharePoint.Commands

- Microsoft.SharePoint

## <a name="deploying-the-command"></a>コマンドの配置
 このコマンドを配置するには、このコマンドを使用する拡張機能アセンブリが含まれているのと同じ [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 拡張機能 (*vsix*) パッケージにコマンド アセンブリを含めます。 また、コマンド アセンブリのエントリを extension.vsixmanifest ファイルに追加することも必要です。 詳細については、「[Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint オブジェクト モデルの呼び出し](../sharepoint/calling-into-the-sharepoint-object-models.md)
- [方法: SharePoint コマンドを実行する](../sharepoint/how-to-execute-a-sharepoint-command.md)
- [チュートリアル: サーバー エクスプローラーを拡張して Web パーツを表示する](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
