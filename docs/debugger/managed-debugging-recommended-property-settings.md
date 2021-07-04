---
title: C#、VB で推奨されるデバッガー プロパティ設定 | Microsoft Docs
description: すべてのマネージド デバッグで同じである必要がある、ビルドとコンパイルのプロパティ設定を確認します。 その他の設定は、プロジェクトの種類によって異なる場合があります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], managed
- debugging managed code, recommended property settings
ms.assetid: 3d14a8d4-2925-44d0-be41-ec546d411db9
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: c2262194dbb6a8f4b0a47b4fcfc7f9f696c60167
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390399"
---
# <a name="managed-debugging-recommended-property-settings"></a>マネージド デバッグ:プロパティの推奨設定
一部のプロパティは、すべてのマネージド デバッグ シナリオで同じように設定する必要があります。

 プロパティの推奨設定を以下に示します。

 ここに記載されていない設定は、マネージド プロジェクトの種類によって異なる場合があります。 たとえば、 **[開始動作]** は、Windows フォーム プロジェクトと [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] プロジェクトとで設定が異なります。

### <a name="configuration-properties-on-the-build-c-or-compile-visual-basic-tab"></a>[ビルド] タブ (C#) または [コンパイル] タブ (Visual Basic) の構成プロパティ

|**プロパティ名**|**設定**|
|-----------------------|-----------------|
|**定数 DEBUG の定義**|C# および F#: チェック ボックスをオンに設定します。 これにより、アプリケーションで Debug クラスを使用できます。|
|**定数 TRACE の定義**|C# および F#: チェック ボックスをオンに設定します。 これにより、アプリケーションで Trace クラスを使用できます。|
|**コードの最適化**|C#、F#、および Visual Basic: false に設定します。 最適化されたコードは、生成された命令がソース コードと直接対応していないため、デバッグが困難です。 プログラムで、最適化されたコードだけに現れるバグが見つかった場合は、この設定を有効にできます。 **[逆アセンブル]** ウィンドウに表示されるコードは最適化されたソースから生成されているため、コード エディターに表示されるコードとは一致しない可能性があります。 最適化されたコードをデバッグするには、[マイ コードのみ] をオフにする必要があります。 (「[ステップ実行をマイ コードのみに制限する](../debugger/navigating-through-code-with-the-debugger.md#BKMK_Restrict_stepping_to_Just_My_Code)」を参照)。<br /><br /> 詳細については、「[C# デバッグ構成のプロジェクト設定](../debugger/project-settings-for-csharp-debug-configurations.md)」または「[Visual Basic デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)」を参照してください。|
|**出力パス**|bin\Debug\\ に設定します。|
|**詳細コンパイル オプション**|Visual Basic のみ。 **[詳細]** をクリックして、次の表に示す詳細なプロパティを設定できるようにします。|

### <a name="advanced-compiler-settings-dialog-box"></a>[ビルドの詳細設定] ダイアログ ボックス

|**プロパティ名**|**設定**|
|-----------------------|-----------------|
|**最適化を有効にする**|上の表の **[コードの最適化]** オプションと同じ理由で false に設定します。|
|**デバッグ情報の生成**|このチェック ボックスをオンにすると、コンパイル時に /DEBUG フラグが設定され、デバッグを円滑に実行するうえで必要な情報が生成されます。|
|**定数 DEBUG の定義**|このチェック ボックスをオンにすると、`DEBUG` 定数が定義され、アプリケーションで <xref:System.Diagnostics.Debug> クラスを使用できるようになります。|
|**定数 TRACE の定義**|このチェック ボックスをオンにすると、`TRACE` 定数が定義され、アプリケーションで <xref:System.Diagnostics.Trace> クラスを使用できるようになります。|

## <a name="see-also"></a>関連項目
- [マネージド コードをデバッグする](../debugger/debugging-managed-code.md)
- [C#、F#、および Visual Basic のプロジェクト](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)