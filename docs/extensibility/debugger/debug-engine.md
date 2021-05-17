---
title: デバッグ エンジン | Microsoft Docs
description: デバッグ エンジンがインタープリターまたはオペレーティング システムと連携して、実行制御、ブレークポイント、式の評価などのサービスを提供するしくみについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines
ms.assetid: 148b1efc-ca07-4d8e-bdfc-c723a760c620
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c13dd7165a5f85dc0122f97aaee838c528207f96
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067947"
---
# <a name="debug-engine"></a>デバッグ エンジン
デバッグ エンジン (DE) は、インタープリターまたはオペレーティング システムと連携して、実行制御、ブレークポイント、式の評価などのデバッグ サービスを提供します。 DE は、デバッグ中のプログラムの状態を監視する役割を担います。 DE ではこれを実現するために、CPU から、ランタイムによって提供される API に至るまで、サポートされているランタイムで利用可能なあらゆる手段を駆使します。

 たとえば、共通言語ランタイム (CLR) では、ICorDebugXXX インターフェイスを通じて、実行中のプログラムを監視するためのメカニズムを提供します。 CLR をサポートする DE は、適切な ICorDebugXXX インターフェイスを使用して、デバッグ中のマネージド コード プログラムを追跡します。 その後、状態の変化が DE からセッション デバッグ マネージャー (SDM) に伝達され、SDM から [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE にその情報が転送されます。

> [!NOTE]
> デバッグ エンジンは特定のランタイム、つまり、デバッグ中のプログラムが実行されているシステムをターゲットにします。 CLR はマネージド コード用のランタイムであり、Win32 ランタイムはネイティブ Windows アプリケーション用です。 作成する言語でこれら 2 つのランタイムのいずれかをターゲットにできる場合、必要なデバッグ エンジンは [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に既に用意されています。 実装する必要があるのは、式エバリュエーターだけです。

## <a name="debug-engine-operation"></a>デバッグ エンジンの操作
 監視サービスは DE のインターフェイスを通じて実装され、デバッグ パッケージの動作モードをさまざまに遷移させる可能性があります。 詳細については、「[操作モード](../../extensibility/debugger/operational-modes.md)」を参照してください。 通常は、ランタイム環境ごとに 1 つの DE 実装のみが存在します。

> [!NOTE]
> Transact-SQL および [!INCLUDE[jsprjscript](../../debugger/debug-interface-access/includes/jsprjscript_md.md)] 用には個別の DE 実装が存在しますが、VBScript と [!INCLUDE[jsprjscript](../../debugger/debug-interface-access/includes/jsprjscript_md.md)] は単一の DE を共有します。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のデバッグでは、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] シェルと同じプロセスか、デバッグ中のターゲット プログラムと同じプロセスのいずれかでデバッグ エンジンを実行できます。 後者の方式が採られるのは通常、デバッグ中のプロセスが、実際にはインタープリター下で実行されるスクリプトである場合です。 スクリプトを監視するために、デバッグ エンジンには、インタープリターに関する詳細な情報が必要です。 この場合、インタープリターは実際にはランタイムであり、デバッグ エンジンは特定のランタイム実装用です。 さらに、(たとえば、リモート デバッグのために) 単一 DE の実装をプロセスとコンピューターの境界をまたいで分割することができます。

 DE は [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のデバッグ インターフェイスを公開します。 すべての通信は COM 経由で行われます。 DE は、その読み込み形態 (インプロセス、アウトプロセス、別のコンピューター上) にかかわらず、コンポーネントの通信には影響しません。

 DE では、その特定のランタイム用の DE で式の構文を理解できるよう、式エバリュエーター コンポーネントと連携します。 DE では、言語コンパイラによって生成されたシンボリック デバッグ情報にアクセスするために、シンボル ハンドラー コンポーネントとも連携します。 詳細については、「[式エバリュエーター](../../extensibility/debugger/expression-evaluator.md)」および「[シンボル プロバイダー](../../extensibility/debugger/symbol-provider.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [デバッガー コンポーネント](../../extensibility/debugger/debugger-components.md)
- [式エバリュエーター](../../extensibility/debugger/expression-evaluator.md)
- [シンボル プロバイダー](../../extensibility/debugger/symbol-provider.md)
