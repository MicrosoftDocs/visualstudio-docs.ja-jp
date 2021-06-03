---
title: '方法: フィーチャーの依存関係を追加および削除する | Microsoft Docs'
description: Visual Studio のフィーチャー デザイナーを使用して、SharePoint ソリューションにフィーチャーの依存関係を追加および削除する方法を確認します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- MICROSOFT.VISUALSTUDIO.SHAREPOINT.DESIGNERS.CUSTOMDEPENDENCYWINDOW
- VS.SHAREPOINTTOOLS.RAD.FEATUREDESIGNERDEPENDENCY
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, features
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: ebec7f6b1f6d777ce7b3b914ac5c1d5629190fcc
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99923581"
---
# <a name="how-to-add-and-remove-feature-dependencies"></a>方法: フィーチャーの依存関係を追加および削除する
  SharePoint フィーチャーは、機能またはデータの他のフィーチャーに依存している場合があります。 このような場合は、フィーチャーの依存関係として、これらの他のフィーチャーをマークできます。 これにより、SharePoint サーバーでは、フィーチャーがアクティブ化される前に依存しているフィーチャーがアクティブになります。

## <a name="add-dependencies"></a>依存関係を追加する
 ソリューション内の他のフィーチャーを依存関係として追加できます。 これにより、フィーチャーをインストールする前に、必要なフィーチャーがインストールされ、アクティブ化されることを保証できます。

#### <a name="to-add-a-dependency-on-a-feature-in-the-solution"></a>ソリューションのフィーチャーに依存関係を追加するには

1. フィーチャー デザイナーを開き、 **[フィーチャー アクティブ化依存関係]** ノードを展開し、 **[追加]** ボタンを選択します。

2. **[フィーチャー アクティブ化依存関係の追加]** ダイアログ ボックスで、 **[フィーチャーの依存関係をソリューションに追加する]** オプション ボタンを選択し、依存関係として追加するフィーチャーのタイトルを選択し、 **[追加]** ボタンを選択します。

     複数のフィーチャーを追加するには、**Ctrl** キーを押しながら複数のタイトルを選択します。

## <a name="addi-custom-dependencies"></a>カスタム依存関係を追加する
 SharePoint サーバーに既にデプロイされているフィーチャーを依存関係として追加できます。 これにより、SharePoint のアクティブ化プロセスでは、フィーチャーがインストールされる前にすべての依存フィーチャーがアクティブ化されているかどうかが確認されます。

#### <a name="to-add-a-dependency-by-the-feature-id"></a>フィーチャー ID により依存関係を追加するには

1. フィーチャー デザイナーを開き、 **[フィーチャー アクティブ化依存関係]** ノードを展開し、 **[追加]** ボタンを選択します。

2. **[フィーチャー アクティブ化依存関係の追加]** ダイアログ ボックスで、 **[カスタム依存関係を追加する]** オプション ボタンを選択します。

3. **[フィーチャー ID]** テキスト ボックスに、アクティブ化依存関係としてマークするフィーチャーの GUID を入力し、 **[追加]** ボタンを選択します。

## <a name="edit-custom-dependencies"></a>カスタム依存関係を編集する
 前に追加したカスタム依存関係を編集できます。 ただし、ソリューション内の依存フィーチャーは削除のみ可能であり、編集することはできません。

#### <a name="to-change-a-dependency-on-a-feature-in-the-solution"></a>ソリューション内のフィーチャーの依存関係を変更するには

1. フィーチャー デザイナーを開き、 **[フィーチャー アクティブ化依存関係]** ノードを展開します。

2. 編集するフィーチャーの名前を選択して、 **[編集]** ボタンを選択します。

3. **[カスタム フィーチャー アクティブ化依存関係の編集]** ダイアログ ボックスで、タイトル、フィーチャー ID、または説明を変更し、 **[送信]** ボタンを選択します。

## <a name="remove-dependencies"></a>依存関係を削除する

#### <a name="to-remove-a-dependency-on-a-feature-in-the-solution"></a>ソリューション内のフィーチャーの依存関係を削除するには

1. フィーチャー デザイナーで、 **[フィーチャー アクティブ化依存関係]** ノードを展開し、削除するフィーチャーの名前を選択して、 **[削除]** ボタンを選択します。

## <a name="see-also"></a>関連項目
- [SharePoint フィーチャーを作成する](../sharepoint/creating-sharepoint-features.md)
- [方法: SharePoint フィーチャーをカスタマイズする](../sharepoint/how-to-customize-a-sharepoint-feature.md)
- [方法: SharePoint フィーチャーの項目を追加および削除する](../sharepoint/how-to-add-and-remove-items-to-sharepoint-features.md)
