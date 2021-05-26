---
title: VSPackage の登録 | Microsoft Docs
description: VSPackage の登録について説明します。これは、パッケージがインストールされており、読み込む必要があることを、レジストリに情報を書き込むことによって Visual Studio に通知する処理です。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- registration, VSPackages
- VSPackages, registering
ms.assetid: ecd20da8-b04b-4141-a8f4-a2ef91dd597a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: afa2ac0f8608e7cafe8c465ea5ff0b8c0031dd58
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069154"
---
# <a name="vspackage-registration"></a>VSPackage の登録
VSPackage は、自らがインストールされていて読み込みが必要であることを [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に通知する必要があります。 このプロセスは、レジストリに情報を書き込むことによって行われます。 これは、インストーラーの一般的な処理です。

> [!NOTE]
> VSPackage の開発中は、自己登録の使用が認められています。 ただし、[!INCLUDE[vsipprvsip](../../extensibility/includes/vsipprvsip_md.md)]のパートナーは、セットアップの一環として自己登録を使用する自社製品を出荷することはできません。

 Windows インストーラー パッケージ内のレジストリ エントリは、通常はレジストリ テーブルに作成されます。 レジストリ テーブルにはファイル拡張子も登録できます。 ただし、Windows インストーラーでは、プログラム識別子 (ProgId)、クラス、拡張子、動詞テーブルを通じて組み込みのサポートを提供しています。 詳細については、「[データベース テーブル](/windows/desktop/Msi/database-tables)」を参照してください。

 レジストリ エントリが、選択したサイドバイサイド戦略に適したコンポーネントに関連付けられていることを確認してください。 たとえば、共有ファイルのレジストリ エントリは、そのファイルの Windows インストーラー コンポーネントに関連付けられている必要があります。 同様に、バージョン固有ファイルのレジストリ エントリは、そのファイルのコンポーネントに関連付けられている必要があります。 そのようにしないと、あるバージョンの [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 用に VSPackage をインストールまたはアンインストールした場合に、他のバージョンで VSPackage が破損する可能性があります。 詳細については、「[複数バージョンの Visual Studio をサポートする](../../extensibility/supporting-multiple-versions-of-visual-studio.md)」を参照してください。

> [!NOTE]
> 登録を管理する最も簡単な方法は、開発者登録とインストール時登録の両方に、同じファイル内の同じデータを使用することです。 たとえば、一部のインストーラー開発ツールでは、ビルド時に .reg 形式のファイルを使用できます。 開発者が独自の日常的な開発とデバッグのために .reg ファイルを保持している場合は、それらの同じファイルをインストーラーに自動的に含めることができます。 登録データを自動的に共有できない場合は、インストーラーの登録データのコピーが最新であることを確認する必要があります。

## <a name="registering-unmanaged-vspackages"></a>アンマネージド VSPackage の登録
 アンマネージド VSPackage (Visual Studio パッケージ テンプレートによって生成されたものを含む) は、ATL スタイルの .rgs ファイルを使用して登録情報を格納します。 .rgs ファイル形式は ATL に固有であり、通常、インストール オーサリング ツールでそのまま使用することはできません。 VSPackage インストーラーの登録情報は、個別に管理する必要があります。 たとえば開発者は、.reg 形式のファイルについて、.rgs ファイルの変更との同期を維持することができます。 .reg ファイルは、開発作業のために RegEdit とマージすることも、インストーラーで使用することもできます。

## <a name="registering-managed-vspackages"></a>マネージド VSPackage の登録
 RegPkg ツールでは、マネージド VSPackage から登録属性を読み取ります。そして、情報をレジストリに直接書き込むか、インストーラーで使用できる .reg 形式のファイルを書き込むことができます。

> [!NOTE]
> RegPkg ツールは再頒布可能ではなく、ユーザーのシステムに VSPackage を登録するために使用することはできません。

## <a name="why-vspackages-should-not-self-register-at-install-time"></a>インストール時に VSPackage を自己登録してはならない理由
 VSPackage インストーラーは自己登録に依存してはなりません。 一見すると、VSPackage のレジストリ値を VSPackage 自体にのみ保持するのは良いアイデアであるように思われます。 日常の作業やテストに使用できるレジストリ値が開発者に必要であることを考えると、レジストリ データの別個のコピーをインストーラーに保持するのを避けることは理にかなっています。 インストーラーでは、VSPackage 自体に依拠してレジストリ値を書き込むことができます。

 理論上は問題なさそうですが、自己登録には、VSPackage のインストールには適さないいくつかの欠点があります。

- インストール、アンインストール、インストールのロールバック、そしてアンインストールのロールバックを正しくサポートするには、RegPkg を呼び出して自己登録を行う 4 つのカスタム アクションを、すべてのマネージド VSPackage に対して作成する必要があります。

- サイドバイサイド サポートの方法では、サポートされている [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のバージョンごとに、RegSvr32 または RegPkg を呼び出す 4 つのカスタム アクションを作成することが必要な場合があります。

- 自己登録モジュールを使用するインストールは、安全にロールバックできません。なぜなら、自己登録されたキーが別の機能またはアプリケーションによって使用されているかどうかを判別する手段がないからです。

- 自己登録 DLL は、存在しないかバージョンが誤っている補助 DLL にリンクする場合があります。 これに対し、Windows インストーラーでは、システムの現在の状態に依存することなく、レジストリ テーブルを使用して DLL を登録できます。

- "ソースから実行" として指定されている、また SelfReg テーブルに含まれているという両方の条件にコンポーネントが該当する場合、自己登録コードは、タイプ ライブラリなどのネットワーク リソースへのアクセスを拒否される可能性があります。 これにより、管理インストール中にコンポーネントのインストールが失敗する可能性があります。

## <a name="see-also"></a>関連項目
- [Windows インストーラー](/windows/desktop/Msi/windows-installer-portal)
- [マネージド パッケージ登録](/previous-versions/bb166783(v=vs.100))