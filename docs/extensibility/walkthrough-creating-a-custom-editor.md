---
title: 'チュートリアル: カスタム エディターの作成 | Microsoft Docs'
description: このチュートリアルを使用して、VSPackage プロジェクト テンプレートを使用して C++ で簡単なカスタム エディターを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], custom - create
ms.assetid: d090abb6-d99f-4083-a3db-cd16bf81ce7d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 79adcf719091619fe4c4eb62b1fe89ba3da388f5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062019"
---
# <a name="walkthrough-create-a-custom-editor"></a>チュートリアル: カスタム エディターを作成する
VSPackage プロジェクト テンプレートでは、C++ で単純なカスタム エディターを作成できます。 VSPackage プロジェクト テンプレートでは、C# および Visual Basic プロジェクトはサポートされなくなりました。 詳細については、「[Visual Studio SDK](../extensibility/visual-studio-sdk.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="the-visual-studio-package-project-template"></a>Visual Studio パッケージ プロジェクト テンプレート
 Visual Studio パッケージ プロジェクト テンプレートは、 **[新しいプロジェクト]** ダイアログの **C++ の [機能拡張]** フォルダーにあります。

### <a name="to-create-a-vspackage-using-the-visual-studio-package-template"></a>Visual Studio パッケージ テンプレートを使用して VSPackage を作成するには

1. Visual Studio パッケージ テンプレートを使用してプロジェクトを作成します。

2. **[カスタム エディター]** オプションを選択し、 **[次へ]** をクリックします。 **[エディター オプション]** ページが表示されます。

3. **[エディター名]** ボックスにエディターの名前を入力します。 エディターに関連付けるファイル拡張子を **[ファイル拡張子]** ボックスに入力します。 このエディターは、この拡張子を持つファイルに対して使用できます。 このファイル拡張子は Visual Studio にのみ登録され、Windows には登録されません。 このエディターで作成した新しいドキュメントの既定のファイル名を **[既定のファイル名]** ボックスに入力します。

4. **[完了]** をクリックして、指定したフォルダーに VSPackage を作成します。

### <a name="to-test-your-custom-editor"></a>カスタム エディターをテストするには

1. **[ファイル]** メニューの **[新規作成]** をポイントしてから、 **[ファイル]** をクリックします。

2. **[新しいファイル]** ダイアログ ボックスの **[インストールされたテンプレート]** ペインで、ファイルのテンプレート、登録したファイルの種類の順に選択します。

3. **[開く]** をクリックして、ドキュメントを表示し、編集します。

     このエディターでは、切り取りと貼り付け、検索と置換、開いて読み込みの各操作がサポートされています。

## <a name="see-also"></a>関連項目
- [VSPackages](../extensibility/internals/vspackages.md)
