---
title: ウィザード (.Vsz) ファイル |Microsoft Docs
description: IDE がウィザードを起動するために使用する .vsz ファイルについて説明します。 ファイルには、呼び出すウィザードとウィザードに渡す内容に関する情報が含まれています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- .vsz files
- vsz files
- wizards, files
ms.assetid: 72e1d0f3-eef1-455e-b803-96827f030f50
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: de687dae79fa1613090fb400f73ab658ee5d66cb
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900656"
---
# <a name="wizard-vsz-file"></a>ウィザード (.Vsz) ファイル

統合開発環境 (IDE) では、.vsz ファイルを使用してウィザードを起動します。 これらの .vsz ファイルには、どのウィザードを呼び出すか、およびどの情報をウィザードに渡すかを決定するために IDE が使用する情報が含まれています。

.vsz ファイルは、セクションのない .ini 形式のテキスト ファイルのバージョンです。 IDE に知らせる情報は、ファイルの先頭に格納されます。 これにより、IDE が呼び出すウィザードと、IDE に渡される .vsz ファイル内のパラメーターとの間のリンクが提供されます。 ファイルの残りの部分では、ウィザードに固有のパラメーター、および IDE によって収集され、特定のウィザードに渡されるパラメーターが提供されます。

.vsz ファイルの内容の例を次に示します。

```
VSWizard 8.0
Wizard=VsWizard.CBlankSiteWizard -or- {123-1234556-123334}
Param="WIZARDNAME = Wizard One"
Param="WIZARDUI = FALSE"
```

.vsz ファイルの各パーツを次に示します。

|パーツ|説明|
|----------|-----------------|
|VSWizard|ファイルの最初のパラメーターは、テンプレート ファイル形式のバージョン番号です。 このバージョン番号は 6.0、7.0、7.1、または 8.0 である必要があります。 その他の番号は起動できず、無効な形式エラーが発生します。|
|ウィザード|このフィールドには、ウィザードの OLE ProgID、または IDE で一緒に作成されるウィザードの CLSID の GUID 文字列表現が含まれます。|
|Param|これらのパーツはオプションです。 必要な数だけ追加できます。|

パラメーターにより、.vsz ファイルからウィザードに追加のカスタム パラメーターを渡すことができます。 各値は、変数の配列内の文字列要素としてウィザードに渡されます。 詳細については、「[カスタム パラメーター](../../extensibility/internals/custom-parameters.md)」を参照してください。

既定のロケール ID を .vsz ファイルに追加するには、`FALLBACK_LCID`= xxxx を指定します。ここで、xxxx はロケール ID です (たとえば、英語の場合は 1033)。 `FALLBACK_LCID` パラメーターが定義されているとき、現在の ID が見つからない場合、ウィザードでは指定されたフォールバック ロケール ID を使用します。

## <a name="see-also"></a>関連項目

- [カスタム パラメーター](../../extensibility/internals/custom-parameters.md)
- [ウィザード](../../extensibility/internals/wizards.md)
- [テンプレート ディレクトリの説明 (.Vsdir) ファイル](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)
