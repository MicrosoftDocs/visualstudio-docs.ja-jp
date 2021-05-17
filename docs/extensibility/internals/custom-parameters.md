---
title: カスタム パラメーター | Microsoft Docs
description: .vsz ファイルを変更して、ウィザードが開始された後にウィザードの操作を制御するカスタム パラメーターを作成する方法を学習します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- wizards, custom parameters
- custom parameters
ms.assetid: ba5c364b-66e6-47ea-9760-a0b70de8f0a0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3e5d8d9bf78f06dd55a88a2fbd47749224be3949
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091098"
---
# <a name="custom-parameters"></a>カスタム パラメーター
カスタム パラメーターは、ウィザードが開始された後のウィザードの操作を制御します。 関連する *.vsz* ファイルは、統合開発環境 (IDE) によってパッケージ化され、ウィザードの開始時に文字列の配列としてウィザードに渡される、ユーザー定義パラメーターの配列を提供します。 その後、ウィザードは、文字列の配列を解析し、その情報を使用してウィザードの実際の操作を制御します。 ウィザードでは、この方法で、 *.vsz* ファイルの内容に応じて機能をカスタマイズすることができます。

 一方、コンテキスト パラメーターは、ウィザードの開始時のプロジェクトの状態を定義します。 詳細については、[コンテキスト パラメーター](../../extensibility/internals/context-parameters.md)に関するページを参照してください。

 カスタム パラメーターを持つ *.vsz* ファイルの例を次に示します。

```
VSWIZARD 8.0
Wizard=VsWizard.VsWizard_Engine
Param="WIZARD_NAME = Sample Wizard"
Param="WIZARD_UI = FALSE"
Param="RELATIVE_PATH = VSWizards\Classwiz\ATL"
Param="PREPROCESS_FUNCTION = CanAddATLSupport"
Param="PROJECT_TYPE = CSPROJ"
```

 *.vsz* ファイルの作成者は、パラメーターの値を追加します。 ユーザーが **[ファイル]** メニューで、または **ソリューション エクスプローラー** でプロジェクトを右クリックして、 **[新しいプロジェクト]** または **[新しい項目の追加]** を選択すると、IDE によってこれらの値が文字列の配列に収集されます。 その後、IDE は <xref:Microsoft.VisualStudio.Shell.Interop.VSADDITEMOPERATION> フラグが設定されたプロジェクトの <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.AddItem%2A> メソッドを呼び出し、プロジェクトはウィザードを実行して結果を返す <xref:EnvDTE.IVsExtensibility.RunWizardFile%2A> メソッドを呼び出します。

 ウィザードは、文字列の配列を解析し、文字列を適切に処理する役割を果たします。 このようにして、カスタム パラメーターを実装することで、さまざまな機能を実行する 1 つのウィザードを作成できます。 言い換えると、1 つのウィザードには 3 つの異なる *.vsz* ファイルが含まれていることがあります。 各ファイルは、さまざまな状況でウィザードの動作を制御するために、さまざまなカスタム パラメーターのセットを渡します。

 詳細については、[ウィザード (.vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)に関するページを参照してください。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>
- [コンテキスト パラメーター](../../extensibility/internals/context-parameters.md)
- [ウィザード](../../extensibility/internals/wizards.md)
- [ウィザード (.vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)
