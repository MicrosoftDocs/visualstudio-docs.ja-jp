---
title: VSIX プロジェクト テンプレート | Microsoft Docs
description: VSIX プロジェクト テンプレートを使用して Visual Studio 拡張機能を VSIX プロジェクトにラップし、パッケージを Visual Studio Marketplace で公開する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- deploy packages
- publish extension
ms.assetid: b6c82167-e2a5-4cff-8c8b-2d72e2a9092c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8f8e5e9f9a5a21600aa894ee8b7f6c3730bc1fc7
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062266"
---
# <a name="vsix-project-template"></a>VSIX プロジェクト テンプレート

VSIX プロジェクト テンプレートを使用して、1 つ以上の Visual Studio 拡張機能を VSIX プロジェクトにラップし、パッケージを [Visual Studio Marketplace](https://marketplace.visualstudio.com/) Web サイトに公開することができます。

 VSIX の展開は、VSPackage、アセンブリ、MEF コンポーネント、プロジェクト テンプレート、項目テンプレート、ツールボックス コントロール、およびカスタム拡張機能の種類をサポートしています。

> [!NOTE]
> VSIX プロジェクトを使用するには、Visual Studio SDK をインストールする必要があります。 Visual Studio SDK の詳細については、「[Visual Studio SDK](../extensibility/visual-studio-sdk.md)」を参照してください。

## <a name="where-to-find-the-vsix-project-template"></a>VSIX プロジェクト テンプレートを探す場所

VSIX プロジェクト テンプレートは、 **[新しいプロジェクト]** ダイアログ ボックスで「vsix」を検索することで入手できます。  C# バージョンと Visual Basic バージョンの両方があります。

> [!TIP]
> **[新しいプロジェクト]** ダイアログの上部にあるドロップダウン リスト ボックスで、.NET Framework 4.5 以降が指定されていることを確認してください。

## <a name="uses-of-the-vsix-project-template"></a>VSIX プロジェクト テンプレートの用途

VSIX プロジェクト テンプレートには、主に次の 2 つの用途があります。

- プロジェクト テンプレート、項目テンプレート、拡張機能を展開するため。

- 複数の拡張機能の出力を 1 つの展開パッケージにラップするため。

## <a name="packaging-an-extension-in-an-empty-vsix-project"></a>空の VSIX プロジェクトに拡張機能をパッケージ化する

空の VSIX プロジェクトでラップすることにより、既存の拡張機能、または VSIX をまだサポートしていない拡張機能をパッケージ化することができます。 ラップする拡張機能は、[VSIX スキーマ](../extensibility/vsix-extension-schema-2-0-reference.md)でサポートされている種類のものである必要があります。

### <a name="to-package-an-extension-by-using-a-vsix-project"></a>VSIX プロジェクトを使用して拡張機能をパッケージ化するには

1. 拡張機能を構成するプロジェクトをビルドします。

2. **VSIX プロジェクト** テンプレートを使用して VSIX プロジェクトを作成します。

    **マニフェスト デザイナー** に *Source.extension.vsixmanifest* が開かれます。

3. **[資産]** タブで **[新規]** ボタンを選択します。

    **[新しい資産の追加]** ダイアログ ボックスが表示されます。

4. **[種類]** リストで、追加する拡張機能の種類を選択します。

5. 現在のソリューションに含まれている拡張機能またはコンテンツ要素 (項目テンプレートやコンパイル済みアセンブリなど) を追加するには、次の手順を実行します。

   1. **[ソース]** リストで、 **[現在のソリューション内のプロジェクト]** を選択します。

   2. **[プロジェクト]** リストで、拡張機能の名前を選択します。

   3. **[このフォルダーに埋め込まれます]** ボックスに、資産を埋め込むフォルダーの名前を入力し、 **[OK]** ボタンを選択します。

6. 現在のソリューションに含まれていない拡張機能またはコンテンツ要素を追加するには、次の手順を実行します。

   1. **[ソース]** リスト ボックスで、 **[ファイル システム上のファイル]** を選択します。

   2. **[パス]** フィールドに、コンパイルまたは圧縮された拡張機能ファイルへの完全なパスを入力するか、 **[参照]** ボタンを使用してファイルを参照します。

   3. **[このフォルダーに埋め込まれます]** ボックスに、資産を埋め込むフォルダーの名前を入力し、 **[OK]** ボタンを選択します。

7. パッケージに追加の拡張機能を含める場合は、同じ方法で追加します。

8. ソリューションをビルドします。

    [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] により、VSIX マニフェスト ファイル、[Content_Types] *.xml* ファイル、プロジェクトに追加したすべての拡張機能資産を含む *.vsix* ファイルがビルドされます。

## <a name="see-also"></a>こちらもご覧ください

- [VSIX 拡張機能スキーマ 2.0 リファレンス](../extensibility/vsix-extension-schema-2-0-reference.md)
- [Visual Studio 拡張機能の検索と使用](../ide/finding-and-using-visual-studio-extensions.md)
