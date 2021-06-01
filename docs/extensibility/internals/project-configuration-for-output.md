---
title: 出力のプロジェクト構成 | Microsoft Docs
description: 各構成でサポート可能なビルド プロセス、および出力項目を使用できるようにするためのインターフェイスとメソッドについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project configurations, output
ms.assetid: a4517f73-45af-4745-9d7f-9fddf887b636
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 13e37999ad9f3bada375c1897207e1e4c15546e8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105082011"
---
# <a name="project-configuration-for-output"></a>出力のためのプロジェクト構成
すべての構成は、実行可能ファイルやリソース ファイルなどの出力項目を生成する一連のビルド プロセスをサポートできます。 これらの出力項目はユーザーには非公開であり、実行可能ファイル (.exe、.dll、.lib) やソース ファイル (.idl、.h ファイル) などの関連する種類の出力をリンクするグループに配置することができます。

 出力項目は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutput2> メソッドを使用して使用可能にし、<xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumOutputs> メソッドを使用して列挙することができます。 出力項目をグループ化する場合、プロジェクトに <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputGroup> インターフェイスも実装する必要があります。

 `IVsOutputGroup` を実装して開発されたコンストラクトを使用することで、用途に応じてプロジェクトの出力をグループ化することができます。 たとえば、DLL をそのプログラム データベース (PDB) とグループ化することができます。

> [!NOTE]
> PDB ファイルにはデバッグ情報が含まれており、.dll または .exe のビルド時に [デバッグ情報の生成] オプションが指定されている場合に作成されます。 通常、.pdb ファイルはデバッグ プロジェクト構成の場合にのみ生成されます。

 グループ内に含まれる出力の数が構成ごとに異なる場合でも、プロジェクトでは、サポートする構成ごとに同じ数のグループを返す必要があります。 たとえば、プロジェクト Matt の DLL の場合、デバッグ構成には mattd.dll と mattd.pdb が含まれ、リテール構成には Matt.dll のみが含まれます。

 また、グループには、プロジェクト内のそれぞれの構成で同じ識別子情報 (正規名、表示名、グループ情報など) も含まれています。 この一貫性により、構成が変更された場合でも、配置とパッケージが引き続き機能します。

 また、グループには、パッケージのショートカットが意味のあるものを指すように、キー出力を含めることができます。 ある構成で任意のグループが空になる可能性があるため、グループのサイズについては想定しないでください。 任意の構成の各グループのサイズ (出力数) は、同じ構成の別のグループのサイズとは異なることがあります。 また、別の構成の同じグループのサイズとは異なることがあります。

 ![出力グループの図](../../extensibility/internals/media/vsoutputgroups.gif "vsOutputGroups")出力グループ

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg> インターフェイスの主な用途は、管理オブジェクトをビルド、配置、およびデバッグするためのアクセスを提供し、プロジェクトから自由に出力をグループ化できるようにするためです。 このインターフェイスの用途の詳細については、「[プロジェクト構成オブジェクト](../../extensibility/internals/project-configuration-object.md)」を参照してください。

 前の図で、"Group Built" (ビルドされたグループ) には構成 (bD.exe または b.exe) 全体のキー出力があるため、ユーザーは "Built" (ビルド済み) へのショートカットを作成して、配置された構成に関係なくショートカットが機能することを把握することができます。 "Group Source" (グループ ソース) にはキー出力がないため、ユーザーはそのショートカットを作成できません。 "Debug Group Built" (ビルドされたデバッグ グループ) にはキー出力があり、"Retail Group Built" (ビルドされたリテール グループ) にはない場合、それは誤った実装になります。 そのため、いずれかの構成に出力を含まないグループがあり、その結果、キー ファイルがない場合、出力を含むそのグループがある他の構成にはキー ファイルを含めることができません。 インストーラーのエディターは、グループの正規名と表示名、およびキー ファイルの存在が、構成によって変わらないことを前提としています。

 パッケージ化または配置しない `IVsOutputGroup` がプロジェクト内にある場合は、その出力をグループに入れなければ十分であることに注意してください。 グループ化に関係なく、構成のすべての出力を返す <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg.EnumOutputs%2A> メソッドを実装することにより、通常どおり出力を列挙できます。

 詳細については、「[MPF for Projects (プロジェクト用 MPF)](https://github.com/tunnelvisionlabs/MPFProj10)」のカスタム プロジェクト サンプルに含まれる `IVsOutputGroup` の実装を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [構成オプションの管理](../../extensibility/internals/managing-configuration-options.md)
- [ビルドのためのプロジェクト構成](../../extensibility/internals/project-configuration-for-building.md)
- [プロジェクト構成オブジェクト](../../extensibility/internals/project-configuration-object.md)
- [ソリューション構成](../../extensibility/internals/solution-configuration.md)
