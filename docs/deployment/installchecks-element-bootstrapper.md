---
title: '&lt;InstallChecks&gt; 要素 (ブートストラップ) |Microsoft Docs'
description: InstallChecks 要素は、アプリケーションのすべての前提条件がインストール済みであることを確認するためのローカル コンピューター上でのさまざまなテストの開始をサポートします。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- <InstallChecks> element [bootstrapper]
ms.assetid: ad329c87-b0ad-4304-84de-ae9496514c42
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 550baf52347c1128ef50509e7787861355c9428f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99903394"
---
# <a name="ltinstallchecksgt-element-bootstrapper"></a>&lt;InstallChecks &gt; 要素 (ブートストラップ)
`InstallChecks` 要素は、アプリケーションに該当するすべての前提条件がインストール済みであることを確認するためのローカル コンピューターへのさまざまなテストの開始をサポートします。

## <a name="syntax"></a>構文

```xml
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
        FileName
        SearchDepth
    />
</InstallChecks>
```

## <a name="assemblycheck"></a>AssemblyCheck
 この要素は、`InstallChecks` 要素の省略可能な子要素です。 `AssemblyCheck` の各インスタンスについて、ブートストラップは、要素によって識別されるアセンブリがグローバル アセンブリ キャッシュ (GAC) に存在することを確認します。 要素は含まれず、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`Property`|必須。 結果を格納するプロパティの名前。 このプロパティは、`Command` 要素の子である、`InstallConditions` 要素の下にあるテストから参照できます。 詳細については、[\<Commands> 要素](../deployment/commands-element-bootstrapper.md)に関するページを参照してください。|
|`Name`|必須。 チェックするアセンブリの完全修飾名。|
|`PublicKeyToken`|必須。 この厳密な名前を持つアセンブリに関連付けられている公開キーの省略形。 GAC に格納されているすべてのアセンブリは、名前、バージョン、および公開キーを持っている必要があります。|
|`Version`|必須。 アセンブリのバージョン。<br /><br /> バージョン番号の形式は \<*major version*>.\<*minor version*>.\<*build version*>.\<*revision version*> です。|
|`Language`|省略可能。 ローカライズされたアセンブリの言語。 既定値は `neutral` です。|
|`ProcessorArchitecture`|省略可能。 このインストールの対象となるコンピューター プロセッサ。 既定値は `msil` です。|

## <a name="externalcheck"></a>ExternalCheck
 この要素は、`InstallChecks` 要素の省略可能な子要素です。 `ExternalCheck` の各インスタンスについて、ブートストラップは、指定された外部プログラムを別のプロセスで実行し、`Property` によって示されるプロパティにその終了コードを格納します。 `ExternalCheck` は、複雑な依存関係のチェックを実装する場合や、コンポーネントの存在を確認する唯一の方法がインスタンス化である場合に便利です。

 `ExternalCheck` には要素は含まれず、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`Property`|必須。 結果を格納するプロパティの名前。 このプロパティは、`Command` 要素の子である、`InstallConditions` 要素の下にあるテストから参照できます。 詳細については、[\<Commands> 要素](../deployment/commands-element-bootstrapper.md)に関するページを参照してください。|
|`PackageFile`|必須。 実行する外部プログラム。 プログラムは、セットアップ配布パッケージの一部である必要があります。|
|`Arguments`|省略可能。 `PackageFile` によって指定された実行可能ファイルにコマンドライン引数を渡します。|

## <a name="filecheck"></a>FileCheck
 この要素は、`InstallChecks` 要素の省略可能な子要素です。 `FileCheck` の各インスタンスについて、ブートストラップは、指定されたファイルが存在するかどうかを判断し、そのファイルのバージョン番号を返します。 ファイルにバージョン番号がない場合、ブートストラップは `Property` によって指定されたプロパティを 0 に設定します。 ファイルが存在しない場合、`Property` はどのような値にも設定されません。

 `FileCheck` には要素は含まれず、次の属性があります。

| 属性 | 説明 |
|-----------------| - |
| `Property` | 必須。 結果を格納するプロパティの名前。 このプロパティは、`Command` 要素の子である、`InstallConditions` 要素の下にあるテストから参照できます。 詳細については、[\<Commands> 要素](../deployment/commands-element-bootstrapper.md)に関するページを参照してください。 |
| `FileName` | 必須。 検索するファイルの名前。 |
| `SearchPath` | 必須。 ファイルを検索するディスクまたはフォルダー。 `SpecialFolder` が割り当てられている場合、これは相対パスである必要があります。それ以外の場合は、絶対パスである必要があります。 |
| `SpecialFolder` | 省略可能。 Windows または [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] のいずれかにとって特別な意味を持つフォルダー。 既定では、`SearchPath` は絶対パスとして解釈されます。 有効な値は次のとおりです。<br /><br /> `AppDataFolder`. 現在のユーザーに固有な、この [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションのアプリケーション データ フォルダー。<br /><br /> `CommonAppDataFolder`. すべてのユーザーが使用するアプリケーション データ フォルダー。<br /><br /> `CommonFilesFolder`. 現在のユーザーの Common Files フォルダー。<br /><br /> `LocalDataAppFolder`. 非ローミング アプリケーションのデータ フォルダー。<br /><br /> `ProgramFilesFolder`. 32 ビット アプリケーションの標準の Program Files フォルダー。<br /><br /> `StartUpFolder`. システムの起動時に起動されるすべてのアプリケーションを含むフォルダー。<br /><br /> `SystemFolder`. 32 ビットシステム DLL を格納するフォルダー。<br /><br /> `WindowsFolder`. Windows システムのインストールが含まれるフォルダー。<br /><br /> `WindowsVolume`. Windows システムのインストールが含まれるドライブまたはパーティション。 |
| `SearchDepth` | 省略可能。 指定されたファイルのサブフォルダーを検索する深さ。 検索は深さ優先です。 既定値は 0 です。これにより、`SpecialFolder` と **SearchPath** によって指定される最上位フォルダーに検索が制限されます。 |

## <a name="msiproductcheck"></a>MsiProductCheck
 この要素は、`InstallChecks` 要素の省略可能な子要素です。 `MsiProductCheck` の各インスタンスについて、ブートストラップは、指定された Microsoft Windows インストーラーのインストールが完了まで実行したかどうかを確認します。 プロパティ値は、そのインストールされる製品の状態に応じて設定されます。 正の値は、製品がインストールされていることを示します。0 または -1 は、インストールされていないことを示します。 (詳細については、Windows インストーラー SDK 関数 MsiQueryFeatureState を参照してください)。 コンピューターに Windows インストーラーがインストールされていない場合、`Property` は設定されません。

 `MsiProductCheck` には要素は含まれず、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`Property`|必須。 結果を格納するプロパティの名前。 このプロパティは、`Command` 要素の子である、`InstallConditions` 要素の下にあるテストから参照できます。 詳細については、[\<Commands> 要素](../deployment/commands-element-bootstrapper.md)に関するページを参照してください。|
|`Product`|必須。 インストールされる製品の GUID。|
|`Feature`|省略可能。 インストールされるアプリケーションの特定の機能の GUID。|

## <a name="registrycheck"></a>RegistryCheck
 この要素は、`InstallChecks` 要素の省略可能な子要素です。 `RegistryCheck` の各インスタンスについて、ブートストラップは、指定されたレジストリ キーが存在するかどうか、または示された値を持つかどうかを確認します。

 `RegistryCheck` には要素は含まれず、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`Property`|必須。 結果を格納するプロパティの名前。 このプロパティは、`Command` 要素の子である、`InstallConditions` 要素の下にあるテストから参照できます。 詳細については、[\<Commands> 要素](../deployment/commands-element-bootstrapper.md)に関するページを参照してください。|
|`Key`|必須。 レジストリ キーの名前。|
|`Value`|省略可能。 取得するレジストリ値の名前。 既定では、既定値のテキストが返されます。 `Value` は、文字列または DWORD のいずれかである必要があります。|

## <a name="registryfilecheck"></a>RegistryFileCheck
 この要素は、`InstallChecks` 要素の省略可能な子要素です。 `RegistryFileCheck` の各インスタンスについて、ブートストラップは、指定されたファイルのバージョンを取得します。最初に、指定したレジストリ キーからファイル パスを取得しようとします。 これは、レジストリで値として指定されているディレクトリでファイルを検索する場合に特に便利です。

 `RegistryFileCheck` には要素は含まれず、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`Property`|必須。 結果を格納するプロパティの名前。 このプロパティは、`Command` 要素の子である、`InstallConditions` 要素の下にあるテストから参照できます。 詳細については、[\<Commands> 要素](../deployment/commands-element-bootstrapper.md)に関するページを参照してください。|
|`Key`|必須。 レジストリ キーの名前。 その値は、`File` 属性が設定されていない限り、ファイル パスとして解釈されます。 このキーが存在しない場合、`Property` は設定されません。|
|`Value`|省略可能。 取得するレジストリ値の名前。 既定では、既定値のテキストが返されます。 `Value` は文字列である必要があります。|
|`FileName`|省略可能。 ファイルの名前。 指定した場合、レジストリ キーから取得される値はディレクトリ パスであると見なされ、この名前が追加されます。 指定しない場合、レジストリから返される値は、ファイルの完全パスであると見なされます。|
|`SearchDepth`|省略可能。 指定されたファイルのサブフォルダーを検索する深さ。 検索は深さ優先です。 既定値は 0 です。これにより、レジストリ キーの値によって指定される最上位フォルダーに検索が制限されます。|

## <a name="remarks"></a>解説
 `InstallChecks` の下にある要素によって、実行するテストが定義されますが、テストは実行されません。 テストを実行するには、`Commands` 要素の下に `Command` 要素を作成する必要があります。

## <a name="example"></a>例
 次のコード例に、.NET Framework の製品ファイルで使用されている `InstallChecks` 要素を示します。

```xml
<InstallChecks>
    <ExternalCheck Property="DotNetInstalled" PackageFile="dotnetchk.exe" />
    <RegistryCheck Property="IEVersion" Key="HKLM\Software\Microsoft\Internet Explorer" Value="Version" />
</InstallChecks>
```

## <a name="installconditions"></a>InstallConditions
 `InstallChecks` が評価されると、プロパティが生成されます。 次に、プロパティが `InstallConditions` によって使用されて、パッケージのインストール、バイパス、または失敗のいずれを行うかを決定します。 次の表に `InstallConditions` を示します。

|条件|説明|
|-|-|
|`FailIf`|いずれかの `FailIf` 条件が true と評価された場合、パッケージは失敗します。 残りの条件は評価されません。|
|`BypassIf`|いずれかの `BypassIf` 条件が true と評価された場合、パッケージはバイパスされます。 残りの条件は評価されません。|

## <a name="predefined-properties"></a>事前定義済みプロパティ
 `BypassIf` および `FailIf` 要素を次の表に示します。

|プロパティ|Notes|指定できる値|
|--------------|-----------|---------------------|
|`Version9X`|Windows 9X オペレーティング システムのバージョン番号。|4.10 = Windows 98|
|`VersionNT`|Windows NT ベースのオペレーティング システムのバージョン番号。|Major.Minor.ServicePack<br /><br /> 5.0 = Windows 2000<br /><br /> 5.1.0 = Windows XP<br /><br /> 5.1.2 = Windows XP Professional SP2<br /><br /> 5.2.0 = Windows Server 2003|
|`VersionNT64`|64 ビット Windows NT ベースのオペレーティング システムのバージョン番号。|上記の説明と同じ。|
|`VersionMsi`|Windows インストーラー サービスのバージョン番号。|2.0 = Windows インストーラー 2.0|
|`AdminUser`|ユーザーが Windows NT ベースのオペレーティング システムに対する管理者特権を持っているかどうかを指定します。|0 = 管理者特権なし<br /><br /> 1 = 管理者特権|

 たとえば、Windows 95 を実行しているコンピューターでインストールをブロックするには、次のようなコードを使用します。

```xml
    <!-- Block install on Windows 95 -->
    <FailIf Property="Version9X" Compare="VersionLessThan" Value="4.10" String="InvalidPlatform"/>
```

 FailIf または BypassIf 条件が満たされる場合にインストール チェックの実行をスキップするには、BeforeInstallChecks 属性を使用します。  次に例を示します。

```xml
    <!-- Block install and do not evaluate install checks if user does not have admin privileges -->
    <FailIf Property="AdminUser" Compare="ValueEqualTo" Value="false" String="AdminRequired" BeforeInstallChecks="true"/>
```

>[!NOTE]
>`BeforeInstallChecks` 属性は、Visual Studio 2019 Update 9 リリース以降でサポートされます。

## <a name="see-also"></a>関連項目
- [\<Commands> 要素](../deployment/commands-element-bootstrapper.md)
- [製品およびパッケージ スキーマ リファレンス](../deployment/product-and-package-schema-reference.md)