---
title: 入れ子になったプロジェクト向けのウィザード サポート |Microsoft Docs
description: Visual Studio SDK の VSPackage 内の入れ子になったプロジェクトに対して親プロジェクトで実装できる 2 つのウィザードについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Add Item wizard
- nested projects, wizard support
- New Project wizard
ms.assetid: 1b496acc-b326-4cdb-bb48-e3b5c6f12e05
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7f52b42462fdc4b7878f97c01bdc65322f32eb5b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074146"
---
# <a name="wizard-support-for-nested-projects"></a>入れ子になったプロジェクト向けのウィザード サポート
IDE では、入れ子になったプロジェクトの親プロジェクトで実装できる 2 つのウィザードを実行します。 **[新しいプロジェクト]** ウィザードと **[項目の追加]** ウィザードです。

 **[プロジェクトの追加]** を選択し、[ファイル] メニューの **[新しいプロジェクト]** をクリックするか、ソリューション エクスプローラーで **[追加]** を選択し、 **[新しいプロジェクト]** を右クリックして、ユーザーが **[新しいプロジェクト]** ウィザードを開始した場合、IDE では **Addproject** コマンドを実行し、親プロジェクトの **Addproject** の実装ではテンプレート プロジェクト ファイル、つまりコンテキスト パラメーターのセットを含むウィザード (.vsz) ファイルを返します。

 同様に、親プロジェクトの **AddItem** ウィザードの実装では、異なるコンテキスト パラメーターのセットを含む .vsz ファイルが返されます。

 ウィザードの詳細については、「[ウィザード (.Vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)」、「[コンテキスト パラメーター](../../extensibility/internals/context-parameters.md)」、および「[プロジェクトと項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)」を参照してください。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>
- [入れ子になったプロジェクト](../../extensibility/internals/nesting-projects.md)
