---
title: '&lt;dependency&gt; 要素 (ClickOnce 配置) | Microsoft Docs'
description: dependency 要素では、インストールするアプリケーションのバージョンと、アプリケーション マニフェストの場所を識別します。
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
- <dependency> element [ClickOnce deployment manifest]
ms.assetid: 9b4d2082-0347-4922-ac70-85f11b913039
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 172f3ea546565554c5f0701b81a88b9ca99b4100
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99881101"
---
# <a name="ltdependencygt-element-clickonce-deployment"></a>&lt;dependency&gt; 要素 (ClickOnce 配置)
インストールするアプリケーションのバージョンと、アプリケーション マニフェストの場所を識別します。

## <a name="syntax"></a>構文

```xml

      <dependency>
   <dependentAssembly
      preRequisite
      visible
      dependencyType
      codeBase
      size
   >
      <assemblyIdentity
         name
         version
         publicKeyToken
         processorArchitecture
         language
         type
      />
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

   </dependentAssembly>
</dependency>
```

## <a name="elements-and-attributes"></a>要素と属性
 `dependency` 要素は必須です。 属性はありません。 配置マニフェストには、複数の `dependency` 要素を含めることができます。

 `dependency` 要素は、通常、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーション内に含まれるアセンブリに対するメイン アプリケーションの依存関係を表します。 実際の Main.exe アプリケーションが DotNetAssembly.dll という名前のアセンブリを使用している場合は、そのアセンブリを、依存関係セクションの一覧に示す必要があります。 ただし依存関係を使用すると、特定のバージョンの共通言語ランタイム、グローバル アセンブリ キャッシュ (GAC) 内のアセンブリ、COM オブジェクトに対する依存関係など、その他の種類の依存関係も表現できます。 これは非介入の配置テクノロジであるため、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] では、これらの種類の依存関係のダウンロードとインストールを開始することはできませんが、指定された依存関係が 1 つ以上が存在しない場合は、確かにアプリケーションの実行が妨げられます。

## <a name="dependentassembly"></a>dependentAssembly
 必須。 この要素には、`assemblyIdentity` 要素が含まれています。 次の表に、`dependentAssembly` でサポートされている属性を示します。

| 属性 | 説明 |
|------------------| - |
| `preRequisite` | 省略可能。 このアセンブリが既に GAC 内に存在している必要があることを指定します。 有効な値は、`true`、`false` です。 `true` の場合、指定されたアセンブリが GAC 内に存在しないとアプリケーションの実行が失敗します。 |
| `visible` | 省略可能。 最上位レベルのアプリケーション ID を、その依存関係を含めて識別します。 アプリケーションのストレージとアクティブ化を管理するため、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] によって内部的に使用されます。 |
| `dependencyType` | 必須。 この依存関係とアプリケーションとの関係。 次の値を指定できます。<br /><br /> -   `install`. コンポーネントは、現在のアプリケーションからは独立したインストールを表します。<br />-   `preRequisite`. コンポーネントは、現在のアプリケーションに必要とされています。 |
| `codebase` | 省略可能。 アプリケーション マニフェストへの完全なパス。 |
| `size` | 省略可能。 アプリケーション マニフェストのサイズ (バイト単位)。 |

## <a name="assemblyidentity"></a>assemblyIdentity
 必須。 この要素は `dependentAssembly` 要素の子です。 `assemblyIdentity` の内容は、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーション マニフェストに記述されている内容と同じである必要があり ます。 次の表に、`assemblyIdentity` 要素の属性を示します。

|属性|説明|
|---------------|-----------------|
|`Name`|必須。 アプリケーションの名前を識別します。|
|`Version`|必須。 アプリケーションのバージョン番号を次の形式で指定します: `major.minor.build.revision`|
|`publicKeyToken`|必須。 アプリケーションまたはアセンブリが署名されたときに使われた公開キーの、SHA-1 ハッシュの最後の 8 バイトを表わす 16 文字の 16 進数文字列を指定します。 署名に使用する公開キーは、2048 ビット以上である必要があります。|
|`processorArchitecture`|必須。 マイクロプロセッサを指定します。 有効な値は、32 ビット Windows の場合は `x86`、64 ビット Windows の場合は `IA64` です。|
|`Language`|省略可能。 アセンブリの、2 つの部分から成る言語コードを識別します。 たとえば EN-US は、英語 (米国) を表します。 既定では、 `neutral`です。 この要素は `asmv2` 名前空間内にあります。|
|`type`|省略可能。 Windows のサイド バイ サイドのインストール テクノロジとの下位互換性用です。 使用できる値は `win32` のみです。|

## <a name="hash"></a>hash
 `hash` 要素は、`file` 要素の省略可能な子です。 `hash` 要素に属性はありません。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] では、アプリケーション内のすべてのファイルのアルゴリズム ハッシュをセキュリティ チェックとして使用し、配置後にどのファイルも変更されていないことを確認します。 `hash` 要素が含まれていない場合、このチェックは実行されません。 そのため、`hash` 要素を省略することはお勧めできません。

## <a name="dsigtransforms"></a>dsig:Transforms
 `dsig:Transforms` 要素は、`hash` 要素の必須の子です。 `dsig:Transforms` 要素に属性はありません。

## <a name="dsigtransform"></a>dsig:Transform
 `dsig:Transform` 要素は、`dsig:Transforms` 要素の必須の子です。 次の表に、`dsig:Transform` 要素の属性を示します。

| 属性 | 説明 |
|-------------| - |
| `Algorithm` | このファイルのダイジェストの計算に使用されるアルゴリズム。 現在 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] によって使用されている値は `urn:schemas-microsoft-com:HashTransforms.Identity` のみです。 |

## <a name="dsigdigestmethod"></a>dsig:DigestMethod
 `dsig:DigestMethod` 要素は、`hash` 要素の必須の子です。 次の表に、`dsig:DigestMethod` 要素の属性を示します。

| 属性 | 説明 |
|-------------| - |
| `Algorithm` | このファイルのダイジェストの計算に使用されるアルゴリズム。 現在 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] によって使用されている値は `http://www.w3.org/2000/09/xmldsig#sha1` のみです。 |

## <a name="dsigdigestvalue"></a>dsig:DigestValue
 `dsig:DigestValue` 要素は、`hash` 要素の必須の子です。 `dsig:DigestValue` 要素に属性はありません。 そのテキスト値は、指定されたファイルについて計算されたハッシュです。

## <a name="remarks"></a>解説
 配置マニフェストには、一般に、アプリケーション マニフェストの名前とバージョンを識別する `assemblyIdentity` 要素が 1 つあります。

## <a name="example-1"></a>例 1
 次のコード例は、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置マニフェストの `dependency` 要素を示しています。

```xml
<!-- Identify the assembly dependencies -->
<dependency>
  <dependentAssembly dependencyType="install" allowDelayedBinding="true" codebase="MyApplication.exe" size="16384">
    <assemblyIdentity name="MyApplication" version="0.0.0.0" cultural="neutral" processorArchitecture="msil" />
    <hash>
      <dsig:Transforms>
        <dsig:Transform Algorithm="urn:schemas-microsoft-com:HashTransforms.Identity" />
      </dsig:Transforms>
      <dsig:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
       <dsig:DigestValue>YzXYZJAvj9pgAG3y8jXUjC7AtHg=</dsig:DigestValue>
    </hash>
  </dependentAssembly>
</dependency>
```

## <a name="example-2"></a>例 2
 次のコード例では、既に GAC 内にインストールされているアセンブリに対する依存関係を指定しています。

```xml
<dependency>
  <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true">
    <assemblyIdentity name="GACAssembly" version="1.0.0.0" language="neutral" processorArchitecture="msil" />
  </dependentAssembly>
</dependency>
```

## <a name="example-3"></a>例 3
 次のコード例では、共通言語ランタイムの特定のバージョンに対する依存関係を指定しています。

```xml
<dependency>
  <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true">
    <assemblyIdentity name="Microsoft.Windows.CommonLanguageRuntime" version="2.0.50215.0" />
  </dependentAssembly>
</dependency>
```

## <a name="example-4"></a>例 4
 次のコード例では、オペレーティング システムの依存関係を指定しています。

```xml
<dependency>
   <dependentOS supportUrl="http://www.microsoft.com" description="Microsoft Windows Operating System">
      <osVersionInfo>
         <os majorVersion="4" minorVersion="10" />
      </osVersionInfo>
   </dependentOS>
</dependency>
```

## <a name="see-also"></a>関連項目
- [ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)
- [\<dependency> 要素](../deployment/dependency-element-clickonce-application.md)