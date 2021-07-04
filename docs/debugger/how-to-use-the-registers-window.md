---
title: デバッガーでレジスタ値を表示する | Microsoft Docs
description: Visual Studio の [レジスタ] ウィンドウにレジスタの値を表示します。 デバッグ中、アプリでコードが実行されるとレジスタ値が変化します。
ms.custom: SEO-VS-2020
ms.date: 11/19/2018
ms.topic: how-to
f1_keywords:
- vs.debug.registers
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- registers, debugging
- register contents
- flags, Registers window
- register groups
- debugging [Visual Studio], Registers window
- Registers window
ms.assetid: 2918ffa2-562f-40d6-9053-ef321bbeb767
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: e2648f74453f51cd8d655ccb0c2344eb1030c1ed
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112385397"
---
# <a name="view-register-values-in-the-registers-window-c-c-visual-basic-f"></a>[レジスタ] ウィンドウでレジスタ値を表示する (C#、C++、Visual Basic、F#)

**[レジスタ]** ウィンドウには、Visual Studio デバッグ中のレジスタの内容が表示されます。 レジスタの背後にある概念について大まかな概要について、**登録** ウィンドウを参照してください [デバッグの基礎: [レジスタ] ウィンドウ](../debugger/debugging-basics-registers-window.md)します。

> [!NOTE]
> スクリプトまたは SQL アプリのレジスタ情報は表示できません。

デバッグ中、アプリでコードが実行されるとレジスタ値が変化します。 最近変更された値は **[レジスタ]** ウィンドウに赤で表示されます。

**[レジスタ]** ウィンドウでは、見やすいようにレジスタがグループ別に整理されますが、グループはプラットフォームやプロセッサの種類によって異なります。 レジスタ グループの表示と非表示を切り替えることができます。 詳細については、[レジスタ グループの表示と非表示を切り替える](../debugger/how-to-display-and-hide-register-groups.md)」をご覧ください。

**[レジスタ]** ウィンドウに表示されるフラグに関する詳細については、[[レジスタ] ウィンドウの概要](../debugger/debugging-basics-registers-window.md)に関するページを参照してください。

レジスタの値は編集できます。 詳細については、[レジスタ値を編集する](../debugger/how-to-edit-a-register-value.md)」をご覧ください。

**[レジスタ] ウィンドウを開くには**

1. **[ツール]** (または **[デバッグ]** )、 **[オプション]** 、 **[デバッグ]** の順に選択し、 **[アドレス レベルのデバッグを有効にする]** を選択することでアドレスレベルのデバッグを有効にします。

1. デバッグの実行中、あるいはブレークポイントで **[デバッグ]** 、 **[Windows]** 、 **[レジスタ]** の順に選択するか、**Alt**+**5** を押します。

>[!NOTE]
>ダイアログ ボックスとメニュー コマンドは、Visual Studio のエディションや設定によっては異なることがあります。 設定を変更するには、Visual Studio の **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[リセット設定](../ide/environment-settings.md#reset-settings)」を参照してください。

### <a name="see-also"></a>関連項目

- [デバッグの基礎: [レジスタ] ウィンドウ](../debugger/debugging-basics-registers-window.md)
- [デバッガーでのデータ表示](../debugger/viewing-data-in-the-debugger.md)
