---
title: VSIX パッケージのローカライズ | Microsoft Docs
description: 対象言語ごとに Extension.vsixlangpack ファイルを作成し、これらを適切なフォルダーに配置することによって VSIX パッケージをローカライズする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 10/26/2017
ms.topic: conceptual
helpviewer_keywords:
- localize package
- localize extension
- localized deployment
ms.assetid: 10e80b13-b39e-466c-a7c8-774a862355af
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7d2e297484e89f1ae2cfb9f2be7af25f1fe92714
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073223"
---
# <a name="localizing-vsix-packages"></a>VSIX パッケージのローカライズ

VSIX パッケージのローカライズは、対象言語ごとに *Extension.vsixlangpack* ファイルを作成し、これらを適切なフォルダーに配置することによって行うことができます。 ローカライズされたパッケージをインストールすると、拡張機能のローカライズされた名前がローカライズされた説明と共に表示されます。 ローカライズされたライセンス ファイル、またはローカライズされた情報を示す URL を指定すると、それらも表示されます。

VSIX パッケージの内容に、メニュー コマンドやその他の UI を追加する VSPackage が含まれている場合は、「[メニュー コマンドをローカライズする](../extensibility/localizing-menu-commands.md)」を参照して、新しい UI 要素のローカライズについて調べてください。

## <a name="directory-structure"></a>ディレクトリの構造

 ユーザーが拡張機能をインストールすると、 **[拡張機能と更新プログラム]** によって、ターゲット コンピューターの Visual Studio ロケールに一致する名前を持つフォルダーの VSIX パッケージの最上位レベルがチェックされます。 **[拡張機能と更新プログラム]** によってフォルダー内の *.vsixlangpack* ファイルが検出されると、そのファイル内のローカライズされた値で、 *.vsixmanifest* ファイル内の対応する値が置き換えられます。 これらの値は、拡張機能をインストールするときに表示されます。 次の例は、スペイン語 (es-ES) とフランス語 (fr-FR) にローカライズされた VSIX パッケージのディレクトリ構造を示しています。

```text
.
├── MyExtension.dll
├── Extension.vsixmanifest
├── [Content_Types].xml
├── es-ES
│   └── Extension.vsixlangpack
└── fr-FR
    └── Extension.vsixlangpack
```

> [!NOTE]
> [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] 内の VSIX でサポートされているプロジェクト テンプレートでは、VSIX マニフェストを生成し、これに *source.extension.vsixmanifest* という名前を付けます。 Visual Studio によってプロジェクトがビルドされると、そのファイルの内容が VSIX パッケージの Extension.VsixManifest にコピーされます。

## <a name="the-extensionvsixlangpack-file"></a>Extension.vsixlangpack ファイル

*Extension.vsixlangpack* ファイルは [VSIX 言語パックのスキーマ 2.0](../extensibility/vsix-language-pack-schema-2-0-reference.md) に従います。 このスキーマには `PackageLanguagePackManifest` があり、その直後に `Metadata` 子要素が続きます。 メタデータ要素には、最大 6 つの子要素 (`DisplayName`、`Description`、`MoreInfo`、`License`、`ReleaseNotes`、および `Icon`) を含めることができます。 これらの子要素は、*Extension.vsixmanifest* ファイルの `Metadata` 要素である子要素 (`DisplayName`、`Description`、`MoreInfo`、`License`、`ReleaseNotes`、および `Icon`) に対応します。

vsixlangpack ファイルを作成する場合、`Include in Vsix` プロパティを `true` に設定する必要があります。 それ以外の場合、ローカライズされたインストール テキストは無視されます。

### <a name="to-set-the-include-in-vsix-property"></a>[Vsix に含める] プロパティを設定するには

1. **ソリューション エクスプローラー** で、Extension.vsixlangpack ファイルを右クリックし、 **[プロパティ]** をクリックします。

2. **[プロパティ グリッド]** で、 **[Vsix に含める]** をクリックし、値を `true` に設定します。

## <a name="example"></a>例

### <a name="description"></a>説明

次の例は、*Extension.vsixmanifest* ファイルの関連する部分を示しています。 このファイルには、スペイン語の対応する *Extension.vsixlangpack* ファイルも含まれています。 ターゲット コンピューターの Visual Studio ロケールがスペイン語に設定されている場合、言語パックの値によってマニフェストの値が置き換えられます。

### <a name="code"></a>コード

- [*Extension.vsixmanifest*]

```xml
<?xml version="1.0" encoding="utf-8"?>
<PackageManifest ...>
  <Metadata ...>
    <DisplayName>Family Tree</DisplayName>
    <Description>This extension places a custom treeview control in the toolbox that is optimized for handling family tree information.</Description>
    <MoreInfo>http://www.contoso.com/products/FamilyTree.htm</MoreInfo>
    <License>Eula.rtf</License>
    <ReleaseNotes>ReleaseNotes.rtf</ReleaseNotes>
    <Icon>Icon.png</Icon>
  </Metadata>
  <Installation .../>
  <Dependencies .../>
  <Prerequisites .../>
  <Assets .../>
</PackageManifest>
```

- [*Extension.vsixlangpack*]

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
|[VSIX 言語パック スキーマ 2.0 リファレンス](vsix-language-pack-schema-2-0-reference.md)|VSIX 言語パックには、.vsix 配置ファイルのローカライズ情報が記述されています。|
|[VSIX パッケージの構造](../extensibility/anatomy-of-a-vsix-package.md)|Vsix パッケージの構造と内容が記述されています。|
|[メニュー コマンドをローカライズする](../extensibility/localizing-menu-commands.md)|拡張機能の他のテキスト リソースをローカライズする方法について説明します。|
