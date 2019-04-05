---
title: Vspackage の管理 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, autoloading
- VSPackages, delayed loading
- delay loading
- VSPackages, loading
ms.assetid: 386e0ce5-4107-4164-b0cd-1cf43eb5e7cf
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a316d2af6ecb76c573cfb43e1334df1933a2989b
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56694713"
---
# <a name="manage-vspackages"></a>Vspackage を管理します。
ほとんどの場合は、プロジェクトと項目テンプレートの登録し、パッケージを自動的に読み込むため、Vspackage の管理について心配する必要はありません。 ただし、状況によっては、パッケージを管理するためにさらに詳しくを学習する必要があります。

## <a name="use-the-experimental-instance"></a>実験用インスタンスを使用して、
 実験用インスタンスの詳細についてを参照してください。[実験用インスタンス](../extensibility/the-experimental-instance.md)します。

## <a name="register-and-unregister-vspackages"></a>登録して、Vspackage の登録解除
 登録し、Vspackage とその他の種類の拡張機能の登録を解除する方法については、[登録し、Vspackage の登録解除](../extensibility/registering-and-unregistering-vspackages.md)を参照してください。

## <a name="load-a-vspackage"></a>VSPackage を読み込む
 Vspackage は、autoload 特定 CMDUICONTEXT GUID の電源がオンに設定できます。 詳細については、[ロード Vspackage](../extensibility/loading-vspackages.md)を参照してください。

## <a name="use-asyncpackage-to-load-vspackages-in-the-background"></a>AsyncPackage を使用して、バック グラウンドで Vspackage を読み込む
 `AsyncPackage`クラスは、Visual Studio での UI の応答性の向上のバック グラウンド スレッドでのパッケージの読み込みを使用できます。 詳細については、「[方法 :AsyncPackage を使用して、バック グラウンドで Vspackage を読み込む](../extensibility/how-to-use-asyncpackage-to-load-vspackages-in-the-background.md)します。

## <a name="rule-based-ui-context-for-extensions"></a>ルール ベースの UI コンテキストの拡張機能
 ルール ベースの UI コンテキストを使用する UI コンテキストがアクティブになるし、関連付けられている Vspackage が読み込まれる正確な条件を定義する拡張機能の作成者。 詳細については、「[方法 :Visual Studio 拡張機能のルール ベースの UI コンテキストを使用して](../extensibility/how-to-use-rule-based-ui-context-for-visual-studio-extensions.md)します。

## <a name="diagnose-extension-performance"></a>拡張機能のパフォーマンスを診断する
拡張機能は、起動とソリューションの読み込みのパフォーマンスに影響します。 Visual Studio 拡張機能への影響を計算する方法およびどのできます分析することがローカルで拡張機能を拡張機能に影響を与えるパフォーマンスとして表示することがあるかどうかを説明します。 詳細については、「[方法 :拡張機能のパフォーマンス診断](how-to-diagnose-extension-performance.md)します。

## <a name="troubleshoot-vspackages"></a>Vspackage をトラブルシューティングします。
 読み込まれないか、エラーが発生する Vspackage のトラブルシューティングの手法を確認します。[Vspackage をトラブルシューティングします。](../extensibility/troubleshooting-vspackages.md)

## <a name="see-also"></a>関連項目
- [VSPackage](../extensibility/internals/vspackages.md)