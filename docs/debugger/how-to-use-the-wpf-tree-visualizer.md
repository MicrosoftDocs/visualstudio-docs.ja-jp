---
title: '方法: WPF ツリー ビジュアライザーを使用する |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- WPF, debugging
- debugging, WPF
ms.assetid: 2a1bf1cd-90f9-4d06-9fb4-1bfc925afef3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4e005c1b41d2c563c5b47f358e87912cba64bf7f
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/11/2019
ms.locfileid: "67821374"
---
# <a name="how-to-use-the-wpf-tree-visualizer"></a>方法: WPF ツリー ビジュアライザーを使用する
WPF ツリー ビジュアライザーを使用すると、WPF オプションのビジュアル ツリーを調べたり、ツリーに含まれるオブジェクトの WPF 依存関係プロパティを表示したりすることができます。 ビジュアル ツリーの詳細については、次を参照してください。 [WPF のツリー](/dotnet/framework/wpf/advanced/trees-in-wpf)します。 依存関係プロパティの詳細については、次を参照してください。[依存関係プロパティの概要](/dotnet/framework/wpf/advanced/dependency-properties-overview)します。

 WPF ツリー ビジュアライザーを開くと、2 つのペインが表示されます。**ビジュアル ツリー**左側、**プロパティの**_名前_ **:** _型_右側のウィンドウ。 内のオブジェクトを選択、**ビジュアル ツリー**ウィンドウで、および**のプロパティ**_名前_ **:** _型_ペインがそのオブジェクトのプロパティを表示する自動的に更新されます。

### <a name="to-open-the-wpf-tree-visualizer"></a>WPF ツリー ビジュアライザーを開くには

1. データヒント、 **[ウォッチ]** ウィンドウ、 **[自動変数]** ウィンドウ、または **[ローカル]** ウィンドウで、WPF オブジェクト名の横の、虫眼鏡アイコンの横にある矢印をクリックします。

     ビジュアライザーの一覧が表示されます。

2. **[WPF ツリー ビジュアライザー]** をクリックします。

### <a name="to-search-the-visual-tree"></a>ビジュアル ツリーを検索するには

- **[ビジュアル ツリー]** ウィンドウで、検索する文字列を **[検索]** ボックスに入力します。

  WPF ツリー ビジュアライザーで、入力した文字列と一致するビジュアル ツリー内の最初のオブジェクトが即時に検索されます。 より正確に一致する項目を検索するには、次の文字を入力します。

  - ビジュアル ツリー内の次の一致項目に移動するには、 **[次へ]** をクリックします。

  - 前の一致項目に戻るには、 **[前へ]** をクリックします。

  - 検索条件を消去するには、 **[クリア]** をクリックします。

### <a name="to-search-the-properties-list"></a>プロパティ リストを検索するには

- **プロパティの**_名前_ **:** _型_ウィンドウ内で検索する文字列を入力、 **をフィルター処理**ボックス。

  WPF ツリー ビジュアライザーで、入力した文字列と一致するプロパティが即時に検索され、入力した文字列と一致したこれらのプロパティのみが一覧に表示されます。 より正確に一致する項目を検索するには、次の文字を入力します。

  - 検索条件を消去するには、 **[クリア]** をクリックします。

### <a name="to-close-the-visualizer"></a>ビジュアライザーを閉じるには

- ダイアログ ボックスの右上隅にある **[閉じる]** をクリックします。

## <a name="see-also"></a>関連項目
- [カスタム ビジュアライザーを作成する](../debugger/create-custom-visualizers-of-data.md)
- [WPF のツリー](/dotnet/framework/wpf/advanced/trees-in-wpf)
- [依存関係プロパティの概要](/dotnet/framework/wpf/advanced/dependency-properties-overview)
