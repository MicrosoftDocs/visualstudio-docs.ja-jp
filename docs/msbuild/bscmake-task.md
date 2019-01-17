---
title: BscMake タスク | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vc.task.bscmake
- VC.Project.VCBscMakeTool.PreserveSBR
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- MSBuild (Visual C++), tasks
- BscMake task (MSBuild (Visual C++))
ms.assetid: bb98fc67-cad8-43a7-9598-60df6d734db2
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 6f5a8d7f60793bbd6864fdfa98fc1864d1612955
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2019
ms.locfileid: "53887449"
---
# <a name="bscmake-task"></a>BscMake タスク
> [!IMPORTANT]
>  Visual Studio IDE では、BscMake は使用されなくなりました。 Visual Studio 2008 以降、ブラウザー情報は、*ソリューション* フォルダーの *sdf* ファイルに自動的に格納されます。  
  
 Microsoft Browse Information Maintenance Utility ツール (*bscmake.exe*) をラップします。  *bscmake.exe* ツールは、コンパイル時に作成されるソース ブラウザー ファイル (*.sbr*) からブラウザー情報ファイル (*.bsc*) をビルドします。 *.bsc* ファイルを表示するには、**オブジェクト ブラウザー**を使用します。 詳細については、「[BSCMAKE リファレンス](/cpp/build/reference/bscmake-reference)」を参照してください。  
  
## <a name="parameters"></a>パラメーター  
 **BscMake** タスクのパラメーターの説明を次の表に示します。 タスク パラメーターの大部分は、コマンド ライン オプションに対応します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|**AdditionalOptions**|省略可能な **String** 型のパラメーターです。<br /><br /> コマンド ラインで指定するオプションのリストです。 例: /\<option1> /\<option2> /\<option#> 他の **BscMake** タスク パラメーターでは表されないオプションを指定する場合は、このパラメーターを使用します。<br /><br /> 詳細については、「[BSCMAKE オプション](/cpp/build/reference/bscmake-options)」でオプションの説明を参照してください。|  
|**OutputFile**|省略可能な **String** 型のパラメーターです。<br /><br /> 既定の出力ファイル名をオーバーライドするファイル名を指定します。<br /><br /> 詳細については、「[BSCMAKE オプション](/cpp/build/reference/bscmake-options)」で **/o** オプションの説明を参照してください。|  
|**PreserveSBR**|省略可能な **Boolean** 型のパラメーターです。<br /><br /> `true` の場合、ノンインクリメンタル ビルドを強制的に実行します。 フル ノンインクリメンタル ビルドは *.bsc* ファイルが存在するかどうかに関係なく実行され、*.sbr* ファイルの切り詰めは行われません。<br /><br /> 詳細については、「[BSCMAKE オプション](/cpp/build/reference/bscmake-options)」で **/n** オプションの説明を参照してください。|  
|**Sources**|省略可能な **ITaskItem[]** パラメーターです。<br /><br /> タスクで使用および生成できる MSBuild ソース ファイル アイテムの配列を定義します。|  
|**SuppressStartupBanner**|省略可能な **Boolean** 型のパラメーターです。<br /><br /> `true` の場合、タスクの開始時に著作権およびバージョン番号のメッセージが表示されないようにします。<br /><br /> 詳細については、「[BSCMAKE オプション](/cpp/build/reference/bscmake-options)」で **/NOLOGO** オプションの説明を参照してください。|  
|**TrackerLogDirectory**|省略可能な **String** 型のパラメーターです。<br /><br /> トラッカー ログのディレクトリを指定します。|  
  
## <a name="see-also"></a>関連項目  
 [タスク リファレンス](../msbuild/msbuild-task-reference.md)