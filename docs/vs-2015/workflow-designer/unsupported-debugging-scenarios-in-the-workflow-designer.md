---
title: デバッグする場合、ワークフロー デザイナーでサポートされていない |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: 6adbe379-41d0-4681-9cd0-b91f187c3c2c
caps.latest.revision: 4
author: steved0x
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 7b3b47264190afcc75431a55ad6b8b4512f26ea0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62858185"
---
# <a name="unsupported-debugging-scenarios-in-the-workflow-designer"></a>ワークフロー デザイナーでサポートされていないデバッグ シナリオ
[!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)] のワークフロー デザイナーには多くの新機能が追加されていますが、いくつかサポートされていないデバッグ シナリオがあります。 このドキュメントでは、サポートされていないワークフロー デザイナーのデバッグ シナリオについて詳しく説明します。  
  
- コードを編集した後では実行を続行できません。  
  
- ワークフローの任意の場所から実行を続行することはできません (次の設定)。  
  
- カーソルが到達するまで実行を続行できません (カーソル行の前まで実行)。  
  
- デザイナーを使用せずにコード内に作成されたワークフローをデバッグするためにワークフロー デザイナーを使用することはできません。  
  
- 以前のバージョンの [!INCLUDE[wf](../includes/wf-md.md)] で作成されたワークフローを [!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)] デザイナーでデバッグすることはできません。  
  
- アクティビティまたは <xref:System.Activities.Statements.Flowchart> ノード間のリンクにブレークポイントを定義することはできません。  
  
- クリップボードは、デバッグ時には使用できません。  
  
- アクティビティをコピーまたは貼り付けた場合にはブレークポイントは保持されません。  
  
- ワークフローのブレークポイントを呼び出し履歴ウィンドウに設定することはできません。  
  
- デザイナーでブレークポイントを作成するときに、**行**と**文字**の設定、**新しいブレークポイント**ダイアログは使用されません。  
  
- [ブレークポイント] ウィンドウまたはショートカット メニューは、ワークフローのデバッグで、次の列またはオプションをサポートしていません。  
  
    - 条件  
  
    - ヒット カウント  
  
    - ヒット時   
  
    - 関数  
  
    - データ  
  
    - プロセス  
  
    - 逆アセンブルを表示