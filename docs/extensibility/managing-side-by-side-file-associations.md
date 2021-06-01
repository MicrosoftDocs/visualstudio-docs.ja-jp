---
title: サイドバイサイドのファイルの関連付けの管理 | Microsoft Docs
description: VSPackage により、ファイルの関連付けを指定する場合は、ファイルを開く特定のバージョンの Visual Studio でサイドバイサイド インストールをどのように処理するかを決定します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- verbs, setting default
ms.assetid: 9b6df3bc-d15c-4a5d-9015-948a806193b7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 083eef2454a9e805b1cb8b3e85a6d7d81263a0dd
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073054"
---
# <a name="manage-side-by-side-file-associations"></a>サイドバイサイドのファイルの関連付けを管理する

VSPackage により、ファイルの関連付けを指定する場合は、ファイルを開くために呼び出される特定のバージョンの [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] でサイドバイサイド インストールをどのように処理するかを決定する必要があります。 互換性のないファイル形式があると、この問題がさらに悪化します。

ユーザーは、製品の新しいバージョンが以前のバージョンと互換性があり、データを失うことなく既存のファイルを新しいバージョンで読み込むことができることを期待しています。 VSPackage によって以前のバージョンのファイル形式を読み込み、保存できることが理想的です。 そうではない場合は、ファイル形式を新しいバージョンの VSPackage にアップグレードすることを提案する必要があります。 このアプローチの欠点は、アップグレードされたファイルを以前のバージョンで開くことができないことです。

この問題を回避するには、ファイル形式に互換性がなくなったときに、拡張子を変更する方法があります。 たとえば、VSPackage のバージョン 1 では拡張子 *.mypkg10* を、バージョン 2 では拡張子 *.mypkg20* を使用できます。 この違いにより、特定のファイルを開く VSPackage が特定されます。 以前の拡張機能に関連付けられているプログラムの一覧に新しい VSPackage を追加すると、ユーザーはファイルを右クリックして、新しい VSPackage で開くことを選択できます。 その時点で、VSPackage により、ファイルを新しい形式にアップグレードするか、ファイルを開いて以前のバージョンの VSPackage との互換性を維持するかを提案できます。

> [!NOTE]
> これらのアプローチを組み合わせることができます。 たとえば、以前のファイルを読み込むことで下位互換性を提供し、ユーザーがファイルを保存するときにファイル形式のアップグレードを提供することができます。

## <a name="face-the-problem"></a>問題に直面する

複数のサイドバイサイド VSPackage で同じ拡張機能を使用する場合は、その拡張機能に関連付けられている [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] のバージョンを選択する必要があります。 ここに 2 つの選択肢があります。

- ユーザーのコンピューターにインストールされている最新バージョンの [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] でファイルを開きます。

   このアプローチの場合、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] の最新バージョンを判断し、ファイルの関連付け用に作成されたレジストリ エントリにそれを含めるのは、インストーラーが担当します。 Windows インストーラー パッケージには、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] の最新バージョンを示すプロパティを設定するためのカスタム アクションを含めることができます。

  > [!NOTE]
  > このコンテキストでは、"最新" とは "サポートされている最新バージョン" を意味します。 このようなインストーラー エントリによって、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] の後続のリリースは自動的に検出されません。 「[システム要件の検出](../extensibility/internals/detecting-system-requirements.md)」と「[インストール後に実行する必要があるコマンド](../extensibility/internals/commands-that-must-be-run-after-installation.md)」のエントリは、ここに示されているものと同様であり、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] の追加バージョンをサポートする必要があります。

   CustomAction テーブルの次の行により、DEVENV_EXE_LATEST プロパティは、「[インストール後に実行する必要があるコマンド](../extensibility/internals/commands-that-must-be-run-after-installation.md)」で説明されている AppSearch テーブルと RegLocator テーブルに設定されるプロパティに設定されます。 InstallExecuteSequence テーブルの行により、実行シーケンスの早い段階でカスタム アクションがスケジュールされます。 「条件」列の値により、ロジックが機能します。

  - Visual Studio .NET 2002 が存在する唯一のバージョンである場合、それが最新バージョンになります。

  - Visual Studio .NET 2003 が最新バージョンになるのは、それが存在し、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] が存在しない場合のみです。

  - [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] が存在する唯一のバージョンである場合、それが最新バージョンになります。

    最終的な結果として、DEVENV_EXE_LATEST には最新バージョンの devenv.exe のパスが含まれます。

  **Visual Studio の最新バージョンを決定する CustomAction テーブルの行**

  |アクション|Type|source|移行先|
  |------------|----------|------------|------------|
  |CA_SetDevenvLatest_2002|51|DEVENV_EXE_LATEST|[DEVENV_EXE_2002]|
  |CA_SetDevenvLatest_2003|51|DEVENV_EXE_LATEST|[DEVENV_EXE_2003]|
  |CA_SetDevenvLatest_2005|51|DEVENV_EXE_LATEST|[DEVENV_EXE_2005]|

  **Visual Studio の最新バージョンを決定する InstallExecuteSequence テーブルの行**

  |アクション|条件|シーケンス|
  |------------|---------------|--------------|
  |CA_SetDevenvLatest_2002|DEVENV_EXE_2002 AND NOT (DEVENV_EXE_2003 OR DEVENV_EXE_2005)|410|
  |CA_SetDevenvLatest_2003|DEVENV_EXE_2003 AND NOT DEVENV_EXE_2005|420|
  |CA_SetDevenvLatest_2005|DEVENV_EXE_2005|430|

   Windows インストーラー パッケージの Registry テーブルの DEVENV_EXE_LATEST プロパティを使用して、**HKEY_CLASSES_ROOT *ProgId* ShellOpenCommand** キーの既定値 [DEVENV_EXE_LATEST] "%1" を書き込むことができます

- 使用できる VSPackage バージョンから最適な選択を行うことができる共有ランチャー プログラムを実行します。

   [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] の開発者は、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] の多くのバージョンから生成されるソリューションとプロジェクトの複数の形式の複雑な要件を処理するために、このアプローチを選択しました。 このアプローチでは、ランチャー プログラムを拡張ハンドラーとして登録します。 ランチャーによってファイルが検査され、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] のどのバージョンと VSPackage でその特定のファイルを処理できるかが決定されます。 たとえば、ユーザーが VSPackage の特定のバージョンによって最後に保存されたファイルを開いた場合、ランチャーから、一致するバージョンの [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] でその VSPackage を起動することができます。 さらに、ユーザーは常に最新バージョンを起動するようにランチャーを構成できます。 ランチャーにより、ファイルの形式をアップグレードするようにユーザーに求めることもできます。 ファイルの形式にバージョン番号が含まれている場合、ランチャーにより、ファイル形式がインストールされている VSPackage よりも 1 つ以上後のバージョンかどうかをユーザーに通知できます。

   ランチャーは、VSPackage のすべてのバージョンと共有される Windows インストーラー コンポーネントに含まれている必要があります。 このプロセスにより、最新バージョンが常にインストールされ、VSPackage のすべてのバージョンがアンインストールされるまで削除されません。 このようにして、VSPackage の 1 つのバージョンがアンインストールされた場合でも、ランチャー コンポーネントのファイルの関連付けおよびその他のレジストリ エントリは保持されます。

## <a name="uninstall-and-file-associations"></a>アンインストールとファイルの関連付け

ファイルの関連付けのレジストリ エントリを書き込む VSPackage をアンインストールすると、ファイルの関連付けは削除されます。 そのため、この拡張機能に関連するプログラムはありません。 Windows インストーラーによって、VSPackage のインストール時に追加されたレジストリ エントリは "回復" されません。 ユーザーのファイルの関連付けを修正する方法の一部を次に示します。

- 前述のように、共有ランチャー コンポーネントを使用します。

- ユーザーがファイルの関連付けを所有するバージョンの VSPackage の修復を実行するように、ユーザーに指示します。

- 適切なレジストリ エントリを書き換える別の実行可能プログラムを用意します。

- ユーザーがファイルの関連付けを選択し、失われた関連付けを再利用できるように、構成オプション ページまたはダイアログ ボックスを用意します。 アンインストール後に実行するようにユーザーに指示します。

## <a name="see-also"></a>こちらもご覧ください

- [サイド バイ サイドの配置に対してファイル名拡張子を登録する](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)
- [ファイル名拡張子の動詞を登録する](../extensibility/registering-verbs-for-file-name-extensions.md)
