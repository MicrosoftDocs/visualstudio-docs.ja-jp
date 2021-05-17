---
title: VSPackage のセットアップ シナリオ | Microsoft Docs
description: VSPackage の共有またはサイドバイサイド インストールを使用して Visual Studio のサイドバイサイド インストールをサポートするためのベスト プラクティスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, deployment considerations
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2d305d03e17d0e55c2366e71452c4391ccc0ff57
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060745"
---
# <a name="vspackage-setup-scenarios"></a>VSPackage のセットアップ シナリオ

VSPackage インストーラーは、柔軟性を向上させるように設計することが重要です。 たとえば、将来セキュリティ更新プログラムをリリースする必要が発生したり、徹底的なサイドバイサイドのバージョン管理サポートが必要なビジネス戦略を変更したりする可能性があります。

「[複数バージョンの Visual Studio をサポートする](../../extensibility/supporting-multiple-versions-of-visual-studio.md)」では、VSPackage の共有またはサイドバイサイド インストールを使用して [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のサイドバイサイド インストールをサポートすることの利点と問題点を確認できます。 つまり、サイドバイサイド VSPackage によって、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の新機能をサポートするための最も高い柔軟性が提供されます。

このトピックで説明されているシナリオは、唯一の選択肢というわけではなく、推奨されるベスト プラクティスとして示されています。

## <a name="components-privacy-and-sharing"></a>コンポーネント、プライバシー、共有

### <a name="make-your-components-independent"></a>コンポーネントを独立したものにする

コンポーネントを識別して設定し、`GUID` を割り当ててから、そのコンポーネントを配置すると、その構成はもう変更できません。 コンポーネントの構成を変更する場合、結果として得られるコンポーネントは、新しい `GUID` を持つ新しいコンポーネントである必要があります。 これらの点を考慮すると、バージョン管理の最大の柔軟性は、各コンポーネントを独立した、自立的な単位にすることによって得られます。 コンポーネントを管理するルールの詳細については、[コンポーネント コードの変更](/windows/desktop/Msi/changing-the-component-code)および[コンポーネント ルールに違反した場合の動作](/windows/desktop/Msi/what-happens-if-the-component-rules-are-broken)に関するページを参照してください。

### <a name="do-not-mix-shared-and-private-resources-in-a-component"></a>コンポーネント内で共有リソースとプライベート リソースを混在させない

参照のカウントは、コンポーネント レベルで行われます。 その結果、1 つのコンポーネント内で共有リソースとプライベート リソースを混在させると、共有リソースも同時に上書きされることを防ぎながら、プライベート リソース (実行可能ファイルなど) を更新することはできなくなります。 このシナリオにより、下位互換性の問題が発生し、サイドバイサイド機能の作成が制限されます。

たとえば、VSPackage を [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] に登録するために使用されるレジストリ値は、VSPackage を Visual Studio に登録するために使用されるものとは別のコンポーネントに保持する必要があります。 共有されるファイルやレジストリ値は、さらに別のコンポーネントに格納されます。

## <a name="scenario-1-shared-vspackage"></a>シナリオ 1: 共有 VSPackage

このシナリオでは、共有 VSPackage (複数バージョンの Visual Studio をサポートする 1 つのバイナリ) が Windows インストーラー パッケージで発送されます。 各バージョンの Visual Studio への登録は、ユーザーが選択可能な機能によって制御されます。 これはまた、別の機能に割り当てられている場合は各コンポーネントをインストールまたはアンインストールのために個別に選択できるため、異なるバージョンの [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] への VSPackage の統合をユーザーが制御できるようになることも示しています。 (Windows インストーラー パッケージの機能を使用する方法の詳細については、[Windows インストーラーの機能](/windows/desktop/Msi/windows-installer-features)に関するページを参照してください)。

![VS 共有 VSPackage インストーラー](../../extensibility/internals/media/vs_sharedpackage.gif "VS_SharedPackage")

この図に示すように、共有コンポーネントは、常にインストールされる Feat_Common 機能の一部になっています。 Feat_VS2002 および Feat_VS2003 機能を表示することによって、ユーザーは、VSPackage をどのバージョンの Visual Studio に統合するかをインストール時に選択できます。 ユーザーはまた、Windows インストーラーのメンテナンス モードを使用して機能を追加または削除することもできます。この場合は、VSPackage の登録情報が異なるバージョンの Visual Studio に追加または削除されます。

> [!NOTE]
> 機能の [表示] 列を 0 に設定すると、その機能が非表示になります。 [レベル] 列を小さな値 (1 など) にすると、常にインストールされるようになります。 詳細については、[INSTALLLEVEL プロパティ](/windows/desktop/Msi/installlevel)および[機能テーブル](/windows/desktop/Msi/feature-table)に関するページを参照してください。

## <a name="scenario-2-shared-vspackage-update"></a>シナリオ 2: 共有 VSPackage 更新プログラム

このシナリオでは、シナリオ 1 の VSPackage インストーラーの更新されたバージョンが発送されます。 ここで、この更新プログラムでは Visual Studio のサポートが追加されますが、より簡単なセキュリティ更新プログラムまたはバグ修正の Service Pack であってもかまいません。 より新しいコンポーネントをインストールするための Windows インストーラーのルールでは、既にシステム上にある変更されないコンポーネントが再コピーされないようにする必要があります。 この場合、更新されたコンポーネント Comp_MyVSPackage.dll は既に存在するバージョン 1.0 のシステムによって上書きされるため、ユーザーは、コンポーネント Comp_VS2005_Reg を含む新機能 Feat_VS2005 を追加することを選択できます。

> [!CAUTION]
> VSPackage が複数バージョンの [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の間で共有されている場合は常に、以降のリリースの VSPackage で以前のバージョンの Visual Studio との下位互換性が維持されることが不可欠です。 下位互換性を維持できない場合は、サイドバイサイドのプライベート VSPackage を使用する必要があります。 詳細については、「[複数バージョンの Visual Studio をサポートする](../../extensibility/supporting-multiple-versions-of-visual-studio.md)」を参照してください。

![VS 共有 VSPackage 更新プログラム インストーラー](../../extensibility/internals/media/vs_sharedpackageupdate.gif "VS_SharedPackageUpdate")

このシナリオでは、マイナー アップグレードに対する Windows インストーラーのサポートを利用する新しい VSPackage インストーラーを提供します。 ユーザーがバージョン 1.1 をインストールするだけで、それによりバージョン 1.0 がアップグレードされます。 ただし、システム上にバージョン 1.0 は必要ありません。 同じインストーラーによって、バージョン 1.0 がないシステムにもバージョン 1.1 がインストールされます。 この方法でマイナー アップグレードを提供する利点は、アップグレード インストーラーと完全な製品インストーラーを開発する作業を実行する必要がないことです。 1 つのインストーラーが両方のジョブを実行します。 セキュリティ修正プログラムまたは Service Pack では、代わりに Windows インストーラーの修正プログラムを利用することがあります。 詳細については、[修正プログラムの適用とアップグレード](/windows/desktop/Msi/patching-and-upgrades)に関するページを参照してください。

## <a name="scenario-3-side-by-side-vspackage"></a>シナリオ 3: サイドバイサイド VSPackage

このシナリオでは、各バージョンの Visual Studio .NET 2003 と Visual Studio に 1 つずつの 2 つの VSPackage インストーラーを提供します。 各インストーラーでは、サイドバイサイドまたはプライベート VSPackage (特定のバージョンの Visual Studio 専用にビルドおよびインストールされるもの) をインストールします。 各 VSPackage が独自のコンポーネントに含まれています。 その結果、それぞれを修正プログラムまたはメンテナンス リリースで個別に処理できます。 VSPackage DLL は現在、バージョン固有であるため、その登録情報を DLL と同じコンポーネントに安全に含めることができます。

![VS サイドバイサイド VSPackage インストーラー](../../extensibility/internals/media/vs_sbys_package.gif "VS_SbyS_Package")

各インストーラーには、2 つのインストーラー間で共有されるコードも含まれています。 共有コードが共通の場所にインストールされる場合は、両方の .msi ファイルをインストールすると、その共有コードは 1 回だけインストールされます。 2 番目のインストーラーは、コンポーネント上の参照カウントを増分するだけです。 参照カウントによって、いずれかの VSPackage がアンインストールされても、共有コードは他の VSPackage のために残ることが保証されます。 2 番目の VSPackage もアンインストールされた場合は、共有コードが削除されます。

## <a name="scenario-4-side-by-side-vspackage-update"></a>シナリオ 4: サイドバイサイド VSPackage 更新プログラム

このシナリオでは、Visual Studio 用の VSPackage でセキュリティの脆弱性が発生したため、更新プログラムを発行する必要があります。 シナリオ 2 の場合と同様に、セキュリティ修正プログラムを含むように既存のインストールを更新する新しい .msi ファイルを作成するだけでなく、セキュリティ修正プログラムが既に含まれている新しいインストールを配置することもできます。

この場合、この VSPackage は、グローバル アセンブリ キャッシュ (GAC) にインストールされているマネージド VSPackage です。 これをセキュリティ修正プログラムを含むようにリビルドする場合は、アセンブリ バージョン番号のリビジョン番号の部分を変更する必要があります。 新しいアセンブリ バージョン番号の登録情報によって以前のバージョンが上書きされ、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では修正されたアセンブリが読み込まれるようになります。

![VS サイドバイサイド VSPackage 更新プログラム インストーラー](../../extensibility/internals/media/vs_sbys_packageupdate.gif "VS_SbyS_PackageUpdate")

サイドバイサイド アセンブリの配置の詳細については、[.NET Framework を使用した配置の簡素化と DLL 地獄の解決](/previous-versions/dotnet/articles/ms973843(v=msdn.10))に関するページを参照してください。

## <a name="see-also"></a>関連項目

- [Windows インストーラー](/windows/desktop/Msi/windows-installer-portal)
- [複数バージョンの Visual Studio をサポートする](../../extensibility/supporting-multiple-versions-of-visual-studio.md)