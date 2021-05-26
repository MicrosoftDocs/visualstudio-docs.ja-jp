---
title: ウィザード | Microsoft Docs
description: Visual Studio で使用可能なウィザードとテンプレートの中に自身のウィザードを列挙する方法、およびウィザードが IDE で満たす必要のある要件について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], providing wizard support
ms.assetid: 59d9a77f-ee80-474b-a14f-90f477ab717b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b5c5cb9649689f711844f97e0b57ab23248e9a00
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074159"
---
# <a name="wizards"></a>ウィザード
ウィザードを作成した後は、通常、他のユーザーが使用できるように、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE) に追加します。 追加したウィザードは、 **[新しいプロジェクトの追加]** または **[新しい項目の追加]** ダイアログ ボックスに表示されます。 **[新しいプロジェクトの追加]** または **[新しい項目の追加]** ダイアログ ボックスを表示するには、**ソリューション エクスプローラー** で開いているソリューションを右クリックし、 **[追加]** をポイントして、 **[新しいプロジェクト]** または **[新しい項目]** をクリックします。

 ユーザーが **[新しいプロジェクトの追加]** ダイアログ ボックスまたは **[新しい項目の追加]** ダイアログ ボックスを開いたとき、あるいは **ソリューション エクスプローラー** 内の項目を右クリックしたときに、使用可能な値のツリー ビューから選択できるよう、ウィザードを [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] で実装することができます。

 ウィザードでは、新しいプロジェクトまたはサイトの名前をローカライズするオプションを提供し、ユーザーがウィザードを選択したときに表示されるアイコンを決定できます。 使用可能な他の項目と相対的に新しい項目を表示する順序を制御することもできます。項目をアルファベット順に整理する必要はありません。

 ウィザードが開かれたときに渡されるカスタム パラメーターに基づいて、異なる方法で起動するウィザードを提供することもできます。

 このセクションの各トピックでは、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の **[新しいプロジェクトの追加]** ダイアログ ボックスと **[新しい項目の追加]** ダイアログ ボックスで自身のウィザードが使用可能なウィザードの中に列挙されるようにするために実装するファイル、およびウィザードが IDE で正しく動作するために満たす必要がある要件について説明します。

## <a name="in-this-section"></a>このセクションの内容
- [テンプレート ディレクトリの説明 (.Vsdir) ファイル](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)

 テンプレート ディレクトリの説明ファイルの概要と、それらがどのように IDE で機能して、プロジェクトに関連付けられているフォルダー、ウィザード .vsz ファイル、およびテンプレート ファイルをダイアログ ボックスに表示するかについて説明します。

- [ウィザード (.Vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)

 IDE によってウィザードがどのように起動され、.vsz ファイルの 3 つのパートが列挙されるかを説明します。

- [ウィザード インターフェイス (IDTWizard)](../../extensibility/internals/wizard-interface-idtwizard.md)

 IDE で動作するためにウィザードで実装する必要がある `IDTWizard` インターフェイスについて説明します。

- [コンテキスト パラメーター](../../extensibility/internals/context-parameters.md)

 ウィザードの実装方法と、IDE がコンテキスト パラメーターを実装に渡すときに発生する動作について説明します。

- [カスタム パラメーター](../../extensibility/internals/custom-parameters.md)

 ウィザードが起動された後、カスタム パラメーターを使用してウィザードの操作を制御する方法について説明します。

## <a name="related-sections"></a>関連項目
- [プロジェクトの種類](../../extensibility/internals/project-types.md)

 新しいプロジェクト タイプを設計する方法に関する情報を提供するその他のトピックへのリンクを紹介します。

- [プロジェクトの拡張](../../extensibility/extending-projects.md)

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] プロジェクトおよびソリューションを使用してコード ファイルとリソース ファイルを編成する方法、またソース管理を実装する方法について説明します。
