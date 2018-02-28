---
title: "[単体テストの作成] コマンドを使用した単体テスト メソッド スタブの作成 | Microsoft Docs"
ms.custom: 
ms.date: 05/02/2017
ms.reviewer: 
ms.suite: 
ms.technology: vs-devops-test
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- IntelliTest, Get started
ms.author: gewarren
manager: ghogen
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: 9016006f9774c4a9eff2937f32543b9f8d9f5fb8
ms.sourcegitcommit: 7ae502c5767a34dc35e760ff02032f4902c7c02b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/09/2018
---
# <a name="get-started-with-microsoft-intellitest"></a>Microsoft IntelliTest の概要

* IntelliTest を初めて使用する場合
  * [Channel 9 ビデオ](https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Intellitest)を見る
  * この [MSDN マガジンに記載されている概要](https://msdn.microsoft.com/magazine/dn904672.aspx)を読む
  * Microsoft の[ドキュメント](../../test/generate-unit-tests-for-your-code-with-intellitest.md)を読む
* [Stack Overflow](http://stackoverflow.com/questions/tagged/intellitest) で質問する
* このリファレンス マニュアルの残りの部分を読む
* クイック リファレンスのこのページを印刷する

## <a name="important-attributes"></a>重要な属性

* [PexClass](attribute-glossary.md#pexclass): **PUT** を含む型をマークします。
* [PexMethod](attribute-glossary.md#pexmethod): **PUT** をマークします。
* [PexAssumeNotNull](attribute-glossary.md#pexassumenotnull): null 以外のパラメーターをマークします。

```csharp
using Microsoft.Pex.Framework;

[..., PexClass(typeof(Foo))]
public partial class FooTest {
    [PexMethod]
    public void Bar([PexAssumeNotNull]Foo target, int i) {
        target.Bar(i);
    }
}
```

* [PexAssemblyUnderTest](attribute-glossary.md#pexassemblyundertest): テスト プロジェクトをプロジェクトにバインドします。
* [PexInstrumentAssembly](attribute-glossary.md#pexinstrumentassemblyattribute): インストルメント化するアセンブリを指定します。

```csharp
[assembly: PexAssemblyUnderTest("MyAssembly")] // also instruments "MyAssembly"
[assembly: PexInstrumentAssembly("Lib")]
```

## <a name="helper-classes"></a> 重要な静的ヘルパー クラス

* [PexAssume](static-helper-classes.md#pexassume): 前提事項 (入力フィルター) を評価します。
* [PexAssert](static-helper-classes.md#pexassert): アサーションを評価します。
* [PexChoose](static-helper-classes.md#pexchoose): 新しい選択項目 (追加入力) を生成します。
* [PexObserve](static-helper-classes.md#pexobserve): ライブ値を生成されたテストに記録します。

```csharp
[PexMethod]
void StaticHelpers(Foo target) {
    PexAssume.IsNotNull(target);

    int i = PexChoose.Value<int>("i");
    string result = target.Bar(i);

    PexObserve.ValueForViewing<string>("result", result);
    PexAssert.IsNotNull(result);
}
```

## <a name="got-feedback"></a>フィードバックをお寄せください

ご意見や機能に関するご要望を [UserVoice](https://visualstudio.uservoice.com/forums/121579-visual-studio-2015/category/157869-test-tools?query=IntelliTest) で投稿してください。
