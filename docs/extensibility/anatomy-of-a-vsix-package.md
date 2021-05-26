---
title: VSIX パッケージの構造 | Microsoft Docs
description: Visual Studio の VSIX パッケージ、Visual Studio の拡張機能が 1 つ以上含まれるファイル、メタデータ マニフェスト ファイルの内容について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- visual studio extension
- vsix
- packages
ms.assetid: 8b86d62f-c274-4e91-82e0-38cdb9a423d5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 67b3775509e330ad55a2531a9e42a7cca93c50a6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097501"
---
# <a name="anatomy-of-a-vsix-package"></a>VSIX パッケージの構造
VSIX パッケージは、1 つ以上の Visual Studio 拡張機能と一緒に、拡張機能の分類とインストールのために Visual Studio で使用されるメタデータが含まれる *.vsix* ファイルです。 そのメタデータは、VSIX マニフェストと *[Content_Types].xml* ファイルに含まれています。 VSIX パッケージには、ローカライズされたセットアップ テキストを提供するための *Extension.vsixlangpack* ファイルが 1 つ以上含まれている場合もあります。また、依存関係をインストールする追加の VSIX パッケージが含まれる場合があります。

 VSIX パッケージ形式は、Open Packaging Conventions (OPC) 標準に従っています。 パッケージには、バイナリやサポート ファイルと共に、 *[Content_Types].xml* ファイルと *.vsix* マニフェスト ファイルが含まれています。 1 つの VSIX パッケージに、複数のプロジェクトの出力が含まれることがあります。または、独自のマニフェストを持つ複数のパッケージが含まれる場合さえあります。

> [!NOTE]
> [\[RFC2396\]](https://www.rfc-editor.org/rfc/rfc2396.txt) で定義されているように、VSIX パッケージに含められるファイルの名前には、スペースも、Uniform Resource Identifier (URI) 内で予約されている文字も含めないでください。

## <a name="the-vsix-manifest"></a>VSIX マニフェスト
 VSIX マニフェストにはインストールされる拡張機能に関する情報が含まれていて、このマニフェストは VSX スキーマに従っています。 詳細については、[VSIX 拡張機能スキーマ 1.0 リファレンス](/previous-versions/dd393700(v=vs.110))に関するページを参照してください。 VSIX マニフェストの例については、「[PackageManifest 要素 (ルート要素、VSX スキーマ)](/previous-versions/dd393754(v=vs.110))」を参照してください。

 VSIX マニフェストは、^.vsix* ファイルに含まれている場合は `extension.vsixmanifest` という名前にする必要があります。

## <a name="the-content"></a>コンテンツ
 VSIX パッケージには、テンプレート、ツールボックス項目、VSPackage、Visual Studio でサポートされている、その他任意の種類の拡張機能が含まれている場合があります。

## <a name="language-packs"></a>言語パック
 VSIX パッケージには、ローカライズされたテキストをインストール時に提供するための *Extension.vsixlangpack* ファイルが 1 つ以上含まれている場合があります。 詳細については、「[VSIX パッケージのローカライズ](../extensibility/localizing-vsix-packages.md)」を参照してください。

## <a name="dependencies-and-references"></a>依存関係と参照
 1 つの VSIX パッケージには、参照として他の VSIX パッケージを含めることができます。 これらの他のパッケージそれぞれのために、独自の VSIX マニフェストが含まれている必要があります。

 依存関係がある拡張機能をユーザーがインストールしようとすると、インストーラーにより、必要なアセンブリがユーザー システムにインストールされていることが確認されます。 必要なアセンブリが見つからない場合は、 **[拡張機能と更新プログラム]** に、不足しているアセンブリの一覧が表示されます。

 拡張機能マニフェストに [Reference](/previous-versions/visualstudio/visual-studio-2010/dd393687(v=vs.100)) 要素が 1 つ以上含まれている場合、 **[拡張機能と更新プログラム]** では、各参照のマニフェストが、システムにインストールされている拡張機能と比較され、まだインストールされていない場合は、参照されている拡張機能をインストールします。 参照されている拡張機能の以前のバージョンがインストールされている場合は、新しいバージョンに置き換えられます。

 複数プロジェクト ソリューションのプロジェクトに、同じソリューション内の別のプロジェクトへの参照が含まれる場合、VSIX パッケージにはそのプロジェクトの依存関係が含められます。 内部プロジェクトのための参照を選択してから、 **[プロパティ]** ウィンドウで **[VSIX プロパティに含まれる出力グループ]** を `BuiltProjectOutputGroup` に設定すると、この動作をオーバーライドできます。

 参照されているアセンブリのサテライト DLL を VSIX パッケージに含めるには、 **[VSIX プロパティに含まれる出力グループ]** に `SatelliteDllsProjectOutputGroup` を追加します。

## <a name="installation-location"></a>インストール場所
 インストール中、 **[拡張機能と更新プログラム]** によって、 *%LocalAppData%\Microsoft\VisualStudio\14.0\Extensions* の下にあるフォルダーで VSIX パッケージの内容が探されます。

 既定では、 *%LocalAppData%* はユーザー固有のディレクトリであるため、インストールは現在のユーザーにのみ適用されます。 ただし、マニフェストの [AllUsers](/previous-versions/ee191547(v=vs.110)) 要素を `True` に設定すると、拡張機能は <em>..\\</em>VisualStudioInstallationFolder<em>\Common7\IDE\Extensions</em> にインストールされて、コンピューターのユーザー全員が使用できるようになります。

## <a name="content_typesxml"></a>[Content_Types].xml
 *[Content_Types].xml* ファイルでは、展開された *.vsix* ファイル内のファイルの種類が識別されます。 Visual Studio では、パッケージのインストール時にこのファイルが使用されますが、ファイル自体はインストールされません。 このファイルの詳細については、「[[Content_types].xml ファイルの構造](the-structure-of-the-content-types-dot-xml-file.md)」を参照してください。

 Open Packaging Conventions (OPC) 標準では、 *[Content_Types].xml* ファイルは必須となっています。 OPC の詳細については、MSDN Web サイトの「[OPC: データをパッケージ化するための新しい標準](/archive/blogs/msdnmagazine/opc-a-new-standard-for-packaging-your-data)」を参照してください。