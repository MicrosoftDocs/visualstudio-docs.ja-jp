---
title: VSPackage のインストール ディレクトリの選択 | Microsoft Docs
description: VSPackage とそのサポート ファイルのインストール ディレクトリを、これがマネージドかアンマネージドかどうかなどの要因を使用して選択する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, installation directory
ms.assetid: 01fbbb5b-f747-446c-afe0-2a081626a945
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6442a8475c862693b851be783ae85bbb0a2e90af
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105082115"
---
# <a name="choose-the-installation-directory-for-a-vspackage"></a>VSPackage のインストール ディレクトリの選択
VSPackage とそのサポート ファイルは、ユーザーのファイル システム上にある必要があります。 場所は、VSPackage がマネージドかアンマネージドかどうか、サイド バイ サイドのバージョン管理スキーム、ユーザーの選択によって異なります。

## <a name="unmanaged-vspackages"></a>アンマネージド VSPackage
 アンマネージド VSPackage は、任意の場所にインストールできる COM サーバーです。 その登録情報は、その場所を正確に反映している必要があります。 インストーラーのユーザー インターフェイス (UI) では、既定の場所を `ProgramFilesFolder` Windows インストーラー プロパティ値のサブディレクトリとして指定する必要があります。 次に例を示します。

*&lt;ProgramFilesFolder&gt;\\&lt;MyCompany&gt;\\&lt;MyVSPackageProduct&gt;\V1.0\\*

 小さいブート パーティションを保持し、別のボリュームにアプリケーションやツールをインストールすることを希望するユーザーに対応するために、ユーザーは既定のディレクトリを変更できる必要があります。

 バージョン管理された VSPackage がサイド バイ サイドのスキームで使用されている場合は、サブディレクトリを使用して異なるバージョンを格納できます。 次に例を示します。

 *&lt;ProgramFilesFolder&gt;\\&lt;MyCompany&gt;\\&lt;MyVSPackageProduct&gt;\\V1.0\\2002\\*

 *&lt;ProgramFilesFolder&gt;\\&lt;MyCompany&gt;\\&lt;MyVSPackageProduct&gt;\\V1.0\\2003\\*

 *&lt;ProgramFilesFolder&gt;\\&lt;MyCompany&gt;\\&lt;MyVSPackageProduct&gt;\\V1.0\\2005\\*

## <a name="managed-vspackages"></a>マネージド VSPackage
 マネージド VSPackage は、任意の場所にインストールすることもできます。 ただし、アセンブリの読み込み時間を短縮するには、常にグローバル アセンブリ キャッシュ (GAC) にインストールすることを検討する必要があります。 マネージド VSPackage は常に厳密な名前付きアセンブリなので、GAC にインストールすると、厳密な名前の署名の検証はインストール時にのみ行われます。 ファイル システム内の他の場所にインストールされている厳密な名前付きアセンブリでは、読み込まれるたびに署名を検証する必要があります。 マネージド VSPackage を GAC にインストールする場合は、regpkg ツールの **/assembly** スイッチを使用して、アセンブリの厳密な名前を指すレジストリ エントリを書き込みます。

 マネージド VSPackage を GAC 以外の場所にインストールする場合は、アンマネージド VSPackage でのディレクトリ階層の選択に関する前述のアドバイスに従ってください。 regpkg ツールの **/codebase** スイッチを使用して、VSPackage アセンブリのパスを指すレジストリ エントリを書き込みます。

 詳細については、[VSPackage の登録および登録解除](../../extensibility/registering-and-unregistering-vspackages.md)に関するページを参照してください。

## <a name="satellite-dlls"></a>サテライト DLL
 慣例により、特定のロケールのリソースを含む VSPackage サテライト DLL は、*VSPackage* ディレクトリのサブディレクトリに配置されます。 サブディレクトリはロケール ID (LCID) 値に対応します。

 「[VSPackage を管理する](../../extensibility/managing-vspackages.md)」の記事は、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] で VSPackage のサテライト DLL を実際に検索する場所をレジストリ エントリで制御することを示しています。 ただし、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、LCID 値に対して名前が付けられたサブディレクトリでサテライト DLL の読み込みが次の順序で試行されます。

1. 既定の LCID (Visual Studio LCID。たとえば、英語の場合は *\1033*)

2. 既定のサブ言語を持つ既定の LCID。

3. システムの既定の LCID。

4. 既定のサブ言語を持つシステムの既定の LCID。

5. 米国英語 ( *.\1033* または *.\0x409*)。

VSPackage DLL にリソースが含まれており、**SatelliteDll\DllName** レジストリ エントリがこれを指す場合、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ではこれらを上記の順序で読み込もうとします。

## <a name="see-also"></a>関連項目
- [共有 VSPackage と バージョン管理 VSPackage の選択](../../extensibility/choosing-between-shared-and-versioned-vspackages.md)
- [VSPackage を管理する](../../extensibility/managing-vspackages.md)
- [パッケージ登録を管理する](/previous-versions/bb166783(v=vs.100))