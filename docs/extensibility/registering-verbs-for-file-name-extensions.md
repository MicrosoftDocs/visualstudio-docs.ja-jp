---
title: ファイル名拡張子の動詞の登録 | Microsoft Docs
description: Shell キーを使用して、ファイル名拡張子のプログラム識別子に関連付けられた動詞を登録する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- verbs, registering
ms.assetid: 81a58e40-7cd0-4ef4-a475-c4e1e84d6e06
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c223dea7e265d8d040d502c99ded09380e89690f
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901228"
---
# <a name="register-verbs-for-file-name-extensions"></a>ファイル名拡張子の動詞を登録する
ファイル名拡張子のアプリケーションとの関連付けには、一般に、ユーザーがファイルをダブルクリックしたときに実行される優先アクションが含まれています。 この優先アクションは、そのアクションに対応する動詞 (Open など) にリンクされています。

 **HKEY_CLASSES_ROOT\{progid}\shell** にある Shell キーを使用して、拡張子のプログラム識別子 (ProgID) に関連付けられた動詞を登録できます。 詳細については、「[ファイルの種類](/windows/desktop/shell/fa-file-types)」を参照してください。

## <a name="register-standard-verbs"></a>標準動詞を登録する
 オペレーティング システムでは、次の標準動詞を認識します。

- [ファイル]

- 編集

- [再生]

- 印刷

- プレビュー

  可能な場合は常に、標準動詞を登録します。 最も一般的な選択肢は Open 動詞です。 Edit 動詞は、ファイルを開くアクションとファイルを編集するアクションの間に明確な違いが存在する場合にのみ使用します。 たとえば、 *.htm* ファイルを開くとそれがブラウザーに表示されるのに対して、 *.htm* ファイルの編集では HTML エディターが起動されます。 標準動詞は、オペレーティング システムのロケールでローカライズされています。

> [!NOTE]
> 標準動詞を登録するときは、Open キーの既定値を設定しないでください。 この既定値には、メニューの表示文字列が含まれています。 オペレーティング システムでは、標準動詞に対してこの文字列を提供します。

 ユーザーがファイルを開いたときに [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] の新しいインスタンスを起動するには、プロジェクト ファイルを登録する必要があります。 次の例は、[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] プロジェクトでの標準動詞の登録を示しています。

```
[HKEY_CLASSES_ROOT\.csproj]
@="VisualStudio.csproj.8.0"

[HKEY_CLASSES_ROOT\.csproj\OpenWithList]
[HKEY_CLASSES_ROOT\.csproj\OpenWithList\VSLauncher.exe]
@=""

[HKEY_CLASSES_ROOT\.csproj\OpenWithProgids]
"VisualStudio.csproj.8.0"=""

[HKEY_CLASSES_ROOT\Applications\VSLauncher.exe]
[HKEY_CLASSES_ROOT\Applications\VSLauncher.exe\Shell]
[HKEY_CLASSES_ROOT\Applications\VSLauncher.exe\Shell\Open]
[HKEY_CLASSES_ROOT\Applications\VSLauncher.exe\Shell\Open\Command]
@="C:\\Program Files\\Common Files\\Microsoft Shared\\MSEnv\\VSLauncher.exe \"%1\""

[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0]
@="C# Project file"

[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0\DefaultIcon]
@="C:\\VisualStudioPath\\VC#\\VCSPackages\\csproj.dll,0"

[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0\shell]
[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0\shell\Open]
[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0\shell\Open\Command]
@="\"C:\\Program Files\\Common Files\\Microsoft Shared\\MSEnv\\VSLauncher.exe\" \"%1\""
```

 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] の既存のインスタンスでファイルを開くには、DDEEXEC キーを登録します。 次の例は、[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] *.cs* ファイルでの標準動詞の登録を示しています。

```
[HKEY_CLASSES_ROOT\.cs]
@="VisualStudio.cs.8.0"

[HKEY_CLASSES_ROOT\.cs\OpenWithList]
[HKEY_CLASSES_ROOT\.cs\OpenWithList\devenv.exe]
@=""

[HKEY_CLASSES_ROOT\.cs\OpenWithProgids]
"VisualStudio.cs.8.0"=""

[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0]
@="C# Source file"

[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\DefaultIcon]
@="C:\\VisualStudioPath\\VC#\\VCSPackages\\csproj.dll,1"

[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell]
[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open]
[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open\Command]
@="\"C:\\VisualStudioPath\\Common7\\IDE\\devenv.exe\" /dde \"%1\""

[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open\ddeexec]
@="Open(\"%1\")"

[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open\ddeexec\Application]
@="VisualStudio.8.0"

[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open\ddeexec\Topic]
@="system"
```

## <a name="set-the-default-verb"></a>既定の動詞を設定する
 既定の動詞は、ユーザーが Windows エクスプローラーでファイルをダブルクリックしたときに実行されるアクションです。 既定の動詞は、**HKEY_CLASSES_ROOT\\*progid*\Shell** キーの既定値として指定されている動詞です。 値が指定されていない場合、既定の動詞は、**HKEY_CLASSES_ROOT\\*progid*\Shell** キー リストで指定されている最初の動詞です。

> [!NOTE]
> サイドバイサイド展開で拡張子の既定の動詞を変更する予定がある場合は、インストールや削除への影響を考慮してください。 インストール中に、元の既定値は上書きされます。

## <a name="see-also"></a>関連項目
- [サイドバイサイドのファイルの関連付けを管理する](../extensibility/managing-side-by-side-file-associations.md)
