---
title: プロパティ関数 | Microsoft Docs
description: MSBuild のプロパティ定義に含まれている .NET Framework メソッドの呼び出しであるプロパティ関数を使用する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/21/2017
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, property functions
ms.assetid: 2253956e-3ae0-4bdc-9d3a-4881dfae4ddb
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a47ff76c98c5788fdfca3d633c87664b6802de70
ms.sourcegitcommit: 8b75524dc544e34d09ef428c3ebbc9b09f14982d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2021
ms.locfileid: "113222956"
---
# <a name="property-functions"></a>プロパティ関数

プロパティ関数は、MSBuild のプロパティ定義に含まれている .NET Framework メソッドの呼び出しです。 タスクとは異なり、プロパティ関数はターゲットの外側でも使用でき、ターゲットが実行される前に評価されます。

MSBuild タスクを使用しなくても、システム時刻の読み取り、文字列の比較、正規表現の照合、その他の処理をビルド スクリプト内で実行できます。 MSBuild は、文字列を数値に、数値を文字列に変換しようと試みます。また、必要に応じて他の変換も実行します。

プロパティ関数から返される文字列値は、[特殊文字](msbuild-special-characters.md)がエスケープされます。 プロジェクト ファイルに直接配置した場合と同様に値を扱う場合は、`$([MSBuild]::Unescape())` を使用して特殊文字のエスケープを解除します。

プロパティ関数は .NET Framework 4 以降で使用できます。

## <a name="property-function-syntax"></a>プロパティ関数の構文

次に 3 種類のプロパティ関数を示します。各関数には異なる構文があります。

- 文字列 (インスタンス) プロパティ関数
- 静的プロパティ関数
- MSBuild プロパティ関数

### <a name="string-property-functions"></a>文字列プロパティ関数

ビルド プロパティの値はすべて文字列値です。 文字列 (インスタンス) メソッドを使用してプロパティ値を操作できます。 たとえば、次のコードを使用して、完全パスを表すビルド プロパティからドライブ名 (最初の 3 文字) を抽出できます。

```
$(ProjectOutputFolder.Substring(0,3))
```

### <a name="static-property-functions"></a>静的プロパティ関数

ビルド スクリプトで、各種システム クラスの静的プロパティおよびメソッドにアクセスできます。 静的プロパティの値を取得するには、次の構文を使用します。ここで、\<Class> はシステム クラスの名前、\<Property> はプロパティの名前です。

```
$([Class]::Property)
```

たとえば、次のコードを使用して、ビルド プロパティを現在の日付と時刻に設定します。

```xml
<Today>$([System.DateTime]::Now)</Today>
```

静的メソッドを呼び出すには、次の構文を使用します。ここで、\<Class> はシステム クラスの名前、\<Method> はメソッドの名前、(\<Parameters>) はメソッドのパラメーター リストです。

```
$([Class]::Method(Parameters))
```

たとえば、ビルド プロパティを新しい GUID に設定するには、次のスクリプトを使用できます。

```xml
<NewGuid>$([System.Guid]::NewGuid())</NewGuid>
```

静的プロパティ関数では、次のシステム クラスの任意の静的メソッドやプロパティを使用できます。

- <xref:System.Byte?displayProperty=nameWithType>
- <xref:System.Char?displayProperty=nameWithType>
- <xref:System.Convert?displayProperty=nameWithType>
- <xref:System.DateTime?displayProperty=nameWithType>
- <xref:System.Decimal?displayProperty=nameWithType>
- <xref:System.Double?displayProperty=nameWithType>
- <xref:System.Enum?displayProperty=nameWithType>
- <xref:System.Guid?displayProperty=nameWithType>
- <xref:System.Int16?displayProperty=nameWithType>
- <xref:System.Int32?displayProperty=nameWithType>
- <xref:System.Int64?displayProperty=nameWithType>
- <xref:System.IO.Path?displayProperty=nameWithType>
- <xref:System.Math?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.OSPlatform?displayProperty=nameWithType>
- <xref:System.Runtime.InteropServices.RuntimeInformation?displayProperty=nameWithType>
- <xref:System.UInt16?displayProperty=nameWithType>
- <xref:System.UInt32?displayProperty=nameWithType>
- <xref:System.UInt64?displayProperty=nameWithType>
- <xref:System.SByte?displayProperty=nameWithType>
- <xref:System.Single?displayProperty=nameWithType>
- <xref:System.String?displayProperty=nameWithType>
- <xref:System.StringComparer?displayProperty=nameWithType>
- <xref:System.TimeSpan?displayProperty=nameWithType>
- <xref:System.Text.RegularExpressions.Regex?displayProperty=nameWithType>
- <xref:System.UriBuilder?displayProperty=nameWithType>
- <xref:System.Version?displayProperty=nameWithType>
- <xref:Microsoft.Build.Utilities.ToolLocationHelper?displayProperty=nameWithType>

さらに、次の静的メソッドおよびプロパティを使用できます。

- [System.Environment::CommandLine](xref:System.Environment.CommandLine*)
- [System.Environment::ExpandEnvironmentVariables](xref:System.Environment.ExpandEnvironmentVariables*)
- [System.Environment::GetEnvironmentVariable](xref:System.Environment.GetEnvironmentVariable*)
- [System.Environment::GetEnvironmentVariables](xref:System.Environment.GetEnvironmentVariables*)
- [System.Environment::GetFolderPath](xref:System.Environment.GetFolderPath*)
- [System.Environment::GetLogicalDrives](xref:System.Environment.GetLogicalDrives*)
- [System.IO.Directory::GetDirectories](xref:System.IO.Directory.GetDirectories*)
- [System.IO.Directory::GetFiles](xref:System.IO.Directory.GetFiles*)
- [System.IO.Directory::GetLastAccessTime](xref:System.IO.Directory.GetLastAccessTime*)
- [System.IO.Directory::GetLastWriteTime](xref:System.IO.Directory.GetLastWriteTime*)
- [System.IO.Directory::GetParent](xref:System.IO.Directory.GetParent*)
- [System.IO.File::Exists](xref:System.IO.File.Exists*)
- [System.IO.File::GetCreationTime](xref:System.IO.File.GetCreationTime*)
- [System.IO.File::GetAttributes](xref:System.IO.File.GetAttributes*)
- [System.IO.File::GetLastAccessTime](xref:System.IO.File.GetLastAccessTime*)
- [System.IO.File::GetLastWriteTime](xref:System.IO.File.GetLastWriteTime*)
- [System.IO.File::ReadAllText](xref:System.IO.File.ReadAllText*)

### <a name="calling-instance-methods-on-static-properties"></a>静的プロパティ上でインスタンス メソッドを呼び出す

オブジェクト インスタンスを返す静的プロパティにアクセスすると、そのオブジェクトのインスタンス メソッドを呼び出すことができます。 インスタンス メソッドを呼び出すには、次の構文を使用します。ここで、\<Class> はシステム クラスの名前、\<Property> はプロパティの名前、\<Method> はメソッドの名前、(\<Parameters>) はメソッドのパラメーター リストです。

```
$([Class]::Property.Method(Parameters))
```

クラスの名前は、名前空間を使用して完全修飾する必要があります。

たとえば、次のコードを使用して、ビルド プロパティを現在の日付 (今日) に設定します。

```xml
<Today>$([System.DateTime]::Now.ToString('yyyy.MM.dd'))</Today>
```

### <a name="msbuild-property-functions"></a>MSBuild プロパティ関数

ビルド内のいくつかの静的メソッドにアクセスすると、算術、ビットごとの論理、およびエスケープ文字のサポートが提供されます。 次の構文を使用して、これらのメソッドにアクセスします。ここで、\<Method> はメソッドの名前、(\<Parameters>) はメソッドのパラメーター リストです。

```
$([MSBuild]::Method(Parameters))
```

たとえば、数値を持つ 2 つのプロパティを合計するには、次のコードを使用します。

```
$([MSBuild]::Add($(NumberOne), $(NumberTwo)))
```

次に MSBuild プロパティ関数の一覧を示します。

|関数シグネチャ|説明|
|------------------------|-----------------|
|double Add(double a, double b)|2 個の倍精度浮動小数点数を加算します。|
|long Add(long a, long b)|2 個の長整数を加算します。|
|double Subtract(double a, double b)|2 個の倍精度浮動小数点数を減算します。|
|long Subtract(long a, long b)|2 個の長整数を減算します。|
|double Multiply(double a, double b)|2 個の倍精度浮動小数点数を乗算します。|
|long Multiply(long a, long b)|2 個の長整数を乗算します。|
|double Divide(double a, double b)|2 個の倍精度浮動小数点数を除算します。|
|long Divide(long a, long b)|2 個の長整数を除算します。|
|double Modulo(double a, double b)|2 個の倍精度浮動小数点数を剰余します。|
|long Modulo(long a, long b)|2 個の長整数を剰余します。|
|string Escape(string unescaped)|MSBuild のエスケープ ルールに従って文字列をエスケープします。|
|string Unescape(string escaped)|MSBuild のエスケープ ルールに従って文字列をエスケープ解除します。|
|int BitwiseOr(int first, int second)|1 番目と 2 番目 (first &#124; second) でビットごとの `OR` を実行します。|
|int BitwiseAnd(int first, int second)|1 番目と 2 番目 (first & second) でビットごとの `AND` を実行します。|
|int BitwiseXor(int first, int second)|1 番目と 2 番目 (first ^ second) でビットごとの `XOR` を実行します。|
|int BitwiseNot(int first)|ビットごとの `NOT` (~first) を実行します。|
|bool IsOsPlatform(string platformString)|現在の OS プラットフォームが `platformString` かどうかを指定します。 `platformString` は <xref:System.Runtime.InteropServices.OSPlatform> のメンバーである必要があります。|
|bool IsOSUnixLike()|現在の OS が Unix システムの場合は true です。|
|string NormalizePath(params string[] path)|指定されたパスの正規化された完全なパスを取得し、現在のオペレーティング システムの適切なディレクトリ区切り文字が含まれていることを確認します。|
|string NormalizeDirectory(params string[] path)|指定されたディレクトリの正規化された完全なパスを取得し、現在のオペレーティング システムの適切なディレクトリ区切り文字が含まれていて、末尾にスラッシュがあることを確認します。|
|string EnsureTrailingSlash(string path)|指定されたパスの末尾にスラッシュがない場合は、追加します。 パスが空の文字列の場合は変更されません。|
|string GetPathOfFileAbove(string file, string startingDirectory)|現在のビルド ファイルの場所の上にあるディレクトリ構造内のファイルへの完全なパスを検索して返します。指定した場合は `startingDirectory` が起点となります。|
|GetDirectoryNameOfFileAbove(string startingDirectory, string fileName)|指定したディレクトリか、そのディレクトリの上のディレクトリ構造内の場所から、ファイルのディレクトリを探して返します。|
|string MakeRelative(string basePath, string path)|`path` を `basePath` に対して相対的にします。 `basePath` は絶対ディレクトリである必要があります。 `path` を相対にできない場合、verbatim が返されます。 `Uri.MakeRelativeUri` と似ています。|
|string ValueOrDefault(string conditionValue, string defaultValue)|パラメーター 'conditionValue' が空の場合にのみ、パラメーター 'defaultValue' に文字列を返します。それ以外の場合は、値 conditionValue を返します。|

## <a name="nested-property-functions"></a>入れ子になったプロパティ関数

次の例が示すように、プロパティ関数を組み合わせてより複雑な関数を形成します。

```
$([MSBuild]::BitwiseAnd(32, $([System.IO.File]::GetAttributes(tempFile))))
```

この例では、<xref:System.IO.FileAttributes> というパスにより与えられたファイルの `Archive``tempFile` ビット (32 または 0) の値が返されます。 列挙データ値はプロパティ関数内で名前によって表示できないことに注意してください。 代わりに数値 (32) を使用する必要があります。

入れ子になったプロパティ関数では、メタデータも表示される可能性があります。 詳細については、「[MSBuild バッチ](../msbuild/msbuild-batching.md)」をご覧ください。

## <a name="msbuild-doestaskhostexist"></a>MSBuild の DoesTaskHostExist

MSBuild の `DoesTaskHostExist` プロパティ関数は、指定したランタイムとアーキテクチャ値に対してタスク ホストが現在インストールされているかどうかを返します。

このプロパティ関数には次の構文があります。

```
$([MSBuild]::DoesTaskHostExist(string theRuntime, string theArchitecture))
```

## <a name="msbuild-ensuretrailingslash"></a>MSBuild EnsureTrailingSlash

MSBuild の `EnsureTrailingSlash` プロパティ関数は、末尾のスラッシュがないときにそれを追加します。

このプロパティ関数には次の構文があります。

```
$([MSBuild]::EnsureTrailingSlash('$(PathProperty)'))
```

## <a name="msbuild-getdirectorynameoffileabove"></a>MSBuild の GetDirectoryNameOfFileAbove

MSBuild の `GetDirectoryNameOfFileAbove` プロパティ関数は、パスの現在のディレクトリの上にあるディレクトリ内でファイルを探します。

 このプロパティ関数には次の構文があります。

```
$([MSBuild]::GetDirectoryNameOfFileAbove(string ThePath, string TheFile))
```

 次のコードはこの構文の例です。

```xml
<Import Project="$([MSBuild]::GetDirectoryNameOfFileAbove($(MSBuildThisFileDirectory), EnlistmentInfo.props))\EnlistmentInfo.props" Condition=" '$([MSBuild]::GetDirectoryNameOfFileAbove($(MSBuildThisFileDirectory), EnlistmentInfo.props))' != '' " />
```

## <a name="msbuild-getpathoffileabove"></a>MSBuild GetPathOfFileAbove

MSBuild の `GetPathOfFileAbove` プロパティ関数では、指定したファイルのパスが返されます (現在のディレクトリの上のディレクトリ構造内にある場合)。 呼び出しと同じ機能です

```xml
<Import Project="$([MSBuild]::GetDirectoryNameOfFileAbove($(MSBuildThisFileDirectory), dir.props))\dir.props" />
```

このプロパティ関数には次の構文があります。

```
$([MSBuild]::GetPathOfFileAbove(dir.props))
```

## <a name="msbuild-getregistryvalue"></a>MSBuild の GetRegistryValue

MSBuild の `GetRegistryValue` プロパティ関数は、レジストリ キーの値を返します。 この関数は、キー名と値の名前という 2 つの引数を取り、レジストリの値を返します。 値の名前を指定しない場合は、既定値が返されます。

この関数を使用する方法を次の例に示します。

```
$([MSBuild]::GetRegistryValue(`HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\10.0\Debugger`, ``))                                  // default value
$([MSBuild]::GetRegistryValue(`HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\10.0\Debugger`, `SymbolCacheDir`))
$([MSBuild]::GetRegistryValue(`HKEY_LOCAL_MACHINE\SOFTWARE\(SampleName)`, `(SampleValue)`))             // parens in name and value
```

## <a name="msbuild-getregistryvaluefromview"></a>MSBuild の GetRegistryValueFromView

MSBuild の `GetRegistryValueFromView` プロパティ関数は、レジストリ キー、値、および 1 つ以上の順序づけられたレジストリ ビューを含むシステム レジストリ データを取得します。 キーと値は見つかるまで各レジストリ ビューで順番に検索されます。

このプロパティ関数の構文を次に示します。

```
[MSBuild]::GetRegistryValueFromView(string keyName, string valueName, object defaultValue, params object[] views)
```

Windows 64 ビット オペレーティング システムは、**HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node** というレジストリ キーを保持しています。このキーは、32 ビット アプリケーションに対して **HKEY_LOCAL_MACHINE\SOFTWARE** というレジストリ ビューを提供します。

既定では、WOW64 で実行されている 32 ビット アプリケーションは 32 ビットのレジストリ ビューにアクセスし、64 ビット アプリケーションは 64 ビットのレジストリ ビューにアクセスします。

次のレジストリ ビューが使用できます。

|レジストリ ビュー|定義|
|-------------------|----------------|
|RegistryView.Registry32|32 ビット アプリケーションのレジストリ ビュー。|
|RegistryView.Registry64|64 ビット アプリケーションのレジストリ ビュー。|
|RegistryView.Default|アプリケーションが実行されているプロセスに対応するレジストリ ビュー。|

次に例を示します。

 ```
$([MSBuild]::GetRegistryValueFromView('HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SDKs\Silverlight\v3.0\ReferenceAssemblies', 'SLRuntimeInstallPath', null, RegistryView.Registry64, RegistryView.Registry32))
```

最初に 64 ビットのレジストリ ビュー、次に 32 ビットのレジストリ ビューを参照して、**ReferenceAssemblies** キーの **SLRuntimeInstallPath** データを取得します。

## <a name="msbuild-makerelative"></a>MSBuild の MakeRelative

MSBuild の `MakeRelative` プロパティ関数は、最初のパスに対する 2 番目のパスの相対パスを返します。 各パスはファイルまたはフォルダです。

このプロパティ関数には次の構文があります。

```
$([MSBuild]::MakeRelative($(FileOrFolderPath1), $(FileOrFolderPath2)))
```

次のコードはこの構文の例です。

```xml
<PropertyGroup>
    <Path1>c:\users\</Path1>
    <Path2>c:\users\username\</Path2>
</PropertyGroup>

<Target Name = "Go">
    <Message Text ="$([MSBuild]::MakeRelative($(Path1), $(Path2)))" />
    <Message Text ="$([MSBuild]::MakeRelative($(Path2), $(Path1)))" />
</Target>

<!--
Output:
   username\
   ..\
-->
```

## <a name="msbuild-valueordefault"></a>MSBuild の ValueOrDefault

MSBuild の `ValueOrDefault` プロパティ関数は、null または空でない限り、最初の引数を返します。 最初の引数が null または空の場合、関数は 2 番目の引数を返します。

この関数を使用する方法を次の例に示します。

```xml
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
        <Value1>$([MSBuild]::ValueOrDefault('$(UndefinedValue)', 'a'))</Value1>
        <Value2>$([MSBuild]::ValueOrDefault('b', '$(Value1)'))</Value2>
    </PropertyGroup>

    <Target Name="MyTarget">
        <Message Text="Value1 = $(Value1)" />
        <Message Text="Value2 = $(Value2)" />
    </Target>
</Project>

<!--
Output:
  Value1 = a
  Value2 = b
-->
```

<a name="TargetFramework"></a>

## <a name="msbuild-targetframework-and-targetplatform-functions"></a>MSBuild の TargetFramework と TargetPlatform の関数

MSBuild 16.7 以降には、[TargetFramework と TargetPlatform のプロパティ](msbuild-target-framework-and-target-platform.md)を処理するための関数がいくつか定義されています。

|関数シグネチャ|説明|
|------------------------|-----------------|
|GetTargetFrameworkIdentifier(string targetFramework)|TargetFramework から TargetFrameworkIdentifier を解析します。|
|GetTargetFrameworkVersion(string targetFramework)|TargetFramework から TargetFrameworkVersion を解析します。|
|GetTargetPlatformIdentifier(string targetFramework)|TargetFramework から TargetPlatformIdentifier を解析します。|
|GetTargetPlatformVersion(string targetFramework)|TargetFramework から TargetPlatformVersion を解析します。|
|IsTargetFrameworkCompatible(string targetFrameworkTarget, string targetFrameworkCandidate)|ターゲット フレームワーク候補がこのターゲット フレームワークと互換性がある場合は、'True' を返します。それ以外の場合は、False を返します。|

これらの関数を使用する方法を次の例に示します。 

```xml
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
        <Value1>$([MSBuild]::GetTargetFrameworkIdentifier('net5.0-windows7.0'))</Value1>
        <Value2>$([MSBuild]::GetTargetFrameworkVersion('net5.0-windows7.0'))</Value2>
        <Value3>$([MSBuild]::GetTargetPlatformIdentifier('net5.0-windows7.0'))</Value3>
        <Value4>$([MSBuild]::GetTargetPlatformVersion('net5.0-windows7.0'))</Value4>
        <Value5>$([MSBuild]::IsTargetFrameworkCompatible('net5.0-windows', 'net5.0'))</Value5>
    </PropertyGroup>

    <Target Name="MyTarget">
        <Message Text="Value1 = $(Value1)" />
        <Message Text="Value2 = $(Value2)" />
        <Message Text="Value3 = $(Value3)" />
        <Message Text="Value4 = $(Value4)" />
        <Message Text="Value5 = $(Value5)" />
    </Target>
</Project>
```

```output
Value1 = .NETCoreApp
Value2 = 5.0
Value3 = windows
Value4 = 7.0
Value5 = True
```

## <a name="msbuild-version-comparison-functions"></a>MSBuild のバージョン比較関数

MSBuild 16.5 以降には、バージョンを表す文字列を比較する関数がいくつか定義されています。

> [!Note]
> 条件に比較演算子を使用して[文字列を比較し、それを `System.Version` オブジェクトとして解析できます](msbuild-conditions.md#comparing-versions)が、比較によって予期しない結果になる可能性があります。 プロパティ関数を使用することをお勧めします。

|関数シグネチャ|説明|
|------------------------|-----------------|
|VersionEquals(string a, string b)|以下の規則に従ってバージョン `a` と `b` が等しい場合は `true` を返します。|
|VersionGreaterThan(string a, string b)|以下の規則に従ってバージョン `a` が `b` よりも大きい場合、`true` を返します。|
|VersionGreaterThanOrEquals(string a, string b)|以下の規則に従ってバージョン `a` が `b` よりも大きいか等しい場合、`true` を返します。|
|VersionLessThan(string a, string b)|以下の規則に従ってバージョン `a` が `b` よりも小さい場合、`true` を返します。|
|VersionLessThanOrEquals(string a, string b)|以下の規則に従ってバージョン `a` が `b` よりも小さいか等しい場合、`true` を返します。|
|VersionNotEquals(string a, string b)|以下の規則に従ってバージョン `a` と `b` が等しい場合は `false` を返します。|

これらのメソッドでは、以下の例外を除き、バージョンは <xref:System.Version?displayProperty=fullName> のように解析されます。

* 先頭の `v` または `V` は無視されるので、`$(TargetFrameworkVersion)` と比較できます。

* バージョン文字列の最初の '-' または '+' から末尾までのすべてが無視されます。 これにより、セマンティック バージョン (semver) を渡すことはできますが、その順序は semver と同じではありません。 その代わり、プレリリース指定子とビルド メタデータには並べ替えの重み付けがありません。 これは、たとえば、`>= x.y` の場合に機能を有効にして、`x.y.z-pre` の場合に起動する場合に役立ちます。

* 指定されていない部分は、ゼロ値の部分と同じです。 (`x == x.0 == x.0.0 == x.0.0.0`).

* 整数部には空白を使用できません。

* メジャー バージョンのみが有効です (`3` は `3.0.0.0` と同じです)。

* `+` は整数部の正符号としては使用できません (semver のメタデータとして扱われ、無視されます)。

> [!TIP]
> [TargetFramework プロパティ](msbuild-target-framework-and-target-platform.md)の比較には、一般的に、バージョンを抽出して比較するのではなく、[IsTargetFrameworkCompatible](#TargetFramework) を使用するようにします。 これにより、バージョンだけでなく `TargetFrameworkIdentifier` が異なる `TargetFramework`s を比較することができます。

## <a name="msbuild-condition-functions"></a>MSBuild 条件関数

関数 `Exists` と `HasTrailingSlash` は、プロパティ関数ではありません。 これらは、`Condition` 属性と一緒に使用することができます。 「[MSBuild の条件](msbuild-conditions.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [MSBuild プロパティ](../msbuild/msbuild-properties.md)

- [MSBuild の概要](../msbuild/msbuild.md)
