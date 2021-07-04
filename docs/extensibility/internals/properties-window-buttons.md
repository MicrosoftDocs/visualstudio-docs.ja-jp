---
title: プロパティ ウィンドウのボタン | Microsoft Docs
description: プロパティ ウィンドウのツールバーに既定で表示されるボタンと、それらのボタンの実装について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Properties window, buttons
ms.assetid: bdd2e3a7-ae6e-4e88-be1a-e0e3b7ddbbcc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a9c45d6cf0f271683c3c708bd71ef46377a5c5ca
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903451"
---
# <a name="properties-window-buttons"></a>プロパティ ウィンドウのボタン
開発言語や製品の種類に応じて、 **[プロパティ]** ウィンドウのツールバーには特定のボタンが既定で表示されます。 どの場合でも、 **[項目別]** 、 **[アルファベット順]** 、 **[プロパティ]** 、 **[プロパティ ページ]** ボタンが表示されます。 Visual C# と Visual Basic では、 **[イベント]** ボタンも表示されます。 特定の Visual C++ プロジェクトでは、 **[VC++ メッセージ]** および **[VC オーバーライド]** ボタンが表示されます。 他のプロジェクトの種類では、追加のボタンが表示される可能性があります。 **[プロパティ]** ウィンドウのボタンの詳細については、「[プロパティ ウィンドウ](../../ide/reference/properties-window.md)」を参照してください。

## <a name="implementation-of-properties-window-buttons"></a>プロパティ ウィンドウのボタンの実装
 **[項目別]** ボタンをクリックすると、Visual Studio では、フォーカスのあるオブジェクトの <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties> インターフェイスを呼び出して、そのプロパティをカテゴリ別に並べ替えます。 <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties> は、 **[プロパティ]** ウィンドウに表示される `IDispatch` オブジェクトに実装されます。

 定義済みのプロパティ カテゴリが 11 個あり、これらは負の値を持っています。 カスタム カテゴリを定義できますが、定義済みのカテゴリと区別するために、これには正の値を割り当てることをお勧めします。

 <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties.MapPropertyToCategory%2A> メソッドは、指定されたプロパティの適切なプロパティ カテゴリ値を返します。 <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties.GetCategoryName%2A> メソッドは、カテゴリ名を含む文字列を返します。 標準のプロパティ カテゴリ値は Visual Studio によって認識されているため、ユーザーは、カスタム カテゴリ値のサポートを提供するだけで済みます。

 **[アルファベット順]** ボタンをクリックすると、プロパティが名前のアルファベット順に表示されます。 これらの名前は、ローカライズされた並べ替えアルゴリズムに従って `IDispatch` によって取得されます。

 **[プロパティ]** ウィンドウが開いているとき、 **[プロパティ]** ボタンは自動的に選択済みとして表示されます。 環境の他の部分にも同じボタンが表示されるため、それをクリックして **[プロパティ]** ウィンドウを表示できます。

 選択されたオブジェクトに対して `ISpecifyPropertyPages` が実装されていない場合、 **[プロパティ ページ]** ボタンは使用できません。 プロパティ ページには、通常はソリューションやプロジェクトに関連付けられている、構成に依存するプロパティが表示されますが、これらのプロパティを (たとえば、Visual C++ の) プロジェクト項目に関連付けることもできます。

> [!NOTE]
> アンマネージド コードを使用して **[プロパティ]** ウィンドウにツールバー ボタンを追加することはできません。 ツールバー ボタンを追加するには、<xref:System.Windows.Forms.Design.PropertyTab> から派生するマネージド オブジェクトを作成する必要があります。

## <a name="see-also"></a>関連項目
- [プロパティの拡張](../../extensibility/internals/extending-properties.md)
