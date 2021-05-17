---
title: '方法: カスタム デバッグ エンジンをデバッグする | Microsoft Docs'
description: Visual Studio を使用してカスタム デバッグ エンジンまたはカスタム プロジェクトの種類をデバッグできるようにするための手順について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- debug engines, debugging
- debugging [Debugging SDK], custom debug engines
ms.assetid: df27a8d6-3938-45ff-b47f-b684e80b38a0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ffd21fb08e920209d47ff66feb436f8a83aab53e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059926"
---
# <a name="how-to-debug-a-custom-debug-engine"></a>方法: カスタム デバッグ エンジンをデバッグする
プロジェクトの種類では、<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg.DebugLaunch%2A> メソッドからデバッグ エンジン (DE) を起動します。 つまり、DE は、そのプロジェクトの種類を制御している [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のインスタンスの制御下で起動されます。 ただし、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のそのインスタンスでは DE をデバッグできません。 以下に示すのは、カスタム DE をデバッグできるようにするための手順です。

> [!NOTE]
> :     「カスタム デバッグ エンジンをデバッグする」の手順では、DE が起動するまで待ってから DE にアタッチする必要があります。 DE が起動したときに表示される DE の開始近くにメッセージ ボックスを配置した場合は、その時点でアタッチしてから、メッセージ ボックスをクリアして続行できます。 それにより、すべての DE イベントをキャッチできます。

> [!WARNING]
> 次の手順を試みる前に、リモート デバッグがインストールされている必要があります。 詳細については、「[リモート デバッグ](../../debugger/remote-debugging.md)」を参照してください。

## <a name="debug-a-custom-debug-engine"></a>カスタム デバッグ エンジンをデバッグする

1. リモート デバッグ モニター *msvsmon.exe* を起動します。

2. *msvsmon.exe* の **[ツール]** メニューから、 **[オプション]** を選択して **[オプション]** ダイアログ ボックスを開きます。

3. [認証なし] オプションを選択し、 **[OK]** をクリックします。

4. [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のインスタンスを起動し、カスタム DE プロジェクトを開きます。

5. [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の 2 番目のインスタンスを起動し、DE を起動するカスタム プロジェクトを開きます (開発の場合、これは通常、VSIP がインストールされるときに設定される実験用レジストリ ハイブにあります)。

6. この [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の 2 番目のインスタンスで、カスタム プロジェクトからソース ファイルを読み込み、デバッグされるプログラムを起動します。 しばらく待ってから DE が読み込まれるようにするか、またはブレークポイントにヒットするまで待ちます。

7. [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の最初のインスタンス (DE プロジェクト) で、 **[デバッグ]** メニューから **[プロセスにアタッチ]** を選択します。

8. **[プロセスにアタッチ]** ダイアログ ボックスで、 **[トランスポート]** を **[リモート (認証なしでのみネイティブ)]** に変更します。

9. **[修飾子]** をコンピューターの名前に変更します (注: 入力の履歴が存在するため、この名前は 1 回しか入力する必要がありません)。

10. **[選択可能なプロセス]** 一覧で、実行されている DE のインスタンスを選択し、 **[アタッチ]** ボタンをクリックします。

11. シンボルが DE に読み込まれたら、DE コードにブレークポイントを設定します。

12. デバッグ プロセスを停止して再起動するたびに、手順 6. ～ 10. を繰り返します。

## <a name="debug-a-custom-project-type"></a>カスタム プロジェクトの種類をデバッグする

1. 通常のレジストリ ハイブで [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] を起動し、プロジェクトの種類のプロジェクトを読み込みます (これは、プロジェクトの種類のインスタンス化ではなく、プロジェクトの種類へのソースです)。

2. プロジェクトのプロパティを開き、 **[デバッグ]** ページに移動します。 **[コマンド]** に、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE のパスを入力します (これは、既定では *[ドライブ]* \Program Files\Microsoft [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 8\Common7\IDE\devenv.exe です)。

3. **[コマンド引数]** に、(VSIP がインストールされるときに作成された) 実験用レジストリ ハイブの「`/rootsuffix exp`」と入力します。

4. [ **OK** ] をクリックして変更内容を確定します。

5. **F5** キーを押して、プロジェクトの種類を起動します。 これにより、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の 2 番目のインスタンスが起動されます。

6. この時点で、プロジェクトの種類のソース コードにブレークポイントを設定できます。

7. [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の 2 番目のインスタンスで、プロジェクトの種類の新しいインスタンスを読み込むか、または作成します。 この読み込みまたは作成中に、ブレークポイントにヒットする可能性があります。

8. プロジェクトの種類をデバッグします。

9. DE を起動するプロセスをデバッグすることを選択した場合は、「カスタム デバッグ エンジンをデバッグする」の手順を実行して、DE が起動されてから DE にアタッチできます。 これにより、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の 3 つのインスタンスが実行されます。つまり、1 つはプロジェクトの種類のソース用、2 番目はインスタンス化されたプロジェクトの種類用、3 番目は DE にアタッチされたインスタンスです。

## <a name="see-also"></a>関連項目
- [カスタム デバッグ エンジンの作成](../../extensibility/debugger/creating-a-custom-debug-engine.md)
