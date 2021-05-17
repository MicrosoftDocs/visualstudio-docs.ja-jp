---
title: ビジュアル デザイナーへの型の公開 | Microsoft Docs
description: クラスと型の定義を、カスタム ツールでの定義を含めて公開し、Visual Studio のビジュアル デザイナーで利用できるようにする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- types [Visual Studio SDK], exposing to visual designers
- designers [Visual Studio SDK], exposing types
- custom tools, exposing types to visual designers
ms.assetid: a7a32ad4-3a0a-4eb8-a6ac-491c42885639
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5208de3af52e4dad5fb9bb59b16f7b59efb72340
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069674"
---
# <a name="expose-types-to-visual-designers"></a>ビジュアル デザイナーに型を公開する
ビジュアル デザイナーを表示するために、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、デザイン時にクラスと型の定義にアクセスできる必要があります。 クラスは、現在のプロジェクトの完全な依存関係セット (参照に加えてその依存関係) を含む、事前定義されたアセンブリのセットから読み込まれます。 カスタム ツールによって生成されたファイルで定義されているクラスと型にビジュアル デザイナーがアクセスすることが必要な場合もあります。

 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] および [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] プロジェクト システムでは、一時的なポータブル実行可能ファイル (一時的 PE) を通じて、生成されたクラスと型にアクセスするためのサポートを提供しています。 カスタム ツールによって生成されたファイルなら何でも一時的なアセンブリにコンパイルできるため、それらのアセンブリから型を読み込んでデザイナーに公開できます。 各カスタム ツールの出力は個別の一時的 PE にコンパイルされ、この一時的なコンパイルの成否は、生成されたファイルのコンパイル可否のみによって決まります。 プロジェクトが全体としてビルドされない場合でも、デザイナーは個々の一時的 PE を利用できる場合があります。

 プロジェクト システムは、カスタム ツールの出力ファイルへの変更を追跡するための完全なサポートを提供しますが、これらの変更がカスタム ツールの実行の結果であることが条件です。 カスタム ツールが実行されるたびに、新しい一時的 PE が生成され、適切な通知がデザイナーに送信されます。

> [!NOTE]
> 一時的なプログラム実行可能ファイルの生成ファイルはバックグラウンドで行われるため、コンパイルが失敗した場合でも、ユーザーにエラーは報告されません。

 一時的 PE のサポートを利用するカスタム ツールでは、次の規則に従う必要があります。

- レジストリで **GeneratesDesignTimeSource** を 1 に設定する必要があります。

     この設定がないと、プログラムの実行可能ファイルのコンパイルは行われません。

- 生成されるコードは、グローバル プロジェクト設定と同じ言語である必要があります。

     レジストリで **GeneratesDesignTimeSource** が 1 に設定されている場合、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.DefaultExtension%2A> で要求された拡張機能としてカスタム ツールが報告する内容にかかわらず、一時的 PE はコンパイルされます。 拡張子は *.vb*、 *.cs*、または *.jsl* である必要はありません。任意の拡張子にすることができます。

- カスタム ツールによって生成されるコードは有効である必要があり、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.Generate%2A> が実行を終了した時点でプロジェクトに存在する参照のセットのみを使用して独力でコンパイル可能である必要があります。

     一時的 PE がコンパイルされるとき、コンパイラに提供される唯一のソース ファイルはカスタム ツールの出力です。 そのため、一時的 PE を使用するカスタム ツールでは、プロジェクト内の他のファイルに依存せずにコンパイル可能な出力ファイルを生成する必要があります。

## <a name="see-also"></a>関連項目
- [BuildManager オブジェクトの概要](/previous-versions/8f9kffa8(v=vs.140))
- [単一ファイル ジェネレーターの実装](../../extensibility/internals/implementing-single-file-generators.md)
- [単一ファイル ジェネレーターの登録](../../extensibility/internals/registering-single-file-generators.md)