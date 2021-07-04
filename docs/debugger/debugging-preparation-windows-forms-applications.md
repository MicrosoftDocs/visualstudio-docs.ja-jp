---
title: Windows フォームアプリのデバッグを準備する | Microsoft Docs
description: Visual Studio で Windows フォーム プロジェクト テンプレートによって作成された Windows フォーム アプリケーションをデバッグするための準備手順を行います。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging Windows applications
- Windows applications, debugging
- debugging [Visual Studio], Windows applications
- debugging [C#], Windows applications
- debugging [Visual Basic], Windows applications
ms.assetid: 7092ee7f-8378-4def-aef8-1695bd97cf14
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c2181fe0b0189b0c0472f4d7cadd6a7c8e172a9b
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112387750"
---
# <a name="debugging-preparation-windows-forms-applications"></a>デバッグの準備: Windows フォーム アプリケーション

Windows フォーム アプリ プロジェクト テンプレートを使用すると、Windows フォーム アプリケーションが作成されます。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] では、この種類のアプリケーションを簡単にデバッグできます。 この種類のプロジェクトを作成する方法については、[Windows フォーム アプリの作成](../ide/create-csharp-winform-visual-studio.md)に関する記事を参照してください。

 プロジェクト テンプレートを使用して Windows フォーム プロジェクトを作成する場合、デバッグ構成とリリース構成に必要な設定は [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] によって自動的に作成されます。 この設定は必要に応じて変更できます。 設定の変更は、 **[\<project name> プロパティ ページ]** ダイアログ ボックス (Visual Basic の場合は **[マイ プロジェクト]** ) で行います。

 詳細については、「[プロパティの推奨設定](../debugger/managed-debugging-recommended-property-settings.md)」を参照してください。

 推奨される追加のプロパティ設定を次の表に示します。

### <a name="configuration-properties-in-debug-tab"></a>[デバッグ] タブの構成プロパティ

|**プロパティ名**|**設定**|
|-----------------------|-----------------|
|**開始動作**|ほとんどの場合、 **[スタート プロジェクト]** に設定します。 デバッグの開始時に他の実行可能ファイルを起動する場合 (通常は DLL をデバッグする場合) には、 **[外部プログラムの開始]** に設定します。|

 Windows フォーム アプリケーションは、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 内から、または既に実行中のアプリケーションにアタッチすることによってデバッグできます。 アタッチの詳細については、[実行中のプロセスへのアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)に関するページを参照してください。

### <a name="to-debug-a-c-f-or-visual-basic-windows-forms-application"></a>C#、F#、または Visual Basic の Windows フォーム アプリケーションをデバッグするには

1. [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] でプロジェクトを開きます。

2. 必要に応じて、ブレークポイントを作成します。

    Windows フォーム アプリケーションはイベント ドリブンであるため、ブレークポイントはイベント ハンドラー コード内またはイベント ハンドラー コードによって呼び出されるメソッド内に設定します。 ブレークポイントが配置される一般的なイベントは次のとおりです。

   1. Click、Enter などのコントロールに関連付けられたイベント。

   2. Load、Activated など、アプリケーションの起動またはシャットダウンに関連付けられたイベント。

   3. フォーカス イベントと検証イベント。

      詳細については、「[Windows フォーム内でのイベント ハンドラーの作成](/dotnet/framework/winforms/creating-event-handlers-in-windows-forms)」を参照してください。

3. **[デバッグ]** メニューの **[開始]** をクリックします。

4. 「[デバッガーでのはじめに](../debugger/debugger-feature-tour.md)」で説明されている手法を使用してデバッグ ます。

## <a name="see-also"></a>関連項目
- [マネージド コードをデバッグする](../debugger/debugging-managed-code.md)
- [C#、F#、および Visual Basic のプロジェクト](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)
- [方法: デバッグ構成とリリース構成を設定する](../debugger/how-to-set-debug-and-release-configurations.md)
- [C# デバッグ構成のプロジェクト設定](../debugger/project-settings-for-csharp-debug-configurations.md)
- [Visual Basic デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)
- [実行中のプロセスへのアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)
- [Windows フォーム](/dotnet/framework/winforms/index)