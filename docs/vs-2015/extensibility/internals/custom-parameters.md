---
title: カスタム パラメーター |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- wizards, custom parameters
- custom parameters
ms.assetid: ba5c364b-66e6-47ea-9760-a0b70de8f0a0
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1a595861be835ec1aaa7079b3e3fe1962d5055e9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68154989"
---
# <a name="custom-parameters"></a>カスタム パラメーター
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

カスタム パラメーターは、ウィザードが開始した後に、ウィザードの操作を制御します。 関連の .vsz ファイルは、統合開発環境 (IDE) によってパッケージ化され、ウィザードが開始されると、文字列の配列として、ウィザードに渡されますユーザー定義のパラメーターの配列を提供します。 ウィザードは、文字列の配列を解析し、情報を使用して、ウィザードの実際の操作を制御します。 この方法で、ウィザードは、.vsz ファイルの内容に応じて機能をカスタマイズできます。  
  
 コンテキストのパラメーターは、ウィザードの開始時にその一方で、プロジェクトの状態を定義します。 詳細については、次を参照してください。[コンテキスト パラメーター](../../extensibility/internals/context-parameters.md)します。  
  
 カスタム パラメーターを持つ .vsz ファイルの例を次に示します。  
  
```  
VSWIZARD 8.0  
Wizard=VsWizard.VsWizard_Engine  
Param="WIZARD_NAME = Sample Wizard"  
Param="WIZARD_UI = FALSE"  
Param="RELATIVE_PATH = VSWizards\Classwiz\ATL"  
Param="PREPROCESS_FUNCTION = CanAddATLSupport"  
Param="PROJECT_TYPE = CSPROJ"  
```  
  
 .Vsz ファイルの作成者は、パラメーターの値を追加します。 ユーザーが選択すると**新しいプロジェクト**または**新しい項目の追加**でプロジェクトを右クリックし、[ファイル] メニュー**ソリューション エクスプ ローラー**IDE の配列にこれらの値を収集します文字列。 IDE を呼び出して、プロジェクトの<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.AddItem%2A>メソッドを<xref:Microsoft.VisualStudio.Shell.Interop.VSADDITEMOPERATION>フラグのセット、およびプロジェクトの呼び出し、<xref:EnvDTE.IVsExtensibility.RunWizardFile%2A>ウィザードを実行し、結果を返すことを担当するメソッド。  
  
 ウィザードは、文字列の配列を解析し、文字列に対して適切に機能する責任を負います。 カスタム パラメーターを実装することで、この方法でさまざまな機能を実行する 1 つのウィザードを作成できます。 つまり、1 つのウィザードでは、3 つの異なる .vsz ファイルを可能性があります。 各ファイルは、異なるさまざまな状況で、ウィザードの動作を制御するカスタムのパラメーターのセットを渡します。  
  
 詳細については、次を参照してください。[ウィザード (します。Vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)します。  
  
## <a name="see-also"></a>関連項目  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>   
 [コンテキスト パラメーター](../../extensibility/internals/context-parameters.md)   
 [ウィザード](../../extensibility/internals/wizards.md)   
 [ウィザード (.Vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)
