---
title: "デザイン警告 |Microsoft ドキュメント"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-code-analysis
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vs.codeanalysis.designrules
helpviewer_keywords:
- design warnings
- managed code analysis warnings, design warnings
- warnings, design
ms.assetid: 34e65a18-560c-423f-814f-519089e318cf
caps.latest.revision: 
author: gewarren
ms.author: gewarren
manager: ghogen
ms.workload:
- multiple
ms.openlocfilehash: 1ed7e9109e36255a8c8390d26455d6c3c568e550
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/22/2017
---
# <a name="design-warnings"></a>デザイン上の警告
デザイン警告は、.NET Framework デザイン ガイドラインに従っていることをサポートします。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|ルール|説明|  
|----------|-----------------|  
|[CA1000: ジェネリック型の静的メンバーを宣言しません](../code-quality/ca1000-do-not-declare-static-members-on-generic-types.md)|ジェネリック型の静的メンバーを呼び出すときには、その型の型引数も指定する必要があります。 推論をサポートしないジェネリック インスタンス メンバーを呼び出すときには、そのメンバーに型引数を指定する必要があります。 この 2 つの場合、型引数を指定するときに使用される構文は異なりますが、混同される可能性があります。|  
|[CA1001: 破棄可能なフィールドを所有する型は、破棄可能でなければなりません](../code-quality/ca1001-types-that-own-disposable-fields-should-be-disposable.md)|クラスの宣言および System.IDisposable 型ではインスタンス フィールドを実装し、クラスが IDisposable を実装していません。 IDisposable フィールドを宣言するクラスは間接的にアンマネージ リソースを所有しているため、IDisposable インターフェイスを実装する必要があります。|  
|[CA1002: ジェネリック リストを公開しません](../code-quality/ca1002-do-not-expose-generic-lists.md)|System.Collections.Generic.List < (の\<(T >) >) は、パフォーマンス、継承されません用に設計されたジェネリック コレクション。 このため、List には仮想メンバーは含まれません。 代わりに、継承を目的としたジェネリック コレクションを公開する必要があります。|  
|[CA1003: 汎用イベント ハンドラーのインスタンスを使用します](../code-quality/ca1003-use-generic-event-handler-instances.md)|型が void を返す、2 つのパラメーター (1 つはオブジェクトと、2 つ目は EventArgs に割り当て可能な型) と包含アセンブリの対象を含むシグネチャを持つデリゲートを含む[!INCLUDE[dnprdnlong](../code-quality/includes/dnprdnlong_md.md)]です。|  
|[CA1004: ジェネリック メソッドは型パラメーターを指定しなければなりません](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md)|型引数を明示的に指定するのではなく、メソッドに渡す引数の型によってジェネリック メソッドの型引数を決定する方法が推論されます。 推論を有効にするには、ジェネリック メソッドのパラメーター シグネチャに、そのメソッドの型パラメーターと同じ型のパラメーターが含まれている必要があります。 この場合、型引数を指定する必要がなくなります。 ジェネリックと非ジェネリック インスタンス メソッドを呼び出す構文は同じです。 すべての型パラメーターの推論を使用する場合これには、ジェネリック メソッドの使用が簡素化されます。|  
|[CA1005: ジェネリック型でパラメーターを使用しすぎないでください](../code-quality/ca1005-avoid-excessive-parameters-on-generic-types.md)|ジェネリック型に含まれる型パラメーターが増えれば増えるほど、それぞれの型パラメーターが表す意味を調べることや覚えることが難しくなります。 List のように、1 つの型パラメーターを持つ通常意味は明確です\<T >、および場合によってはディクショナリと同様に、2 つの型パラメーターを持つ\<TKey, TValue >。 しかし、型パラメーターが 3 つ以上になると、ほとんどのユーザーには意味を把握することが困難になります。|  
|[CA1006: ジェネリック型をメンバー シグネチャ内で入れ子にしません](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md)|入れ子にされた型引数は、ジェネリック型の型引数でもあります。 入れ子にされた型引数を含むシグネチャを持つメンバーを呼び出すには、ユーザーが 1 つのジェネリック型をインスタンス化し、別のジェネリック型のコンストラクターにこの型を渡す必要があります。 複雑な手順と構文が必要となるため、これは避けるようにしてください。|  
|[CA1007: 適切な場所にジェネリックを使用します](../code-quality/ca1007-use-generics-where-appropriate.md)|外部から参照できるメソッドに、System.Object 型の参照パラメーターが含まれています。 ジェネリック メソッドを使用することで、型を最初に参照パラメーターの型にキャストせずに、制約の影響を受けるすべての型をメソッドに渡すことができます。|  
|[CA1008: Enums は 0 値を含んでいなければなりません](../code-quality/ca1008-enums-should-have-zero-value.md)|初期化されていない列挙型の既定値は、他の値型と同様に、ゼロです。 属性付き付いた列挙体は、されるため、既定値は、列挙の有効な値に 0 の値を使用してメンバーを定義する必要があります。 FlagsAttribute 属性を適用した列挙型でゼロ値のメンバーを定義する場合、名前を "None" にして、列挙型に設定済みの値がないことを示します。|  
|[CA1009: イベント ハンドラーを正しく宣言します](../code-quality/ca1009-declare-event-handlers-correctly.md)|イベント ハンドラー メソッドでは 2 つのパラメーターを使用します。 1 つ目は System.Object 型で、"sender" という名前です。 これは、イベントを発生させるオブジェクトです。 2 つ目は System.EventArgs 型で、"e" という名前です。 これは、イベントに関連付けられるデータです。 イベント ハンドラー メソッドでは値を返さないでください。C# プログラミング言語では、これは戻り値の型 void で示されます。|  
|[CA1010: コレクションは、ジェネリック インターフェイスを実装しなければなりません](../code-quality/ca1010-collections-should-implement-generic-interface.md)|コレクションの操作性を拡充するために、ジェネリック コレクション インターフェイスの 1 つを実装します。 これにより、コレクションを使用してジェネリック コレクション型を設定できます。|  
|[CA1011: 基本型をパラメーターとして渡すことを考慮します](../code-quality/ca1011-consider-passing-base-types-as-parameters.md)|メソッドの宣言で基本型をパラメーターとして指定すると、その基本型から派生した型は、メソッドに対応する引数として渡すことができます。 派生パラメーター型で実現する追加機能が不要である場合、基本型を使用することでメソッドをより広範囲に利用できるようになります。|  
|[CA1012: 抽象型にはコンストラクターを含めません](../code-quality/ca1012-abstract-types-should-not-have-constructors.md)|抽象型上のコンストラクターは、派生型からのみ呼び出すことができます。 パブリック コンストラクターで型のインスタンスが作成され、抽象型のインスタンスは自分で作成できないため、パブリック コンストラクターが含まれる抽象型のデザインは不適切になります。|  
|[CA1013: オーバーロードする加算および減算で、演算子 equals をオーバーロードします](../code-quality/ca1013-overload-operator-equals-on-overloading-add-and-subtract.md)|パブリック型またはプロテクト型で、等値演算子を実装しないまま、加算演算子または減算演算子を実装しています。|  
|[CA1014: アセンブリに CLSCompliantAttribute を設定します](../code-quality/ca1014-mark-assemblies-with-clscompliantattribute.md)|共通言語仕様 (CLS) には、名前付けの制約、データ型、および規則が定義されています。アセンブリを複数のプログラミング言語で使用する場合、この仕様に準拠する必要があります。 優れた設計では、すべてのアセンブリは、CLSCompliantAttribute を使用して、CLS 準拠を明示的に示すによって決まります。 この属性が使用されていないアセンブリは、CLS に準拠しません。|  
|[CA1016: アセンブリに AssemblyVersionAttribute を設定します](../code-quality/ca1016-mark-assemblies-with-assemblyversionattribute.md)|.NET Framework は、厳密な名前付きアセンブリの型にバインドして、アセンブリを一意に識別するバージョン番号を使用します。 バージョン番号は、バージョンと発行者のポリシーと共に使用されます。 既定で、アプリケーションは、ビルドされたアセンブリのバージョンでのみ実行されます。|  
|[CA1017: アセンブリに ComVisibleAttribute を設定します](../code-quality/ca1017-mark-assemblies-with-comvisibleattribute.md)|ComVisibleAttribute 属性によって、COM クライアントからマネージ コードにアクセスする方法が決まります。 アセンブリで COM の参照範囲を明示することをお勧めします。 COM の参照範囲は、アセンブリ全体に設定し、個々の型と型のメンバー用にオーバーライドできます。 この属性がない場合、アセンブリのコンテンツは COM クライアントから参照できます。|  
|[CA1018: 属性を AttributeUsageAttribute に設定します](../code-quality/ca1018-mark-attributes-with-attributeusageattribute.md)|カスタム属性を定義する場合、AttributeUsageAttribute を使用してマークし、カスタム属性を適用できるソース コードの位置を示します。 属性の意味と用途によって、コード内の有効な位置が決まります。|  
|[CA1019: 属性引数にアクセサーを定義します](../code-quality/ca1019-define-accessors-for-attribute-arguments.md)|属性では、対象に適用するときに必ず指定する必須の引数を定義できます。 この引数は、コンストラクターに位置指定パラメーターで属性を指定できるようになるため、位置指定引数とも呼ばれます。 必須のすべての引数について、対応する読み取り専用のプロパティも属性で規定する必要があります。これは、引数値を実行時に取得できるようにするためです。 また、属性ではオプションの引数も定義できます。これは名前付き引数とも呼ばれます。 この引数は、名前でコンストラクターに属性を指定するときに使用されます。また、対応する読み取り/書き込みプロパティが必要です。|  
|[CA1020: 型をほとんど含まない名前空間を使用しません](../code-quality/ca1020-avoid-namespaces-with-few-types.md)|論理構造がある各名前空間および付けます名前空間に型を記述する正当な理由があるか確認してください。|  
|[CA1021: out パラメーターを使用しません](../code-quality/ca1021-avoid-out-parameters.md)|(out または ref を使用した) 型の参照渡しには、ポインターの使用経験、値型と参照型の違いの理解、および複数の戻り値を持つメソッドの処理が必要です。 また、out パラメーターと ref パラメーターの違いはあまり理解されていません。|  
|[CA1023: インデクサーを多次元にすることはできません](../code-quality/ca1023-indexers-should-not-be-multidimensional.md)|インデクサー (つまり、インデックス付きのプロパティ) では、インデックスを 1 つだけ使用します。 多次元のインデクサーがあると、ライブラリの操作性が著しく低下することがあります。|  
|[CA1024: 適切な場所にプロパティを使用します](../code-quality/ca1024-use-properties-where-appropriate.md)|パブリック メソッドまたはプロテクト メソッドに、"Get" で始まる名前が付けられ、パラメーターは使用されていません。また、配列ではない値を返します。 このメソッドは、プロパティに変更できる可能性があります。|  
|[CA1025: 反復する引数を params 配列で置き換えます](../code-quality/ca1025-replace-repetitive-arguments-with-params-array.md)|引数の正確な数が不明で、可変個の引数が同じ型である場合、または同じ型で渡すことができる場合、引数を繰り返すのではなく、パラメーター配列を使用します。|  
|[CA1026: 既定のパラメーターを使用できません](../code-quality/ca1026-default-parameters-should-not-be-used.md)|既定のパラメーターを使用するメソッドは、CLS で許可されていますが、CLS では、既定のパラメーターに割り当てられた値をコンパイラで無視することもできます。 複数のプログラミング言語間で動作を維持するために、既定のパラメーターを使用するメソッドは、既定のパラメーターを指定したメソッドのオーバーロードで置換します。|  
|[CA1027: FlagsAttribute で列挙値をマークします](../code-quality/ca1027-mark-enums-with-flagsattribute.md)|列挙型は、関連する名前付き定数が複数定義された値型です。 名前付き定数を有意に結合できる場合、列挙型に FlagsAttribute を適用します。|  
|[CA1028: 列挙ストレージは Int32 でなければなりません](../code-quality/ca1028-enum-storage-should-be-int32.md)|列挙型は、関連する名前付き定数が複数定義された値型です。 既定で、System.Int32 データ型は、定数値を格納するために使用されます。 場合でも、この基になる型を変更できますが、したりされていないために必要なほとんどのシナリオのことをお勧めします。|  
|[CA1030: 適切な場所にイベントを使用します](../code-quality/ca1030-use-events-where-appropriate.md)|この規則では、通常はイベントに使用される名前を持つメソッドを検出します。 明示的に定義された状態変化に応答してメソッドが呼び出される場合、メソッドはイベント ハンドラーから呼び出す必要があります。 メソッドを呼び出すオブジェクトは、メソッドを直接呼び出すのではなく、イベントを発生させる必要があります。|  
|[CA1031: 一般的な例外の種類はキャッチしません](../code-quality/ca1031-do-not-catch-general-exception-types.md)|汎用的な例外はキャッチしないでください。 具体的な例外をキャッチまたは catch ブロック内の最後のステートメントとして一般的な例外を再スローします。|  
|[CA1032: 標準例外コンストラクターを実装します](../code-quality/ca1032-implement-standard-exception-constructors.md)|コンストラクターを完全に宣言していないと、例外を正しく処理するのが困難になります。|  
|[CA1033: インターフェイス メソッドは、子型によって呼び出し可能でなければなりません](../code-quality/ca1033-interface-methods-should-be-callable-by-child-types.md)|シールされていない外部から参照できる型によって、パブリック インターフェイスを持つメソッドを明示的に実装しています。また、同じ名前を持つ外部から参照できる代替のメソッドがありません。|  
|[CA1034: 入れ子にされた型を参照可能にすることはできません](../code-quality/ca1034-nested-types-should-not-be-visible.md)|入れ子にされた型とは、別の型のスコープ内で宣言された型のことです。 入れ子にされた型は、包含型のプライベート実装の詳細をカプセル化するときに便利です。 このような用途なので、入れ子にされた型は外部から参照できないようにします。|  
|[CA1035: ICollection の実装は、厳密に型指定されたメンバーを含んでいます](../code-quality/ca1035-icollection-implementations-have-strongly-typed-members.md)|この規則では、ICollection で厳密に型指定されたメンバーを実装する必要があります。これは、ユーザーがインターフェイスに備わっている機能を使用するときに、必ずしも引数を Object 型にキャストするとは限らないためです。 この規則では、ICollection を実装する型でこの処理を行って、Object よりも厳密な型のインスタンス コレクションを管理すると想定しています。|  
|[CA1036: 比較可能な型でメソッドをオーバーライドします](../code-quality/ca1036-override-methods-on-comparable-types.md)|パブリック型またはプロテクト型で System.IComparable インターフェイスを実装しています。 これによって、Object.Equals はオーバーライドされません。また、"等しい"、"等しくない"、"未満"、"より大きい" を示す言語固有の演算子はオーバーロードされません。|  
|[CA1038: 列挙子は厳密に型指定されていなければなりません](../code-quality/ca1038-enumerators-should-be-strongly-typed.md)|この規則では、IEnumerator で、厳密に型指定された形式の Current プロパティを実装する必要があります。これは、ユーザーは、インターフェイスに備わっている機能を使用するときに、必ずしも戻り値を厳密な型にキャストするとは限らないためです。|  
|[CA1039: リストは厳密に型指定されています](../code-quality/ca1039-lists-are-strongly-typed.md)|この規則では、IList で厳密に型指定されたメンバーを実装する必要があります。これは、ユーザーがインターフェイスに備わっている機能を使用するときに、必ずしも引数を System.Object 型にキャストするとは限らないためです。|  
|[CA1040: 空のインターフェイスは使用しないでください](../code-quality/ca1040-avoid-empty-interfaces.md)|インターフェイスには、動作や使用のコントラクトを実現するメンバーが定義されます。 インターフェイスで示される機能は、継承の階層構造内に型が存在するかどうかにかかわらず、どの型からも適用できます。 型ではインターフェイスのメンバーに実装することで、インターフェイスが実装されます。 空のインターフェイスではメンバーが定義されません。そのため、実装できるコントラクトも定義されません。|  
|[CA1041: ObsoleteAttribute メッセージを指定します](../code-quality/ca1041-provide-obsoleteattribute-message.md)|型またはメンバーが System.ObsoleteAttribute 属性を使用してマークされていますが、この属性で ObsoleteAttribute.Message プロパティが指定されていません。 型または obsoleteattribute でマークされているメンバーがコンパイルされると、旧式の型またはメンバーに関するユーザー情報が表示される属性の Message プロパティが表示されます。|  
|[CA1043: インデクサーには整数または文字列引数を使用します](../code-quality/ca1043-use-integral-or-string-argument-for-indexers.md)|インデクサー (つまり、インデックスされたプロパティ) では、インデックスに整数型または文字列型を使用します。 一般に、このような型はデータ構造のインデックス作成に使用され、ライブラリの操作性も改善されます。 Object 型の使用は、デザイン時に特定の整数型または文字列型を指定できない場合に限定してください。|  
|[CA1044: プロパティを書き込み専用にすることはできません](../code-quality/ca1044-properties-should-not-be-write-only.md)|読み取り専用のプロパティは許容され、必要な場合もよくありますが、書き込み専用のプロパティを使用することはデザインのガイドラインで禁止されています。 これは、値を設定できてもその値を参照できず、セキュリティが確保されないためです。 また、読み取りアクセスがないと、共有オブジェクトのステータスを参照できないため、実用性が制限されます。|  
|[CA1045: 型を参照によって渡しません](../code-quality/ca1045-do-not-pass-types-by-reference.md)|(out または ref を使用した) 型の参照渡しには、ポインターの使用経験、値型と参照型の違いの理解、および複数の戻り値を持つメソッドの処理が必要です。 開発者全般に向けてライブラリをデザインする場合、ユーザーが out パラメーターまたは ref パラメーターの扱い方を習得することは期待しないでください。|  
|[CA1046: 参照型で、演算子 equals をオーバーロードしないでください](../code-quality/ca1046-do-not-overload-operator-equals-on-reference-types.md)|参照型の場合、等値演算子は既定の実装でほぼ問題がありません。 既定で、2 つの参照が等値と見なされるのは、同じオブジェクトを参照する場合のみです。|  
|[CA1047: Sealed 型の保護されたメンバーを宣言しません](../code-quality/ca1047-do-not-declare-protected-members-in-sealed-types.md)|型でプロテクト メンバーを宣言するのは、継承する型からメンバーにアクセスまたはオーバーライドできるようにするためです。 定義により、シールされた型から継承することはできません。これは、シールされた型のプロテクト メソッドを呼び出すことができないということを意味します。|  
|[CA1048: Sealed 型の仮想メンバーを宣言しません](../code-quality/ca1048-do-not-declare-virtual-members-in-sealed-types.md)|型でメソッドを仮想と宣言するのは、継承する型が仮想メソッドの実装をオーバーライドできるようにするためです。 定義により、シールされた型から継承することはできません。 これにより、シールされた型の仮想メソッドの意味がなくなります。|  
|[CA1049: ネイティブ リソースを所有する型は、破棄可能でなければなりません](../code-quality/ca1049-types-that-own-native-resources-should-be-disposable.md)|アンマネージ リソースを割り当てる型では、IDisposable を実装することで、呼び出し元が必要に応じてリソースを解放し、リソースを保持するオブジェクトの有効期間を短縮できるようにする必要があります。|  
|[CA1050: 名前空間で型を宣言します](../code-quality/ca1050-declare-types-in-namespaces.md)|型を名前空間内で宣言するのは、名前が衝突しないようにするためと、関連する型をオブジェクト階層形式で編成するためです。|  
|[CA1051: 参照できるインスタンス フィールドを宣言しないでください](../code-quality/ca1051-do-not-declare-visible-instance-fields.md)|フィールドの主な用途は、実装の詳細にする必要があります。 フィールドは private または internal にし、プロパティによって公開するようにします。|  
|[CA1052: スタティック ホルダー型はシールされていなければなりません](../code-quality/ca1052-static-holder-types-should-be-sealed.md)|パブリックまたはプロテクト型では、静的なメンバーのみが含まれています、sealed (c#) または NotInheritable (Visual Basic) 修飾子を使用して宣言されていません。 継承を意図していない型は、sealed 修飾子を使用してマークし、基本型として使用できないようにします。|  
|[CA1053: スタティック ホルダー型にはコンストラクターを含めません](../code-quality/ca1053-static-holder-types-should-not-have-constructors.md)|パブリック型または入れ子になったパブリック型で、静的なメンバーのみが宣言されています。また、パブリックまたはプロテクトの既定のコンストラクターが含まれます。 静的メンバーの呼び出しに型のインスタンスは必要ないため、コンストラクターは不要です。 安全性とセキュリティを確保するために、文字列引数を使用して文字列オーバーロードで URI (Uniform Resource Identifier) オーバーロードを呼び出してください。|  
|[CA1054: URI パラメーターを文字列にすることはできません](../code-quality/ca1054-uri-parameters-should-not-be-strings.md)|メソッドで URI の文字列形式を使用する場合、対応するオーバーロードを宣言し、URI クラスのインスタンスを使用します。こうすることで、安全な方法でこのサービスを実現できます。|  
|[CA1055: URI 戻り値を文字列にすることはできません](../code-quality/ca1055-uri-return-values-should-not-be-strings.md)|この規則では、メソッドは URI を返すと想定されます。 URI の文字列表現は解析エラーやエンコーディング エラーが発生しやすく、セキュリティ上の脆弱性の原因となる場合があります。 System.Uri クラスを使用すると、安全な方法でこのサービスを実現できます。|  
|[CA1056: URI プロパティを文字列にすることはできません](../code-quality/ca1056-uri-properties-should-not-be-strings.md)|このルールでは、URI を表すことを前提としています。 URI の文字列表現は解析エラーやエンコーディング エラーが発生しやすく、セキュリティ上の脆弱性の原因となる場合があります。 System.Uri クラスを使用すると、安全な方法でこのサービスを実現できます。|  
|[CA1057: 文字列 URI オーバーロードが、System.Uri オーバーロードを呼び出します](../code-quality/ca1057-string-uri-overloads-call-system-uri-overloads.md)|文字列パラメーターが System.Uri パラメーターに置き換えられている点だけが異なるメソッド オーバーロードが型で宣言されています。 文字列パラメーターを使用するオーバーロードは、URI パラメーターを使用するオーバーロードを呼び出しません。|  
|[CA1058: 型は、一定の基本型を拡張することはできません](../code-quality/ca1058-types-should-not-extend-certain-base-types.md)|外部から参照可能な型では、特定の基本型が拡張されます。 別の型を使用してください。|  
|[CA1059: メンバーは特定の具象型を公開できません](../code-quality/ca1059-members-should-not-expose-certain-concrete-types.md)|具象型は、完全な実装を含む型であるため、インスタンス化できます。 このメンバーを広範囲に使用するには、具象型を推奨インターフェイスによって置き換えます。|  
|[CA1060: 移動 P/invoke を NativeMethods クラス](../code-quality/ca1060-move-p-invokes-to-nativemethods-class.md)|マークされているなど、プラットフォーム呼び出しメソッド、<xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName>で Declare キーワードを使用して定義されているメソッドまたは[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]、アンマネージ コードにアクセスします。 これらのメソッドは、NativeMethods、SafeNativeMethods、UnsafeNativeMethods の各クラスのいずれかに含まれる必要があります。|  
|[CA1061: 基本クラス メソッドを非表示にしません](../code-quality/ca1061-do-not-hide-base-class-methods.md)|派生メソッドのパラメーター シグネチャ内のある型が、基本メソッドのパラメーター シグネチャ内のそれに対応する型より弱く型指定されていることが、両者の唯一の相違点である場合、基本型内のメソッドが派生型内の同じ名前のメソッドによって隠ぺいされます。|  
|[CA1062: パブリック メソッドの引数の検証](../code-quality/ca1062-validate-arguments-of-public-methods.md)|外部から参照可能なメソッドに渡されるすべての参照引数について、null かどうかをチェックする必要があります。|  
|[CA1063: IDisposable を正しく実装します](../code-quality/ca1063-implement-idisposable-correctly.md)|すべての IDisposable 型は、Dispose パターンを適切に実装する必要があります。|  
|[CA1064: 例外は public として設定する必要があります](../code-quality/ca1064-exceptions-should-be-public.md)|内部例外は、その内部スコープ内でのみ認識されます。 内部スコープの外側にある例外は、基本例外を使用しなければキャッチできません。 場合、内部例外から継承<xref:System.Exception?displayProperty=fullName>、 <xref:System.SystemException?displayProperty=fullName>、または<xref:System.ApplicationException?displayProperty=fullName>、外部のコードには、例外を行うには何かを認識するための十分な情報はありません。|  
|[CA1065: 予期しない場所に例外を発生させません](../code-quality/ca1065-do-not-raise-exceptions-in-unexpected-locations.md)|例外をスローしないはずのメソッドが例外をスローします。|  
|[CA2210: アセンブリには有効な厳密な名前が必要です](../code-quality/ca2210-assemblies-should-have-valid-strong-names.md)|厳密な名前によって、改ざんされたアセンブリを、クライアントが無意識のうちに読み込む問題を防ぐことができます。 厳密な名前のないアセンブリが配置される状況は、限定されます。 適切に署名されていないアセンブリを共有または配布すると、アセンブリが改ざんされる場合、共通言語ランタイムでアセンブリを読み込むことができない場合、またはユーザーのコンピューターで検証を無効にする必要がある場合などの問題が考えられます。|