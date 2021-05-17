---
title: OpenCV
description: devinit を使用して Linux と Windows の両方を OpenCV リポジトリの対象とするカスタマイズの例。
ms.date: 08/28/2020
ms.topic: reference
author: andysterland
ms.author: andster
manager: jmartens
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.prod: visual-studio-windows
ms.technology: devinit
ms.openlocfilehash: 319f560e4661f12acbef941692e5fd2c257c25ee
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635352"
---
# <a name="opencv"></a>OpenCV

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

この例では、[opencv/OpenCV](https://github.com/opencv/opencv) などのマルチプラットフォーム プロジェクトを使って開発するために [GitHub Codespaces](https://github.com/features/codespaces) をカスタマイズする方法を示します。

次のカスタマイズは、既に [microsoft/OpenCV](https://github.com/microsoft/opencv) フォークに適用されており、Windows と Ubuntu を対象としたビルドを可能にします。

## <a name="customization-with-devcontainerjson-and-devinitjson"></a>devcontainer.json と devinit.json でのカスタマイズ

`.devcontainer` ディレクトリには、次のファイルが含まれている必要があります。

* devcontainer.json
* devinit.json

### <a name="devcontainerjson"></a>devcontainer.json

_devcontainer.json_ ファイルの内容は次のとおりです。

```json
{
  "postCreateCommand": "devinit init"
}
```

`postCreateCommand` によって [devinit](devinit-and-codespaces.md) ツールが起動され、_devinit.json_ が使用されます。

### <a name="devinitjson"></a>devinit.json

[_devinit.json_](devinit-json.md) ファイルの内容は次のとおりです。

```json
{
    "run": [
        {
            "comments": "Example that will install Ubuntu 20.04 using WSL2, and configure it with various packages useful for C++ development.",
            "tool": "wsl-install",
            "input": "https://aka.ms/wslubuntu2004",
            "additionalOptions": "--wsl-version 2 --post-create-command 'apt-get update && apt-get install g++ gcc g++-9 gcc-9 cmake gdb ninja-build zip rsync -y'"
        }
    ]
}
```

_devinit.json_ は、[devinit](devinit-and-codespaces.md) ツールによって使用されるファイルであり、_devcontainer.json_ と同じディレクトリに配置されている必要があります。

このサンプルでは、[wsl-install](tool-wsl-install.md) ツールを使用して、Ubuntu 20.04 を実行する WSL インスタンスを作成し、不可欠な C++ 開発ツールをプロビジョニングします。
## <a name="targeting-windows-or-linux"></a>Windows または Linux を対象とする

Windows を対象とする既定のビルド構成は、常に `x64-Debug` という名前で作成されます。

前述のファイルを追加することで、Codespace インスタンスの作成時に、Visual Studio は新しい SSH 接続を[接続マネージャー](/cpp/linux/connect-to-your-remote-linux-computer)でプロビジョニングし、SSH 接続を介して Ubuntu インスタンスを対象とする新しい構成を構成ピッカーで作成します。

![Ubuntu を対象とする構成](media/wsl-ssh-linux-configuration.png).

強調表示された、WSL を対象とする構成を選択することで、OpenCV のビルド ターゲットのビルドとデバッグを行うことができます。
