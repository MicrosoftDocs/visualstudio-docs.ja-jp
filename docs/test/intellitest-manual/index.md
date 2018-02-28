---
title: "IntelliTest リファレンス マニュアル | Microsoft Developer Test Tools | Microsoft Docs"
ms.custom: 
ms.date: 05/02/2017
ms.reviewer: 
ms.suite: 
ms.technology: vs-devops-test
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- IntelliTest Reference Manual, IntelliTest
ms.author: gewarren
manager: ghogen
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: 30c23fc51f136d7fc3dcfeca191f5c469fb1e331
ms.sourcegitcommit: 7ae502c5767a34dc35e760ff02032f4902c7c02b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/09/2018
---
# <a name="intellitest-reference-manual"></a>IntelliTest リファレンス マニュアル

## <a name="contents"></a>目次

* **[IntelliTest の概要](introduction.md)**
  - [IntelliTest の Hello World](introduction.md#hello-world)
  - [制限事項](introduction.md#limitations)
    * [非決定論的](introduction.md#nondeterminism)
    * [同時実行](introduction.md#concurrency)
    * [ネイティブ コード](introduction.md#native-code)
    * [プラットフォーム](introduction.md#platform)
    * [Language](introduction.md#language)
    * [シンボリック推論](introduction.md#symbolic-reasoning)
    * [スタック トレースの誤り](introduction.md#incorrect-stack)
  - [関連資料](introduction.md#further-reading)<p>&nbsp;</p>

* **[IntelliTest の使用を開始する](getting-started.md)**
  - [重要な属性](getting-started.md#important-attributes)
  - [重要な静的ヘルパー クラス](getting-started.md#helper-classes)<p>&nbsp;</p>
 
* **[テスト生成](test-generation.md)**
  - [テスト ジェネレーター](test-generation.md#test-generators)
  - [パラメーター化した単体テスト](test-generation.md#parameterized-unit-testing)
  - [ジェネリックなパラメーター化した単体テスト](test-generation.md#generic-parameterized)
  - [例外を許可する](test-generation.md#allowing-exceptions)
  - [内部型をテストする](test-generation.md#internal-types)
  - [前提事項とアサーション](test-generation.md#assumptions-and-assertions)
  - [事前条件](test-generation.md#precondition)
  - [事後条件](test-generation.md#postcondition)
  - [テスト不合格](test-generation.md#test-failures)
  - [セットアップと破棄](test-generation.md#setup-teardown)
  - [関連資料](test-generation.md#further-reading)<p>&nbsp;</p>

* **[入力生成](input-generation.md)**
  - [制約ソルバー](input-generation.md#constraint-solver)
  - [動的コード カバレッジ](input-generation.md#dynamic-code-coverage)
  - [整数と浮動小数点数](input-generation.md#integers-and-floats)
  - [オブジェクト](input-generation.md#objects)
  - [既存クラスのインスタンス化](input-generation.md#existing-classes)
  - [可視性](input-generation.md#visibility)
  - [パラメーター化されたモック](input-generation.md#parameterized-mocks)
  - [構造体](input-generation.md#structs)
  - [配列と文字列](input-generation.md#arrays-and-strings)
  - [追加の入力を取得する](input-generation.md#additional-inputs)
  - [関連資料](input-generation.md#further-reading)<p>&nbsp;</p>

* **[探索の範囲](exploration-bounds.md)**
  - [MaxConstraintSolverTime](exploration-bounds.md#maxconstraintsolvertime)
  - [MaxConstraintSolverMemory](exploration-bounds.md#maxconstraintsolvermemory)
  - [MaxBranches](exploration-bounds.md#maxbranches)
  - [MaxCalls](exploration-bounds.md#maxcalls)
  - [MaxStack](exploration-bounds.md#maxstack)
  - [MaxConditions](exploration-bounds.md#maxconditions)
  - [MaxRuns](exploration-bounds.md#maxruns)
  - [MaxRunsWithoutNewTests](exploration-bounds.md#maxrunswithoutnewtests)
  - [MaxRunsWithUniquePaths](exploration-bounds.md#maxrunswithuniquepaths)
  - [MaxExceptions](exploration-bounds.md#maxexceptions)
  - [TestExcludePathBoundsExceeded](exploration-bounds.md#testexcludepathboundsexceeded)
  - [TestEmissionFilter](exploration-bounds.md#testemissionfilter)
  - [TestEmissionBranchHits](exploration-bounds.md#testemissionbranchhits)<p>&nbsp;</p>

* **[属性の解説](attribute-glossary.md)**
  - [PexAssumeNotNull](attribute-glossary.md#pexassumenotnull)
  - [PexClass](attribute-glossary.md#pexclass)
  - [PexGenericArguments](attribute-glossary.md#pexgenericarguments)
  - [PexMethod](attribute-glossary.md#pexmethod)
  - [PexExplorationAttributeBase](attribute-glossary.md#pexexplorationattributebase)
  - [PexAssemblySettings](attribute-glossary.md#pexassemblysettings)
  - [PexAssemblyUnderTest](attribute-glossary.md#pexassemblyundertest)
  - [PexInstrumentAssemblyAttribute](attribute-glossary.md#pexinstrumentassemblyattribute)
  - [PexUseType](attribute-glossary.md#pexusetype)
  - [PexAllowedException](attribute-glossary.md#pexallowedexception)
  - [PexAllowedExceptionFromAssembly](attribute-glossary.md#pexallowedexceptionfromassembly)
  - [PexAllowedExceptionFromType](attribute-glossary.md#pexallowedexceptionfromtype)
  - [PexAllowedExceptionFromTypeUnderTest](attribute-glossary.md#pexallowedexceptionfromtypeundertest)<p>&nbsp;</p>

* **[設定ウォーターフォール](settings-waterfall.md)**

* **[静的ヘルパー クラス](static-helper-classes.md)**
  - [PexAssume](static-helper-classes.md#pexassume)
  - [PexAssert](static-helper-classes.md#pexassert)
  - [PexChoose](static-helper-classes.md#pexchoose)
  - [PexObserve](static-helper-classes.md#pexobserve)
  - [PexSymbolicValue](static-helper-classes.md#pexsymbolicvalue)<p>&nbsp;</p>

* **[Warnings and Errors](warnings-and-errors.md)**
  - [MaxBranches を超えました](warnings-and-errors.md#maxbranches-exceeded)
  - [MaxConstraintSolverTime を超えました](warnings-and-errors.md#maxconstraintsolvertime-exceeded)
  - [MaxConditions を超えました](warnings-and-errors.md#maxconditions-exceeded)
  - [MaxCalls を超えました](warnings-and-errors.md#maxcalls-exceeded)
  - [MaxStack を超えました](warnings-and-errors.md#maxstack-exceeded)
  - [MaxRuns を超えました](warnings-and-errors.md#maxruns-exceeded)
  - [MaxRunsWithoutNewTests を超えました](warnings-and-errors.md#maxrunswithoutnewtests-exceeded)
  - [ソリューションを具体化できません](warnings-and-errors.md#cannot-concretize-solution)
  - [オブジェクトを構築するための情報を指定してください](warnings-and-errors.md#help-construct)
  - [型を見つけるための情報を指定してください](warnings-and-errors.md#help-types)
  - [使用可能な型を推測しました](warnings-and-errors.md#usable-type-guessed)
  - [探索中に予期しないエラーが発生しました](warnings-and-errors.md#unexpected-exploration)
  - [TargetInvocationException](warnings-and-errors.md#targetinvocationexception)
  - [インストルメント化されていないメソッドが呼び出されました](warnings-and-errors.md#uninstrumented-method-called)
  - [外部メソッドが呼び出されました](warnings-and-errors.md#external-method-called)
  - [インストルメント不能なメソッドが呼び出されました](warnings-and-errors.md#uninstrumentable-method-called)
  - [テストの容易性の問題](warnings-and-errors.md#testability-issue)
  - [制限](warnings-and-errors.md#limitation)
  - [観察された呼び出しが一致しません](warnings-and-errors.md#observed-call-mismatch)
  - [静的フィールドに格納された値](warnings-and-errors.md#value-static-field)<p>&nbsp;</p>

## <a name="got-feedback"></a>フィードバックをお寄せください

ご意見や機能に関するご要望を **[UserVoice](https://visualstudio.uservoice.com/forums/121579-visual-studio-2015/category/157869-test-tools?query=IntelliTest)** で投稿してください。
