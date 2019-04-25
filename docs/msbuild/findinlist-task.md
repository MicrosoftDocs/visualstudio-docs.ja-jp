---
title: FindInList タスク | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- FindInList task [MSBuild]
- MSBuild, FindInList task
ms.assetid: d49b9f84-52a2-4242-9269-b741a7a7e9f7
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7c2f6c5f14f6eff818a265e097f02e2bc76c7372
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62996679"
---
# <a name="findinlist-task"></a>FindInList タスク
指定したリストで、一致する itemspec を含む項目を検索します。

## <a name="parameters"></a>パラメーター
 次の表では、[FindInList タスク](../msbuild/findinlist-task.md)のパラメーターについて説明します。

|パラメーター|説明|
|---------------|-----------------|
|`CaseSensitive`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、検索では大文字と小文字が区別されます。それ以外の場合は区別されません。 既定値は `true`にする必要があります。|
|`FindLastMatch`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、最後の一致を返します。それ以外の場合は最初の一致を返します。 既定値は `false`にする必要があります。|
|`ItemFound`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の読み取り専用の出力パラメーターです。<br /><br /> リスト内で最初に見つかった、一致する項目 (存在する場合)。|
|`ItemSpecToFind`|必須の `String` 型のパラメーターです。<br /><br /> 検索する itemspec です。|
|`List`|必須の <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> itemspec が検索されるリストです。|
|`MatchFileNameOnly`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合は、itemspec のファイル名の部分のみと照合します。それ以外の場合は、itemspec 全体と照合します。 既定値は `true`にする必要があります。|

## <a name="remarks"></a>解説
 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)