---
title: インストール後に実行する必要があるコマンド | Microsoft Docs
description: Visual Studio で .msi ファイルを使用して展開された拡張機能のインストールの一部として実行する必要があるコマンドについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- post-install commands
ms.assetid: c9601f2e-2c6e-4da9-9a6e-e707319b39e2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ef557c0c679fad0dff25a51a8529270e4bd7ced2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057144"
---
# <a name="commands-that-must-be-run-after-installation"></a>インストール後に実行する必要があるコマンド
*.msi* ファイルを使用して拡張機能を展開する場合は、Visual Studio で拡張機能を検出するために、インストールの一部として **devenv/setup** を実行する必要があります。

> [!NOTE]
> このトピックの情報は、Visual Studio 2008 以前のバージョンで *devenv.exe* を検出する場合に適用されます。 新しいバージョンの Visual Studio で *devenv.exe* を検出する方法の詳細については、「[システム必要条件の検出](../../extensibility/internals/detecting-system-requirements.md)」を参照してください。

## <a name="find-devenvexe"></a>devenv.exe の検出
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] インストーラーによって書き込まれたレジストリ値から各バージョンの *devenv.exe* を見つけることができます。RegLocator テーブルと AppSearch テーブルを使用して、レジストリ値をプロパティとして格納します。 詳細については、「[システム必要条件の検出](../../extensibility/internals/detecting-system-requirements.md)」をご覧ください。

### <a name="reglocator-table-rows-to-locate-devenvexe-from-different-versions-of-visual-studio"></a>さまざまなバージョンの Visual Studio で devenv.exe を検索するための RegLocator テーブル行

|署名|Root|キー|名前|Type|
|-----------------|----------|---------|----------|----------|
|RL_DevenvExe_2002|2|SOFTWARE\Microsoft\VisualStudio\7.0\Setup\VS|EnvironmentPath|2|
|RL_DevenvExe_2003|2|SOFTWARE\Microsoft\VisualStudio\7.1\Setup\VS|EnvironmentPath|2|
|RL_DevenvExe_2005|2|SOFTWARE\Microsoft\VisualStudio\8.0\Setup\VS|EnvironmentPath|2|
|RL_DevenvExe_2008|2|SOFTWARE\Microsoft\VisualStudio\9.0\Setup\VS|EnvironmentPath|2|

### <a name="appsearch-table-rows-for-corresponding-reglocator-table-rows"></a>対応する RegLocator テーブル行の AppSearch テーブル行

|プロパティ|署名|
|--------------|-----------------|
|DEVENV_EXE_2002|RL_DevenvExe_2002|
|DEVENV_EXE_2003|RL_DevenvExe_2003|
|DEVENV_EXE_2005|RL_DevenvExe_2005|
|DEVENV_EXE_2008|RL_DevenvExe_2008|

 たとえば、Visual Studio インストーラーでは、**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0\Setup\VS\EnvironmentPath** レジストリ値がインストーラーが実行する必要のある実行可能ファイルへの完全なパスである *C:\VS2008\Common7\IDE\devenv.exe* として書き込まれます。

> [!NOTE]
> RegLocator テーブルの Type 列は 2 であるため、Signature テーブルで追加のバージョン情報を指定する必要はありません。

## <a name="run-devenvexe"></a>devenv.exe の実行
 AppSearch の標準アクションがインストーラーで実行された後、AppSearch テーブル内の各プロパティには、対応するバージョンの Visual Studio の *devenv.exe* ファイルをポイントする値が含まれます。 そのバージョンの Visual Studio がインストールされていないため、指定したレジストリ値が存在しない場合は、指定したプロパティは null 値に設定されます。

 Windows インストーラーでは、カスタム アクション タイプ 50 を通じてプロパティがポイントする実行可能ファイルの実行がサポートされています。 カスタム アクションには、VSPackage を [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に統合する前に正常にインストールされたことを確認するために、スクリプト内実行オプション `msidbCustomActionTypeInScript` (1024) と `msidbCustomActionTypeCommit` (512) が含まれている必要があります。 詳細については、「[CustomAction テーブル](/windows/desktop/msi/customaction-table)」と「[カスタム アクションのスクリプト内実行オプション](/windows/desktop/msi/custom-action-in-script-execution-options)」を参照してください。

 タイプ 50 のカスタム アクションでは、実行可能ファイルを含むプロパティを、ターゲット列の Source 列とコマンドライン引数の値として指定します。

### <a name="customaction-table-rows-to-run-devenvexe"></a>devenv.exe を実行する CustomAction テーブル行

|アクション|Type|source|移行先|
|------------|----------|------------|------------|
|CA_RunDevenv2002|1586|DEVENV_EXE_2002|/setup|
|CA_RunDevenv2003|1586|DEVENV_EXE_2003|/setup|
|CA_RunDevenv2005|1586|DEVENV_EXE_2005|/setup|
|CA_RunDevenv2008|1586|DEVENV_EXE_2008|/setup|

 インストール中に実行するようにスケジュールを設定するには、カスタム アクションを InstallExecuteSequence テーブルに作成する必要があります。 Condition 列の各行で対応するプロパティを使用して、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のそのバージョンのがシステムにインストールされていない場合にカスタム アクションが実行されないようにします。

> [!NOTE]
> null 値のプロパティは、条件で使用されると `False` に評価されます。

 各カスタム アクションの Sequence 列の値は、Windows インストーラー パッケージ内の他のシーケンス値によって異なります。 シーケンス値は、 *devenv.exe* カスタム アクションが InstallFinalize の標準アクションの直前にできるだけ近いタイミングで実行されるようにする必要があります。

### <a name="installexecutesequence-table-to-schedule-the-devenvexe-custom-actions"></a>devenv.exe カスタム アクションをスケジュールするための InstallExecuteSequence テーブル

|アクション|条件|シーケンス|
|------------|---------------|--------------|
|CA_RunDevenv2002|DEVENV_EXE_2002|6602|
|CA_RunDevenv2003|DEVENV_EXE_2003|6603|
|CA_RunDevenv2005|DEVENV_EXE_2005|6605|
|CA_RunDevenv2008|DEVENV_EXE_2008|6608|

## <a name="see-also"></a>関連項目
- [Windows インストーラーによる VSPackage のインストール](../../extensibility/internals/installing-vspackages-with-windows-installer.md)
