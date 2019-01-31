---
title: MSBuild 応答ファイル | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- response files, MSBuild
- MSBuild, response files
- MSBuild, .rsp files
- .rsp files
ms.assetid: 9f53987b-20ee-470a-ab62-fce997bb5e15
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c3777be5701e9876352db41a5454d5e12668f6f1
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2019
ms.locfileid: "54932118"
---
# <a name="msbuild-response-files"></a>MSBuild 応答ファイル
応答 (*.rsp*) ファイルは、*MSBuild.exe* のコマンド ライン スイッチを含むテキスト ファイルです。 各スイッチを個別の行に記述することも、すべてのスイッチを 1 つの行に記述することもできます。 コメント行は **#** 記号で始まります。 **@** スイッチは、*MSBuild.exe* に別の応答ファイルを渡すために使用されます。  
  
## <a name="msbuildrsp"></a>MSBuild.rsp
自動応答ファイルは、プロジェクトをビルドする際に *MSBuild.exe* によって自動的に使用される特別な *.rsp* ファイルです。 この *MSBuild.rsp* ファイルは、*MSBuild.exe* と同じディレクトリに配置する必要があります。それ以外の場合は検出されません。 このファイルを編集して、既定のコマンド ライン スイッチを *MSBuild.exe* に指定できます。 たとえば、プロジェクトをビルドする際に毎回同じロガーを使用する場合は、**-logger** スイッチを *MSBuild.rsp* に追加することで、プロジェクトをビルドするたびに *MSBuild.exe* でそのロガーが使用されるようになります。 

## <a name="directorybuildrsp"></a>Directory.Build.rsp
バージョン 15.6 以降では、MSBuild は、プロジェクトの親ディレクトリで *Directory.Build.rsp* という名前のファイルを検索します。  これは、ソース コード リポジトリでコマンド ライン ビルド中に既定の引数を指定する場合に役立つことがあります。  ホスト型ビルドのコマンド ライン引数を指定する場合にも使用できます。 

## <a name="see-also"></a>関連項目  
 [MSBuild リファレンス](../msbuild/msbuild-reference.md)   
 [コマンド ライン リファレンス](../msbuild/msbuild-command-line-reference.md)