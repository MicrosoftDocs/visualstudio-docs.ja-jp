---
title: '方法: XML ファイルを編集する'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 07fa3ecf-6345-4d30-9d85-d5ef5b083319
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b25eebad9efc70e4fda45131e232983e81961625
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62840370"
---
# <a name="how-to-edit-xml-files"></a>方法: XML ファイルを編集する

XML エディターは、XML ファイル用の新しいエディターです。 スタンドアロンの XML ファイル、または Visual Studio プロジェクトと関連付けられたファイルに対して使用できます。 XML エディターは、次のファイル拡張子に関連付けられている: *.config*、 *.dtd*、 *.xml*、 *.xsd*、 *.xdr*、 *.xsl*、 *.xslt*、および *.vssettings*します。 XML エディターは、特定のエディターで登録されると、指定されていないと、XML や DTD のコンテンツを格納している他のファイル種類と関連付けられているもできます。

> [!NOTE]
> XHTML ドキュメントは HTML エディターによって処理されます。

XML ファイルを編集するには、編集するファイルをダブルクリックします。

## <a name="add-a-new-xml-file-to-a-project"></a>新しい XML ファイルをプロジェクトに追加します。

1. **プロジェクト**メニューの **新しい項目の追加**します。

2. 選択**XML ファイル**から、**テンプレート**ウィンドウ。

3. 内のファイル名を入力、**名前**フィールドとキーを押して**追加**します。

   XML ファイルは、プロジェクトに追加し、XML エディターで開きます。 ファイルには既定の XML 宣言 `<?xml version="1.0" encoding="utf-8" ?>` が含まれています。

## <a name="add-an-existing-xml-file-to-a-project"></a>既存の XML ファイルをプロジェクトに追加します。

1. **プロジェクト**メニューの **既存項目の追加**します。

   **既存項目の追加** ダイアログ ボックスが表示されます。

2. XML ファイルとキーを押して選択**追加**します。

## <a name="create-a-new-xml-or-xslt-file"></a>新しい XML または XSLT ファイルを作成します。

1. **ファイル**メニューの **新規**します。

   **新しいファイル** ダイアログ ボックスが表示されます。

2. 選択**XML ファイル**; 新しい XML ファイルを作成するか、選択する**XSLT ファイル**新しい XSLT スタイル シートを作成します。

3. **[開く]** をクリックします。

## <a name="create-an-empty-project-for-xml-files"></a>XML ファイルの空のプロジェクトを作成します。

::: moniker range="vs-2017"

1. **ファイル**メニューの **新規** > **プロジェクト**します。

   **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

2. 任意のコード言語を選択して**空のプロジェクト**します。

3. **[OK]** をクリックします。

::: moniker-end

::: moniker range=">=vs-2019"

1. **ファイル**メニューの **新規** > **プロジェクト**します。

2. 入力**空のプロジェクト**テンプレートの検索ボックスで選択、**空のプロジェクト (.NET Framework)** テンプレート、およびクリック **[次へ]**。

3. **[作成]** をクリックします。

::: moniker-end

4. プロジェクトに XML ファイルを追加します。

   XML エディターでは、このプロジェクトに追加したスキーマを検索し、検証と IntelliSense の XML、スキーマ、またはこのプロジェクトが開いている間に編集する XSLT ファイルのために使用します。

## <a name="see-also"></a>関連項目

- [XML エディター](../xml-tools/xml-editor.md)
- [XML ドキュメントのプロパティと [プロパティ] ウィンドウ](../xml-tools/xml-document-properties-properties-window.md)
- [方法: XML ドキュメントから XML スキーマを作成します。](../xml-tools/how-to-create-an-xml-schema-from-an-xml-document.md)