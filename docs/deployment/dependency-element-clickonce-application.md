---
title: '&lt;dependency&gt; 要素 (ClickOnce アプリケーション) | Microsoft Docs'
description: dependency 要素では、アプリケーションに必要なプラットフォームまたはアセンブリの依存関係を識別します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#osVersionInfo
- urn:schemas-microsoft-com:asm.v2#os
- http://www.w3.org/2000/09/xmldsig#Transform
- urn:schemas-microsoft-com:asm.v2#dependency
- http://www.w3.org/2000/09/xmldsig#DigestValue
- urn:schemas-microsoft-com:asm.v2#assemblyIdentity
- http://www.w3.org/2000/09/xmldsig#DigestMethod
- http://www.w3.org/2000/09/xmldsig#Transforms
- urn:schemas-microsoft-com:asm.v2#hash
- urn:schemas-microsoft-com:asm.v2#dependentAssembly
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- manifests [ClickOnce], dependency element
- <dependency> element [ClickOnce application manifest]
ms.assetid: 09d6a1e0-60f8-4fbd-843b-8e49ee3115a3
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1e716c0e9ebe88a8007296f1dad870424a0def0b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99881114"
---
# <a name="ltdependencygt-element-clickonce-application"></a>&lt;dependency&gt; 要素 (ClickOnce アプリケーション)
アプリケーションに必要なプラットフォームまたはアセンブリの依存関係を識別します。

## <a name="syntax"></a>構文

```xml

      <dependency>
   <dependentOS
      supportURL
      description
   >
      <osVersionInfo>
         <os
            majorVersion
            minorVersion
            buildNumber
            servicePackMajor
            servicePackMinor
            productType
            suiteType
         />
      </osVersionInfo>
   </dependentOS>
   <dependentAssembly
      dependencyType
      allowDelayedBinding
      group
      codeBase
      size
   >
      <assemblyIdentity
         name
         version
         processorArchitecture
         language
      >
         <hash>
            <dsig:Transforms>
               <dsig:Transform
                  Algorithm
            />
            </dsig:Transforms>
            <dsig:DigestMethod />
            <dsig:DigestValue>
            </dsig:DigestValue>
    </hash>

      </assemblyIdentity>
   </dependentAssembly>
</dependency>
```

## <a name="elements-and-attributes"></a>要素と属性
 `dependency` 要素は必須です。 同じアプリケーション マニフェスト内に、`dependency` のインスタンスが複数存在する場合があります。

 `dependency` 要素には属性がなく、以下の子要素が含まれています。

### <a name="dependentos"></a>dependentOS
 省略可能。 `osVersionInfo` 要素を含みます。 `dependentOS` 要素と `dependentAssembly` 要素は相互に排他的です。1 つの `dependency` 要素に対して一方は存在する必要がありますが、両方が存在してはいけません。

 `dependentOS` では、以下の属性がサポートされています。

|属性|説明|
|---------------|-----------------|
|`supportUrl`|省略可能。 依存しているプラットフォームのサポート URL を指定します。 この URL は、必要なプラットフォームが見つかった場合にユーザーに表示されます。|
|`description`|省略可能。 `dependentOS` 要素によって記述されているオペレーティング システムを、人間が判読できる形式で記述します。|

### <a name="osversioninfo"></a>osVersionInfo
 必須。 この要素は `dependentOS` 要素の子であり、 `os` 要素を含んでいます。 この要素には属性はありません。

### <a name="os"></a>os
 必須。 この要素は `osVersionInfo` 要素の子です。 この要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`majorVersion`|必須。 OS のメジャー バージョン番号を指定します。|
|`minorVersion`|必須。 OS のマイナー バージョン番号を指定します。|
|`buildNumber`|必須。 OS のビルド番号を指定します。|
|`servicePackMajor`|必須。 OS の Service Pack メジャー番号を指定します。|
|`servicePackMinor`|省略可能。 OS の Service Pack マイナー番号を指定します。|
|`productType`|省略可能。 製品の種類の値を識別します。 有効な値は `server`、`workstation`、`domainController` です。 たとえば Windows 2000 Professional の場合、この属性値は `workstation` です。|
|`suiteType`|省略可能。 システムで使用可能な製品スイートや、システムの構成の種類を識別します。 有効な値は、`backoffice`、`blade`、`datacenter`、`enterprise`、`home`、`professional`、`smallbusiness`、`smallbusinessRestricted`、および `terminal` です。 たとえば Windows 2000 Professional の場合、この属性値は `professional` です。|

### <a name="dependentassembly"></a>dependentAssembly
 省略可能。 `assemblyIdentity` 要素を含みます。 `dependentOS` 要素と `dependentAssembly` 要素は相互に排他的です。1 つの `dependency` 要素に対して一方は存在する必要がありますが、両方が存在してはいけません。

 `dependentAssembly` には以下の属性があります。

| 属性 | 説明 |
|-----------------------| - |
| `dependencyType` | 必須。 依存関係の種類を指定します。 有効な値は、`preprequisite`、`install` です。 `install` アセンブリは、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションの一部としてインストールされています。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションをインストールする前に、`prerequisite` アセンブリがグローバル アセンブリ キャッシュ (GAC) 内に存在している必要があります。 |
| `allowDelayedBinding` | 必須。 実行時にプログラムによってアセンブリを読み込むことができるかどうかを指定します。 |
| `group` | 省略可能。 `dependencyType` 属性が `install` に設定されている場合、オンデマンドでのみインストールされるアセンブリの名前付きグループを指定します。 詳細については、「[チュートリアル:デザイナーを使用し、ClickOnce 配置 API で必要に応じてアセンブリをダウンロードする](../deployment/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer.md)」を参照してください。<br /><br /> `framework` に設定され、`dependencyType` 属性が `prerequisite` に設定されている場合、アセンブリを .NET Framework の一部として指定します。 .NET Framework 4 以降のバージョンにインストールする場合、このアセンブリのグローバル アセンブリ キャッシュ (GAC) はチェックされません。 |
| `codeBase` | `dependencyType` 属性が `install` に設定されているときには必須です。 依存アセンブリへのパス。 絶対パス、またはマニフェストのコード ベースを基準とした相対パスのいずれかです。 このパスは、アセンブリ マニフェストが有効であるためには、有効な URI である必要があります。 |
| `size` | `dependencyType` 属性が `install` に設定されているときには必須です。 依存アセンブリのサイズ (バイト単位)。 |

### <a name="assemblyidentity"></a>assemblyIdentity
 必須。 この要素は `dependentAssembly` 要素の子であり、以下の属性があります。

|属性|説明|
|---------------|-----------------|
|`name`|必須。 アプリケーションの名前を識別します。|
|`version`|必須。 アプリケーションのバージョン番号を次の形式で指定します: `major.minor.build.revision`|
|`publicKeyToken`|省略可能。 アプリケーションまたはアセンブリが署名されたときに使われた公開キーの、`SHA-1` ハッシュ値の最後の 8 バイトを表わす 16 文字の 16 進数文字列を指定します。 カタログの署名に使用される公開キーは、2048 ビット以上である必要があります。|
|`processorArchitecture`|省略可能。 プロセッサを指定します。 有効な値は、32 ビット Windows の場合は `x86`、64 ビット Windows の場合は `I64` です。|
|`language`|省略可能。 アセンブリの、2 つの部分から成る言語コード (EN-US など) を識別します。|

### <a name="hash"></a>hash
 `hash` 要素は、`assemblyIdentity` 要素の省略可能な子です。 `hash` 要素に属性はありません。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] では、アプリケーション内のすべてのファイルのアルゴリズム ハッシュをセキュリティ チェックとして使用し、配置後にどのファイルも変更されていないことを確認します。 `hash` 要素が含まれていない場合、このチェックは実行されません。 そのため、`hash` 要素を省略することはお勧めできません。

### <a name="dsigtransforms"></a>dsig:Transforms
 `dsig:Transforms` 要素は、`hash` 要素の必須の子です。 `dsig:Transforms` 要素に属性はありません。

### <a name="dsigtransform"></a>dsig:Transform
 `dsig:Transform` 要素は、`dsig:Transforms` 要素の必須の子です。 `dsig:Transform` 要素には、次の属性があります。

| 属性 | 説明 |
|-------------| - |
| `Algorithm` | このファイルのダイジェストの計算に使用されるアルゴリズム。 現在 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] によって使用されている値は `urn:schemas-microsoft-com:HashTransforms.Identity` のみです。 |

### <a name="dsigdigestmethod"></a>dsig:DigestMethod
 `dsig:DigestMethod` 要素は、`hash` 要素の必須の子です。 `dsig:DigestMethod` 要素には、次の属性があります。

| 属性 | 説明 |
|-------------| - |
| `Algorithm` | このファイルのダイジェストの計算に使用されるアルゴリズム。 現在 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] によって使用されている値は `http://www.w3.org/2000/09/xmldsig#sha1` のみです。 |

### <a name="dsigdigestvalue"></a>dsig:DigestValue
 `dsig:DigestValue` 要素は、`hash` 要素の必須の子です。 `dsig:DigestValue` 要素に属性はありません。 そのテキスト値は、指定されたファイルについて計算されたハッシュです。

## <a name="remarks"></a>解説
 アプリケーションによって使用されるすべてのアセンブリに、対応する `dependency` 要素が必要です。 依存アセンブリには、プラットフォーム アセンブリとしてグローバル アセンブリ キャッシュにプレインストールされている必要があるアセンブリは含まれません。

## <a name="example"></a>例
 次のコード例は、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーション マニフェスト内の `dependency` 要素を示しています。 このコード例は、「[ClickOnce アプリケーション マニフェスト](../deployment/clickonce-application-manifest.md)」トピックに記載されている、より大きな例の一部です。

```xml
<dependency>
  <dependentOS>
    <osVersionInfo>
      <os
        majorVersion="4"
        minorVersion="10"
        buildNumber="0"
        servicePackMajor="0" />
    </osVersionInfo>
  </dependentOS>
</dependency>
<dependency>
  <dependentAssembly
    dependencyType="preRequisite"
    allowDelayedBinding="true">
    <assemblyIdentity
      name="Microsoft.Windows.CommonLanguageRuntime"
      version="4.0.20506.0" />
  </dependentAssembly>
</dependency>

<dependency>
  <dependentAssembly
    dependencyType="install"
    allowDelayedBinding="true"
    codebase="MyApplication.exe"
    size="4096">
    <assemblyIdentity
      name="MyApplication"
      version="1.0.0.0"
      language="neutral"
      processorArchitecture="x86" />
    <hash>
      <dsig:Transforms>
        <dsig:Transform Algorithm="urn:schemas-microsoft-com:HashTransforms.Identity" />
      </dsig:Transforms>
      <dsig:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
      <dsig:DigestValue>DpTW7RzS9IeT/RBSLj54vfTEzNg=</dsig:DigestValue>
    </hash>
  </dependentAssembly>
</dependency>
```

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーション マニフェスト](../deployment/clickonce-application-manifest.md)
- [\<dependency> 要素](../deployment/dependency-element-clickonce-deployment.md)