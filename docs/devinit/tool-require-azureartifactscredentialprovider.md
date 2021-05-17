---
title: require-azureartifactscredentialprovider
description: devinit ツール require-azureartifactscredentialprovider。
ms.date: 11/20/2020
ms.topic: reference
author: andysterland
ms.author: andster
manager: jmartens
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.prod: visual-studio-windows
ms.technology: devinit
ms.openlocfilehash: e5ba9847b09f06f853f48a0885de5e0d63664fac
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635302"
---
# <a name="require-azureartifactscredentialprovider"></a>require-azureartifactscredentialprovider

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

`require-azureartifactscredentialprovider` ツールでは、Azure Artifacts 資格情報プロバイダーがインストールされます。 Azure Artifacts 資格情報プロバイダーにより、.NET 開発ワークフローの一部として NuGet パッケージを復元するために必要な資格情報の取得が自動化されます。 Azure Artifacts 資格情報プロバイダーの詳細については、[こちら](https://github.com/microsoft/artifacts-credprovider/blob/master/README.md)を参照してください。

## <a name="usage"></a>使用方法

`input` と `additionalOptions` の両方のプロパティが省略されているか空の場合、ツールは次に示す[既定の](#default-behavior)動作に従います。

| 名前                                             | Type   | 必須 | 値                                                                                |
|--------------------------------------------------|--------|----------|--------------------------------------------------------------------------------------|
| **コメント**                                     | string | No       | comments は省略可能なプロパティです。 使用しません。                                                |
| [**input**](#input)                              | string | No       | 使用しません。 詳細については、下の「[入力](#input)」を参照してください。 |
| [**additionalOptions**](#additional-options)     | string | No       | 詳細については、下の「[追加オプション](#additional-options)」を参照してください。                     |

### <a name="input"></a>入力

使用しません。 言及されている場合、入力はすべて無視されます。

### <a name="additional-options"></a>追加オプション

追加オプションは、資格情報プロバイダーのコマンドにそのまま渡されます。

### <a name="default-behavior"></a>既定の動作

`require-azureartifactscredentialprovider` ツールの既定の動作では、Azure Artifacts 資格情報プロバイダーの最新バージョンがインストールされます。

## <a name="example-usage"></a>使用例
`.devinit.json` を使用して `require-azureartifactscredentialprovider` を実行する方法の例を次に示します。

#### <a name="devinitjson-that-will-install-azure-artifacts-credential-provider"></a>Azure Artifacts 資格情報プロバイダーをインストールする .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-azureartifactscredentialprovider",
        }
    ]
}
```
