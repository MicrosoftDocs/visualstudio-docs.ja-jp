---
title: VSIX パッケージの署名 | Microsoft Docs
description: 拡張機能アセンブリに署名する方法について説明します。 VSIX インストーラーには、VSIX が署名されていることを示すメッセージと、その署名自体に関する情報が表示されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- signature
- signing
- authenticode
- vsix
- packages
ms.assetid: e34cfc2c-361c-44f8-9cfe-9f2be229d248
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c2a2c9703eb41c1a3e5baa023d8240b56ccbb13b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056364"
---
# <a name="signing-vsix-packages"></a>VSIX パッケージの署名
拡張機能アセンブリは、Visual Studio で実行する前に署名する必要はありませんが、これを行うことをお勧めします。

 拡張機能をセキュリティで保護し、改ざんされていないことを確認するには、VSIX パッケージにデジタル署名を追加します。 VSIX が署名されると、VSIX インストーラーには、その VSIX が署名されていることを示すメッセージが表示され、さらに署名自体に関する情報も表示されます。 VSIX の内容が変更されていて、VSIX が再度署名されていない場合は、その署名が無効であることが VSIX インストーラーによって表示されます。 インストールは停止されませんが、ユーザーに対する警告が出てきます。

> [!IMPORTANT]
> Visual Studio 2015 以降では、SHA256 暗号化以外のものを使用して署名された VSIX パッケージは、無効な署名があるものとして識別されます。 VSIX のインストールは停止されませんが、ユーザーに対する警告が出てきます。

## <a name="signing-a-vsix-with-vsixsigntool"></a>VSIXSignTool を使用した VSIX への署名
 nuget.org の [VisualStudioExtensibility](https://www.nuget.org/profiles/VisualStudioExtensibility) の [VsixSignTool](https://www.nuget.org/packages/Microsoft.VSSDK.Vsixsigntool) で取得できる、SHA256 暗号化署名ツールがあります。

#### <a name="to-use-the-vsixsigntool"></a>VSIXSignTool を使用する方法

1. プロジェクトに VSIX を追加します。

2. ソリューション エクスプローラーでプロジェクト ノードを右クリックし、 **[追加 &#124; NuGet パッケージの管理]** を選択します。  NuGet と NuGet パッケージの追加の詳細については、「[NuGet のドキュメント](/NuGet)」と[パッケージ マネージャーの UI](/NuGet/Tools/Package-Manager-UI) に関するトピックを参照してください。

3. VisualStudioExtensibility で VSIXSignTool を検索し、NuGet パッケージをインストールします。

4. これで、プロジェクトのローカル パッケージの場所から VSIXSignTool を実行できるようになりました。 署名シナリオ (VSIXSignTool.exe/?) については、ツールのコマンド ライン ヘルプを参照してください。

   たとえば、パスワードで保護された証明書ファイルで署名するには、次のようにします。

   VSIXSignTool.exe sign /f \<certfile> /p \<password> \<VSIXfile>

## <a name="see-also"></a>関連項目
- [Visual Studio 拡張機能の配布](../extensibility/shipping-visual-studio-extensions.md)
