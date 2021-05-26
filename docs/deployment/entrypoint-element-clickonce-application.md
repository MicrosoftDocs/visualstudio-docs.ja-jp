---
title: '&lt;entryPoint&gt; 要素 (ClickOnce アプリケーション) | Microsoft Docs'
description: entryPoint 要素では、この ClickOnce アプリケーションがクライアント コンピューターで実行されるときに実行する必要があるアセンブリを指定します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#commandLine
- urn:schemas-microsoft-com:asm.v2#entryPoint
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <entryPoint> element [ClickOnce application manifest]
- manifests [ClickOnce], entryPoint element
ms.assetid: 10ad3083-10c1-4189-a870-9bba2eab244f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d5c35d94001ae1e883e2bd76650f248d7e0364d2
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99893894"
---
# <a name="ltentrypointgt-element-clickonce-application"></a>&lt;entryPoint&gt; 要素 (ClickOnce アプリケーション)
この [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションがクライアント コンピューターで実行されるときに実行する必要があるアセンブリを指定します。

## <a name="syntax"></a>構文

```xml
<entryPoint
   name
>
   <assemblyIdentity
      name
      version
      processorArchitecture
      language
   />
   <commandLine
      file
      parameters
   />
   <customHostRequired />
   <customUX />
</entryPoint>
```

## <a name="elements-and-attributes"></a>要素と属性
 `entryPoint` 要素は必須です。この要素は `urn:schemas-microsoft-com:asm.v2` 名前空間にあります。 アプリケーション マニフェストで定義できる `entryPoint` 要素は 1 つだけです。

 `entryPoint` 要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`name`|省略可能。 この値は .NET Framework では使用されません。|

 `entryPoint` には、次の要素があります。

## <a name="assemblyidentity"></a>assemblyIdentity
 必須。 `assemblyIdentity` とその属性の役割は、[\<assemblyIdentity> 要素](../deployment/assemblyidentity-element-clickonce-application.md)で定義されます。

 この要素の `processorArchitecture` 属性と、アプリケーション マニフェスト内の他の場所にある `assemblyIdentity` で定義されている `processorArchitecture` 属性が一致している必要があります。

## <a name="commandline"></a>commandLine
 必須。 `entryPoint` 要素の子である必要があります。 子要素はなく、次の属性があります。

| 属性 | 説明 |
|--------------| - |
| `file` | 必須。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションのスタートアップ アセンブリへのローカル参照。 この値には、パス区切り文字のスラッシュ (/) または円記号 (\\) を含めることはできません。 |
| `parameters` | 必須。 エントリ ポイントで実行するアクションを記述します。 有効な値は `run` だけです。空白の文字列を指定すると、`run` と見なされます。 |

## <a name="customhostrequired"></a>customHostRequired
 省略可能。 含まれている場合、カスタム ホスト内に配置され、スタンドアロンのアプリケーションではないコンポーネントがこの配置に含まれていることを示します。

 この要素が存在する場合、`assemblyIdentity` 要素と `commandLine` 要素が存在することはできません。 存在すると、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] でインストール中に検証エラーが発生します。

 この要素には属性も子もありません。

## <a name="customux"></a>customUX
 省略可能。 アプリケーションがカスタム インストーラーによってインストールおよび管理され、[スタート] メニュー エントリ、ショートカット、[プログラムの追加と削除] エントリは作成されないことを指定します。

```xml
<customUX xmlns="urn:schemas-microsoft-com:clickonce.v1" />
```

 customUX 要素を含むアプリケーションでは、<xref:System.Deployment.Application.InPlaceHostingManager> クラスを使用してインストール操作を実行するカスタム インストーラーを提供する必要があります。 この要素を含むアプリケーションは、マニフェストまたは setup.exe 前提条件ブートストラップをダブルクリックしてインストールすることはできません。 カスタム インストーラーでは、[スタート] メニュー エントリ、ショートカット、[プログラムの追加と削除] エントリを作成できます。 カスタム インストーラーでは、[プログラムの追加と削除] エントリを作成しない場合、<xref:System.Deployment.Application.GetManifestCompletedEventArgs.SubscriptionIdentity%2A> プロパティで指定されたサブスクリプション識別子を保存し、ユーザーが <xref:System.Deployment.Application.InPlaceHostingManager.UninstallCustomUXApplication%2A> メソッドを呼び出して後でアプリケーションをアンインストールできるようにする必要があります。 詳細については、「[チュートリアル: ClickOnce アプリケーションのカスタム インストーラーの作成](../deployment/walkthrough-creating-a-custom-installer-for-a-clickonce-application.md)」を参照してください。

## <a name="remarks"></a>解説
 この要素では、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションのアセンブリとエントリ ポイントを指定します。

 `commandLine` を使用して、実行時にパラメーターをアプリケーションに渡すことはできません。 アプリケーションの <xref:System.AppDomain> から、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置のクエリ文字列パラメーターにアクセスできます。 詳細については、「[方法: オンライン ClickOnce アプリケーションでクエリ文字列の情報を取得する](../deployment/how-to-retrieve-query-string-information-in-an-online-clickonce-application.md)」を参照してください。

## <a name="example"></a>例
 次のコード例は、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションのアプリケーション マニフェストの `entryPoint` 要素を示しています。 このコード例は、「[ClickOnce アプリケーション マニフェスト](../deployment/clickonce-application-manifest.md)」に記載されている、より大きな例の一部です。

```xml
<!-- Identify the main code entrypoint. -->
<!-- This code runs the main method in an executable assembly. -->
  <entryPoint>
    <assemblyIdentity
      name="MyApplication"
      version="1.0.0.0"
      language="neutral"
      processorArchitecture="x86" />
    <commandLine file="MyApplication.exe" parameters="" />
  </entryPoint>
```

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーション マニフェスト](../deployment/clickonce-application-manifest.md)
