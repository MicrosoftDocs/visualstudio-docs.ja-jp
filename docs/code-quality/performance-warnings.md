---
title: パフォーマンスに関する警告
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.performancerules
helpviewer_keywords:
- warnings, performance
- performance warnings
- performance, warnings
- managed code analysis warnings, performance warnings
ms.assetid: e014ac3a-02e6-46d9-942c-3491dd63782f
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0ebbe15bdcef27b7b19474b2c42f0b62741fd53a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72649155"
---
# <a name="performance-warnings"></a>パフォーマンスに関する警告
パフォーマンスの警告は、高パフォーマンスのライブラリとアプリケーションをサポートします。

## <a name="in-this-section"></a>このセクションの内容

| 規則 | 説明 |
| - | - |
| [CA1800: 不必要にキャストしません](../code-quality/ca1800.md) | 二重のキャストがあるとパフォーマンスが低下します。特に、小さな繰り返しステートメントでキャストが実行される場合はそうです。 |
| [CA1801: 使用されていないパラメーターをレビューします](../code-quality/ca1801.md) | メソッドのシグネチャに、メソッドの本体で使用されていないパラメーターがあります。 |
| [CA1802: 適切な場所にリテラルを使用します](../code-quality/ca1802.md) | フィールドが静的および読み取り専用として宣言されており ([!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] では Shared および ReadOnly)、コンパイル時に計算できるである値で初期化されています。 対象のフィールドに割り当てられた値はコンパイル時に計算できるであるため、宣言を const ([!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]) フィールドに変更して、実行時ではなくコンパイル時に値が計算されるようにします。 |
| [CA1804: 使用されていないローカルを削除します](../code-quality/ca1804.md) | 使用されていないローカル変数や不要な引数があると、アセンブリのサイズが大きくなり、パフォーマンスが低下します。 |
| [CA1806: メソッドの結果を無視しない](../code-quality/ca1806.md) | 新しいオブジェクトが作成されましたが、使用されていないか、新しい文字列を作成して返すメソッドが呼び出され、新しい文字列が使用されていないか、またはコンポーネントオブジェクトモデル (COM) または P/Invoke メソッドが、使用されていない HRESULT またはエラーコードを返しています。 |
| [CA1809: ローカルを使用しすぎないでください](../code-quality/ca1809.md) | パフォーマンス最適化の一般的な方法として、メモリではなくプロセッサのレジスタに値を格納する方法があります。これは "値のレジスタ格納" と呼ばれます。  すべてのローカル変数が enregistered される可能性を高めるには、ローカル変数の数を64に制限します。 |
| [CA1810: 参照型の静的フィールドをインラインで初期化します](../code-quality/ca1810.md) | 型で明示的な静的コンストラクターを宣言すると、Just-In-Time (JIT) コンパイラが、静的コンストラクターが呼び出されたことを確認するために、型の静的メソッドと静的インスタンス コンストラクターに個別にチェックを追加します。 静的コンストラクターのチェックによってパフォーマンスが低下することがあります。 |
| [CA1811: 呼び出されていないプライベート コードを使用しません](../code-quality/ca1811.md) | プライベートまたは内部 (アセンブリレベル) のメンバーは、アセンブリ内の呼び出し元を持っていません。また、共通言語ランタイムによって呼び出されず、デリゲートによって呼び出されません。 |
| [CA1812: インスタンス化されていない内部クラスを使用しないでください](../code-quality/ca1812.md) | アセンブリ レベルの型のインスタンスが、アセンブリ内のコードから作成されません。 |
| [CA1813: シールされていない属性を使用しません](../code-quality/ca1813.md) | .NET には、カスタム属性を取得するためのメソッドが用意されています。 既定では、これらのメソッドで属性の継承階層が検索されます。 属性をシールすると、継承階層の全体が検索されなくなるため、パフォーマンスが向上します。 |
| [CA1814: 複数次元の配列ではなくジャグ配列を使用します](../code-quality/ca1814.md) | ジャグ配列とは、その要素も配列である配列です。 要素を構成する配列のサイズは異なる可能性があるため、一部のデータセットで無駄な領域が生じる可能性があります。 |
| [CA1815: equals および operator equals を値型でオーバーライドします](../code-quality/ca1815.md) | 値型の場合、Equals を継承した実装が Reflection ライブラリを使用して、すべてのフィールドの内容を比較します。 Reflection は計算コストが高いため、場合によってはすべてのフィールドで等値性を比較する必要はありません。 ユーザーがインスタンスの比較または並べ替えを行うことや、ハッシュ テーブル キーとしてインスタンスを使用することが予想される場合には、値型に Equals を実装する必要があります。 |
| [CA1816: GC.SuppressFinalize を正しく呼び出します](../code-quality/ca1816.md) | Dispose の実装であるメソッドは、GC を呼び出しません。Gc.suppressfinalize、または Dispose の実装ではないメソッドは GC を呼び出します。Gc.suppressfinalize、またはメソッドは GC を呼び出します。Gc.suppressfinalize は、この ([!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]) 以外のものを渡します。 |
| [CA1819: プロパティは、配列を返すことはできません](../code-quality/ca1819.md) | プロパティが読み取り専用の場合でも、プロパティによって返される配列は書き込み禁止になりません。 配列の改ざんを防ぐには、プロパティで配列のコピーを返す必要があります。 一般に、このようなプロパティを呼び出すときのパフォーマンス低下は理解されません。 |
| [CA1820: 文字列の長さを使用して空の文字列をテストします](../code-quality/ca1820.md) | String.Length プロパティまたは String.IsNullOrEmpty メソッドを使用して文字列を比較する方法は、Equals を使用する場合よりもはるかに高速です。 |
| [CA1821: 空のファイナライザーを削除します](../code-quality/ca1821.md) | オブジェクトの有効期間の追跡に関連するパフォーマンス オーバーヘッドが増大するため、ファイナライザーは可能な限り使用しないでください。 空のファイナライザーを使用すると、追加のオーバーヘッドが発生します。 |
| [CA1822: メンバーを static に設定します](../code-quality/ca1822.md) | インスタンス データにアクセスしない、またはインスタンス メソッドを呼び出さないメンバーは、静的 ([!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] では共有) としてマークできます。 メソッドを静的としてマークすると、コンパイラはこれらのメンバーに対する非仮想呼び出しサイトを出力します。 パフォーマンス重視のコードでは、これにより大きくパフォーマンスを向上できます。 |
| [CA1823: 使用されていないプライベート フィールドを使用しません](../code-quality/ca1823.md) | アセンブリ内でアクセスされていないと思われるプライベート フィールドが検出されました。 |
| [CA1824: アセンブリを NeutralResourcesLanguageAttribute に設定します](../code-quality/ca1824.md) | NeutralResourcesLanguage 属性は、ResourceManager に対し、アセンブリのニュートラル カルチャのリソースを表示するために使用した言語を通知します。 これにより、読み込んだ最初のリソースに対する検索のパフォーマンスが向上し、ワーキング セットを縮小できます。 |
| [CA1825: 長さ0の配列割り当てを回避する](../code-quality/ca1825.md) | 長さ0の配列を初期化すると、不要なメモリ割り当てにつながります。 代わりに、<xref:System.Array.Empty%2A?displayProperty=nameWithType> を呼び出すことによって、静的に割り当てられた空の配列インスタンスを使用します。 メモリ割り当ては、このメソッドのすべての呼び出しで共有されます。 |
