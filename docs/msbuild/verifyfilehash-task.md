---
title: VerifyFileHash タスク | Microsoft Docs
ms.date: 01/28/2019
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- VerifyFileHash task [MSBuild]
- MSBuild, VerifyFileHash task
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: faf7738019680085020b9650094931d5860bc29b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62577363"
---
# <a name="verifyfilehash-task"></a>VerifyFileHash タスク

ファイルが予想されるファイル ハッシュと一致することを確認します。

このタスクは 15.8 で追加されましたが、16.0 より前の MSBuild バージョンで使用するには[回避策](https://github.com/Microsoft/msbuild/pull/3999#issuecomment-458193272)が必要です。

## <a name="task-parameters"></a>タスク パラメーター

 `VerifyFileHash` タスクのパラメーターの説明を次の表に示します。

|パラメーター|説明|
|---------------|-----------------|
|`File`|必須の <xref:Microsoft.Build.Framework.ITaskItem> 型のパラメーターです。<br /><br />ハッシュ値を計算し、検証するファイル。|
|`Hash`|必須の `String` 型のパラメーターです。<br /><br />予想されるファイル ハッシュ。|
|`Items`|<xref:Microsoft.Build.Framework.ITaskItem>`[]` 出力パラメーター。<br /><br />`Files` 入力と、ファイル ハッシュに設定された追加メタデータ。|
|`Algorithm`|省略可能な `String` 型のパラメーターです。<br /><br />アルゴリズム。 許可値: `SHA256`、`SHA384`、`SHA512`。 既定値 = `SHA256`。|
|`HashEncoding`|省略可能な `String` 型のパラメーターです。<br /><br />生成されたハッシュに使用するエンコード。 既定値は `hex` です。 許可値 = `hex`、`base64`。|

## <a name="example"></a>例

次の例では、`VerifyFileHash` タスクを使用してそのチェックサムが検証されます。

```xml
<Project>
  <Target Name="VerifyHash">
    <GetFileHash Files="$(MSBuildProjectFullPath)">
      <Output
          TaskParameter="Items"
          ItemName="FilesWithHashes" />
    </GetFileHash>

    <Message Importance="High"
             Text="@(FilesWithHashes->'%(Identity): %(FileHash)')" />

    <VerifyFileHash File="$(MSBuildThisFileFullPath)"
                    Hash="$(ExpectedHash)" />
  </Target>
</Project>
```

## <a name="see-also"></a>関連項目

- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)