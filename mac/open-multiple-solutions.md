---
title: '方法: 複数のソリューションを開く'
description: Visual Studio for Mac で複数のソリューションを開く方法、およびアプリケーションの複数のインスタンスを開く方法について説明します。
author: asb3993
ms.author: amburns
ms.date: 07/19/2018
ms.assetid: 592BA4E3-8DEF-4FCD-8BA0-519A4CEEE03E
ms.openlocfilehash: 85d300c5131dad2d6f4480fceb4770e2e8a126a5
ms.sourcegitcommit: b544e2157ac20866baf158eef9cfed3e3f1d68b9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/01/2018
ms.locfileid: "39388494"
---
# <a name="opening-multiple-solutions-or-instances-of-visual-studio-for-mac"></a>Visual Studio for Mac の複数のソリューションまたはインスタンスを開く

既定では、Visual Studio for Mac など、Mac のすべてのアプリケーションは、"_単一インスタンス_" アプリです。 つまり、使いたいアプリケーションが既に開かれている場合 (ドックのアイコンの下の "ドット" で示されます)、アイコンを再度クリックすると、新しいインスタンスではなく、実行中のインスタンスが開かれます。  [次のセクション](#open-a-second-instance-of-visual-studio-for-mac)で説明するように、アプリケーションのインスタンスを追加する必要がある場合は、インスタンスを開くようシステムに指示できます。

さらに、ソリューションを開くときは、新しいワークスペースでソリューションを開き、現在のワークスペースを閉じる (必要な場合) のが既定の動作です。 「[単一のインスタンス内で 2 つ目のソリューションを開く](#open-a-second-solution-inside-a-single-instance)」セクションで説明されているように、現在のワークスペースを開いたままにすることで、この既定の動作をオーバーライドできます。

## <a name="open-a-second-instance-of-visual-studio-for-mac"></a>Visual Studio for Mac の 2 つ目のインスタンスを開く

IDE の 2 つ目のインスタンスを開くには、**ターミナル** アプリケーションを開いて、次の行を入力します。

```bash
open -n "/Applications/Visual Studio.app"
```

## <a name="open-a-second-solution-inside-a-single-instance"></a>単一のインスタンス内で 2 つ目のソリューションを開く

1 つ目のソリューションをそのままにして 2 つ目のソリューションを開くには、次の手順を使います。

1. 1 つ目のソリューションを既に開いた状態で、**[ファイル] > [開く]** を選択します。
2. ファイル システムを参照して、既存のソリューションを検索します。
3. **.sln** ファイルを選択して、**[オプション]** ボタンを選択します。
    
    ![[オプション] ボタンの場所](media/open-multiple-solutions-image3.png)
4. **[現在のワークスペースを閉じる]** ボックスをオフにします。

    ![現在のワークスペースのスクリーンショット](media/open-multiple-solutions-image1.png)

1. [開く] ボタンを選択して、Solution Pad で 2 つ目のソリューションを開きます。

**または**、最近ソリューションを開いた場合は、次の手順を使うこともできます。

1. [ファイル] > [最近のソリューション] メニュー項目に移動します。

    ![[最近のソリューション] メニューのスクリーンショット](media/open-multiple-solutions-image2.png)

1. **Ctrl** キーを押しながら、ソリューションを選択します。 この組み合わせにより、Solution Pad で 2 つ目のソリューションが開きます。
