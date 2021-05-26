---
title: ファイル名拡張子について | Microsoft Docs
description: VSPackage のファイル名拡張子を登録して、Visual Studio の特定のバージョンに関連付ける方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- file extensions
- file name extensions
ms.assetid: 99f4f9ff-fb84-4258-9787-6890f308a57f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f38bee1b62340f7d557ac2e5190fc5c48d9268fe
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060147"
---
# <a name="about-file-name-extensions"></a>ファイル名拡張子について
VSPackage のファイル拡張子を登録すると、それを [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] のバージョンに関連付けることになります。 これは、1 台のコンピューターに複数のバージョンの [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] がインストールされている場合に重要です。

 VSPackage のファイル拡張子は、関連付けられているプログラム ID (ProgID) をポイントする既定値と共に **HKEY_CLASSES_ROOT** キーの下に登録されます。

 次の例では、 *.vcproj* ファイル拡張子の登録情報を示します。

```
HKEY_CLASSES_ROOT\
   .vcproj\
      (default)=" VisualStudio.vcproj.8.0"
```

 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] に関連付けられたファイルには、`VisualStudio.vcproj.8.0` のようにバージョン管理された ProgID が必要です。 バージョン付きの ProgID により、製品のバージョン間のファイル拡張子の関連付けを維持するために、製品をサイド バイ サイドでインストールできます。 また、バージョン固有の ProgID を使用すると、上書きや、の他のアプリケーションや [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] のバージョンによる上書きを気にすることなく、標準の動詞 (open、edit など) を使用することもできます。

 場合によっては、ファイル拡張子に関連付けられている ProgID を変更してはなりません。 たとえば、 *.htm* ファイル拡張子の ProgID (progid = htmlfile) は、オペレーティング システムのさまざまな場所にハード コーディングされており、 *.htm* ファイルと *.html* ファイルとの関連付けで広く知られています。

## <a name="see-also"></a>関連項目
- [サイド バイ サイドの配置に対してファイル名拡張子を登録する](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)
- [ファイル名拡張子のファイル ハンドラーを指定する](../extensibility/specifying-file-handlers-for-file-name-extensions.md)
