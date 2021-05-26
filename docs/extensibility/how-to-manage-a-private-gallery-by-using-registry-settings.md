---
title: レジストリ設定を使用してプライベート ギャラリーを管理する
description: Visual Studio ギャラリー、サンプル ギャラリー、またはプライベート ギャラリーで、コントロール、テンプレート、およびツールへのアクセスを制御する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSIX private galleries, managing
- managing VSIX private galleries
ms.assetid: 86b86442-4293-4cad-9fe2-876eef65f426
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5981dc4399e09df207b154b900fa163895c344c9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070064"
---
# <a name="how-to-manage-a-private-gallery-by-using-registry-settings"></a>方法: レジストリ設定を使用してプライベート ギャラリーを管理する
管理者、または Isolated Shell 拡張機能の開発者は、Visual Studio ギャラリー、サンプル ギャラリー、またはプライベート ギャラリーで、コントロール、テンプレート、およびツールへのアクセスを制御できます。 ギャラリーを利用できるようにする、または使用できないようにするには、変更するレジストリ キーとその値を記述した *.pkgdef* ファイルを作成します。

## <a name="manage-private-galleries"></a>プライベート ギャラリーの管理
 複数のコンピューター上にあるギャラリーへのアクセスを制御するために、 *.pkgdef* ファイルを作成できます。 このファイルは、次の形式にする必要があります。

```
[$RootKey$\ExtensionManager\Repositories\{UniqueGUID}]
@={URI}  (REG_SZ)
Disabled=0 | 1 (DWORD)
Priority=0 (highest priority) ... MaxInt (lowest priority) (DWORD) (uint)
Protocol=Atom Feed|Sharepoint (REG_SZ)
DisplayName={DisplayName} (REG_SZ)
DisplayNameResourceID={ID} (REG_SZ)
DisplayNamePackageGuid={GUID} (REG_SZ)

```

 `Repositories` キーは、有効または無効にするギャラリーを参照します。 Visual Studio ギャラリーとサンプル ギャラリーでは、次のリポジトリ GUID を使用します。

- Visual Studio ギャラリー: 0F45E408-7995-4375-9485-86B8DB553DC9

- サンプル ギャラリー: AEB9CB40-D8E6-4615-B52C-27E307F8506C

  `Disabled` 値はオプションです。 既定では、ギャラリーは有効になっています。

  `Priority` 値では、 **[オプション]** ダイアログ ボックスでギャラリーが表示される順序を決定します。 Visual Studio ギャラリーの優先度は 10 で、サンプル ギャラリーの優先度は 20 です。 プライベート ギャラリーは、優先度 100 で開始します。 複数のギャラリーに同じ優先度値が設定されている場合、それらが表示される順序は、ローカライズされた `DisplayName` 属性の値によって決まります。

  `Protocol` 値は、Atom ベースまたは SharePoint ベースのギャラリーで必須です。

  `DisplayName`、または `DisplayNameResourceID` と `DisplayNamePackageGuid` の両方を指定する必要があります。 すべてを指定した場合は、`DisplayNameResourceID` と `DisplayNamePackageGuid` のペアが使用されます。

## <a name="disable-the-visual-studio-gallery-using-a-pkgdef-file"></a>.pkgdef ファイルを使用して Visual Studio ギャラリーを無効にする
 *.pkgdef* ファイルでギャラリーを無効にすることができます。 次のエントリでは、Visual Studio ギャラリーを無効にします。

```
[$RootKey$\ExtensionManager\Repositories\{0F45E408-7995-4375-9485-86B8DB553DC9}]
"Disabled"=dword:00000001

```

 次のエントリでは、サンプル ギャラリーを無効にします。

```
[$RootKey$\ExtensionManager\Repositories\{AEB9CB40-D8E6-4615-B52C-27E307F8506C}]
"Disabled"=dword:00000001

```

## <a name="see-also"></a>関連項目
- [プライベート ギャラリー](../extensibility/private-galleries.md)
