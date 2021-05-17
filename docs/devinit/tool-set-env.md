---
title: set-env
description: devinit ツール require-set-env。
ms.date: 11/20/2020
ms.topic: reference
author: andysterland
ms.author: andster
manager: jmartens
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.prod: visual-studio-windows
ms.technology: devinit
ms.openlocfilehash: 86e6f7c22ac75d976050858eb2853f9036377fee
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635374"
---
# <a name="set-env"></a>set-env

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

`set-env` ツールを使用すると、現在のプロセスで使用する環境変数を設定できます。 環境変数は現在のプロセスでのみ設定され、他の `devinit` ツールがそのプロセスで実行される場合、それによって使用されます。

このツールでは、.NET Core `Environment.SetEnvironment` API が使用され、その API と同じ制限があります。 詳細については、`Environment.SetEnvironment` の [ドキュメント](/dotnet/api/system.environment.setenvironmentvariable?view=netcore-3.1&preserve-view=true)をご覧ください。

## <a name="usage"></a>使用法

| 名前                                         | Type   | 必須 | 値                                                                       |
|----------------------------------------------|--------|----------|-----------------------------------------------------------------------------|
| **コメント**                                 | string | No       | comments は省略可能なプロパティです。 使用しません。                                       |
| [**input**](#input)                          | string | No       | ツールへの入力。 詳細については、下の「[入力](#input)」を参照してください。               |
| [**additionalOptions**](#additional-options) | string | No       | 詳細については、下の「[追加オプション](#additional-options)」を参照してください。            |

### <a name="input"></a>入力

`set-env` ツールは、`input` プロパティの入力として 1 つの文字列を受け取ります。 文字列は、セミコロン (;) で区切ったキーと値のペア (name=value) 形式の文字列にする必要があります。`input` プロパティの値に基づく 4 つのアクションがあります。

| アクション       | 入力            | 説明                                                                                                                                                              | 例             |
|--------------|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------|
| **list all** | 空または省略 | 現在のすべての環境変数を一覧表示します。                                                                                                                           | `"input":""`        |
| **list one** | string           | 名前によって特定の環境変数の値を表示します。                                                                                                               | `"input":"foo"`     |
| **add**      | string           | 環境変数の値をキーと値のペアとして設定します。 存在しない場合は新しい環境変数を追加し、存在する場合は既存の環境変数の値を設定します。 | `"input":"foo=bar"` |
| **delete**   | string           | 空の値文字列を渡すことによって、既存の環境変数を削除します。                                                                                            | `"input":"foo="`    |

`input` 文字列には、環境変数の展開を含めることができます。たとえば `%userprofile%` は、値が読み取られるときに展開されます。

### <a name="additional-options"></a>追加オプション

 環境変数を設定する場所を指定するために、`--user`、`--process`、または `--machine` を含めることができます。 デフォルトでは、ユーザーを対象とします。 環境変数に使用できるターゲットの詳細については、[EnvironmentVariableTarget](https://docs.microsoft.com/dotnet/api/system.environmentvariabletarget) を参照してください。

### <a name="default-behavior"></a>既定の動作

`set-env` ツールの既定の動作は、現在の環境変数の一覧の表示です。

## <a name="usage-in-a-codespace"></a>codespace での使用

codespace を使用している場合は、[`.devcontainer.json`](https://code.visualstudio.com/docs/remote/devcontainerjson-reference) ファイルで `remoteEnv` プロパティをカスタマイズすることによって、codespace で使用される環境変数を設定できます。

## <a name="example-usage"></a>使用例
`.devinit.json` を使用して `set-env` を実行する方法の例を次に示します。

#### <a name="devinitjson-that-will-set-an-environment-variable-foo-to-value-bar"></a>環境変数 `foo` に値 `bar` を設定する .devinit.json:
```json
{
  "$schema": "https://json.schemastore.org/devinit.schema-3.0",
  "run": [
    {
      "tool": "set-env",
      "input": "foo=bar",
    }
  ]
}
```

#### <a name="devinitjson-that-will-set-an-environment-variable-foo-to-value-bar-stored-in-the-environment-block-associated-with-the-current-process"></a>現在のプロセスに関連付けられている環境ブロックに格納されている環境変数 `foo` に値 `bar` を設定する .devinit.json:
```json
{
  "$schema": "https://json.schemastore.org/devinit.schema-3.0",
  "run": [
    {
      "tool": "set-env",
      "input": "foo=bar",
      "additionalOptions": "--process",
    }
  ]
}
```

#### <a name="devinitjson-that-will-display-the-value-of-an-environment-variable"></a>環境変数の値を表示する .devinit.json:
```json
{
  "$schema": "https://json.schemastore.org/devinit.schema-3.0",
  "run": [
    {
      "tool": "set-env",
      "input": "foo",
    }
  ]
}
```

#### <a name="devinitjson-that-will-list-all-the-environment-variables"></a>すべての環境変数を一覧表示する .devinit.json:
```json
{
  "$schema": "https://json.schemastore.org/devinit.schema-3.0",
  "run": [
    {
      "tool": "set-env",
    }
  ]
}
```

#### <a name="devinitjson-that-will-delete-an-environment-variable"></a>環境変数を削除する .devinit.json:
```json
{
  "$schema": "https://json.schemastore.org/devinit.schema-3.0",
  "run": [
    {
      "tool": "set-env",
      "input": "foo=",
    }
  ]
}
```


#### <a name="devinitjson-that-will-use-environment-variable-expansion"></a>環境変数の拡張を使用する .devinit.json:
```json
{
  "$schema": "https://json.schemastore.org/devinit.schema-3.0",
  "run": [
    {
      "tool": "set-env",
      "input": "_savedPath=%path%",
    }
  ]
}
```

#### <a name="devinitjson-that-will-set-an-environment-variable-value-using-path-manipulation"></a>パス操作を使用して環境変数の値を設定する .devinit.json:
```json
{
  "$schema": "https://json.schemastore.org/devinit.schema-3.0",
  "run": [
    {
      "tool": "set-env",
      "input": "path=%path%;%userprofile%\\CustomFolder",
    }
  ]
}
```

#### <a name="devinitjson-that-will-restore-path-from-saved-copy"></a>保存されたコピーからパスを復元する .devinit.json:
```json
{
  "$schema": "https://json.schemastore.org/devinit.schema-3.0",
  "run": [
    {
      "tool": "set-env",
      "input": "path=%_savedPath%",
    }
  ]
}
```
