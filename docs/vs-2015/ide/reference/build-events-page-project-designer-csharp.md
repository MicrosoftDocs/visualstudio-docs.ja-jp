---
title: '[ビルド イベント] ページ (プロジェクト デザイナー) (C#) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- cs.ProjectPropertiesBuildEvents
helpviewer_keywords:
- build events
- Project Designer, Build Events page
- pre-build events
- post-build events
ms.assetid: 3fff9ae5-213c-46ea-a660-1d70acb6c922
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: e55d9d34a4837e2c01d78cc1f52ae2a25f28da8d
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54785785"
---
# <a name="build-events-page-project-designer-c"></a>[ビルド イベント] ページ (プロジェクト デザイナー) (C#)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
**プロジェクト デザイナー**の **[ビルド イベント]** ページを使用して、ビルド構成の手順を指定します。 また、あらゆるビルド後イベントを実行する条件を指定することもできます。 詳細については、「[方法 : ビルド イベントを指定する (C#)](../../ide/how-to-specify-build-events-csharp.md)」および「[方法 : ビルド イベントを指定する (Visual Basic)](../../ide/how-to-specify-build-events-visual-basic.md)」を参照してください。  
  
## <a name="uielement-list"></a>UIElement の一覧  
 **構成**  
 このコントロールは、このページでは編集できません。 このコントロールの詳細については、「[[ビルド] ページ (プロジェクト デザイナー) (C#)](../../ide/reference/build-page-project-designer-csharp.md)」を参照してください。  
  
 **プラットフォーム**  
 このコントロールは、このページでは編集できません。 このコントロールの詳細については、「[[ビルド] ページ (プロジェクト デザイナー) (C#)](../../ide/reference/build-page-project-designer-csharp.md)」を参照してください。  
  
 **ビルド前に実行するコマンド ライン**  
 ビルド開始前に実行する任意のコマンドを指定します。 長いコマンドを入力するには、**[ビルド前の編集]** をクリックして [[ビルド前に実行するコマンド ライン] / [ビルド後に実行するコマンド ライン] ダイアログ ボックス](../../ide/reference/pre-build-event-post-build-event-command-line-dialog-box.md)を表示します。  
  
> [!NOTE]
>  プロジェクトが最新の状態で、ビルドがトリガーされない場合、ビルド前イベントは実行されません。  
  
 **ビルド後に実行するコマンド ライン**  
 ビルド終了後に実行する任意のコマンドを指定します。 長いコマンドを入力するには、**[ビルド後の編集]** をクリックして **[ビルド前に実行するコマンド ライン] / [ビルド後に実行するコマンド ライン] ダイアログ ボックス**を表示します。  
  
> [!NOTE]
>  .bat ファイルを実行するすべてのビルド後コマンドの前に `call` ステートメントを追加します。 たとえば、`call C:\MyFile.bat` または `call C:\MyFile.bat call C:\MyFile2.bat` のようにします。  
  
 **ビルド後イベントの実行**  
 次の表に示すように、実行するビルド後イベントの条件を指定します。  
  
|オプション|結果|  
|------------|------------|  
|**常時**|ビルド後イベントは、ビルドが成功したかどうかに関係なく実行されます。|  
|**ビルドが成功したとき**|ビルド後イベントは、ビルドが成功した場合に実行されます。 したがって、ビルドが成功した場合は、最新のプロジェクトについてもイベントが実行されます。|  
|**ビルドがプロジェクト出力を更新したとき**|ビルド後イベントは、コンパイラの出力ファイル (.exe または .dll) が以前のコンパイラの出力ファイルと異なる場合にのみ実行されます。 したがって、ビルド後イベントは、プロジェクトが最新の場合は実行されません。|  
  
## <a name="see-also"></a>参照  
 [方法 : ビルド イベントを指定する (Visual Basic)](../../ide/how-to-specify-build-events-visual-basic.md)   
 [方法 : ビルド イベントを指定する (C#)](../../ide/how-to-specify-build-events-csharp.md)   
 [プロジェクトのプロパティのリファレンス](../../ide/reference/project-properties-reference.md)   
 [コードのコンパイルとビルド](../../ide/compiling-and-building-in-visual-studio.md)
