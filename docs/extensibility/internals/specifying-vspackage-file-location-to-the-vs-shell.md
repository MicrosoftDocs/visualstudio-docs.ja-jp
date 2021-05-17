---
title: VSPackage ファイルの場所を VS Shell に指定する | Microsoft Docs
description: VSPackage を読み込むために Visual Studio でアセンブリ DLL を見つけられるようにする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- managed VSPackages, file location
- VSPackages, managed package file location
ms.assetid: beb8607a-4183-4ed2-9ac8-7527f11513b1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: efec1ac3f7ccb3884265f3740108aaef261e9378
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064082"
---
# <a name="specifying-vspackage-file-location-to-the-vs-shell"></a>VSPackage ファイルの場所を VS Shell に指定する
VSPackage を読み込むためには、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] でアセンブリ DLL を見つけられることが必要です。 次の表で説明するように、さまざまな方法で見つけることができます。

| メソッド | 説明 |
| - | - |
| CodeBase レジストリ キーを使用します。 | 任意の完全修飾ファイル パスから VSPackage アセンブリを読み込むよう、CodeBase キーを使用して [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に指示することができます。 キーの値は DLL のファイル パスである必要があります。 これは、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] にパッケージ アセンブリを読み込ませるための最良の方法です。 この手法を "CodeBase/プライベート インストール ディレクトリの手法" と呼ぶ場合もあります。 登録中に、<xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.RegistrationContext> 型のインスタンスを通じて、コードベースの値が登録属性クラスに渡されます。 |
| DLL を **PrivateAssemblies** ディレクトリに配置します。 | アセンブリを [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ディレクトリの **PrivateAssemblies** サブディレクトリに配置します。 **PrivateAssemblies** にあるアセンブリは自動的に検出されますが、 **[参照の追加]** ダイアログ ボックスには表示されません。 **PrivateAssemblies** と **PublicAssemblies** の違いは、**PublicAssemblies** 内のアセンブリは **[参照の追加]** ダイアログ ボックスで列挙されることです。 "CodeBase/プライベート インストール ディレクトリ" の手法を使用しないことを選択した場合は、**PrivateAssemblies** ディレクトリにインストールする必要があります。 |
| 厳密な名前のアセンブリと Assembly レジストリ キーを使用します。 | Assembly キーを使用して、厳密な名前の VSPackage アセンブリを読み込むよう [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に明示的に指示することができます。 キーの値はアセンブリの厳密な名前である必要があります。 |
| DLL を **PublicAssemblies** ディレクトリに配置します。 | 最後に、アセンブリは **PublicAssemblies** サブディレクトリにも配置できます。 **PublicAssemblies** にあるアセンブリは自動的に検出され、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の **[参照の追加]** ダイアログ ボックスにも表示されます。<br /><br /> VSPackage アセンブリを **PublicAssemblies** ディレクトリに配置する必要があるのは、他の VSPackage 開発者による再利用が意図されているマネージド コンポーネントがアセンブリに含まれている場合だけです。 アセンブリの大部分は、この条件を満たしていません。 |

> [!NOTE]
> すべての依存アセンブリに対して、厳密な名前の署名付きアセンブリを使用します。 これらのアセンブリは、独自のディレクトリまたはグローバル アセンブリ キャッシュ (GAC) にインストールする必要もあります。 これにより、弱い名前のバインドと呼ばれる、同じベース ファイル名を持つアセンブリとの競合から保護されます。
