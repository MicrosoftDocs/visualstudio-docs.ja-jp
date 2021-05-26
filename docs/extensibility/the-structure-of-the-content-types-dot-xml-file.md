---
title: '[Content_types].xml ファイルの構造 | Microsoft Docs'
description: VSIX パッケージ内のコンテンツの種類に関する情報が含まれる、コンテンツ タイプ ファイルの構造について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- content_types
- content types
- opc
- vsix
ms.assetid: 9c399598-b9fa-4da7-84b5-defbf82e9335
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5dea58176269536ae7f0e5857c938c60f76c5c6b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055896"
---
# <a name="the-structure-of-the-content_typesxml-file"></a>[Content_types] .xml ファイルの構造
VSIX パッケージ内のコンテンツの種類に関する情報が含まれます。 Visual Studio では、[Content_Types].xml ファイルを使用してそのパッケージをインストールしますが、ファイル自体はインストールしません。

> [!NOTE]
> このトピックは VSIX パッケージで使用される [Content_Type].xml ファイルにのみ適用されますが、[Content_Types].xml ファイル タイプは *Open Packaging Conventions (OPC)* 標準の一部です。 詳細については、MSDN Web サイトの [OPC: データをパッケージ化するための新しい標準](/archive/msdn-magazine/2007/august/opc-a-new-standard-for-packaging-your-data)に関するページをご覧ください。

## <a name="attributes-and-elements"></a>属性および要素
 以降のセクションでは、ルート要素とその属性および子要素について説明します。

### <a name="root-element"></a>Root 要素

|要素|説明|
|-------------|-----------------|
|`Types`|VSIX パッケージ内のファイルの種類を列挙する子要素を含めます。|

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|`Xmlns`|(必須。) この [Content_Types].xml ファイルに使用されるスキーマの場所。|

### <a name="attribute-name-attribute"></a>{属性名} 属性

| [値] | 説明 |
| - | - |
| `http://schemas.openformats.org/package/2006/content-types` | コンテンツ タイプ スキーマの場所。 |

### <a name="child-elements"></a>子要素
 `Types` 要素には、任意の数の `Default` 要素を含めることができます。

|要素|説明|
|-------------|-----------------|
|`Default`|VSIX パッケージ内のコンテンツ タイプを記述します。 パッケージ内のどのファイルの種類にも、独自の `Default` 要素が必要です。|

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|`Extension`|VSIX パッケージ内のファイルのファイル名拡張子。|
|`ContentType`|ファイル名拡張子に関連付けられているコンテンツの種類を記述します。|

### <a name="attribute-name-attribute"></a>{属性名} 属性
 Visual Studio では、関連付けられている `Extension` タイプに対して次の `ContentType` 値が認識 されます。

|拡張機能|ContentType|
|---------------|-----------------|
|txt|text/plain|
|pkgdef|text/plain|
|xml|text/xml|
|vsixmanifest|text/xml|
|htm または html|text/html|
|rtf|application/rtf|
|pdf|application/pdf|
|GIF|image/gif|
|jpg または jpeg|image/jpg|
|tiff|image/tiff|
|vsix|application/zip|
|zip|application/zip|
|dll|application/octet-stream|
|他のすべてのファイル タイプ|application/octet-stream|

## <a name="example"></a>例

### <a name="description"></a>説明
 次の [Content_Types].xml ファイルには、一般的な VSIX パッケージが記述されています。

### <a name="code"></a>コード

```
<?xml version="1.0" encoding="utf-8" ?>
<Types xmlns="http://schemas.openxmlformats.org/package/2006/content-types">
    <Default Extension="vsixmanifest" ContentType="text/xml" />
    <Default Extension="dll" ContentType="application/octet-stream" />
    <Default Extension="png" ContentType="application/octet-stream" />
    <Default Extension="txt" ContentType="text/plain" />
    <Default Extension="pkgdef" ContentType="text/plain" />
</Types>
```

## <a name="see-also"></a>関連項目
- [VSIX パッケージの構造](../extensibility/anatomy-of-a-vsix-package.md)
- [VSIX 拡張機能スキーマ 1.0 リファレンス](/previous-versions/dd393700(v=vs.110))
- [OPC: データをパッケージ化するための新しい標準](/archive/msdn-magazine/2007/august/opc-a-new-standard-for-packaging-your-data)