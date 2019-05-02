---
title: '方法: ワークフロー内のブレークポイントの設定 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: e41b21c9-c061-4358-8e2f-eb5e412864a8
caps.latest.revision: 10
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 47d53ad2579ce24f6d5fde2503a0acc98b4f7f5c
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63444134"
---
# <a name="how-to-set-breakpoints-in-workflows"></a>方法: ワークフロー内のブレークポイントを設定する
[!INCLUDE[wfd1](../includes/wfd1-md.md)]を使用すると、Visual Basic コードまたは C# コードを使用する場合と同じように、グラフィカル ワークフローにブレークポイントを設定できます。 設定したそれぞれのブレークポイントで、ワークフローの実行が停止します。  
  
 ブレークポイントでは、次の 3 つの状態があります。*保留中*、*バインド*、および*エラー*します。 ブレークポイントは、設定時には "保留" になり、穴のない赤いアイコンで表示されます。 特定の種類のワークフローがランタイムによって読み込まれると、ブレークポイントの状態は "バインド" になります。 不適切な形式のブレークポイントを指定した場合 (アクティビティ名が無効など) は、エラー ウィンドウが表示されます。 ブレークポイントはブレークポイント ウィンドウに追加されますが、小さな x 印が付きます。  
  
> [!NOTE]
> 呼び出されるワークフローに対してブレークポイントを設定することはできません。  
> 
> [!WARNING]
> オプションを選択するようにして**を有効にする [マイ コードのみ (マネージのみ)** から、**ツール**、**オプション**、**デバッグ**する前に] メニューデバッグします。 別のシーケンス内で入れ子になった 2 つのシーケンスがあり、最初の内部シーケンスにブレークポイントを設定する場合、以下のキーを押して**F11**場合に、2 つ目の内部シーケンスにデバッグは、<strong>を有効にする マイ コードのみ (マネージのみ)</strong>オプションが選択されていません。  
> 
> [!WARNING]
> XAML ファイルのプロパティへの完全パスが正確でない場合、ワークフロー内のブレークポイントにヒットしません。XAML ファイルへの完全パスは、プロジェクトやソリューションを別のフォルダーや別のコンピューターへ移動すると正確ではなくなります。Ctrl キーを押しながら S キーを押すと、完全パスのプロパティが保存および更新されます。  
  
### <a name="to-set-a-breakpoint-on-an-activity-in-the-design-view"></a>デザイン ビューでアクティビティにブレークポイントを設定するには  
  
1. デバッガーを中断する位置にあるアクティビティを選択します。  
  
2. **デバッグ**メニューの **ブレークポイントの切り替え**します。 アクティビティの左上端に赤色のアイコンが表示されます。  
  
     または、ショートカット キーも**F9**するか、アクティビティを選択することができます、アクティビティを右クリックし、選択した後にキー**ブレークポイント**し**ブレークポイントの挿入**、コンテキスト メニュー。  
  
## <a name="see-also"></a>関連項目  
 [方法: ワークフロー デバッガーを起動します。](../workflow-designer/how-to-invoke-the-workflow-debugger.md)   
 [ワークフロー デザイナーでワークフローのデバッグ](../workflow-designer/debugging-workflows-with-the-workflow-designer.md)   
 [方法: ワークフロー デザイナーを使用して XAML をデバッグする](../workflow-designer/how-to-debug-xaml-with-the-workflow-designer.md)