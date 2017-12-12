---
title: "ユーザー補助 | Microsoft Docs"
description: 
author: asb3993
ms.author: amburns
ms.date: 08/15/2017
ms.topic: article
ms.assetid: 2C4AAC2E-3B4A-4496-8BE0-1F5A7F81D1CA
ms.openlocfilehash: 13c69a1c13507a0f856bc652f7ffa0e5ab233081
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2017
---
# <a name="accessibility"></a>ユーザー補助

Visual Studio for Mac は、macOS の機能およびユーティリティに加えて、以下の機能を備えているため、障碍のある方でも、これまで以上に使いやすくなっています。

- Solution Pad とエディター パッドでのテキストの拡大
- エディター内のテキスト サイズ オプション
- エディター内の色のカスタマイズ
- キーボード ショートカットのカスタマイズ
- メソッドおよびパラメーターのコード補完機能 

macOS のユーザー補助機能の詳細については、[Apple 社の Web サイト](https://www.apple.com/accessibility/mac/)をご覧ください。

## <a name="using-accessibility-features-in-visual-studio-for-mac"></a>Visual Studio for Mac でユーザー補助機能を使用する

Visual Studio for Mac のユーザー補助機能は、既定では無効になっています。 有効にするには、次の手順に従います。

1. **[Visual Studio] > [ユーザー設定] > [その他] > [アクセシビリティ]** の順に移動します。

2. 次の図で示すように、**[Enable Accessibility]\(アクセシビリティを有効にする\)** チェックボックスを選択します。

    ![[Enable Accessibility]\(アクセシビリティを有効にする\) チェックボックス](media/accessibility-image1.png)

3. **[Visual Studio を再起動]** ボタンを押し、ユーザー補助機能を有効にします。


または、コマンド ラインを使用してユーザー補助機能を有効にすることもできます。 これを行うには、ターミナルで次のコマンドを入力します。 

```bash
defaults write com.microsoft.visual-studio com.monodevelop.AccessibilityEnabled 1 
```

ユーザー補助機能を有効にした後、Visual Studio を再起動する必要があります。

## <a name="how-to-use-keyboard-navigation"></a>キーボード ナビゲーションを使用するには

キーボード ナビゲーションを有効にするには、**[システム環境設定] > [キーボード] > [ショートカット]** のフル キーボード アクセス オプションを、**[すべてコントロール]** に設定します。

  ![macOS の [システム環境設定] パネル](media/accessibility-image2.png)

フル キーボード アクセスの設定をオンにしたことで、四角形のフォーカスが表示されます。 以下のようにして、コントロールを選択できます。
- Tab キーで次のコントロールに進む
- Shift キーを押しながら Tab キーを押して前のコントロールに戻る
- 方向キーでコントロールの間を矢印の方向に移動する 

スペース バーを押すと、フォーカスされたコントロールがアクティブになります。

## <a name="how-to-enable-and-use-voice-over"></a>読み上げ機能を有効にして使用するには

VoiceOver をオンまたはオフにするには、**Cmd + F5 キー**を押します。

UI VoiceOver コマンドの間を移動するには、次のコマンドを使用します。

- コントロール間で VoiceOver カーソルを移動: **Ctrl + Alt + 左方向キーまたは右方向キー**

VoiceOver は、コントロールの名前、コントールに関するいくつかの詳細、およびそのコントロールで何ができるかを読み上げます。 

- グループやコントロール (例: Solution Pad、ツールボックスなどのパッド) を入力: **Ctrl + Alt + Shift + 下方向キー**

一度コントロール内に入れば、**Ctrl + Alt + 方向キー**を使用して内部を移動できます。 
 
macOS の VoiceOver の使用方法に関する概要については、次のガイドをご覧ください。

- [VoiceOver の概要](https://help.apple.com/voiceover/info/guide/10.12/)
- [macOS の VoiceOver コマンド](http://lab.dotjay.com/notes/voiceover-commands/)
