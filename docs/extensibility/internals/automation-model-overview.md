---
title: オートメーション モデルの概要 | Microsoft Docs
description: Visual Studio のアドインまたは拡張機能を記述できるオブジェクトのセットで構成される Visual Studio オートメーション モデルについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], about automation
- extensibility
ms.assetid: 12b6d6db-0d22-4aaa-aa7d-1365f759b7b0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d763fea140ddac1b4dba955421c563700373dc22
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086236"
---
# <a name="automation-model-overview"></a>オートメーション モデルの概要
オートメーション モデルは、Visual Studio のアドインまたは拡張機能を記述できるオブジェクトのセットで構成されています。 アドインは、Visual Studio 環境を操作したり、一般的なタスクを自動化したりできるアプリケーションです。 Visual Studio 拡張機能では、Visual Studio のカスタム コンポーネントを作成したり、テキスト エディターなどの標準コンポーネントの機能を追加したりできます。

## <a name="objects-in-the-automation-model"></a>オートメーション モデル内のオブジェクト
 オートメーション モデルは、共通環境の主要なファセットを制御するオブジェクトの関連グループで構成されています。 次の図は、オートメーション モデルを構成する Visual Studio オブジェクトの広範なセットを示しています。

 ![Visual Studio オートメーション オブジェクト チャート](../../extensibility/internals/media/vsvisualstudioautomationobjectchart.gif "vsVisualStudioAutomationObjectChart")

 詳細については、「[Visual Studio 環境の拡張](/previous-versions/esk3eey8(v=vs.140))」を参照してください。

 環境によって、さまざまな機能領域のモデルが提供されます。 たとえば、コードで見つかる可能性のあるさまざまな要素のコード モデルがあります。 さまざまなドキュメント要素のドキュメント モデルがあります。 VSPackage プロバイダーにとって特に重要な領域がプロジェクト領域です。 新しいプロジェクトの種類は、[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] と [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] の場合とほぼ同じ方法でオートメーション モデルに寄与させることができます。 このプロセスについては、「[VSPackage でのオートメーションの提供](../../extensibility/internals/providing-automation-for-vspackages.md)」で説明しています。

 環境のオートメーション モデルの拡張を検討できる場所は次のとおりです。

- Project

- ドキュメント

- コード

- ビルド

オートメーションの詳細については、[Visual Studio のオートメーションと拡張性](/previous-versions/visualstudio/visual-studio-2015/extensibility/extensibility-in-visual-studio?preserve-view=true&view=vs-2015)に関するページを参照してください。 このドキュメントとそのリンク先のドキュメントは、VSPackage のオートメーションを提供する方法についての意思決定に役立ちます。

## <a name="see-also"></a>関連項目
- [方法 : アドインを作成する](/previous-versions/80493a3w(v=vs.140))