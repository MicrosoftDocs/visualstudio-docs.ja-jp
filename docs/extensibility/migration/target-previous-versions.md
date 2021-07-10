---
title: Visual Studio 2022 Preview で拡張機能を作成するときに Visual Studio 2019 をターゲットにする
description: Visual Studio 2022 プレビューでプロジェクトを作成する場合、Visual Studio 拡張機能を Visual Studio 2019 で動作させる方法について説明します。
ms.date: 06/08/2021
ms.topic: conceptual
author: leslierichardson95
ms.author: lerich
manager: jmartens
monikerRange: vs-2022
ms.workload:
- vssdk
ms.openlocfilehash: dcf556e271e6a805110eac0c978a845f2195e28f
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112309236"
---
# <a name="target-a-previous-version-when-creating-an-extension-in-visual-studio-2022-preview"></a>Visual Studio 2022 プレビューで拡張機能を作成するとき、前のバージョンをターゲットにする

[!INCLUDE [preview-note](../includes/preview-note.md)]

Visual Studio 2022 プレビューを利用して新しい VSIX プロジェクトを作成すると、Visual Studio 2022 をターゲットにするテンプレートからそのプロジェクトが作成されます。 Visual Studio 2019 以前のバージョンをターゲットにするには、作成済みのプロジェクトを変更する必要があります。

拡張機能でほとんどまたはすべてのコードを共有するとき、Visual Studio 2019 と Visual Studio 2022 をターゲットにするため、[共有プロジェクト](update-visual-studio-extension.md#use-shared-projects-for-multi-targeting)の使用を検討してください。

Visual Studio 2019 をターゲットとする VSIX プロジェクトで次の手順を実行します。

1. `source.extension.vsixmanifest` ファイルを編集し、`ProductArchitecture` 要素とバージョン範囲を削除します。

    ```diff
    -<InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[17.0,18.0)">
    +<InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[16.0,17.0)">
    -  <ProductArchitecture>amd64</ProductArchitecture>
     </InstallationTarget>
    ```

   また、前提条件を更新します。

    ```diff
    -<Prerequisite Id="Microsoft.VisualStudio.Component.CoreEditor" Version="[17.0,18.0)" DisplayName="Visual Studio core editor" />
    +<Prerequisite Id="Microsoft.VisualStudio.Component.CoreEditor" Version="[16.0,17.0)" DisplayName="Visual Studio core editor" />
    ```

    必要な更新が他にないか、ファイルを確認します。

1. プロジェクト ファイルで参照する VS SDK パッケージのバージョンを変更します。

    ```diff
    -<PackageReference Include="Microsoft.VisualStudio.SDK" Version="17.0.0-preview.1" />
    +<PackageReference Include="Microsoft.VisualStudio.SDK" Version="16.0.206" />
    -<PackageReference Include="Microsoft.VSSDK.BuildTools" Version="17.0.63-preview.1" />
    +<PackageReference Include="Microsoft.VSSDK.BuildTools" Version="16.10.32" />
    ```
