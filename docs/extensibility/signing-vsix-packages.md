---
title: VSIX パッケージに署名しています |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- signature
- signing
- authenticode
- vsix
- packages
ms.assetid: e34cfc2c-361c-44f8-9cfe-9f2be229d248
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 08a709b50dd61beb874ea4cb80ebfb92a8fcd49e
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72720050"
---
# <a name="signing-vsix-packages"></a>VSIX パッケージの署名
拡張機能アセンブリは、Visual Studio で実行する前に署名する必要はありませんが、これを行うことをお勧めします。

 拡張機能をセキュリティで保護し、改ざんされていないことを確認するには、VSIX パッケージにデジタル署名を追加します。 VSIX が署名されると、VSIX インストーラーには、その VSIX が署名されていることを示すメッセージが表示され、さらに署名自体に関する情報も表示されます。 Vsix の内容が変更されていて、VSIX が再度署名されていない場合は、その署名が無効であることが VSIX インストーラーによって表示されます。 インストールは停止されませんが、ユーザーに警告が出てきます。

> [!IMPORTANT]
> Visual Studio 2015 以降では、SHA256 暗号化以外のものを使用して署名された VSIX パッケージは、無効な署名があるものとして識別されます。 VSIX のインストールはブロックされませんが、ユーザーに警告が表示されます。

## <a name="signing-a-vsix-with-vsixsigntool"></a>VSIXSignTool を使用した VSIX への署名
 Nuget.org の[VisualStudioExtensibility](http://www.nuget.org/profiles/VisualStudioExtensibility)では、SHA256 暗号化署名ツールを使用でき[ます。](http://www.nuget.org/packages/Microsoft.VSSDK.Vsixsigntool)

#### <a name="to-use-the-vsixsigntool"></a>VSIXSignTool を使用するには

1. プロジェクトに VSIX を追加します。

2. ソリューションエクスプローラーのプロジェクトノードを右クリックし、[**追加&#124; ] [NuGet パッケージの管理**] の順に選択します。  Nuget と NuGet パッケージの追加の詳細については、 [nuget のドキュメント](/NuGet)と[パッケージマネージャーの UI](/NuGet/Tools/Package-Manager-UI)に関するトピックを参照してください。

3. VisualStudioExtensibility から VSIXSignTool を検索し、NuGet パッケージをインストールします。

4. これで、プロジェクトのローカルパッケージの場所から VSIXSignTool を実行できるようになりました。 署名シナリオ (VSIXSignTool/?) については、ツールのコマンドラインヘルプを参照してください。

   たとえば、パスワードで保護された証明書ファイルで署名するには、次のようにします。

   VSIXSignTool sign/f \<certfile >/p \<password > \<VSIXfile >

## <a name="see-also"></a>関連項目
- [Visual Studio 拡張機能の配布](../extensibility/shipping-visual-studio-extensions.md)
