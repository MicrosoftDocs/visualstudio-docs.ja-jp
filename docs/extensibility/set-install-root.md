---
title: VSIX v3 による拡張機能フォルダー外でのインストール | Microsoft Docs
description: 拡張機能フォルダー外の有効な場所に Visual Studio SDK 拡張機能アセットをインストールする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/09/2016
ms.topic: how-to
ms.assetid: 913c3745-8aa9-4260-886e-a05aecfb2225
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 24b1e1a73ff588e5531eec2025c8a3c9e94760a4
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898449"
---
# <a name="install-outside-the-extensions-folder"></a>拡張機能フォルダー外でのインストール

Visual Studio 2017 および VSIX v3 (バージョン 3) 以降では、拡張機能アセットを拡張機能フォルダー外にインストールできます。 現時点で有効なインストール場所は次のとおりです ([INSTALLDIR] は Visual Studio インスタンスのインストール ディレクトリにマップされます)。

* [INSTALLDIR]\MSBuild
* [INSTALLDIR]\Xml\Schemas
* [INSTALLDIR]\Common7\IDE\PublicAssemblies
* [INSTALLDIR]\Licenses
* [INSTALLDIR]\Common7\IDE\ReferenceAssemblies
* [INSTALLDIR]\Common7\IDE\RemoteDebugger
* [INSTALLDIR]\Common7\IDE\VC\VCTargets (Visual Studio 2017 でのみサポートされています。Visual Studio 2019 以降では非推奨です)

> [!NOTE]
> VSIX 形式では、Visual Studio インストール フォルダー構造の外部にインストールすることはできません。 

これらのディレクトリへのインストールをサポートするには、VSIX を "コンピューターごと、インスタンスごと" にインストールする必要があります。 これを有効にするには、extension.vsixmanifest デザイナーで [すべてのユーザー] チェックボックスをオンにします。

![[すべてのユーザー] をオンにする](media/check-all-users.png)

## <a name="how-to-set-the-installroot"></a>InstallRoot を設定する方法

インストール ディレクトリを設定するには、Visual Studio の **[プロパティ]** ウィンドウを使用します。 たとえば、プロジェクト参照の `InstallRoot` プロパティを上記のいずれかの場所に設定できます。

![インストール ルート プロパティ](media/install-root-properties.png)

これにより、VSIX プロジェクトの .csproj ファイル内の対応する `ProjectReference` プロパティにいくつかのメタデータが追加されます。

```xml
 <ProjectReference Include="..\ClassLibrary1\ClassLibrary1.csproj">
        <Project>{69a979f1-eba2-43e7-9346-0e56e803508b}</Project>
        <Name>ClassLibrary1</Name>
        <InstallRoot>PublicAssemblies</InstallRoot>
 </ProjectReference>
```

> [!NOTE]
> 必要に応じて、.csproj ファイルを直接編集できます。

## <a name="how-to-set-a-subpath-under-the-installroot"></a>InstallRoot の下にサブパスを設定する方法

`InstallRoot` の下にあるサブパスにインストールする場合は、`InstallRoot` プロパティと同様に `VsixSubPath` プロパティを設定します。 たとえば、プロジェクト参照の出力を '[INSTALLDIR]\MSBuild\MyCompany\MySDK\1.0' にインストールする必要があるとします。 これはプロパティ デザイナーで簡単に実行できます。

![サブパスを設定する](media/set-subpath.png)

対応する .csproj の変更は次のようになります。

```xml
<ProjectReference Include="..\ClassLibrary1\ClassLibrary1.csproj">
       <Project>{69a979f1-eba2-43e7-9346-0e56e803508b}</Project>
       <Name>ClassLibrary1</Name>
       <InstallRoot>MSBuild</InstallRoot>
       <VSIXSubPath>MyCompany\MySDK\1.0</VSIXSubPath>
</ProjectReference>
```

## <a name="extra-information"></a>追加情報

プロパティ デザイナーの変更は、プロジェクト参照以外にも適用されます。プロジェクト内の項目についても (上記と同じ方法を使用して) `InstallRoot` メタデータを設定できます。
