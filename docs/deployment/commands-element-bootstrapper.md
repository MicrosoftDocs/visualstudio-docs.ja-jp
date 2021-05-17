---
title: '&lt;Commands&gt; 要素 (ブートストラップ) | Microsoft Docs'
description: Commands 要素では、InstallChecks の下にある要素にテストを実装し、ClickOnce ブートストラップ テストが失敗した場合にインストールするパッケージを宣言します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- <Commands> element [bootstrapper]
ms.assetid: e61d5787-fe1f-4ebf-b0cf-0d7909be7ffb
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0f53ca683e40be8e3cc428d013d2b8d3c8c5773e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99881231"
---
# <a name="ltcommandsgt-element-bootstrapper"></a>&lt;Commands&gt; 要素 (ブートストラップ)
`Commands` 要素では、`InstallChecks` 要素の下にある要素によって記述されるテストを実装し、テストが失敗した場合に [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ブートストラップでどのパッケージをインストールする必要があるかを宣言します。

## <a name="syntax"></a>構文

```xml
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
```

## <a name="elements-and-attributes"></a>要素と属性
 `Commands` 要素は必須です。 要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`Reboot`|省略可能。 いずれかのパッケージから再起動終了コードが返された場合に、システムを再起動する必要があるかどうかを指定します。 次の一覧に有効な値を示します。<br /><br /> `Defer`. 再起動は、将来のいつかまで延期されます。<br /><br /> `Immediate`. いずれかのパッケージが再起動終了コードを返した場合は、すぐに再起動が行われるようにします。<br /><br /> `None`. すべての再起動要求が無視されるようにします。<br /><br /> 既定では、 `Immediate`です。|

## <a name="command"></a>コマンド
 `Command` 要素は、`Commands` 要素の子要素です。 `Commands` 要素には、1 つ以上の `Command` 要素を含めることができます。 要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`PackageFile`|必須。 `InstallConditions` によって指定された 1 つ以上の条件から false が返される場合にインストールするパッケージの名前。 このパッケージは、`PackageFile` 要素を使用して、同じファイル内で定義されている必要があります。|
|`Arguments`|省略可能。 パッケージ ファイルに渡すコマンド ライン引数のセット。|
|`EstimatedInstallSeconds`|省略可能。 パッケージをインストールするのにかかる推定時間 (秒単位)。 この値では、ブートストラップからユーザーに表示される進行状況バーのサイズを決定します。 既定値は 0 です。この場合、推定時間は指定されません。|
|`EstimatedDiskBytes`|省略可能。 インストール終了後にパッケージによって占有されると推定されるディスク領域の容量 (バイト単位)。 この値は、ブートストラップによってユーザーに表示されるハード ディスク領域の要件で使用されます。 既定値は 0 です。この場合、ブートストラップによって、ハード ディスク領域の要件は表示されません。|
|`EstimatedTempBytes`|省略可能。 パッケージが必要とする一時ディスク領域の推定容量 (バイト単位)。|
|`Log`|省略可能。 パッケージのルート ディレクトリを基準とした、パッケージによって生成されるログ ファイルへのパス。|

## <a name="installconditions"></a>InstallConditions
 `InstallConditions` 要素は、`Command` 要素の子です。 各 `Command` 要素には、`InstallConditions` 要素を多くても 1 つ含めることができます。 `InstallConditions` 要素が存在しない場合は、`Condition` によって指定されたパッケージが常に実行されます。

## <a name="bypassif"></a>BypassIf
 `BypassIf` 要素は `InstallConditions` 要素の子であり、コマンドを実行してはいけない肯定的な条件を記述します。 各 `InstallConditions` 要素には、0 個以上の `BypassIf` 要素を含めることができます。

 `BypassIf` には以下の属性があります。

|属性|説明|
|---------------|-----------------|
|`Property`|必須。 テストするプロパティの名前。 プロパティは、`InstallChecks` 要素の子によって以前に定義されている必要があります。 詳細については、[\<InstallChecks> 要素](../deployment/installchecks-element-bootstrapper.md)に関するページを参照してください。|
|`Compare`|必須。 実行する比較の種類。 次の一覧に有効な値を示します。<br /><br /> `ValueEqualTo`, `ValueNotEqualTo`, `ValueGreaterThan`, `ValueGreaterThanOrEqualTo`, `ValueLessThan`, `ValueLessThanOrEqualTo`, `VersionEqualTo`, `VersionNotEqualTo`, `VersionGreaterThan`, `VersionGreaterThanOrEqualTo`, `VersionLessThan`, `VersionLessThanOrEqualTo`, `ValueExists`, `ValueNotExists`|
|`Value`|必須。 プロパティと比較する値。|
|`Schedule`|省略可能。 この規則をいつ評価する必要があるかを定義する `Schedule` タグの名前。|

## <a name="failif"></a>FailIf
 `FailIf` 要素は `InstallConditions` 要素の子であり、インストールを停止する必要がある肯定的な条件を記述します。 各 `InstallConditions` 要素には、0 個以上の `FailIf` 要素を含めることができます。

 `FailIf` には以下の属性があります。

|属性|説明|
|---------------|-----------------|
|`Property`|必須。 テストするプロパティの名前。 プロパティは、`InstallChecks` 要素の子によって以前に定義されている必要があります。 詳細については、[\<InstallChecks> 要素](../deployment/installchecks-element-bootstrapper.md)に関するページを参照してください。|
|`Compare`|必須。 実行する比較の種類。 次の一覧に有効な値を示します。<br /><br /> `ValueEqualTo`, `ValueNotEqualTo`, `ValueGreaterThan`, `ValueGreaterThanOrEqualTo`, `ValueLessThan`, `ValueLessThanOrEqualTo`, `VersionEqualTo`, `VersionNotEqualTo`, `VersionGreaterThan`, `VersionGreaterThanOrEqualTo`, `VersionLessThan`, `VersionLessThanOrEqualTo`, `ValueExists`, `ValueNotExists`|
|`Value`|必須。 プロパティと比較する値。|
|`String`|省略可能。 失敗時にユーザーに表示するテキスト。|
|`Schedule`|省略可能。 この規則をいつ評価する必要があるかを定義する `Schedule` タグの名前。|

## <a name="exitcodes"></a>ExitCodes
 `ExitCodes` 要素は、`Command` 要素の子です。 `ExitCodes` 要素には `ExitCode` 要素が 1 つ以上含まれていて、パッケージからの終了コードに応答してどのインストールを実行する必要があるかが決定されます。 `Command` 要素の下には、省略可能な `ExitCode` 要素を 1 つ指定できます。 `ExitCodes` に属性はありません。

## <a name="exitcode"></a>ExitCode
 `ExitCode` 要素は、`ExitCodes` 要素の子です。 `ExitCode` 要素では、パッケージからの終了コードに応答して、どのインストールを実行する必要があるかが決定されます。 `ExitCode` には子要素は含まれず、以下の属性があります。

|属性|説明|
|---------------|-----------------|
|`Value`|必須。 この `ExitCode` 要素が適用される終了コードの値。|
|`Result`|必須。 この終了コードに、どのようにインストールを対応させる必要があるか。 次の一覧に有効な値を示します。<br /><br /> `Success`. 正常にインストールされたとパッケージにフラグを付けます。<br /><br /> `SuccessReboot`. 正常にインストールされたとパッケージにフラグを付けて、再起動するようにシステムに指示します。<br /><br /> `Fail`. 失敗したとパッケージにフラグを付けます。<br /><br /> `FailReboot`. 失敗したとパッケージにフラグを付けて、再起動するようにシステムに指示します。|
|`String`|省略可能。 この終了コードに対する応答でユーザーに表示する値。|
|`FormatMessageFromSystem`|省略可能。 システムによって提供される、終了コードに対応するエラー メッセージを使用するか、`String` で指定されている値を使用するかを決定します。 有効な値は、システムによって提供されるエラーを使用することを意味する `true` と、`String` によって提供される文字列を使用することを意味する `false` です。 既定では、 `false`です。 このプロパティが `false` で、`String` が設定されていない場合は、システムによって提供されるエラーが使用され ます。|

## <a name="example"></a>例
 次のコード例では、.NET Framework 2.0 をインストールするためのコマンドを定義しています。

```xml
<Commands Reboot="Immediate">
    <Command PackageFile="instmsia.exe"
             Arguments= ' /q /c:"msiinst /delayrebootq"'
             EstimatedInstallSeconds="20" >
        <InstallConditions>
           <BypassIf Property="VersionNT" Compare="ValueExists"/>
             BypassIf Property="VersionMsi" Compare="VersionGreaterThanOrEqualTo" Value="2.0"/>
        </InstallConditions>
        <ExitCodes>
            <ExitCode Value="0" Result="SuccessReboot"/>
            <ExitCode Value="1641" Result="SuccessReboot"/>
            <ExitCode Value="3010" Result="SuccessReboot"/>
            <DefaultExitCode Result="Fail" FormatMessageFromSystem="true" String="GeneralFailure" />
        </ExitCodes>
    </Command>
    <Command PackageFile="WindowsInstaller-KB884016-v2-x86.exe"
             Arguments= '/quiet /norestart'
             EstimatedInstallSeconds="20" >
      <InstallConditions>
          <BypassIf Property="Version9x" Compare="ValueExists"/>
          <BypassIf Property="VersionNT" Compare="VersionLessThan" Value="5.0.3"/>
          <BypassIf Property="VersionMsi" Compare="VersionGreaterThanOrEqualTo" Value="3.0"/>
          <FailIf Property="AdminUser" Compare="ValueEqualTo" Value="false" String="AdminRequired"/>
      </InstallConditions>
      <ExitCodes>
          <ExitCode Value="0" Result="Success"/>
          <ExitCode Value="1641" Result="SuccessReboot"/>
          <ExitCode Value="3010" Result="SuccessReboot"/>
          <DefaultExitCode Result="Fail" FormatMessageFromSystem="true" String="GeneralFailure" />
      </ExitCodes>
    </Command>
    <Command PackageFile="dotnetfx.exe"
         Arguments=' /q:a /c:"install /q /l"'
         EstimatedInstalledBytes="21000000"
         EstimatedInstallSeconds="300">

        <!-- These checks determine whether the package is to be installed -->
        <InstallConditions>
            <!-- Either of these properties indicates the .NET Framework is already installed -->
            <BypassIf Property="DotNetInstalled" Compare="ValueNotEqualTo" Value="0"/>

            <!-- Block install if user does not have adminpermissions -->
            <FailIf Property="AdminUser" Compare="ValueEqualTo" Value="false" String="AdminRequired"/>

            <!-- Block install on Windows 95 -->
            <FailIf Property="Version9X" Compare="VersionLessThan" Value="4.10" String="InvalidPlatformWin9x"/>

            <!-- Block install on Windows 2000 SP 2 or less -->
            <FailIf Property="VersionNT" Compare="VersionLessThan" Value="5.0.3" String="InvalidPlatformWinNT"/>

            <!-- Block install if Internet Explorer 5.01 or later is not present -->
            <FailIf Property="IEVersion" Compare="ValueNotExists" String="InvalidPlatformIE" />
            <FailIf Property="IEVersion" Compare="VersionLessThan" Value="5.01" String="InvalidPlatformIE" />

            <!-- Block install if the operating system does not support x86 -->
            <FailIf Property="ProcessorArchitecture" Compare="ValueNotEqualTo" Value="Intel" String="InvalidPlatformArchitecture" />
       </InstallConditions>

        <ExitCodes>
            <ExitCode Value="0" Result="Success"/>
            <ExitCode Value="3010" Result="SuccessReboot"/>
            <ExitCode Value="4097" Result="Fail" String="AdminRequired"/>
            <ExitCode Value="4098" Result="Fail" String="WindowsInstallerComponentFailure"/>
            <ExitCode Value="4099" Result="Fail" String="WindowsInstallerImproperInstall"/>
            <ExitCode Value="4101" Result="Fail" String="AnotherInstanceRunning"/>
            <ExitCode Value="4102" Result="Fail" String="OpenDatabaseFailure"/>
            <ExitCode Value="4113" Result="Fail" String="BetaNDPFailure"/>
            <DefaultExitCode Result="Fail" FormatMessageFromSystem="true" String="GeneralFailure" />
        </ExitCodes>

    </Command>
</Commands>
```

## <a name="see-also"></a>関連項目
- [製品およびパッケージ スキーマ リファレンス](../deployment/product-and-package-schema-reference.md)
- [\<InstallChecks> 要素](../deployment/installchecks-element-bootstrapper.md)