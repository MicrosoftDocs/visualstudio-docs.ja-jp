---
title: '&lt;Package&gt; 要素 (ブートストラップ) | Microsoft Docs'
description: Package 要素は、パッケージ ファイル内の最上位の XML 要素です。 Package 要素は必須です。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- <package> element [bootstrapper]
ms.assetid: ecd06658-ad02-4440-bccd-88437b7fb816
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 2ddb1feb3e5234b26e2ebceb9f899554d55b3015
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99940346"
---
# <a name="ltpackagegt-element-bootstrapper"></a>&lt;Package&gt; 要素 (ブートストラップ)
`Package` 要素は、パッケージ ファイル内の最上位の XML 要素です。

## <a name="syntax"></a>構文

```xml
<Package
    Culture
    Name
    LicenseAgreement
>
    <InstallChecks>
        <AssemblyCheck
            Property
            Name
            PublicKeyToken
            Version
            Language
            ProcessorArchitecture
        />
        <RegistryCheck
            Property
            Key
            Value
        />
        <ExternalCheck
            PackageFile
            Property
            Arguments
            Log
        />
        <FileCheck
            Property
            FileName
            SearchPath
            SpecialFolder
            SearchDepth
        />
        <MsiProductCheck
            Property
            Product
            Feature
        />
        <RegistryFileCheck
            Property
            Key
            Value
            File
            SearchDepth
        />
    </InstallChecks>

    <Commands
        Reboot
    >
        <Command
            PackageFile
            Arguments
            EstimatedInstallSeconds
            EstimatedDiskBytes
            EstimatedTempBytes
            Log
        >
            <InstallConditions>
                <BypassIf
                    Property
                    Compare
                    Value
                    Schedule
                />
                <FailIf
                    Property
                    Compare
                    Value
                    String
                    Schedule
                />
            </InstallConditions>
            <ExitCodes>
                <ExitCode
                    Value
                    Result
                    String
                />
            </ExitCodes>
        </Command>
    </Commands>

    <PackageFiles
        CopyAllComponents
    >
        <PackageFile
            Name
            Path
            HomeSite
            PublicKey
        />
    </PackageFiles>

    <Strings>
        <String
            Name
        >
        </String>
    </Strings>

    <Schedules>
        <Schedule
            Name
        >
           <BuildList />
           <BeforePackage />
           <AfterPackage />
        </Schedule>
    </Schedules>
</Package>
```

## <a name="elements-and-attributes"></a>要素と属性
 `Package` 要素は必須です。 次の属性があります。

| 属性 | 説明 |
|--------------------| - |
| `Culture` | 必須。 このパッケージのカルチャを定義して、使用される言語を決定します。 この属性は `Strings` 要素へのキーであり、インストール時に製品名とエラー メッセージのカルチャ固有の文字列を一覧表示します。 |
| `Name` | 必須。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] などのツール内で開発者に表示されるパッケージの名前。 この属性は `Strings` 要素に対するキーであり、`Package` の `Name` プロパティと `Culture` プロパティに一致するように設定された `Name` プロパティと `Culture` プロパティを持つ `String` 要素が含まれる必要があります。 |
| `LicenseAgreement` | 省略可能。 使用許諾契約書 (EULA) を含む配布パッケージ内のファイルの名前を指定します。  このファイルは、プレーンテキスト ( *.txt*) またはリッチ テキスト形式にすることができます。 ( *.rtf*) |

## <a name="example"></a>例
 次のコード例は、.NET Framework 2.0 を再配布するための完全なパッケージ ファイルを示しています。

```xml
<?xml version="1.0" encoding="utf-8" ?>

<Package
  xmlns="http://schemas.microsoft.com/developer/2004/01/bootstrapper"
  Name="DisplayName"
  Culture="Culture"
  LicenseAgreement="eula.rtf"
>

    <PackageFiles>
        <PackageFile Name="eula.rtf"/>
    </PackageFiles>

    <!-- Defines a localizable string table for error messages-->
    <Strings>
        <String Name="DisplayName">.NET Framework 2.0</String>
        <String Name="Culture">en</String>
        <String Name="AdminRequired">Administrator permissions are required to install the .NET Framework 2.0. Contact your administrator.</String>
        <String Name="InvalidPlatformWin9x">Installation of the .NET Framework 2.0 is not supported on Windows 95. Contact your application vendor.</String>
        <String Name="InvalidPlatformWinNT">Installation of the .NET Framework 2.0 is not supported on Windows NT 4.0. Contact your application vendor.</String>
        <String Name="InvalidPlatformIE">Installation of the .NET Framework 2.0 requires Internet Explorer 5.01 or greater. Contact your application vendor.</String>
        <String Name="InvalidPlatformArchitecture">This version of the .NET Framework 2.0 is not supported on a 64-bit operating system. Contact your application vendor.</String>
        <String Name="WindowsInstallerImproperInstall">Due to an error with Windows Installer, the installation of the .NET Framework 2.0 cannot proceed.</String>
        <String Name="AnotherInstanceRunning">Another instance of setup is already running. The running instance must complete before this setup can proceed.</String>
        <String Name="BetaNDPFailure">A beta version of the .NET Framework was detected on the computer. Uninstall any previous beta versions of .NET Framework before continuing.</String>
        <String Name="GeneralFailure">A failure occurred attempting to install the .NET Framework 2.0.</String>
        <String Name="DotNetFXExe">http://go.microsoft.com/fwlink/?LinkId=37283</String>
        <String Name="InstMsiAExe">http://go.microsoft.com/fwlink/?LinkId=37285</String>
        <String Name="Msi30Exe">http://go.microsoft.com/fwlink/?LinkId=37287</String>
    </Strings>

</Package>
```

## <a name="see-also"></a>関連項目
- [製品およびパッケージ スキーマ リファレンス](../deployment/product-and-package-schema-reference.md)