---
title: システム要件の検出 | Microsoft Docs
description: Microsoft Windows インストーラーを構成して、インストールされている Visual Studio のエディションなどのシステム要件を検出する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- setup, VSPackages
- launch conditions
ms.assetid: 0ba94acf-bf0b-4bb3-8cca-aaac1b5d6737
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ffb00ca42376f8b7c150552c862bba7a24a5c1fb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056767"
---
# <a name="detect-system-requirements"></a>システム要件の検出
Visual Studio がインストールされていない場合、VSPackage は機能できません。 Microsoft Windows のインストーラーを使用して VSPackage のインストールを管理する場合、インストーラーを構成して、Visual Studio がインストールされているかどうかの検出が行われるようにすることができます。 また、Windows の特定バージョンや RAM の特定の容量など、他の要件についてシステムをチェックするように構成することもできます。

## <a name="detect-visual-studio-editions"></a>Visual Studio のエディションの検出
 Visual Studio のあるエディションがインストールされているかどうかを確認するには、次の表に示すように、対応するフォルダー内の **Install** レジストリキーの値が " *(REG_DWORD) 1*" であることを確認します。 Visual Studio のエディションの階層があることに注意してください。

1. エンタープライズ

2. Professional

3. コミュニティ

新しいエディションがインストールされると、そのエディションだけでなく、以前のエディションのレジストリ キーも追加されます。 つまり、Enterprise エディションがインストールされている場合は、Enterprise だけでなく、Professional および Community エディションの **Install** キーも "*1*" に設定されます。 そのため、必要な最新のエディションのみをチェックする必要があります。

> [!NOTE]
> 64 ビット版のレジストリ エディターでは、32 ビットのキーは **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\\** の下に表示されます。 Visual Studio のキーは、**HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\DevDiv\vs\Servicing\\** の下です。

|製品|キー|
|-------------|---------|
|Visual Studio Enterprise 2015|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\enterprise|
|Visual Studio Professional 2015|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\professional|
|Visual Studio Community 2015|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\community|
|Visual Studio 2015 Shell (Integrated および isolated)|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\isoshell|

## <a name="detect-when-visual-studio-is-running"></a>Visual Studio 実行中の検出
 VSPackage がインストールされているときに、Visual Studio が実行されると、VSPackage を正しく登録できません。 Visual Studio が実行されているときは、インストーラーによって検出が行われ、その後、プログラムのインストールが拒否される必要があります。 Windows のインストーラーでは、このような検出を有効にするためにテーブル エントリを使用することはできません。 代わりに、次のように、カスタム アクションを作成する必要があります。`EnumProcesses` 関数を使用して *devenv.exe* プロセスを検出し、その後、起動条件で使用されるインストーラー プロパティを設定するか、または Visual Studio を閉じるようにユーザーに求めるダイアログ ボックスを条件付きで表示します。

## <a name="see-also"></a>関連項目
- [Windows インストーラーによる VSPackage のインストール](../../extensibility/internals/installing-vspackages-with-windows-installer.md)
