---
title: '&lt;deployment&gt; 要素 (ClickOnce 配置) | Microsoft Docs'
description: deployment 要素では、更新プログラムの配置とシステムへの公開に使用される属性を指定します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#subscription
- urn:schemas-microsoft-com:asm.v2#beforeApplicationStartup
- urn:schemas-microsoft-com:asm.v2#deploymentProvider
- urn:schemas-microsoft-com:asm.v2#update
- urn:schemas-microsoft-com:asm.v2#deployment
- urn:schemas-microsoft-com:asm.v2#expiration
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <deployment> element [ClickOnce deployment manifest]
ms.assetid: 4fafa9c2-97a0-4cea-b8fd-9746dca33af4
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 369d48c76ed82825021622af35141ef12ff42c76
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99893920"
---
# <a name="ltdeploymentgt-element-clickonce-deployment"></a>&lt;deployment&gt; 要素 (ClickOnce 配置)
更新プログラムの配置とシステムへの公開に使用される属性を指定します。

## <a name="syntax"></a>構文

```xml

      <deployment
   install
   minimumRequiredVersion
   mapFileExtensions
   disallowUrlActivation
   trustUrlParameters
>
   <subscription>
         <update>
            <beforeApplicationStartup/>
            <expiration
               maximumAge
               unit
            />
         </update>
   </subscription>
   <deploymentProvider
      codebase
   />
</deployment>
```

## <a name="elements-and-attributes"></a>要素と属性
 `deployment` 要素は必須です。この要素は `urn:schemas-microsoft-com:asm.v2` 名前空間にあります。 要素には、次の属性があります。

| 属性 | 説明 |
|--------------------------| - |
| `install` | 必須。 Windows の **[スタート]** メニューとコントロール パネルの **[プログラムの追加と削除]** アプリケーションに表示される内容をこのアプリケーションで定義するかどうかを指定します。 有効な値は、`true`、`false` です。 `false` の場合、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] では、ネットワークからこのアプリケーションの最新バージョンが常に実行され、`subscription` 要素は認識されません。 |
| `minimumRequiredVersion` | 省略可能。 クライアントで実行できる、このアプリケーションの最小バージョンを指定します。 アプリケーションのバージョン番号が配置マニフェストで指定されたバージョン番号よりも小さい場合、アプリケーションは実行されません。 バージョン番号は、`N.N.N.N` の形式で指定する必要があります。`N` は符号なし整数です。 `install` 属性が `false` の場合は、`minimumRequiredVersion` を設定しないでください。 |
| `mapFileExtensions` | 任意。 既定値は `false` です。 `true` の場合、配置内のすべてのファイルに .deploy 拡張子が必要です。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] では、これらのファイルを Web サーバーからダウンロードするとすぐに、この拡張子を削除します。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] を使用してアプリケーションを発行すると、この拡張子がすべてのファイルに自動的に追加されます。 このパラメーターを使用すると、.exe などの "安全ではない" 拡張子で終わるファイルの転送をブロックする Web サーバーから、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置内のすべてのファイルをダウンロードできます。 |
| `disallowUrlActivation` | 任意。 既定値は `false` です。 `true` の場合、URL をクリックしたり、Internet Explorer に URL を入力したりすることによって、インストールされたアプリケーションを起動することはできなくなります。 `install` 属性が存在しない場合、この属性は無視されます。 |
| `trustURLParameters` | 任意。 既定値は `false` です。 `true` の場合、コマンドライン引数がコマンドライン アプリケーションに渡されるのとほぼ同様に、アプリケーションに渡されるクエリ文字列パラメーターを URL に含めることができます。 詳細については、「[方法: オンライン ClickOnce アプリケーションでクエリ文字列の情報を取得する](../deployment/how-to-retrieve-query-string-information-in-an-online-clickonce-application.md)」を参照してください。<br /><br /> `disallowUrlActivation` 属性が `true` の場合は、`trustUrlParameters` をマニフェストから除外するか、明示的に `false` に設定する必要があります。 |

 `deployment` 要素には、次の子要素も含まれます。

## <a name="subscription"></a>subscription
 省略可能。 `update` 要素を含みます。 `subscription` 要素に属性はありません。 `subscription` 要素が存在しない場合、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションが更新プログラムをスキャンすることはありません。 `deployment` 要素の `install` 属性が `false` の場合、ネットワークから起動される [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションで常に最新バージョンが使用されるため、`subscription` 要素は無視されます。

## <a name="update"></a>update
 必須。 この要素は `subscription` 要素の子であり、`beforeApplicationStartup` または `expiration` 要素が含まれます。 `beforeApplicationStartup` と `expiration` の両方を同じ配置マニフェストで指定することはできません。

 `update` 要素に属性はありません。

## <a name="beforeapplicationstartup"></a>beforeApplicationStartup
 省略可能。 この要素は `update` 要素の子であり、属性はありません。 `beforeApplicationStartup` 要素が存在する場合、クライアントがオンラインの場合に [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] によって更新プログラムが確認されるときに、アプリケーションがブロックされます。 この要素が存在しない場合、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] では、`expiration` 要素に指定された値に基づいて、最初に更新プログラムがスキャンされます。 `beforeApplicationStartup` と `expiration` の両方を同じ配置マニフェストで指定することはできません。

## <a name="expiration"></a>expiration
 省略可能。 この要素は `update` 要素の子であり、子はありません。 `beforeApplicationStartup` と `expiration` の両方を同じ配置マニフェストで指定することはできません。 更新チェックが行われ、更新されたバージョンが検出されると、既存のバージョンの実行中に新しいバージョンがキャッシュされます。 新しいバージョンは、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションの次回の起動時にインストールされます。

 `expiration` 要素では、次の属性がサポートされています。

|属性|説明|
|---------------|-----------------|
|`maximumAge`|必須。 アプリケーションで更新チェックを実行するまでに、現在の更新プログラムがどのくらい古くなっている必要があるかを指定します。 時間の単位は、`unit` 属性で指定されます。|
|`unit`|必須。 `maximumAge` の時間の単位を指定します。 有効な単位は、`hours`、`days`、`weeks` です。|

## <a name="deploymentprovider"></a>deploymentProvider
 .NET Framework 2.0 では、配置マニフェストに `subscription` セクションが含まれている場合、この要素は必須です。 .NET Framework 3.5 以降では、この要素は省略可能であり、配置マニフェストが検出されたサーバーとファイル パスに既定で設定されます。

 この要素は `deployment` 要素の子であり、以下の属性があります。

| 属性 | 説明 |
|------------| - |
| `codebase` | 必須。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションの更新に使用される配置マニフェストの場所を Uniform Resource Identifier (URI) で指定します。 この要素により、CD ベースのインストールの更新プログラムの場所を転送することもできます。 有効な URI である必要があります。 |

## <a name="remarks"></a>解説
 起動時に更新プログラムをスキャンするか、起動後に更新プログラムをスキャンするか、または更新プログラムを確認しないように [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを構成できます。 起動時に更新プログラムをスキャンするには、`beforeApplicationStartup` 要素が `update` 要素の下に存在することを確認します。 起動後に更新プログラムをスキャンするには、`expiration` 要素が `update` 要素の下に存在し、更新間隔が指定されていることを確認します。

 更新プログラムの確認を無効にするには、`subscription` 要素を削除します。 更新プログラムをスキャンしないように配置マニフェストで指定した場合でも、<xref:System.Deployment.Application.ApplicationDeployment.CheckForUpdate%2A> メソッドを使用して更新プログラムを手動で確認できます。

 deploymentProvider と更新プログラムの関連性の詳細については、「[ClickOnce の更新方法の選択](../deployment/choosing-a-clickonce-update-strategy.md)」を参照してください。

## <a name="examples"></a>例
 次のコード例は、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置マニフェストの `deployment` 要素を示しています。 この例では、`deploymentProvider` 要素を使用して、優先される更新プログラムの場所を示しています。

```xml
<deployment install="true" minimumRequiredVersion="2.0.0.0" mapFileExtension="true" trustUrlParameters="true">
    <subscription>
      <update>
        <expiration maximumAge="6" unit="hours" />
      </update>
    </subscription>
    <deploymentProvider codebase="http://www.adatum.com/MyApplication.application" />
  </deployment>
```

## <a name="see-also"></a>関連項目
- [ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)