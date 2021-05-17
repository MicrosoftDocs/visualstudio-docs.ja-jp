---
title: '&lt;file&gt; 要素 (ClickOnce アプリケーション) | Microsoft Docs'
description: file 要素では、アプリケーションによってダウンロードされて使用される、アセンブリ以外のすべてのファイルを識別します。 file 要素は省略可能です。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://www.w3.org/2000/09/xmldsig#Transform
- urn:schemas-microsoft-com:asm.v2#file
- http://www.w3.org/2000/09/xmldsig#DigestValue
- http://www.w3.org/2000/09/xmldsig#DigestMethod
- http://www.w3.org/2000/09/xmldsig#Transforms
- urn:schemas-microsoft-com:asm.v2#hash
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <file> element [ClickOnce application manifest]
- manifests [ClickOnce], file element
ms.assetid: 56e3490c-eed5-4841-b1bf-eefe778b6ac9
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 8ad19de19176b7c8ee1d2c2872126a19abb93b67
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99895090"
---
# <a name="ltfilegt-element-clickonce-application"></a>&lt;file&gt; 要素 (ClickOnce アプリケーション)
アプリケーションによってダウンロードされて使用される、アセンブリ以外のすべてのファイルを識別します。

## <a name="syntax"></a>構文

```xml
<file
    name
    size
    group
    optional
    writeableType
>
    <typelib
        tlbid
        version
        helpdir
        resourceid
        flags
    />
    <comClass
        clsid
        description
        threadingModel
        tlbid
        progid
        miscStatus
        miscStatusIcon
        miscStatusContent
        miscStatusDocPrint
        miscStatusThumbnail
    />
    <comInterfaceExternalProxyStub
        iid
        baseInterface
        numMethods
        name
        tlbid
        proxyStubClass32
    />
    <comInterfaceProxyStub
        iid
        baseInterface
        numMethods
        name
        tlbid
        proxyStubClass32
    />
    <windowClass
        versioned
    />
</file>
```

## <a name="elements-and-attributes"></a>要素と属性
 `file` 要素は省略可能です。 要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`name`|必須。 ファイルの名前を識別します。|
|`size`|必須。 ファイルのサイズを指定します (バイト単位)。|
|`group`|`optional` 属性が指定されていないか、`false` に設定されている場合は省略可能で、`optional` が `true` である場合は必須です。 ファイルが所属するグループの名前。 名前には、開発者が選択した任意の Unicode 文字列値を使用できます。また、名前は、<xref:System.Deployment.Application.ApplicationDeployment> クラスを使用してオンデマンドでファイルをダウンロードするために使用されます。|
|`optional`|省略可能。 アプリケーションの初回実行時にこのファイルをダウンロードする必要があるかどうかや、アプリケーションがオンデマンドで要求するまでそのファイルをサーバーにのみ配置する必要があるかどうかを指定します。 `false` または未定義の場合、アプリケーションが最初に実行またはインストールされるときに、ファイルがダウンロードされます。 `true` の場合、アプリケーション マニフェストを有効にするためには `group` を指定する必要があります。 値が `applicationData` である `writeableType` が指定されている場合は、`optional` を true にすることはできません。|
|`writeableType`|省略可能。 このファイルがデータ ファイルであることを指定します。 現在、有効値は `applicationData` のみです。|

## <a name="typelib"></a>typelib
 `typelib` 要素は、file 要素の省略可能な子です。 この要素では、COM コンポーネントに属するタイプ ライブラリについて記述します。 要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`tlbid`|必須。 タイプ ライブラリに割り当てられている GUID。|
|`version`|必須。 タイプ ライブラリのバージョン番号。|
|`helpdir`|必須。 コンポーネントのヘルプ ファイルが含まれるディレクトリ。 長さがゼロの場合があります。|
|`resourceid`|省略可能。 ロケール識別子 (LCID) の 16 進文字列表現。 これは、0x プレフィックスがなく、先頭のゼロがない、1 ～ 4 桁の 16 進数です。 LCID には、中立の副言語識別子が含まれている場合があります。|
|`flags`|省略可能。 このタイプ ライブラリのタイプ ライブラリ フラグの文字列表現。 具体的には、これは "RESTRICTED"、"CONTROL"、"HIDDEN"、"HASDISKIMAGE" のいずれかである必要があります。|

## <a name="comclass"></a>comClass
 `comClass` 要素は、`file` 要素の省略可能な子ですが、登録を必要としない COM を使用して配置する予定の COM コンポーネントが [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションに含まれている場合は必須です。 要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`clsid`|必須。 GUID として表現された COM コンポーネントのクラス ID。|
|`description`|省略可能。 クラス名。|
|`threadingModel`|省略可能。 インプロセス COM クラスによって使用されるスレッド モデル。 このプロパティが null の場合、スレッド モデルは使用されません。 コンポーネントはクライアントのメイン スレッドで作成され、他のスレッドからの呼び出しはこのスレッドにマーシャリングされます。 次の一覧に有効な値を示します。<br /><br /> `Apartment`、`Free`、`Both`、`Neutral`。|
|`tlbid`|省略可能。 COM コンポーネントのタイプ ライブラリの GUID。|
|`progid`|省略可能。 COM コンポーネントに関連付けられている、バージョン依存のプログラム識別子。 `ProgID` の形式は `<vendor>.<component>.<version>` です。|
|`miscStatus`|省略可能。 `MiscStatus` レジストリ キーによって提供される情報を、アセンブリ マニフェスト内に複製します。 `miscStatusIcon`、`miscStatusContent`、`miscStatusDocprint`、`miscStatusThumbnail` 属性の値が見つからない場合、不足している属性には、`miscStatus` に示されている対応する既定値が使用されます。 値として、次の表に示す属性値のコンマ区切りの一覧を指定できます。 COM クラスが、`MiscStatus` レジストリ キー値を必要とする OCX クラスである場合は、この属性を使用できます。|
|`miscStatusIcon`|省略可能。 DVASPECT_ICON によって提供される情報を、アセンブリ マニフェスト内に複製します。 これにより、オブジェクトのアイコンを提供できます。 値として、次の表に示す属性値のコンマ区切りの一覧を指定できます。 COM クラスが、`Miscstatus` レジストリ キー値を必要とする OCX クラスである場合は、この属性を使用できます。|
|`miscStatusContent`|省略可能。 DVASPECT_CONTENT によって提供される情報を、アセンブリ マニフェスト内に複製します。 これにより、画面またはプリンターに表示できる複合ドキュメントを提供できます。 値として、次の表に示す属性値のコンマ区切りの一覧を指定できます。 COM クラスが、`MiscStatus` レジストリ キー値を必要とする OCX クラスである場合は、この属性を使用できます。|
|`miscStatusDocPrint`|省略可能。 DVASPECT_DOCPRINT によって提供される情報を、アセンブリ マニフェスト内に複製します。 プリンターに印刷されるかのように画面に表示できるオブジェクト表現を提供できます。 値として、次の表に示す属性値のコンマ区切りの一覧を指定できます。 COM クラスが、`MiscStatus` レジストリ キー値を必要とする OCX クラスである場合は、この属性を使用できます。|
|`miscStatusThumbnail`|省略可能。 DVASPECT_THUMBNAIL によって提供される情報を、アセンブリ マニフェスト内に複製します。 閲覧ツールで表示できるオブジェクトのサムネイルを提供できます。 値として、次の表に示す属性値のコンマ区切りの一覧を指定できます。 COM クラスが、`MiscStatus` レジストリ キー値を必要とする OCX クラスである場合は、この属性を使用できます。|

## <a name="cominterfaceexternalproxystub"></a>comInterfaceExternalProxyStub
 `comInterfaceExternalProxyStub` 要素は、`file` 要素の省略可能な子ですが、登録を必要としない COM を使用して配置する予定の COM コンポーネントが [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションに含まれている場合は、必要とされる可能性があります。 この要素には、以下の属性が含まれています。

|属性|説明|
|---------------|-----------------|
|`iid`|必須。 このプロキシによってサービスが提供されるインターフェイスの ID (IID)。 IID は中かっこで囲む必要があります。|
|`baseInterface`|省略可能。 `iid` によって参照されているインターフェイスの派生元であるインターフェイスの IID。|
|`numMethods`|省略可能。 そのインターフェイスによって実装されているメソッドの数。|
|`name`|省略可能。 コード内に記述されるインターフェイスの名前。|
|`tlbid`|省略可能。 `iid` 属性によって指定されたインターフェイスの説明が含まれるタイプ ライブラリ。|
|`proxyStubClass32`|省略可能。 IID を、32 ビット プロキシ DLL 内の CLSID にマップします。|

## <a name="cominterfaceproxystub"></a>comInterfaceProxyStub
 `comInterfaceProxyStub` 要素は、`file` 要素の省略可能な子ですが、登録を必要としない COM を使用して配置する予定の COM コンポーネントが [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションに含まれている場合は、必要とされる可能性があります。 この要素には、以下の属性が含まれています。

|属性|説明|
|---------------|-----------------|
|`iid`|必須。 このプロキシによってサービスが提供されるインターフェイスの ID (IID)。 IID は中かっこで囲む必要があります。|
|`baseInterface`|省略可能。 `iid` によって参照されているインターフェイスの派生元であるインターフェイスの IID。|
|`numMethods`|省略可能。 そのインターフェイスによって実装されているメソッドの数。|
|`Name`|省略可能。 コード内に記述されるインターフェイスの名前。|
|`Tlbid`|省略可能。 `iid` 属性によって指定されたインターフェイスの説明が含まれるタイプ ライブラリ。|
|`proxyStubClass32`|省略可能。 IID を、32 ビット プロキシ DLL 内の CLSID にマップします。|
|`threadingModel`|省略可能。 省略可能。 インプロセス COM クラスによって使用されるスレッド モデル。 このプロパティが null の場合、スレッド モデルは使用されません。 コンポーネントはクライアントのメイン スレッドで作成され、他のスレッドからの呼び出しはこのスレッドにマーシャリングされます。 次の一覧に有効な値を示します。<br /><br /> `Apartment`、`Free`、`Both`、`Neutral`。|

## <a name="windowclass"></a>windowClass
 `windowClass` 要素は、`file` 要素の省略可能な子ですが、登録を必要としない COM を使用して配置する予定の COM コンポーネントが [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションに含まれている場合は、必要とされる可能性があります。 この要素は、バージョンが適用されている必要のある COM コンポーネントによって定義されているウィンドウ クラスを参照します。 この要素には、以下の属性が含まれています。

|属性|説明|
|---------------|-----------------|
|`versioned`|省略可能。 登録に使用される内部ウィンドウ クラスの名前に、そのウィンドウ クラスを含むアセンブリのバージョンを含めるかどうかを制御します。 この属性の値は `yes` または `no` にできます。 既定値は、`yes` です。 値 `no` は、同じウィンドウ クラスが、サイドバイサイド コンポーネントおよび同等の非サイドバイサイド コンポーネントによって定義されていて、それらを同じウィンドウ クラスとして扱う場合にのみ使用する必要があります。 ウィンドウ クラスの登録に関する通常の規則が適用されることに注意してください。ウィンドウ クラスを登録する最初のコンポーネントには、バージョンが適用されていないため、そのコンポーネントでのみ登録が可能です。|

## <a name="hash"></a>hash
 `hash` 要素は、`file` 要素の省略可能な子です。 `hash` 要素に属性はありません。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] では、アプリケーション内のすべてのファイルのアルゴリズム ハッシュをセキュリティ チェックとして使用し、配置後にどのファイルも変更されていないことを確認します。 `hash` 要素が含まれていない場合、このチェックは実行されません。 そのため、`hash` 要素を省略することはお勧めできません。

 マニフェストにハッシュされていないファイルが含まれている場合、ユーザーはハッシュされていないファイルの内容を検証できないため、そのマニフェストにはデジタル署名できません。

## <a name="dsigtransforms"></a>dsig:Transforms
 `dsig:Transforms` 要素は、`hash` 要素の必須の子です。 `dsig:Transforms` 要素に属性はありません。

## <a name="dsigtransform"></a>dsig:Transform
 `dsig:Transform` 要素は、`dsig:Transforms` 要素の必須の子です。 `dsig:Transform` 要素には、次の属性があります。

| 属性 | 説明 |
|-------------| - |
| `Algorithm` | このファイルのダイジェストの計算に使用されるアルゴリズム。 現在 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] によって使用されている値は `urn:schemas-microsoft-com:HashTransforms.Identity` のみです。 |

## <a name="dsigdigestmethod"></a>dsig:DigestMethod
 `dsig:DigestMethod` 要素は、`hash` 要素の必須の子です。 `dsig:DigestMethod` 要素には、次の属性があります。

| 属性 | 説明 |
|-------------| - |
| `Algorithm` | このファイルのダイジェストの計算に使用されるアルゴリズム。 現在 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] によって使用されている値は `http://www.w3.org/2000/09/xmldsig#sha1` のみです。 |

## <a name="dsigdigestvalue"></a>dsig:DigestValue
 `dsig:DigestValue` 要素は、`hash` 要素の必須の子です。 `dsig:DigestValue` 要素に属性はありません。 そのテキスト値は、指定されたファイルについて計算されたハッシュです。

## <a name="remarks"></a>解説
 この要素では、アプリケーションを構成するすべての非アセンブリ ファイルと、特に、ファイル検証のためのハッシュ値が識別されます。 この要素には、ファイルに関連付けられているコンポーネント オブジェクト モデル (COM) 分離データを含めることもできます。 ファイルが変更された場合は、変更を反映するため、アプリケーション マニフェスト ファイルも更新する必要があります。

## <a name="example"></a>例
 次のコード例は、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] を使用して配置されるアプリケーションのアプリケーション マニフェスト内にある `file` 要素を示しています。

```xml
<file name="Icon.ico" size="9216">
  <hash>
    <dsig:Transforms>
      <dsig:Transform Algorithm="urn:schemas-microsoft-com:HashTransforms.Identity" />
    </dsig:Transforms>
    <dsig:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
    <dsig:DigestValue>lVoj+Rh6RQ/HPNLOdayQah5McrI=</dsig:DigestValue>
  </hash>
</file>
```

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーション マニフェスト](../deployment/clickonce-application-manifest.md)