---
title: MSBuild プロジェクトの共通項目 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, common project items
ms.assetid: 1eba3721-cc12-4b80-9987-84923ede5e2e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 394a986963ad1d1690535aecbb3355bdbe382516
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56610347"
---
# <a name="common-msbuild-project-items"></a>MSBuild プロジェクトの共通項目
[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] では、項目は 1 つ以上のファイルに対応する名前付きの参照です。 項目には、ファイル名、パス、バージョン番号などのメタデータが含まれます。 項目には、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] のすべてのプロジェクトの種類に共通のものがあります。 これらの項目は、*Microsoft.Build.CommonTypes.xsd* ファイルで定義されています。

## <a name="common-items"></a>共通の項目
 次に、プロジェクトの共通項目の一覧を示します。

### <a name="reference"></a>関連項目
 プロジェクト内のアセンブリ (マネージド) 参照を表します。

|項目メタデータの名前|説明|
|---------------|-----------------|
|HintPath|省略可能な文字列。 アセンブリの相対パスまたは絶対パスを指定します。|
|name|省略可能な文字列。 アセンブリの表示名を指定します (たとえば、"System.Windows.Forms")。|
|FusionName|省略可能な文字列。 項目の簡易または厳密な fusion 名を指定します。<br /><br /> この属性が存在する場合、fusion 名を得るためにアセンブリ ファイルを開く必要がないため、時間を節約できます。|
|SpecificVersion|省略可能なブール値。 fusion 名の特定のバージョンを参照する必要があるかどうかを指定します。|
|Aliases|省略可能な文字列。 参照の任意のエイリアスです。|
|Private|省略可能なブール値。 参照を出力フォルダーにコピーする必要があるかどうかを指定します。 この属性は、Visual Studio IDE に存在する参照の **[ローカルにコピー]** プロパティに一致します。|

### <a name="comreference"></a>COMReference
 プロジェクト内の COM (アンマネージ) コンポーネント参照を表します。

|項目メタデータの名前|説明|
|---------------|-----------------|
|name|省略可能な文字列。 コンポーネントの表示名を指定します。|
|GUID|省略可能な文字列。 コンポーネントの GUID を {12345678-1234-1234-1234-1234567891234} の形式で指定します。|
|VersionMajor|省略可能な文字列。 コンポーネントのメジャー バージョン番号を指定します。 たとえば、完全なバージョン番号が "5.46" である場合、"5" を指定します。|
|VersionMinor|省略可能な文字列。 コンポーネントのマイナー バージョン番号を指定します。 たとえば、完全なバージョン番号が "5.46" である場合、"46" を指定します。|
|LCID|省略可能な文字列。 コンポーネントの LocaleID です。|
|WrapperTool|省略可能な文字列。 コンポーネントで使用されるラッパー ツールの名前を指定します (たとえば、"tlbimp")。|
|Isolated|省略可能なブール値。 コンポーネントが Reg-Free コンポーネントであるかどうかを指定します。|

### <a name="comfilereference"></a>COMFileReference
 ResolvedComreference ターゲットに送られるタイプ ライブラリの一覧を表します。

|項目メタデータの名前|説明|
|---------------|-----------------|
|WrapperTool|省略可能な文字列。 コンポーネントで使用されるラッパー ツールの名前を指定します (たとえば、"tlbimp")。|

### <a name="nativereference"></a>NativeReference
 ネイティブ マニフェスト ファイル、またはこのようなファイルへの参照を表します。

|項目メタデータの名前|説明|
|---------------|-----------------|
|name|必須の文字列。 マニフェスト ファイルの基本名を指定します。|
|HintPath|必須の文字列。 マニフェスト ファイルの相対パスを指定します。|

### <a name="projectreference"></a>ProjectReference
 別のプロジェクトへの参照を表します。

|項目メタデータの名前|説明|
|---------------|-----------------|
|name|省略可能な文字列。 参照の表示名を指定します。|
|Project|省略可能な文字列。 参照の GUID を {12345678-1234-1234-1234-1234567891234} の形式で指定します。|
|Package|省略可能な文字列。 参照されるプロジェクト ファイルのパスを指定します。|
|ReferenceOutputAssembly|省略可能なブール値。 `false` を設定した場合、このプロジェクトの [Reference](#Reference) として参照されたプロジェクトの出力は含まれませんが、このプロジェクトをビルドする前の他のプロジェクトのビルドは保証されます。 既定値は `true` です。|

### <a name="compile"></a>Compile
 コンパイラのソース ファイルを表します。


| 項目メタデータの名前 | 説明 |
|-----------------------| - |
| DependentUpon | 省略可能な文字列。 正しくコンパイルする必要があるファイルを指定します。 |
| AutoGen | 省略可能なブール値。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE) で使用するプロジェクト用にファイルを生成するかどうかを指定します。 |
| Link | 省略可能な文字列。 プロジェクト ファイルの影響が及ばない物理的な場所にファイルが配置されるときに表示される表記パスです。 |
| Visible | 省略可能なブール値。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] の**ソリューション エクスプローラー**にファイルを表示するかどうかを指定します。 |
| CopyToOutputDirectory | 省略可能な文字列。 出力ディレクトリにファイルをコピーするかどうかを判断します。 値は次のとおりです。<br /><br /> 1.Never<br />2.Always<br />3.PreserveNewest |

### <a name="embeddedresource"></a>EmbeddedResource
 生成されるアセンブリに埋め込まれるリソースを表します。


| 項目メタデータの名前 | 説明 |
|-----------------------| - |
| DependentUpon | 省略可能な文字列。 正しくコンパイルするために、このファイルが依存するファイルを指定します |
| Generator | 必須の文字列。 この項目に対して実行される任意のファイル ジェネレーターの名前です。 |
| LastGenOutput | 必須の文字列。 この項目に対して実行された任意のファイル ジェネレーターによって作成されたファイルの名前です。 |
| CustomToolNamespace | 必須の文字列。 名前空間を指定します。指定した名前空間で、この項目に対して実行する任意のファイル ジェネレーターによってコードが作成されます。 |
| Link | 省略可能な文字列。 プロジェクトの影響が及ばない物理的な場所にファイルが配置されるときに表示される表記パスです。 |
| Visible | 省略可能なブール値。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] の**ソリューション エクスプローラー**にファイルを表示するかどうかを指定します。 |
| CopyToOutputDirectory | 省略可能な文字列。 出力ディレクトリにファイルをコピーするかどうかを判断します。 値は次のとおりです。<br /><br /> 1.Never<br />2.Always<br />3.PreserveNewest |
| LogicalName | 必須の文字列。 埋め込まれるリソースの論理名です。 |

### <a name="content"></a>Content
 プロジェクトにコンパイルはされないものの、プロジェクトと共に埋め込まれるか発行されることのあるファイルを表します。


| 項目メタデータの名前 | 説明 |
|-----------------------| - |
| DependentUpon | 省略可能な文字列。 正しくコンパイルする必要があるファイルを指定します。 |
| Generator | 必須の文字列。 この項目に対して実行する任意のファイル ジェネレーターの名前です。 |
| LastGenOutput | 必須の文字列。 この項目に対して実行された任意のファイル ジェネレーターによって作成されたファイルの名前です。 |
| CustomToolNamespace | 必須の文字列。 名前空間を指定します。指定した名前空間で、この項目に対して実行する任意のファイル ジェネレーターによってコードが作成されます。 |
| Link | 省略可能な文字列。 プロジェクトの影響が及ばない物理的な場所にファイルが配置されるときに表示される表記パスです。 |
| PublishState | 必須の文字列。 コンテンツの発行状態を示すもので、以下のいずれかの値を取ります。<br /><br /> -   Default<br />-   Included<br />-   Excluded<br />-   DataFile<br />-   Prerequisite |
| IsAssembly | 省略可能なブール値。 ファイルがアセンブリであるかどうかを指定します。 |
| Visible | 省略可能なブール値。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] の**ソリューション エクスプローラー**にファイルを表示するかどうかを指定します。 |
| CopyToOutputDirectory | 省略可能な文字列。 出力ディレクトリにファイルをコピーするかどうかを判断します。 値は次のとおりです。<br /><br /> 1.Never<br />2.Always<br />3.PreserveNewest |

### <a name="none"></a>なし
 ビルド プロセスでは使用しないことが推奨されるファイルを表します。


| 項目メタデータの名前 | 説明 |
|-----------------------| - |
| DependentUpon | 省略可能な文字列。 正しくコンパイルする必要があるファイルを指定します。 |
| Generator | 必須の文字列。 この項目に対して実行される任意のファイル ジェネレーターの名前です。 |
| LastGenOutput | 必須の文字列。 この項目に対して実行された任意のファイル ジェネレーターによって作成されたファイルの名前です。 |
| CustomToolNamespace | 必須の文字列。 名前空間を指定します。指定した名前空間で、この項目に対して実行する任意のファイル ジェネレーターによってコードが作成されます。 |
| Link | 省略可能な文字列。 プロジェクトの影響が及ばない物理的な場所にファイルが配置されるときに表示される表記パスです。 |
| Visible | 省略可能なブール値。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] の**ソリューション エクスプローラー**にファイルを表示するかどうかを指定します。 |
| CopyToOutputDirectory | 省略可能な文字列。 出力ディレクトリにファイルをコピーするかどうかを判断します。 値は次のとおりです。<br /><br /> 1.Never<br />2.Always<br />3.PreserveNewest |

### <a name="baseapplicationmanifest"></a>BaseApplicationManifest
 ビルドの基本アプリケーション マニフェストを表し、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置セキュリティ情報を含みます。

### <a name="codeanalysisimport"></a>CodeAnalysisImport
 インポートする FxCop プロジェクトを表します。

### <a name="import"></a>インポート
 アセンブリを表します。このアセンブリの名前空間が、[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] コンパイラによってインポートされます。

## <a name="see-also"></a>関連項目
- [MSBuild プロジェクトの共通プロパティ](../msbuild/common-msbuild-project-properties.md)
