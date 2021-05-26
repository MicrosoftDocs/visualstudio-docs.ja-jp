---
title: ウィザード インターフェイス (IDTWizard) |Microsoft Docs
description: IDE では、IDTWizard インターフェイスを使用してウィザードと通信します。 IDE でインストールされるために、ウィザードはこのインターフェイスを実装する必要があります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IDTWizard interface
- wizards, interface
ms.assetid: 09618d9d-d115-45b6-bccc-de328994b39c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b8dc88341bc72755ae0f5011d18182c5b78bb483
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074198"
---
# <a name="wizard-interface-idtwizard"></a>ウィザード インターフェイス (IDTWizard)
統合開発環境 (IDE) では、<xref:EnvDTE.IDTWizard> インターフェイスを使用してウィザードと通信します。 IDE でインストールされるために、ウィザードはこのインターフェイスを実装する必要があります。

 <xref:EnvDTE.IDTWizard.Execute%2A> メソッドは、<xref:EnvDTE.IDTWizard> インターフェイスに関連付けられている唯一のメソッドです。 ウィザードではこのメソッドを実装し、IDE ではインターフェイスに対してメソッドを呼び出します。 次の例は、メソッドのシグネチャを示しています。

```
/* IDTWizard Method */
STDMETHOD(Execute)(THIS_
   /* [in] */ IDispatch *Application,
   /* [in] */ long hwndOwner,
   /* [in] */ SAFEARRAY * *ContextParams,
   /* [in] */ SAFEARRAY * *CustomParams,
   /* [out] [in] */ wizardResult *RetVal
   );
```

 起動メカニズムは、 **[新しいプロジェクト]** ウィザードと **[新しい項目の追加]** ウィザードの両方で同様です。 いずれかを起動するには、Dteinternal.h で定義されている <xref:EnvDTE.IDTWizard> インターフェイスを呼び出します。 唯一の違いは、インターフェイスが呼び出されるときにインターフェイスに渡されるコンテキストとカスタム パラメーターのセットです。

 以下の情報では、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE で動作するためにウィザードで実装する必要がある <xref:EnvDTE.IDTWizard> インターフェイスについて説明します。 IDE では、ウィザードで <xref:EnvDTE.IDTWizard.Execute%2A> メソッドを呼び出し、以下を渡します。

- DTE オブジェクト

     DTE オブジェクトは、オートメーション モデルのルートです。

- コード セグメント `hwndOwner ([in] long)` に示されている、ウィンドウ ダイアログ ボックスのハンドル。

     ウィザードでは、この `hwndOwner` をウィザード ダイアログ ボックスの親として使用します。

- コード セグメント `[in] SAFEARRAY (VARIANT)* ContextParams` に示されている、SAFEARRAY のバリアントとしてインターフェイスに渡されるコンテキスト パラメーター。

     コンテキスト パラメーターには、起動中のウィザードの種類に固有の値の配列とプロジェクトの現在の状態が含まれます。 IDE により、コンテキスト パラメーターがウィザードに渡されます。 詳細については、「[コンテキスト パラメーター](../../extensibility/internals/context-parameters.md)」を参照してください。

- コード セグメント `[in] SAFEARRAY (VARIANT)* CustomParams` に示されている、SAFEARRAY のバリアントとしてインターフェイスに渡されるカスタム パラメーター。

     カスタム パラメーターには、ユーザー定義パラメーターの配列が含まれます。 .vsz ファイルにより、IDE にカスタム パラメーターが渡されます。 値は、`Param=` ステートメントによって決定されます。 詳細については、「[カスタム パラメーター](../../extensibility/internals/custom-parameters.md)」を参照してください。

- インターフェイスの戻り値は次のとおりです

    ```
    wizardResultSuccess = -1,
    wizardResultFailure = 0
    wizardResultCancel = 1
    wizardResultBackout = 2
    ```

## <a name="see-also"></a>関連項目
- [コンテキスト パラメーター](../../extensibility/internals/context-parameters.md)
- [カスタム パラメーター](../../extensibility/internals/custom-parameters.md)
- [ウィザード](../../extensibility/internals/wizards.md)
- [ウィザード (.Vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)
