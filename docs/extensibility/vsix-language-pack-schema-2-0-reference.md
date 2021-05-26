---
title: VSIX 言語パック スキーマ 2.0 リファレンス | Microsoft Docs
description: VSIX 言語パック スキーマには、VSIX パッケージのローカライズされたインストール情報が含まれています。 バージョン 2.0 では、追加のローカライズ要素がサポートされています。
ms.custom: SEO-VS-2020
ms.date: 10/26/2017
ms.topic: conceptual
helpviewer_keywords:
- language pack
- localize vsix
- localize package
- localize extension
ms.assetid: 2a2932bc-cdbe-4d32-91fa-a3e0474f9098
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.openlocfilehash: 0e7107cb90a79e8cd1a052cd73706d95a782781d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062279"
---
# <a name="vsix-language-pack-schema-20-reference"></a>VSIX 言語パック スキーマ 2.0 リファレンス

VSIX 言語パック スキーマには、VSIX パッケージのローカライズされたインストール情報が含まれています。 このスキーマのバージョン 2.0 では、追加のローカライズ要素がサポートされています。

## <a name="language-pack-schema"></a>言語パック スキーマ

言語パック ファイルのルート要素は、言語パック形式のバージョンである `Version` 属性を含む `<PackageLanguagePackManifest>` です。 この記事では、言語パック形式のバージョン 2.0 について説明します。これは、マニフェストで `Version` 属性を値 `Version="2.0.0"` に設定することで指定されます。 ルート要素には、子の `<Metadata>` 要素のみが 1 つだけ含まれています。

### <a name="packagelanguagepackmanifest-element"></a>PackageLanguagePackManifest 要素

`<PackageLanguagePackManifest>` 要素内には、次の要素が存在する必要があります。

|タイトル|説明|
|-----------|-----------------|
|`<Metadata>`| ローカライズされたすべてのパッケージ メタデータのコンテナー要素

### <a name="metadata-element"></a>Metadata 要素

`<Metadata>` 要素内には、次の要素を含めることができます。

|タイトル|説明|
|-----------|-----------------|
|`<DisplayName>`|インストールされる拡張機能のローカライズされた名前|
|`<Description>`|インストールされる拡張機能のローカライズされた説明|
|`<License>`| 拡張機能のライセンスのローカライズ版へのパス|
|`<MoreInfo>`| 拡張機能に関するローカライズされた情報へのリンク|
|`<ReleaseNotes>`| リリース ノートのローカライズ版へのパスまたはリンク|
|`<Icon>`| 拡張機能アイコンのローカライズ版へのパス|

### <a name="sample-manifest"></a>サンプル マニフェスト

```xml
<?xml version="1.0" encoding="utf-8"?>
<PackageLanguagePackManifest Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema/2011">
  <Metadata>
    <DisplayName>Arbol de Familia</DisplayName>
    <Description> Esta extensión pone control personalizado en la caja de herramientas por manejar información de familia.</Description>
    <MoreInfo> http://www.contoso.com/products/es/ArbolDeFamilia.htm</MoreInfo>
    <License>Eula.rtf</License>
    <ReleaseNotes>ReleaseNotes.rtf</ReleaseNotes>
    <Icon>Icon.png</Icon>
  </Metadata>
</PackageLanguagePackManifest>
```

## <a name="see-also"></a>関連項目

|Title|説明|
|-----------|-----------------|
|[VSIX パッケージのローカライズ](../extensibility/localizing-vsix-packages.md)|VSIX パッケージのローカライズされたインストールをサポートする方法について説明します。|
|[VSIX 拡張機能スキーマ 2.0 リファレンス](../extensibility/vsix-extension-schema-2-0-reference.md)|VSIX マニフェストには、 *.vsix* 配置ファイルの内容が記述されます。 配置ファイルを使用すると、 **[拡張機能と更新プログラム]** ダイアログ ボックスを使用して Visual Studio 拡張機能をインストールできます。|
|[Visual Studio 拡張機能の検索と使用](../ide/finding-and-using-visual-studio-extensions.md)|**[拡張機能と更新プログラム]** ダイアログ ボックスを使用して拡張機能のインストール、削除、アクティブ化、非アクティブ化を行う方法について説明します。|
