---
title: DOM Explorer を使用してレイアウトのデバッグ |Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- box model [Windows Store apps], viewing
- debugging layout [Windows Store apps]
- layout, debugging [Windows Store apps]
ms.assetid: ded6566d-fc29-49a7-8029-dee8e50fe733
caps.latest.revision: 36
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ba06e6a8ba95887c0cc6b6acfd14cef10ff03798
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2018
ms.locfileid: "51787757"
---
# <a name="debug-layout-using-dom-explorer"></a>DOM Explorer を使用したレイアウトのデバッグ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Windows および Windows Phone に適用されます] (../Image/windows_and_phone_content.png"windows_and_phone_content")  
  
 DOM Explorer の **[レイアウト]** タブには、 [アプリ、Windows Phone ストア アプリ、または Visual Studio Tools for Apache Cordova を使用して作成されたアプリで選択される要素について、](http://go.microsoft.com/fwlink/?LinkID=238778) CSS ボックス モデル [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] が表示されます。 このボックス モデルのビジュアル表現を使用して、要素の外観に影響するレイアウト関連の値を特定して変更することができます。  
  
> [!TIP]
>  **[レイアウト]** タブで行った変更は永続的ではありません。 ソース コードを永続的に変更してアプリを更新するには、[デバッグ] ツール バーの **[Windows アプリケーションの更新]** ボタン (Windows ストア アプリと Windows Phone ストア アプリのみ) を使用します。 これにより、デバッガーを再起動せずに済みます。  
  
 DOM Explorer を使用して、ボックス モデルに表示されないレイアウトの側面を変更する、次を参照してください。[クイック スタート: デバッグの HTML および CSS](../debugger/quickstart-debug-html-and-css.md)と[DOM Explorer を使用してデバッグの CSS スタイル](../debugger/debug-css-styles-using-dom-explorer.md)します。  
  
## <a name="example-of-fixing-a-layout-issue"></a>レイアウトの問題の修正例  
 この例では、ハブ/ピボット テンプレートでリスト要素を選択し、 **[レイアウト]** タブに表示されるボックス モデルの値を解釈します。その後、プロパティ値のいずれかを変更してレイアウトの問題を修正します。  
  
#### <a name="to-fix-the-layout-issue"></a>レイアウトの問題を修正するには  
  
1.  Visual Studioで、ハブ/ピボット テンプレートを使用する新しいストア アプリを作成します。  
  
2.  共有のページ/ハブ フォルダーで、hub.css を開きます。  
  
3.  次の CSS コードを  
  
    ```css  
    .hubpage .hub .section4 .sub-image-row img {  
        height: 95px;  
        width: 130px;  
    }  
    ```  
  
     次の CSS コードに置き換えます。  
  
    ```css  
    .hubpage .hub .section4 .sub-image-row img {  
        height: 95px;  
        width: 130px;  
        margin-left: 5em;  
    }  
    ```  
  
4.  ソリューション エクスプローラーで、appName.WindowsPhone プロジェクトまたは appName.Windows プロジェクトを選択し、次にプロジェクトのショートカット メニューから **[スタートアップ プロジェクトに設定]** を選択します。  
  
5.  スタートアップ プロジェクトにより、デバッグ ツールバーのドロップダウン リストから **[Emulator 8.1 WVGA 4 inch 512MB]** または **[シミュレーター]** のどちらかを選択します (既定値は **[ローカル コンピューター]** )。  
  
     ![デバッグ対象を選択する](../debugger/media/js-dom-debug-target-emu.png "JS_DOM_Debug_Target_Emu")  
  
6.  F5 キーを押して、アプリをデバッグ モードで実行します。  
  
7.  スクロールまたはフリックの操作によって、セクション 4 を開きます。  
  
    > [!TIP]
    >  Phone エミュレーターまたは シミュレーターを Visual Studio のウィンドウの横に配置して、CSS スタイルに対して行った選択と変更の結果をすぐに確認できるようにします。  
  
     セクション 4 が読み込まれると、下側のイメージが正しく表示されていないことが分かります。 各項目のイメージが半分しか表示されません (左半分が表示されません)。  
  
8.  Visual Studio に切り替え、DOM Explorer で **[要素の選択]** をクリックします (または Ctrl + B キーを押します)。 これで選択モードが変更され、項目をクリックで選択できるようになります。同時に、アプリが前面に表示されます。 モードは、シングルクリックで元に戻ります。  
  
    > [!TIP]
    >  DOM Explorer で HTML 要素を直接選択するために、矢印キーや他のメソッドを使用することもできます。 要素を選択する方法の詳細については、次を参照してください。[クイック スタート: デバッグの HTML および CSS](../debugger/quickstart-debug-html-and-css.md)します。  
  
9. Phone エミュレーターまたはシミュレーターで、半分にカットされたイメージの 1 つのグレーの右半分を選択します。 Windows Phone エミュレーターに示すように、選択された要素の周囲に強調表示があります。  
  
     ![DOM 要素の選択](../debugger/media/js-css-layout-select.png "JS_CSS_Layout_Select")  
  
    > [!TIP]
    >  このシミュレーターでは、DOM 要素の 1 つを選択する前にそれらの周りを強調表示するボックスを表示するために、要素上のホバーリングをサポートしています。 Windows Phone エミュレーターは、この機能をサポートしていません。  
  
     DOM 要素を選択するときに、DOM Explorer は Visual Studio の対応する IMG 要素を自動的に選択します。 DOM エクスプローラーで選択された要素は次のようになります。  
  
    ```html  
    <img src="ms-appx://guid/images/gray.png>   
    </img>  
    ```  
  
10. **[レイアウト]** タブをクリックします。このタブは、次の Windows Phone エミュレーターに示すように、選択した要素のボックス モデルを示します。  
  
     ![DOM Explorer の [レイアウト] タブ](../debugger/media/js-css-layout.png "JS_CSS_Layout")  
  
     このビューは、要素に関する有用な情報を提供します。  
  
    -   表示される色は、シミュレーターで要素にマウス ポインターを置いたときに反転表示されるボックスに対応しています。 青の色が表す、 \<img > 要素の大きさ。 ベージュは余白の値を表します。  
  
    -   左余白 (margin-left) が設定されています。これは、イメージの左側が黒くなるという現象に関連するため、問題の原因を特定するヒントになります。  
  
    -   各ボックス (たとえば、[境界線] および [パディング]) には、0 ピクセルの値が表示されます。これは対応する CSS プロパティが設定されていないことを暗示しています。  
  
11. margin-left 規則がどのように適用されるかを確認するために、 **[計算済み]** タブをクリックし、margin-left 規則を調べます。 この規則が 5em 値で設定されていることを確認できますが、計算値は、対象デバイスによって 66.66px または 146.66px となります。  
  
    > [!TIP]
    >  **計算済み** タブの margin-left 規則設定されていることが表示されます、 `..hubpage .hub. section4 .sub-image-row img` CSS セレクターで、hub.css を記載します。 このデモ アプリでは、その設定を修正する必要があります。  
  
     **[レイアウト]** タブを使用して、レイアウトの値の変更をテストすることもできます。  
  
12. **[レイアウト]** タブでは、 **[余白]** ボックスの左側にある **[66.66]** または **[146.66]** を選択します。  
  
13. 「 `0` 」と入力し、Enter キーを押します。 (上方向キーと下方向キーを使用して値を変更することもできます。)  
  
14. その他、 \<img > 要素は DOM Explorer で、左余白の値を 0 に変更します。  
  
15. Phone エミュレーターまたはシミュレーターに切り替えます。 更新された左余白の値がセクション 4 のイメージに適用されています。 これらの値は、margin-left 規則の **[計算済み]** タブでも更新されます。  
  
## <a name="see-also"></a>関連項目  
 [クイック スタート: HTML と CSS をデバッグします。](../debugger/quickstart-debug-html-and-css.md)   
 [DOM Explorer を使用して CSS スタイルをデバッグします。](../debugger/debug-css-styles-using-dom-explorer.md)   
 [DOM イベント リスナーの表示](../debugger/view-dom-event-listeners.md)



