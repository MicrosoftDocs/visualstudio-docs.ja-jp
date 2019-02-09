---
title: マネージド コードのコード分析警告 (CheckId 別)
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1000
- CA1001
- CA1002
- CA1003
- CA1004
- CA1005
- CA1006
- CA1007
- CA1008
- CA1009
- CA1010
- CA1011
- CA1012
- CS1013
- CS1014
- CA1016
- CA1017
- CA1018
- CA1019
- CA1020
- CA1021
- CA1022
- CA1023
- CA1024
- CS1025
- CA1026
- CA1027
- CA1028
- CA1029
- CA1030
- CA1031
- CA1032
- CA1033
- CA1034
- CA1035
- CA1036
- CA1037
- CA1038
- CA1039
- CA1040
- CA1041
- CA1042
- CA1043
- CA1044
- CA1045
- CA1046
- CA1047
- CA1048
- CA1049
- CA1050
- CA1051
- CA1052
- CA1053
- CA1054
- CA1055
- CA1056
- CA1057
- CA1058
- CA1059
- CA1060
- CA1061
- CA1062
- CA1063
- CA1064
- CA1065
- CA1300
- CA1301
- CA1302
- CA1303
- CA1304
- CA1305
- CA1306
- CA1307
- CA1308
- CA1309
- CA1400
- CA1401
- CA1402
- CA1403
- CA1404
- CA1405
- CA1406
- CA1407
- CA1408
- CA1409
- CA1410
- CA1411
- CA1412
- CA1413
- CA1414
- CA1415
- CA1500
- CA1501
- CA1502
- CA1503
- CA1504
- CA1505
- CA1506
- CA1600
- CA1601
- CA1700
- CA1701
- CA1702
- CA1703
- CA1704
- CA1707
- CA1708
- CA1709
- CA1710
- CA1711
- CA1712
- CA1713
- CA1714
- CA1715
- VA1716
- CA1717
- CA1719
- CA1720
- CA1721
- CA1722
- CA1723
- CA1724
- CA1725
- CA1726
- CA1727
- CA1728
- CA1729
- CA1730
- CA1800
- CA1801
- CA1802
- CA1803
- CA1804
- CA1806
- CA1809
- CA1810
- CA1811
- CA1812
- CA1813
- CA1814
- CA1815
- CA1816
- CA1819
- CA1820
- CA1821
- CA1822
- CA1823
- CA1824
- CA1900
- CA1901
- CA1903
- CA2000
- CA2001
- CA2002
- CA2003
- CA2004
- CA2006
- CA2100
- CA2101
- CA2102
- CA2103
- CA2104
- CA2105
- CA2106
- CA2107
- CA2108
- CA2109
- CA2110
- CA2111
- CA2112
- CA2114
- CA2115
- CA2116
- CA2117
- CA2118
- CA2119
- CA2120
- CA2121
- CA2122
- CA2123
- CA2124
- CA2126
- CA2127
- CA2128
- CA2129
- CA2130
- CA2131
- CA2132
- CA2133
- CA2134
- CA2135
- CA2136
- CA2137
- CA2138
- CA2139
- CA2140
- CA2141
- CA2142
- CA2143
- CA2144
- CA2145
- CA2146
- CA2147
- CA2148
- CA2149
- CA2150
- CA2151
- CA2200
- CA2201
- CA2202
- CA2204
- CA2205
- CA2207
- CA2208
- CA2210
- CA2211
- CA2212
- CA2213
- CA2214
- CA2215
- CA2216
- CA2217
- CA2218
- CA2219
- CA2220
- CA2221
- CA2222
- CA2223
- CA2224
- CA2225
- CA2226
- CA2228
- CA2229
- CA2227
- CA2230
- CA2231
- CA2232
- CA2233
- CA2234
- CA2235
- CA2236
- CA2237
- CA2238
- CA2239
- CA2240
- CA2241
- CA2242
- CA2243
- CA5122
ms.assetid: 5cb221f6-dc59-4abf-9bfa-adbd6f907f96
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 72d03c7a9394e760f24023c47a0c7a27881c0cda
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2019
ms.locfileid: "55909129"
---
# <a name="code-analysis-warnings-for-managed-code-by-checkid"></a>Checkid 別のマネージ コードに対するコード分析の警告

次の表に、マネージド コードのコード分析警告を警告の CheckId 識別子別に示します。

| CheckId | 警告 | 説明 |
|---------| - | - |
| CA1000 | [CA 1000:ジェネリック型で静的メンバーを宣言しません](../code-quality/ca1000-do-not-declare-static-members-on-generic-types.md) | ジェネリック型の静的メンバーを呼び出すときには、その型の型引数も指定する必要があります。 推論をサポートしないジェネリック インスタンス メンバーを呼び出すときには、そのメンバーに型引数を指定する必要があります。 この 2 つの場合、型引数を指定するときに使用される構文は異なりますが、混同される可能性があります。 |
| CA1001 | [CA1001: 破棄可能なフィールドを所有する型は、破棄可能でなければなりません](../code-quality/ca1001-types-that-own-disposable-fields-should-be-disposable.md) | クラスが System.IDisposable 型であるインスタンス フィールドを宣言および実装していますが、IDisposable を実装していません。 IDisposable フィールドを宣言するクラスは間接的にアンマネージ リソースを所有しているため、IDisposable インターフェイスを実装する必要があります。 |
| CA1002 | [CA 1002:ジェネリック リストを公開しません](../code-quality/ca1002-do-not-expose-generic-lists.md) | System.Collections.Generic.List < (の\<(T >) >) はパフォーマンスを継承しないように設計された汎用コレクションです。 このため、List には仮想メンバーは含まれません。 代わりに、継承を目的としたジェネリック コレクションを公開する必要があります。 |
| CA1003 | [CA 1003:汎用イベント ハンドラーのインスタンスを使用して、](../code-quality/ca1003-use-generic-event-handler-instances.md) |型には、void を返す、2 つのパラメーター (1 つはオブジェクトと、2 つ目は EventArgs に割り当て可能な型) を含むシグネチャを持つデリゲートが含まれています。 格納しているアセンブリは、Microsoft .NET Framework 2.0 を対象とします。 |
| CA1004 | [CA 1004:ジェネリック メソッドは、型パラメーターを指定する必要があります。](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md) | 型引数を明示的に指定するのではなく、メソッドに渡す引数の型によってジェネリック メソッドの型引数を決定する方法が推論されます。 推論を有効にするには、ジェネリック メソッドのパラメーター シグネチャに、そのメソッドの型パラメーターと同じ型のパラメーターが含まれている必要があります。 この場合、型引数を指定する必要がなくなります。 すべての型パラメーターについて推論を使用する場合、ジェネリック インスタンス メソッドを呼び出す構文と、非ジェネリック インスタンス メソッドを呼び出す構文は同じになります。これにより、ジェネリック メソッドの使用方法が単純化されます。 |
| CA1005 | [CA1005:ジェネリック型で過剰なパラメーターを回避します。](../code-quality/ca1005-avoid-excessive-parameters-on-generic-types.md) | ジェネリック型に含まれる型パラメーターが増えれば増えるほど、それぞれの型パラメーターが表す意味を調べることや覚えることが難しくなります。 リストのように、1 つの型パラメーターを使用して、通常は明確では\<T >、および場合によっては辞書のように、2 つの型パラメーターを持つ\<TKey, TValue > です。 しかし、型パラメーターが 3 つ以上になると、ほとんどのユーザーには意味を把握することが困難になります。 |
| CA1006 | [CA 1006:ジェネリック型メンバー シグネチャ内で入れ子にしません](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md) | 入れ子にされた型引数は、ジェネリック型の型引数でもあります。 入れ子にされた型引数を含むシグネチャを持つメンバーを呼び出すには、ユーザーが 1 つのジェネリック型をインスタンス化し、別のジェネリック型のコンストラクターにこの型を渡す必要があります。 複雑な手順と構文が必要となるため、これは避けるようにしてください。 |
| CA1007 |[CA 1007:適切な場所にジェネリックを使用します。](../code-quality/ca1007-use-generics-where-appropriate.md) | 外部から参照できるメソッドに、System.Object 型の参照パラメーターが含まれています。 ジェネリック メソッドを使用することで、型を最初に参照パラメーターの型にキャストせずに、制約の影響を受けるすべての型をメソッドに渡すことができます。 |
| CA1008 | [CA1008:列挙がゼロの値](../code-quality/ca1008-enums-should-have-zero-value.md) | 初期化されていない列挙型の既定値は、他の値型と同様に、ゼロです。 フラグではない属性が付いた列挙型では、ゼロの値を使用してメンバーを定義する必要があります。これは、既定値を有効な列挙値にするためです。 FlagsAttribute 属性を適用した列挙型でゼロ値のメンバーを定義する場合、名前を "None" にして、列挙型に設定済みの値がないことを示します。 |
| CA1009 | [CA 1009:イベント ハンドラーを正しく宣言します。](../code-quality/ca1009-declare-event-handlers-correctly.md) | イベント ハンドラー メソッドでは 2 つのパラメーターを使用します。 1 つ目は System.Object 型で、"sender" という名前です。 これは、イベントを発生させるオブジェクトです。 2 つ目は System.EventArgs 型で、"e" という名前です。 これは、イベントに関連付けられるデータです。 イベント ハンドラー メソッドでは値を返さないでください。C# プログラミング言語では、これは戻り値の型 void で示されます。 |
| CA1010 | [CA 1010:コレクションは、ジェネリック インターフェイスを実装する必要があります。](../code-quality/ca1010-collections-should-implement-generic-interface.md) | コレクションの操作性を拡充するために、ジェネリック コレクション インターフェイスの 1 つを実装します。 これにより、コレクションを使用してジェネリック コレクション型を設定できます。 |
| CA1011 |[CA 1011:基本型をパラメーターとして渡すことを検討してください。](../code-quality/ca1011-consider-passing-base-types-as-parameters.md) | メソッドの宣言で基本型をパラメーターとして指定すると、その基本型から派生した型は、メソッドに対応する引数として渡すことができます。 派生パラメーター型で実現する追加機能が不要である場合、基本型を使用することでメソッドをより広範囲に利用できるようになります。 |
| CA1012 | [CA 1012:抽象型には、コンス トラクターはありません。](../code-quality/ca1012-abstract-types-should-not-have-constructors.md) | 抽象型上のコンストラクターは、派生型からのみ呼び出すことができます。 パブリック コンストラクターで型のインスタンスが作成され、抽象型のインスタンスは自分で作成できないため、パブリック コンストラクターが含まれる抽象型のデザインは不適切になります。 |
| CA1013 | [CA1013:オーバー ロードで、演算子 equals をオーバー ロードの加算および減算](../code-quality/ca1013-overload-operator-equals-on-overloading-add-and-subtract.md) | パブリック型またはプロテクト型で、等値演算子を実装しないまま、加算演算子または減算演算子を実装しています。 |
| CA1014 | [CA 1014:アセンブリに clscompliantattribute を設定します](../code-quality/ca1014-mark-assemblies-with-clscompliantattribute.md) | 共通言語仕様 (CLS) には、名前付けの制約、データ型、および規則が定義されています。アセンブリを複数のプログラミング言語で使用する場合、この仕様に準拠する必要があります。 すべてのアセンブリに <xref:System.CLSCompliantAttribute> を使用して、CLS への準拠を明示することをお勧めします。 この属性が使用されていないアセンブリは、CLS に準拠しません。 |
| CA1016 | [CA 1016:アセンブリに assemblyversionattribute を設定します](../code-quality/ca1016-mark-assemblies-with-assemblyversionattribute.md) | .NET Framework は、アセンブリを一意に識別する厳密な名前付きアセンブリの型にバインドして、バージョン番号を使用します。 バージョン番号は、バージョンと発行者のポリシーと共に使用されます。 既定で、アプリケーションは、ビルドされたアセンブリのバージョンでのみ実行されます。 |
| CA1017 | [CA 1017:アセンブリに comvisibleattribute を設定します](../code-quality/ca1017-mark-assemblies-with-comvisibleattribute.md) |ComVisibleAttribute 属性によって、COM クライアントからマネージド コードにアクセスする方法が決まります。 アセンブリで COM の参照範囲を明示することをお勧めします。 COM の参照範囲は、アセンブリ全体に設定し、個々の型と型のメンバー用にオーバーライドできます。 この属性がない場合、アセンブリのコンテンツは COM クライアントから参照できます。 |
| CA1018 | [CA 1018:属性を attributeusageattribute に設定します](../code-quality/ca1018-mark-attributes-with-attributeusageattribute.md) | カスタム属性を定義する場合、AttributeUsageAttribute を使用してマークし、カスタム属性を適用できるソース コードの位置を示します。 属性の意味と用途によって、コード内の有効な位置が決まります。 |
| CA1019 | [CA 1019:属性引数にアクセサーを定義します](../code-quality/ca1019-define-accessors-for-attribute-arguments.md) | 属性では、対象に適用するときに必ず指定する必須の引数を定義できます。 この引数は、コンストラクターに位置指定パラメーターで属性を指定できるようになるため、位置指定引数とも呼ばれます。 必須のすべての引数について、対応する読み取り専用のプロパティも属性で規定する必要があります。これは、引数値を実行時に取得できるようにするためです。 また、属性ではオプションの引数も定義できます。これは名前付き引数とも呼ばれます。 この引数は、名前でコンストラクターに属性を指定するときに使用されます。また、対応する読み取り/書き込みプロパティが必要です。 |
| CA1020 | [CA1020:いくつかの種類と名前空間を回避します。](../code-quality/ca1020-avoid-namespaces-with-few-types.md) | 配置する型数の少ない名前空間を作成する場合、各名前空間を論理的に構成し、有効な理由を付けます。 |
| CA1021 | [CA1021:Out パラメーターを避ける](../code-quality/ca1021-avoid-out-parameters.md) | (out または ref を使用した) 型の参照渡しには、ポインターの使用経験、値型と参照型の違いの理解、および複数の戻り値を持つメソッドの処理が必要です。 また、out パラメーターと ref パラメーターの違いはあまり理解されていません。 |
| CA1023 | [CA 1023:インデクサーを多次元することはできません。](../code-quality/ca1023-indexers-should-not-be-multidimensional.md) | インデクサー (つまり、インデックス付きのプロパティ) では、インデックスを 1 つだけ使用します。 多次元のインデクサーがあると、ライブラリの操作性が著しく低下することがあります。 |
| CA1024 | [CA 1024:適切な場所のプロパティを使用します。](../code-quality/ca1024-use-properties-where-appropriate.md) | パブリック メソッドまたはプロテクト メソッドに、"Get" で始まる名前が付けられ、パラメーターは使用されていません。また、配列ではない値を返します。 このメソッドは、プロパティに変更できる可能性があります。 |
| CA1025 | [CA 1025:反復する引数を params 配列で置き換えます](../code-quality/ca1025-replace-repetitive-arguments-with-params-array.md) | 引数の正確な数が不明で、可変個の引数が同じ型である場合、または同じ型で渡すことができる場合、引数を繰り返すのではなく、パラメーター配列を使用します。 |
| CA1026 | [CA 1026:既定のパラメーターは使用できません。](../code-quality/ca1026-default-parameters-should-not-be-used.md) | 既定のパラメーターを使用するメソッドは、CLS で許可されていますが、CLS では、既定のパラメーターに割り当てられた値をコンパイラで無視することもできます。 複数のプログラミング言語間で動作を維持するために、既定のパラメーターを使用するメソッドは、既定のパラメーターを指定したメソッドのオーバーロードで置換します。 |
| CA1027 |[CA1027:FlagsAttribute で列挙をマークします。](../code-quality/ca1027-mark-enums-with-flagsattribute.md) | 列挙型は、関連する名前付き定数が複数定義された値型です。 名前付き定数を有意に結合できる場合、列挙型に FlagsAttribute を適用します。 |
| CA1028 | [CA 1028:列挙ストレージは Int32 でなければなりません](../code-quality/ca1028-enum-storage-should-be-int32.md) | 列挙型は、関連する名前付き定数が複数定義された値型です。 既定で、System.Int32 データ型は、定数値を格納するために使用されます。 この基になる型を変更できる場合でも、ほとんどの場合、変更する必要はなく、推奨もされません。 |
| CA1030 | [CA 1030:適切な場所、イベントを使用します。](../code-quality/ca1030-use-events-where-appropriate.md) |この規則では、通常はイベントに使用される名前を持つメソッドを検出します。 明示的に定義された状態変化に応答してメソッドが呼び出される場合、メソッドはイベント ハンドラーから呼び出す必要があります。 メソッドを呼び出すオブジェクトは、メソッドを直接呼び出すのではなく、イベントを発生させる必要があります。 |
| CA1031 | [CA 1031:一般的な例外の種類はキャッチしません](../code-quality/ca1031-do-not-catch-general-exception-types.md) | 汎用的な例外はキャッチしないでください。 より具体的な例外をキャッチするか、汎用的な例外を catch ブロックの最後のステートメントでスローし直します。 |
| CA1032 |[CA 1032:標準例外コンス トラクターを実装します。](../code-quality/ca1032-implement-standard-exception-constructors.md) | コンストラクターを完全に宣言していないと、例外を正しく処理するのが困難になります。 |
| CA1033 | [CA 1033:インターフェイス メソッドは、子型によって呼び出し可能でなければなりません](../code-quality/ca1033-interface-methods-should-be-callable-by-child-types.md) | シールされていない外部から参照できる型によって、パブリック インターフェイスを持つメソッドを明示的に実装しています。また、同じ名前を持つ外部から参照できる代替のメソッドがありません。 |
| CA1034 | [CA1034:入れ子にされた型を表示することはできません。](../code-quality/ca1034-nested-types-should-not-be-visible.md) | 入れ子にされた型とは、別の型のスコープ内で宣言された型のことです。 入れ子にされた型は、包含型のプライベート実装の詳細をカプセル化するときに便利です。 このような用途なので、入れ子にされた型は外部から参照できないようにします。 |
| CA1035 | [CA1035:ICollection の実装には、メンバーが厳密に型指定します。](../code-quality/ca1035-icollection-implementations-have-strongly-typed-members.md) | この規則では、ICollection で厳密に型指定されたメンバーを実装する必要があります。これは、ユーザーがインターフェイスに備わっている機能を使用するときに、必ずしも引数を Object 型にキャストするとは限らないためです。 この規則では、ICollection を実装する型でこの処理を行って、Object よりも厳密な型のインスタンス コレクションを管理すると想定しています。 |
| CA1036 | [CA 1036:比較可能な型のメソッドをオーバーライドします。](../code-quality/ca1036-override-methods-on-comparable-types.md) |パブリック型またはプロテクト型で System.IComparable インターフェイスを実装しています。 これによって、Object.Equals はオーバーライドされません。また、"等しい"、"等しくない"、"未満"、"より大きい" を示す言語固有の演算子はオーバーロードされません。 |
| CA1038 | [CA1038:列挙子を厳密に型指定する必要があります。](../code-quality/ca1038-enumerators-should-be-strongly-typed.md) | この規則では、IEnumerator で、厳密に型指定された形式の Current プロパティを実装する必要があります。これは、ユーザーは、インターフェイスに備わっている機能を使用するときに、必ずしも戻り値を厳密な型にキャストするとは限らないためです。 |
| CA1039 | [CA1039:リストは厳密に型指定します。](../code-quality/ca1039-lists-are-strongly-typed.md) | この規則では、IList で厳密に型指定されたメンバーを実装する必要があります。これは、ユーザーがインターフェイスに備わっている機能を使用するときに、必ずしも引数を System.Object 型にキャストするとは限らないためです。 |
| CA1040 |[CA1040:空のインターフェイスを回避します。](../code-quality/ca1040-avoid-empty-interfaces.md) | インターフェイスには、動作や使用のコントラクトを実現するメンバーが定義されます。 インターフェイスで示される機能は、継承の階層構造内に型が存在するかどうかにかかわらず、どの型からも適用できます。 型ではインターフェイスのメンバーに実装することで、インターフェイスが実装されます。 空のインターフェイスではメンバーが定義されません。そのため、実装できるコントラクトも定義されません。 |
| CA1041 | [CA1041:ObsoleteAttribute メッセージを指定します。](../code-quality/ca1041-provide-obsoleteattribute-message.md) | 型またはメンバーが System.ObsoleteAttribute 属性を使用してマークされていますが、この属性で ObsoleteAttribute.Message プロパティが指定されていません。 ObsoleteAttribute でマークされている型またはメンバーをコンパイルすると、属性の Message プロパティが表示されます。 これによって、ユーザーは旧式の型またはメンバーに関する情報を知ることができます。 |
| CA1043 | [CA 1043:インデクサーは整数または文字列引数を使用して、](../code-quality/ca1043-use-integral-or-string-argument-for-indexers.md) | インデクサー (つまり、インデックスされたプロパティ) では、インデックスに整数型または文字列型を使用します。 一般に、このような型はデータ構造のインデックス作成に使用され、ライブラリの操作性も改善されます。 Object 型の使用は、デザイン時に特定の整数型または文字列型を指定できない場合に限定してください。 |
| CA1044 | [CA 1044:プロパティが書き込み専用することはできません。](../code-quality/ca1044-properties-should-not-be-write-only.md) | 読み取り専用のプロパティは許容され、必要な場合もよくありますが、書き込み専用のプロパティを使用することはデザインのガイドラインで禁止されています。 これは、値を設定できてもその値を参照できず、セキュリティが確保されないためです。 また、読み取りアクセスがないと、共有オブジェクトのステータスを参照できないため、実用性が制限されます。 |
| CA1045 |[CA 1045:型を参照によって渡しません](../code-quality/ca1045-do-not-pass-types-by-reference.md) | (out または ref を使用した) 型の参照渡しには、ポインターの使用経験、値の型と参照型の違いの理解、および複数の戻り値を持つメソッドの処理が必要です。 開発者全般に向けてライブラリをデザインする場合、ユーザーが out パラメーターまたは ref パラメーターの扱い方を習得することは期待しないでください。 |
| CA1046 | [CA1046:参照型で、演算子 equals をオーバー ロードしません。](../code-quality/ca1046-do-not-overload-operator-equals-on-reference-types.md) | 参照型の場合、等値演算子は既定の実装でほぼ問題がありません。 既定で、2 つの参照が等値と見なされるのは、同じオブジェクトを参照する場合のみです。 |
| CA1047 |[CA 1047:Sealed 型の保護されたメンバーを宣言しません](../code-quality/ca1047-do-not-declare-protected-members-in-sealed-types.md) | 型でプロテクト メンバーを宣言するのは、継承する型からメンバーにアクセスまたはオーバーライドできるようにするためです。 定義により、シールされた型から継承することはできません。これは、シールされた型のプロテクト メソッドを呼び出すことができないということを意味します。 |
| CA1048 | [CA 1048:Sealed 型の仮想メンバーを宣言しません](../code-quality/ca1048-do-not-declare-virtual-members-in-sealed-types.md) | 型でメソッドを仮想と宣言するのは、継承する型が仮想メソッドの実装をオーバーライドできるようにするためです。 定義により、シールされた型から継承することはできません。 これにより、シールされた型の仮想メソッドの意味がなくなります。 |
| CA1049 | [CA 1049:ネイティブ リソースを所有する型は、破棄可能でなければなりません](../code-quality/ca1049-types-that-own-native-resources-should-be-disposable.md) | アンマネージ リソースを割り当てる型では、IDisposable を実装することで、呼び出し元が必要に応じてリソースを解放し、リソースを保持するオブジェクトの有効期間を短縮できるようにする必要があります。 |
| CA1050 | [CA 1050:名前空間の型を宣言します。](../code-quality/ca1050-declare-types-in-namespaces.md) | 型を名前空間内で宣言するのは、名前が衝突しないようにするためと、関連する型をオブジェクト階層形式で編成するためです。 |
| CA1051 | [CA 1051:インスタンス フィールドを宣言しません](../code-quality/ca1051-do-not-declare-visible-instance-fields.md) | フィールドの主な用途は、実装の詳細にする必要があります。 フィールドは private または internal にし、プロパティによって公開するようにします。 |
| CA1052 | [CA 1052:スタティック ホルダー型をシールする必要があります。](../code-quality/ca1052-static-holder-types-should-be-sealed.md) | パブリック型またはプロテクト型に静的メンバーしかなく、sealed (C# リファレンス) (NotInheritable) 修飾子を使用して宣言されていません。 継承を意図していない型は、sealed 修飾子を使用してマークし、基本型として使用できないようにします。 |
| CA1053 |[CA 1053:スタティック ホルダー型には、コンス トラクターはありません。](../code-quality/ca1053-static-holder-types-should-not-have-constructors.md) | パブリック型または入れ子になったパブリック型で、静的なメンバーのみが宣言されています。また、パブリックまたはプロテクトの既定のコンストラクターが含まれます。 静的メンバーの呼び出しに型のインスタンスは必要ないため、コンストラクターは不要です。 安全性とセキュリティを確保するために、文字列引数を使用して文字列オーバーロードで URI (Uniform Resource Identifier) オーバーロードを呼び出してください。 |
| CA1054 | [CA 1054:URI パラメーターは文字列をすることはできません。](../code-quality/ca1054-uri-parameters-should-not-be-strings.md) | メソッドで URI の文字列形式を使用する場合、対応するオーバーロードを宣言し、URI クラスのインスタンスを使用します。こうすることで、安全な方法でこのサービスを実現できます。 |
| CA1055 | [CA 1055:URI 戻り値は文字列をすることはできません。](../code-quality/ca1055-uri-return-values-should-not-be-strings.md) | この規則では、メソッドは URI を返すと想定されます。 URI の文字列表現は解析エラーやエンコーディング エラーが発生しやすく、セキュリティ上の脆弱性の原因となる場合があります。 System.Uri クラスを使用すると、安全な方法でこのサービスを実現できます。 |
| CA1056 | [CA 1056:URI のプロパティには、文字列がすることはできません。](../code-quality/ca1056-uri-properties-should-not-be-strings.md) | この規則では、プロパティは URI (Uniform Resource Identifier) を表すと想定されます。 URI の文字列表現は解析エラーやエンコーディング エラーが発生しやすく、セキュリティ上の脆弱性の原因となる場合があります。 System.Uri クラスを使用すると、安全な方法でこのサービスを実現できます。 |
| CA1057 | [CA 1057:文字列 URI オーバー ロードは、System.Uri オーバー ロードを呼び出す](../code-quality/ca1057-string-uri-overloads-call-system-uri-overloads.md) | 文字列パラメーターが System.Uri パラメーターに置き換えられている点だけが異なるメソッド オーバーロードが型で宣言されています。 文字列パラメーターを使用するオーバーロードは、URI パラメーターを使用するオーバーロードを呼び出しません。 |
| CA1058 | [CA1058:種類は一定の基本型を拡張する必要がありません。](../code-quality/ca1058-types-should-not-extend-certain-base-types.md) | 外部から参照可能な型では、特定の基本型が拡張されます。 別の型を使用してください。 |
| CA1059 |[CA 1059:メンバーが特定の具象型に公開することはできません。](../code-quality/ca1059-members-should-not-expose-certain-concrete-types.md) | 具象型は、完全な実装を含む型であるため、インスタンス化できます。 このメンバーを広範囲に使用するには、具象型を推奨インターフェイスによって置き換えます。 |
| CA1060 | [CA1060:P/invoke を NativeMethods クラスに移動します。](../code-quality/ca1060-move-p-invokes-to-nativemethods-class.md) | System.Runtime.InteropServices.DllImportAttribute 属性でマークされているメソッドなどのプラットフォーム呼び出しメソッド、または [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] で Declare キーワードを使用して定義されたメソッドが、アンマネージ コードにアクセスしています。 これらのメソッドは、NativeMethods、SafeNativeMethods、UnsafeNativeMethods の各クラスのいずれかに含まれる必要があります。 |
| CA1061 |[CA 1061:基底クラスのメソッドを隠ぺいしません。](../code-quality/ca1061-do-not-hide-base-class-methods.md) | 派生メソッドのパラメーター シグネチャ内のある型が、基本メソッドのパラメーター シグネチャ内のそれに対応する型より弱く型指定されていることが、両者の唯一の相違点である場合、基本型内のメソッドが派生型内の同じ名前のメソッドによって隠ぺいされます。 |
| CA1062 | [CA 1062:パブリック メソッドの引数を検証します。](../code-quality/ca1062-validate-arguments-of-public-methods.md) | 外部から参照可能なメソッドに渡されるすべての参照引数について、null かどうかをチェックする必要があります。 |
| CA1063 | [CA1063:IDisposable を正しく実装します。](../code-quality/ca1063-implement-idisposable-correctly.md) | すべての IDisposable 型は、Dispose パターンを適切に実装する必要があります。 |
| CA1064 | [CA1064:例外はパブリックである必要があります。](../code-quality/ca1064-exceptions-should-be-public.md) | 内部例外は、その内部スコープ内でのみ認識されます。 内部スコープの外側にある例外は、基本例外を使用しなければキャッチできません。 場合、内部例外から継承<xref:System.Exception>、 <xref:System.SystemException>、または<xref:System.ApplicationException>、外部のコードには、例外の処理方法を把握するための十分な情報はありません。 |
| CA1065 | [CA 1065:予期しない場所で例外を発生させません](../code-quality/ca1065-do-not-raise-exceptions-in-unexpected-locations.md) | 例外をスローしないはずのメソッドが例外をスローします。 |
| CA1300 | [CA 1300:Messageboxoption を指定します](../code-quality/ca1300-specify-messageboxoptions.md) | テキストを右から左へ読むカルチャでメッセージ ボックスを正しく表示するには、MessageBoxOptions 列挙体の RightAlign メンバーと RtlReading メンバーを、Show メソッドに渡す必要があります。 |
| CA1301 | [CA 1301:アクセラレータが重複の回避します。](../code-quality/ca1301-avoid-duplicate-accelerators.md) | Alt キーを使用するアクセス キー (アクセラレータとも呼ばれます) によって、キーボードからコントロールにアクセスできます。 アクセス キーの重複したコントロールがあると、アクセス キーの動作は不明確になります。 |
| CA1302 | [CA 1302:ロケール特有の文字列をハードコードしません](../code-quality/ca1302-do-not-hardcode-locale-specific-strings.md) | System.Environment.SpecialFolder 列挙体には、特殊なシステム フォルダーを参照するメンバーが含まれます。 このフォルダーの位置は、オペレーティング システムによって異なる場合、ユーザーが位置を変更する場合、および位置がローカライズされる場合があります。 Environment.GetFolderPath メソッドは、Environment.SpecialFolder 列挙体に関連付けられ、ローカライズされ、現在実行されているコンピューターに適切な位置を返します。 |
| CA1303 | [CA 1303:ローカライズされたパラメーターとしてリテラルを渡さないでください。](../code-quality/ca1303-do-not-pass-literals-as-localized-parameters.md) | 外部から参照できるメソッドに渡し文字列リテラルをパラメーターとしてコンス トラクターまたはメソッドは、.NET Framework クラス ライブラリで、その文字列はローカライズ可能にする必要があります。 |
| CA1304 | [CA1304:CultureInfo を指定します](../code-quality/ca1304-specify-cultureinfo.md) | System.Globalization.CultureInfo パラメーターを受け入れるオーバーロードを持つメンバーを呼び出しているメソッドまたはコンストラクターが、CultureInfo パラメーターを使用するオーバーロードを呼び出していません。 CultureInfo オブジェクトまたは System.IFormatProvider オブジェクトが指定されない場合、オーバーロードされたメンバーから提示された既定値は、すべてのロケールに効果が及ばない可能性があります。 |
| CA1305 | [CA1305:IFormatProvider を指定します](../code-quality/ca1305-specify-iformatprovider.md) | System.IFormatProvider パラメーターを受け入れるオーバーロードを持つメンバーを 1 つ以上呼び出しているメソッドまたはコンストラクターが、IFormatProvider パラメーターを使用するオーバーロードを呼び出していません。 System.Globalization.CultureInfo オブジェクトまたは IFormatProvider オブジェクトが指定されない場合、オーバーロードされたメンバーから提示された既定値は、すべてのロケールに効果が及ばない可能性があります。 |
| CA1306 | [CA 1306:データ型のロケールを設定します。](../code-quality/ca1306-set-locale-for-data-types.md) | ロケールによって、データに関するカルチャ固有の表示要素が決まります。たとえば、数値、通貨記号、並べ替え順序に使用する形式などです。 DataTable または DataSet を作成するときは、ロケールを明示的に設定する必要があります。 |
| CA1307 | [CA 1307:StringComparison を指定します。](../code-quality/ca1307-specify-stringcomparison.md) | 文字列比較演算で、StringComparison パラメーターを設定しないメソッド オーバーロードが使用されています。 |
| CA1308 |[CA1308:文字列を大文字に正規化します。](../code-quality/ca1308-normalize-strings-to-uppercase.md) | 文字列は大文字に正規化する必要があります。 小文字への変換時に 1 つの小さい文字グループをラウンド トリップさせることができません。 |
| CA1309 | [CA1309:StringComparison を使用します](../code-quality/ca1309-use-ordinal-stringcomparison.md) | 非言語的な文字列比較演算で、StringComparison パラメーターが Ordinal または OrdinalIgnoreCase に設定されていません。 パラメーターを StringComparison.Ordinal または StringComparison.OrdinalIgnoreCase に明示的に設定することによって、多くの場合、コードの速度、正確さ、および信頼性が向上します。 |
| CA1400 | [CA1400:P/invoke エントリ ポイントが存在する必要があります。](../code-quality/ca1400-p-invoke-entry-points-should-exist.md) |パブリック メソッドまたはプロテクト メソッドが System.Runtime.InteropServices.DllImportAttribute 属性を使用してマークされています。 アンマネージ ライブラリの位置を特定できないか、メソッドがライブラリ内の関数と一致しません。 |
| CA1401 | [CA1401:P/invoke を表示することはできません。](../code-quality/ca1401-p-invokes-should-not-be-visible.md) | パブリック型のパブリック メソッドまたはプロテクト メソッドに、System.Runtime.InteropServices.DllImportAttribute 属性があります ([!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] では Declare キーワードでも実装されます)。 このようなメソッドは公開しないでください。 |
| CA1402 |[CA 1402:COM 参照可能インターフェイスでのオーバー ロードを避ける](../code-quality/ca1402-avoid-overloads-in-com-visible-interfaces.md) | オーバーロードされたメソッドが COM クライアントに公開されると、最初のメソッド オーバーロードだけが名前を保持します。 後続のオーバーロードは、名前にアンダースコア文字 (_) およびオーバーロードの宣言の順序に対応する整数が付加され、一意の名前に変更されます。 |
| CA1403 | [CA 1403:Auto 配置の型が COM に表示することはできません。](../code-quality/ca1403-auto-layout-types-should-not-be-com-visible.md) | COM 参照可能な値型が、LayoutKind.Auto に設定された System.Runtime.InteropServices.StructLayoutAttribute 属性を使用してマークされています。これらの型のレイアウトは、COM クライアントが特定のレイアウトが予期される動作しなくなる .NET Framework のバージョン間で変更できます。 |
| CA1404 | [CA 1404:P/invoke の直後に GetLastError を呼び出します](../code-quality/ca1404-call-getlasterror-immediately-after-p-invoke.md) | Marshal.GetLastWin32Error メソッドまたは同等に呼び出し[!INCLUDE[TLA2#tla_win32](../code-quality/includes/tla2sharptla_win32_md.md)]GetLastError 関数が、直前の呼び出しでないオペレーティング システムにメソッドを呼び出します。 |
| CA1405 | [CA 1405:COM から参照できる型の基本型が COM 参照可能にする必要があります。](../code-quality/ca1405-com-visible-type-base-types-should-be-com-visible.md) | COM 参照可能な型が、COM 参照不可能な型から派生しています。 |
| CA1406 |[CA1406:Visual Basic 6 クライアントに対しては Int64 引数を避ける](../code-quality/ca1406-avoid-int64-arguments-for-visual-basic-6-clients.md) | Visual Basic 6 COM クライアントは、64 ビット整数値にアクセスできません。 |
| CA1407 |[CA1407:COM 参照可能な型で静的メンバーを回避します。](../code-quality/ca1407-avoid-static-members-in-com-visible-types.md) | COM では静的メソッドをサポートしていません。 |
| CA1408 | [CA 1408:AutoDual ClassInterfaceType を使用します。](../code-quality/ca1408-do-not-use-autodual-classinterfacetype.md) | デュアル インターフェイスを使用する型を使用することで、クライアントを特定のインターフェイス レイアウトに対応付けることができます。 将来のバージョンで、この型またはその基本型のレイアウトに変更が加えられると、インターフェイスに対応付けられた COM クライアントが切り離されます。 既定では、ClassInterfaceAttribute 属性が指定されていない場合、ディスパッチ専用インターフェイスが使用されます。 |
| CA1409 | [CA 1409:Com 参照可能な型は、可能でなければなりません](../code-quality/ca1409-com-visible-types-should-be-creatable.md) |COM から参照できると明確にマークされている参照型に、パブリックのパラメーター付きコンストラクターが含まれますが、パブリックの既定 (パラメーターなし) コンストラクターが含まれません。 パブリックの既定コンストラクターがない型は、COM クライアントで作成できません。 |
| CA1410 | [CA 1410:COM 登録メソッドは一致する必要があります。](../code-quality/ca1410-com-registration-methods-should-be-matched.md) | System.Runtime.InteropServices.ComRegisterFunctionAttribute 属性でマークされたメソッドが型で宣言されていますが、System.Runtime.InteropServices.ComUnregisterFunctionAttribute 属性でマークされたメソッドが宣言されていません。またはその逆の状態になっています。 |
| CA1411 | [CA1411:COM 登録メソッドを表示することはできません。](../code-quality/ca1411-com-registration-methods-should-not-be-visible.md) | System.Runtime.InteropServices.ComRegisterFunctionAttribute 属性または System.Runtime.InteropServices.ComUnregisterFunctionAttribute 属性でマークされたメソッドが外部から参照できます。 |
| CA1412 | [CA 1412:ComSource インターフェイスを IDispatch として設定します](../code-quality/ca1412-mark-comsource-interfaces-as-idispatch.md) | 型が System.Runtime.InteropServices.ComSourceInterfacesAttribute 属性によってマークされていますが、1 つ以上の指定されたインターフェイスが ComInterfaceType.InterfaceIsIDispatch に設定された System.Runtime.InteropServices.InterfaceTypeAttribute 属性によってマークされていません。 |
| CA1413 | [CA1413:COM 参照可能な値の型で非パブリック フィールドを回避します。](../code-quality/ca1413-avoid-non-public-fields-in-com-visible-value-types.md) | COM から参照できる値型の非パブリック インスタンス フィールドは、COM クライアントで表示できます。 フィールドの内容をレビューして、公開するべきではない情報や、設計またはセキュリティに意図しない影響を及ぼす情報が含まれていないかどうかを確認してください。 |
| CA1414 | [CA 1414:ブール型の P/invoke 引数を marshalas に設定します](../code-quality/ca1414-mark-boolean-p-invoke-arguments-with-marshalas.md) | Boolean データ型は、アンマネージ コードの複数の表現を持っています。 |
| CA1415 | [CA1415:P/invoke を正しく宣言します。](../code-quality/ca1415-declare-p-invokes-correctly.md) | この規則では、OVERLAPPED 構造体パラメーターへのポインターを持ち、対応するマネージド型パラメーターが System.Threading.NativeOverlapped 構造体へのポインターではない [!INCLUDE[TLA2#tla_win32](../code-quality/includes/tla2sharptla_win32_md.md)] 関数に対するオペレーティング システム呼び出しメソッド宣言が対象になります。 |
| CA1500 | [CA1500:変数名は、フィールド名と一致する必要があります。](../code-quality/ca1500-variable-names-should-not-match-field-names.md) | インスタンスのメソッドで、宣言する型のインスタンス フィールドと名前が一致するパラメーターまたはローカル変数が宣言されていると、エラーの原因となります。 |
| CA1501 | [CA1501:過剰な継承を回避します。](../code-quality/ca1501-avoid-excessive-inheritance.md) | 型が、その継承階層内の 5 つ以上深いレベルにあります。 深いレベルで入れ子にされた型の確認、理解、および保守は困難です。 |
| CA1502 | [CA1502:過剰な複雑さを回避します。](../code-quality/ca1502-avoid-excessive-complexity.md) | この規則は、線形独立のメソッド経路数を示す尺度で、条件分岐の数と複雑さによって決まります。 |
| CA1504 | [CA 1504:紛らわしいフィールド名を確認してください。](../code-quality/ca1504-review-misleading-field-names.md) | 「S _」で始まるインスタンス フィールドの名前または「m _」で始まる静的 (Visual Basic では Shared) フィールドの名前。 |
| CA1505 | [CA1505:メンテナンスできないコードを避ける](../code-quality/ca1505-avoid-unmaintainable-code.md) | 型またはメソッドの保守容易性指数が低い値です。 保守容易性指数の低い型またはメソッドは、保守が困難な可能性があるため、デザインの変更を検討することをお勧めします。 |
| CA1506 |[CA1506:過剰なクラスの結合を避ける](../code-quality/ca1506-avoid-excessive-class-coupling.md) | この規則は、型またはメソッドに含まれる一意の型参照の数をカウントすることによって、クラス結合度を計測します。 |
| CA1600 | [CA 1600:アイドル状態のプロセスの優先順位を使用しないでください。](../code-quality/ca1600-do-not-use-idle-process-priority.md) | プロセス優先順位に Idle を設定しないでください。 System.Diagnostics.ProcessPriorityClass.Idle を設定したプロセスは、CPU を占有するか、そうでない場合はアイドル状態になるため、スタンバイ状態がブロックされます。 |
| CA1601 | [CA 1601:電源状態の変更を妨げるタイマーを使用しないでください。](../code-quality/ca1601-do-not-use-timers-that-prevent-power-state-changes.md) | 定期的な動作の頻度が高くなると、CPU のビジー状態が続き、ディスプレイとハード ディスクをオフにする省電力アイドル タイマーに影響を与えます。 |
| CA1700 | [CA1700:列挙値 'Reserved' という名前しない操作を行います](../code-quality/ca1700-do-not-name-enum-values-reserved.md) | この規則では、"reserved" を含む名前の列挙体のメンバーは、現在使用されていなくても、将来的なバージョンでは名前を変更するか削除されるプレースホルダーと想定しています。 メンバーの名前変更や削除は、互換性に影響する変更点です。 |
| CA1701 | [CA1701:リソース文字列の複合語では、大文字と小文字が正しく区別する必要があります。](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md) | リソース文字列内の語は、大文字と小文字に基づいてトークンに分割されます。 Microsoft スペル チェック ライブラリは、隣接する 2 つのトークンの組み合わせを個別にチェックします。 それらが認識されると、その語はこの規則への違反となります。 |
| CA1702 | [CA1702:複合語では、大文字と小文字が正しく区別する必要があります。](../code-quality/ca1702-compound-words-should-be-cased-correctly.md) | 識別子の名前に複数の語が含まれており、大文字と小文字が正しく使い分けられていない複合語が 1 つ以上あります。 |
| CA1703 | [CA 1703:リソース文字列を正しく入力されなければなりません](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md) | リソース文字列に Microsoft スペル チェック ライブラリで認識されない語が 1 つ以上含まれています。 |
| CA1704 | [CA 1704:識別子は正しく入力されなければなりません](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md) | 外部から参照できる識別子の名前に Microsoft スペル チェック ライブラリで認識されない語が 1 つ以上含まれています。 |
| CA1707 | [CA 1707:識別子はアンダー スコアを含めることはできません。](../code-quality/ca1707-identifiers-should-not-contain-underscores.md) | 名前付け規則では、識別子名にアンダースコア (_) 文字を含めることができません。 この規則により、名前空間、型、メンバー、およびパラメーターがチェックされます。 |
| CA1708 | [CA1708:識別子は、ケース以外で相違させる必要があります。](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md) | 名前空間、型、メンバー、およびパラメーターの各識別子は、大文字/小文字以外のみでは区別できません。共通言語ランタイムを対象とする言語は、大文字と小文字を区別する必要はないためです。 |
| CA1709 | [CA 1709:識別子では、大文字と小文字が正しく区別する必要があります。](../code-quality/ca1709-identifiers-should-be-cased-correctly.md) | 名前付け規則では、パラメーター名には Camel 形式が使用され、名前空間、型、およびメンバーの名前には Pascal 形式が使用されます。 |
| CA1710 | [CA1710:識別子は、正しいサフィックスをいなければなりません](../code-quality/ca1710-identifiers-should-have-correct-suffix.md) |名前付け規則によると、特定の基本型を拡張した型、特定のインターフェイスを実装する型、またはそのような型の派生型は、基本型やインターフェイスに関連するサフィックスを名前に付けます。 |
| CA1711 | [CA1711:識別子には、不適切なサフィックスはありません。](../code-quality/ca1711-identifiers-should-not-have-incorrect-suffix.md) | 規則では、特定の基本型を拡張する型、特定のインターフェイスを実装する型、またはそのような型から派生した型の名前にのみ、固有の予約済みサフィックスを末尾に付けます。 その他の型名では、予約済みのサフィックスを使用しないでください。 |
| CA1712 | [CA 1712:列挙型の値を型名のプレフィックスにしません](../code-quality/ca1712-do-not-prefix-enum-values-with-type-name.md) | 型情報は開発ツールで表示されるため、列挙型のメンバー名には、型名のプレフィックスを付けません。 |
| CA1713 | [CA1713:Before または after プレフィックス イベントのないです。](../code-quality/ca1713-events-should-not-have-before-or-after-prefix.md) | イベント名が "Before" または "After" で始まっています。 特定のシーケンスで発生する関連イベントに名前を付ける場合、現在時制または過去時制を使用して、アクション シーケンスの相対的な位置を示します。 |
| CA1714 | [CA1714:フラグ列挙型が複数形の名前](../code-quality/ca1714-flags-enums-should-have-plural-names.md) | パブリック列挙体に System.FlagsAttribute 属性があり、その名前の末尾に "s" がありません。 FlagsAttribute でマークされた型は複数形の名前を持ちます。これは、この属性が複数の値を指定できることを示すからです。 |
| CA1715 | [CA1715:識別子は正しいプレフィックスをいなければなりません](../code-quality/ca1715-identifiers-should-have-correct-prefix.md) | 外部から参照できるインターフェイスの名前が大文字の "I" から始まっていません。 外部から参照できる型またはメソッドのジェネリック型パラメーターの名前が、大文字の "T" から始まっていません。 |
| CA1716 | [CA1716:識別子は、キーワードと一致する必要があります。](../code-quality/ca1716-identifiers-should-not-match-keywords.md) | 名前空間の名前または型の名前が、プログラミング言語で、予約済みのキーワードと一致します。 名前空間と型の識別子は、共通言語ランタイムを対象にする言語で定義されているキーワードと一致しないようにします。 |
| CA1717 | [CA1717:FlagsAttribute 列挙のみが複数形の名前](../code-quality/ca1717-only-flagsattribute-enums-should-have-plural-names.md) | 名前付け規則では、列挙体の複数形の名前は同時に複数の列挙値を指定できることを意味します。 |
| CA1719 | [CA1719:パラメーター名は、メンバー名と一致する必要があります。](../code-quality/ca1719-parameter-names-should-not-match-member-names.md) | パラメーターはパラメーターの意味、メンバーはメンバーの意味を伝える名前にします。 この 2 つの名前が一致するデザインは、まれにしか見られません。 パラメーターにメンバーと同じ名前を付けるとわかりづらくなり、ライブラリの操作が難しくなります。 |
| CA1720 |[CA 1720:識別子は型名を含めることはできません。](../code-quality/ca1720-identifiers-should-not-contain-type-names.md) | 外部から参照できるメンバーのパラメーター名にデータ型の名前が含まれているか、外部から参照できるメンバーの名前に言語固有のデータ型の名前が含まれています。 |
| CA1721 | [CA1721:プロパティ名は、get メソッドと一致する必要があります。](../code-quality/ca1721-property-names-should-not-match-get-methods.md) |パブリック メンバーまたはプロテクト メンバーの名前が、"Get" から始まっているか、パブリック プロパティまたはプロテクト プロパティの名前と一致します。 "Get" メソッドとプロパティには、それぞれの機能を明確に区別する名前を指定しなければなりません。 |
| CA1722 | [CA1722:識別子には、不適切なプレフィックスはありません。](../code-quality/ca1722-identifiers-should-not-have-incorrect-prefix.md) | 規則では、特定のプログラミング要素にのみ、固有のプレフィックスで始まる名前を付けることができます。 |
| CA1724 | [CA1724:型名が名前空間と一致する必要があります。](../code-quality/ca1724-type-names-should-not-match-namespaces.md) | 型名は、.NET Framework クラス ライブラリで定義されている名前空間の名前と一致する必要があります。 この規則に違反すると、ライブラリが使いづらくなります。 |
| CA1725 | [CA1725:パラメーター名は基本宣言と一致する必要があります。](../code-quality/ca1725-parameter-names-should-match-base-declaration.md) | オーバーライド階層のパラメーターに対する一貫性のある名前付けによって、メソッド オーバーライドの有用性が高まります。 派生メソッドのパラメーター名が基本宣言のパラメーター名と異なる場合、メソッドが基本メソッドのオーバーライドであるか、またはメソッドの新しいオーバーライドであるかについて混乱が生じる可能性があります。 |
| CA1726 | [CA 1726: 適切な。用語を使用します](../code-quality/ca1726-use-preferred-terms.md) | 外部から参照可能な識別子の名前に含まれている用語に対応する、別の推奨される用語があります。 あるいは、名前に "Flag" または "Flags" という語が含まれています。 |
| CA1800 | [CA 1800:不必要にキャストしません](../code-quality/ca1800-do-not-cast-unnecessarily.md) | 二重のキャストがあるとパフォーマンスが低下します。特に、小さな繰り返しステートメントでキャストが実行される場合はそうです。 |
| CA1801 | [CA 1801:未使用のパラメーターをレビューします](../code-quality/ca1801-review-unused-parameters.md) | メソッドのシグネチャに、メソッドの本体で使用されていないパラメーターがあります。 |
| CA1802 |[CA 1802:適切な場所にリテラルを使用します。](../code-quality/ca1802-use-literals-where-appropriate.md) |フィールドが static および read-only ([!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] では Shared および ReadOnly) として宣言され、コンパイル時に計算できる値によって初期化されています。 対象フィールドに割り当てられている値は、コンパイル時に計算であるため、宣言を const に変更 (で Const [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]) の代わりに実行時のコンパイル時に値を計算するためのフィールドします。 |
| CA1804 | [CA 1804:使用されていないローカルを削除します](../code-quality/ca1804-remove-unused-locals.md) | 使用されていないローカル変数や不要な引数があると、アセンブリのサイズが大きくなり、パフォーマンスが低下します。 |
| CA1806 | [CA 1806:メソッドの結果を無視しません。](../code-quality/ca1806-do-not-ignore-method-results.md) | 新しく作成されたオブジェクトが現在まで使用されていないか、新しい文字列を作成して返すメソッドが呼び出されて作成された新しい文字列が現在まで使用されていません。あるいは、COM または P/Invoke メソッドから返された HRESULT またはエラー コードが現在まで使用されていません。 |
| CA1809 |[CA1809:過剰なローカルします。](../code-quality/ca1809-avoid-excessive-locals.md) | パフォーマンス最適化の一般的な方法として、メモリではなくプロセッサのレジスタに値を格納する方法があります。これは "値のレジスタ格納" と呼ばれます。 すべてのローカル変数は、レジスタである可能性を向上させるのには、64 をローカル変数の数を制限します。 |
| CA1810 | [CA 1810:参照型の静的フィールドのインラインを初期化します](../code-quality/ca1810-initialize-reference-type-static-fields-inline.md) | 型で明示的な静的コンストラクターを宣言すると、Just-In-Time (JIT) コンパイラが、静的コンストラクターが呼び出されたことを確認するために、型の静的メソッドと静的インスタンス コンストラクターに個別にチェックを追加します。 静的コンストラクターのチェックによってパフォーマンスが低下することがあります。 |
| CA1811 | [CA1811:呼び出されていないプライベート コードを避ける](../code-quality/ca1811-avoid-uncalled-private-code.md) | プライベート メンバーまたは内部 (アセンブリ レベル) メンバーが、アセンブリ内において、また共通言語ランタイムおよびデリゲートのいずれからも呼び出されていません。 |
| CA1812 | [CA1812:インスタンス化されていない内部クラスを回避します。](../code-quality/ca1812-avoid-uninstantiated-internal-classes.md) | アセンブリ レベルの型のインスタンスが、アセンブリ内のコードから作成されません。 |
| CA1813 | [CA1813:シールされていない属性します。](../code-quality/ca1813-avoid-unsealed-attributes.md) | .NET Framework クラス ライブラリでは、カスタム属性を取得するメソッドを提供します。 既定では、これらのメソッドで属性の継承階層が検索されます。 属性をシールすると、継承階層の全体が検索されなくなるため、パフォーマンスが向上します。 |
| CA1814 | [CA1814:多次元よりジャグ配列を優先します。](../code-quality/ca1814-prefer-jagged-arrays-over-multidimensional.md) | ジャグ配列とは、その要素も配列である配列です。 要素を構成する配列のサイズは異なってもよいため、データ セットによっては無駄な空間が少なくなります。 |
| CA1815 | [CA1815:equals および operator equals を値型でオーバーライドします](../code-quality/ca1815-override-equals-and-operator-equals-on-value-types.md)」を参照してください。 | 値型の場合、Equals を継承した実装が Reflection ライブラリを使用して、すべてのフィールドの内容を比較します。 Reflection は計算コストが高いため、場合によってはすべてのフィールドで等値性を比較する必要はありません。 ユーザーがインスタンスの比較または並べ替えを行うことや、ハッシュ テーブル キーとしてインスタンスを使用することが予想される場合には、値型に Equals を実装する必要があります。 |
| CA1816 | [CA 1816:GC を呼び出します。SuppressFinalize 正しく](../code-quality/ca1816-call-gc-suppressfinalize-correctly.md) | Dispose の実装であるメソッドでは、GC は呼び出されません。SuppressFinalize;または、Dispose の実装ではないメソッドは、GC を呼び出します。SuppressFinalize;または、GC のメソッド呼び出し。SuppressFinalize およびこの (Visual Basic で Me) 以外は何かのパス。 |
| CA1819 | [CA 1819:プロパティは、配列を返す必要がありますいません。](../code-quality/ca1819-properties-should-not-return-arrays.md) | プロパティが読み取り専用であっても、プロパティで返される配列は書き込みから保護されません。 配列の改ざんを防ぐには、プロパティで配列のコピーを返す必要があります。 一般に、このようなプロパティを呼び出すときのパフォーマンス低下は理解されません。 |
| CA1820 | [CA1820:文字列の長さを使用して空の文字列をテスト](../code-quality/ca1820-test-for-empty-strings-using-string-length.md) | String.Length プロパティまたは String.IsNullOrEmpty メソッドを使用して文字列を比較する方法は、Equals を使用する場合よりもはるかに高速です。 |
| CA1821 | [CA1821: 空のファイナライザーを削除します](../code-quality/ca1821-remove-empty-finalizers.md) | オブジェクトの有効期間の追跡に関連するパフォーマンス オーバーヘッドが増大するため、ファイナライザーは可能な限り使用しないでください。 空のファイナライザーを使用すると、オーバーヘッドが増大するだけで何の利点もありません。 |
| CA1822 |[CA1822:静的メンバーをマーク](../code-quality/ca1822-mark-members-as-static.md) | インスタンス データにアクセスしない、またはインスタンス メソッドを呼び出さないメンバーは、静的 ([!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] では共有) としてマークできます。 メソッドを静的としてマークすると、コンパイラはこれらのメンバーに対する非仮想呼び出しサイトを出力します。 パフォーマンス重視のコードでは、これにより大きくパフォーマンスを向上できます。 |
| CA1823 | [CA1823:使用されていないプライベート フィールドを回避します。](../code-quality/ca1823-avoid-unused-private-fields.md) | アセンブリ内でアクセスされていないと思われるプライベート フィールドが検出されました。 |
| CA1824 |[CA1824:アセンブリを neutralresourceslanguageattribute に設定します](../code-quality/ca1824-mark-assemblies-with-neutralresourceslanguageattribute.md) | NeutralResourcesLanguage 属性は、ResourceManager に対し、アセンブリのニュートラル カルチャのリソースを表示するために使用した言語を通知します。 これにより、読み込んだ最初のリソースに対する検索のパフォーマンスが向上し、ワーキング セットを縮小できます。 |
| CA1900 | [CA 1900:値型フィールドはポータブルでなければなりません](../code-quality/ca1900-value-type-fields-should-be-portable.md) | この規則は、明示的なレイアウトによって宣言された構造体が、64 ビット オペレーティング システムでアンマネージ コードにマーシャリングされるときに、適切にアライメントされるかどうかを確認します。 |
| CA1901 | [CA1901:P/invoke 宣言はポータブルでなければなりません](../code-quality/ca1901-p-invoke-declarations-should-be-portable.md) | この規則では、P/Invoke の各パラメーターのサイズと戻り値が評価され、32 ビットおよび 64 ビット オペレーティング システムのアンマネージ コードにマーシャリングされたときのパラメーターのサイズが正しいことが検証されます。 |
| CA1903 | [CA1903:対象のフレームワークから API のみを使用します。](../code-quality/ca1903-use-only-api-from-targeted-framework.md) | メンバーまたは型が、プロジェクトの対象のフレームワークに含まれていない Service Pack で導入されたメンバーまたは型を使用しています。 |
| CA2000 | [CA 2000:スコープが失われる前にオブジェクトを破棄します。](../code-quality/ca2000-dispose-objects-before-losing-scope.md) | 例外的なイベントが発生するとオブジェクトのファイナライザーを実行できないため、オブジェクトに対するすべての参照がスコープ外になる前に、オブジェクトを明示的に破棄する必要があります。 |
| CA2001 | [CA 2001:問題のあるメソッドは呼び出しません](../code-quality/ca2001-avoid-calling-problematic-methods.md) | メンバーが危険性または問題のあるメソッドを呼び出します。 |
| CA2002 |[CA 2002:Id が不十分なオブジェクトをロックしないでください。](../code-quality/ca2002-do-not-lock-on-objects-with-weak-identity.md) |アプリケーション ドメインの境界を越えてオブジェクトに直接アクセスできる場合、そのオブジェクトの ID は不十分と表現されます。 スレッドで ID が不十分なオブジェクトをロックしようとすると、ブロックされることがあります。たとえば、異なるアプリケーション ドメインの別スレッドで、既に同じオブジェクトがロックされている場合です。 |
| CA2003 |[CA 2003:ファイバーをスレッドとして処理しません](../code-quality/ca2003-do-not-treat-fibers-as-threads.md) | マネージド スレッドが [!INCLUDE[TLA2#tla_win32](../code-quality/includes/tla2sharptla_win32_md.md)] スレッドとして扱われています。 |
| CA2004 | [CA 2004:GC への呼び出しを削除します。KeepAlive](../code-quality/ca2004-remove-calls-to-gc-keepalive.md) | SafeHandle の使用に変更する場合、すべての GC.KeepAlive (object) の呼び出しを削除します。 この場合、クラスに GC.KeepAlive の呼び出しを含めることはできません。 クラスはファイナライザーを持っていない代わりに、SafeHandle を使用して OS ハンドルを終了していることが前提となっています。 |
| CA2006 | [CA2006:SafeHandle を使用して、ネイティブ リソースをカプセル化するには](../code-quality/ca2006-use-safehandle-to-encapsulate-native-resources.md) | マネージド コードで IntPtr を使用すると、セキュリティ上の問題および信頼性の問題が発生する可能性があります。 すべての IntPtr の使用状況をチェックして、SafeHandle または類似のテクノロジに置き換える必要があるかどうかを判断してください。 |
| CA2100 | [CA 2100:SQL クエリのセキュリティの脆弱性を確認します。](../code-quality/ca2100-review-sql-queries-for-security-vulnerabilities.md) | メソッドに渡された文字列引数から構築された文字列を使用して System.Data.IDbCommand.CommandText プロパティが設定されています。 この規則では、文字列引数にユーザー入力が含まれていることが想定されています。 ユーザー入力から構築された SQL コマンド文字列には、SQL 注入攻撃に対する脆弱性があります。 |
| CA2101 |[CA 2101:P/invoke 文字列引数に対してマーシャ リングを指定します。](../code-quality/ca2101-specify-marshaling-for-p-invoke-string-arguments.md) | プラットフォーム呼び出しメンバーが、部分信頼の呼び出し元を許可し、文字列パラメーターを持ち、さらにその文字列を明示的にマーシャリングしていません。 これはセキュリティ上の脆弱性となる可能性があります。 |
| CA2102 | [CA 2102:汎用ハンドラーで非 CLSCompliant の例外をキャッチします。](../code-quality/ca2102-catch-non-clscompliant-exceptions-in-general-handlers.md) | アセンブリ内の RuntimeCompatibilityAttribute でマークされていないメンバーまたは RuntimeCompatibility(WrapNonExceptionThrows = false) でマークされているメンバーには、System.Exception を処理する catch ブロックがあり、その直後に汎用 catch ブロックはありません。 |
| CA2103 | [CA 2103:強制セキュリティを確認してください。](../code-quality/ca2103-review-imperative-security.md) |メソッドが強制セキュリティを使用しています。また、そのメソッドで、確認要求がアクティブな場合に変更できるステータス情報または戻り値を使用して、アクセス許可を構築している可能性があります。 できる限り、宣言セキュリティを使用します。 |
| CA2104 |[CA 2104:読み取りのみ変更可能な参照型を宣言しません](../code-quality/ca2104-do-not-declare-read-only-mutable-reference-types.md) | 外部から参照できる型に、変更可能な参照型である、外部から参照可能な読み取り専用のフィールドがあります。 変更可能な型とは、インスタンス データを変更できる型です。 |
| CA2105 | [CA 2105:配列フィールドいない読み取り専用にします。](../code-quality/ca2105-array-fields-should-not-be-read-only.md) |配列を含むフィールドに read-only ([!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] では ReadOnly) 修飾子を適用すると、そのフィールドで参照先の配列を変更できません。 ただし、読み取り専用フィールドに格納された配列の要素は変更できます。 |
| CA2106 | [CA 2106:セキュリティで保護されたアサートします。](../code-quality/ca2106-secure-asserts.md) | メソッドによってアクセス許可がアサートされますが、呼び出し元に対してセキュリティ チェックが実行されていません。 セキュリティ チェックを実行せずにセキュリティ アクセス許可をアサートすると、悪用される可能性があるセキュリティの弱点がコード内に残る場合があります。 |
| CA2107 | [CA2107:Deny し、permitonly の用法](../code-quality/ca2107-review-deny-and-permit-only-usage.md) |PermitOnly メソッドと CodeAccessPermission.Deny セキュリティ アクションは、.NET Framework のセキュリティの高度な知識を持つユーザーだけが使用する必要があります。 コードにこのセキュリティ アクションを使用する場合、セキュリティを再確認する必要があります。 |
| CA2108 | [CA 2108:値型で宣言型セキュリティを確認してください。](../code-quality/ca2108-review-declarative-security-on-value-types.md) | パブリックまたはプロテクトの値型が、データ アクセスまたはリンク確認要求で保護されています。 |
| CA2109 | [CA 2109:表示するイベント ハンドラーをレビューします](../code-quality/ca2109-review-visible-event-handlers.md) | パブリックまたはプロテクトのイベント ハンドラー メソッドが検出されました。 イベント ハンドラー メソッドは、絶対に必要な場合を除き公開しないでください。 |
| CA2111 |[CA2111:ポインターを表示することはできません。](../code-quality/ca2111-pointers-should-not-be-visible.md) | ポインターがプライベート、内部、読み取り専用のいずれでもありません。 悪意のあるコードで、ポインターの値が変更される可能性があります。結果的に、メモリの任意の位置にアクセスされたり、アプリケーション エラーやシステム障害の原因になります。 |
| CA2112 | [CA 2112:セキュリティで保護された型はフィールドを公開する必要があります。](../code-quality/ca2112-secured-types-should-not-expose-fields.md) | パブリック型またはプロテクト型に、パブリック フィールドが含まれ、リンク確認要求で保護されています。 リンク確認要求で保護されている型のインスタンスに対するアクセス権がコードにある場合、その型のフィールドにアクセスするためにリンク確認要求に適合する必要はありません。 |
| CA2114 | [CA 2114:メソッドのセキュリティの種類のスーパー セットである必要があります。](../code-quality/ca2114-method-security-should-be-a-superset-of-type.md) | メソッドでは、同じアクションについて、メソッド レベルと型レベルの宣言セキュリティの両方を指定することはできません。 |
| CA2115 | [CA 2115:GC を呼び出します。KeepAlive ネイティブ リソースを使用する場合](../code-quality/ca2115-call-gc-keepalive-when-using-native-resources.md) | この規則では、アンマネージ コードでまだ使用されているのに、アンマネージ リソースが終了されたときに発生する可能性のあるエラーを検出します。 |
| CA2116 | [CA2116:APTCA メソッドは APTCA メソッドのみを呼び出す必要があります。](../code-quality/ca2116-aptca-methods-should-only-call-aptca-methods.md) |APTCA (AllowPartiallyTrustedCallersAttribute) が完全に信頼されたアセンブリにあり、部分的に信頼された呼び出し元を許可しない別のアセンブリのコードをアセンブリが実行する場合、セキュリティ上の弱点になります。 |
| CA2117 | [CA2117:APTCA 型は APTCA 基本型のみを拡張する必要があります。](../code-quality/ca2117-aptca-types-should-only-extend-aptca-base-types.md) | APTCA が完全に信頼されたアセンブリにあり、アセンブリの型が部分的に信頼された呼び出し元を許可しない型から継承する場合、セキュリティ上の弱点になります。 |
| CA2118 | [CA2118:SuppressUnmanagedCodeSecurityAttribute の使用法の確認](../code-quality/ca2118-review-suppressunmanagedcodesecurityattribute-usage.md) |COM 相互運用機能またはオペレーティング システム呼び出し機能を使用するアンマネージ コードを実行するメンバーの場合、SuppressUnmanagedCodeSecurityAttribute によって、既定のセキュリティ システムの動作が変わります。 この属性は、主にパフォーマンスを向上するために使用されますが、パフォーマンスが向上するとセキュリティ上のリスクも高くなります。 |
| CA2119 | [CA 2119:プライベート インターフェイスを満たすメソッドをシールします](../code-quality/ca2119-seal-methods-that-satisfy-private-interfaces.md) | 継承可能なパブリック型により、internal ([!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] では Friend) インターフェイスのオーバーライド可能なメソッド実装が提供されます。 この規則違反を修正するには、アセンブリの外側でメソッドがオーバーライドされないようにします。 |
| CA2120 | [CA2120:セキュリティで保護されたシリアル化コンス トラクター](../code-quality/ca2120-secure-serialization-constructors.md) | この型には、System.Runtime.Serialization.SerializationInfo オブジェクトおよび System.Runtime.Serialization.StreamingContext オブジェクトを使用するコンストラクター (シリアル化コンストラクターのシグネチャ) があります。 このコンストラクターはセキュリティ チェックで保護されていませんが、型に含まれる標準コンストラクターの 1 つ以上は保護されています。 |
| CA2121 | [CA 2121:静的コンス トラクターはプライベートでなければなりません](../code-quality/ca2121-static-constructors-should-be-private.md) | システムで静的コンストラクターが呼び出されてから、型の最初のインスタンスが作成されるか、静的メンバーが参照されます。 静的コンストラクターがプライベートである場合、システム以外のコードから呼び出すことができます。 コンストラクターで実行される操作によっては、これによって予期しない動作が発生することがあります。 |
| CA2122 | [CA 2122:リンク確認要求でメソッドを間接的に公開できません。](../code-quality/ca2122-do-not-indirectly-expose-methods-with-link-demands.md) | パブリック メンバーまたはプロテクト メンバーはリンク確認要求を含み、セキュリティ チェックを実行しないメンバーから呼び出されています。 リンク確認要求では、直接の呼び出し元のアクセス許可しかチェックされません。 |
| CA2123 | [CA2123:オーバーライドのリンク確認要求は基本同一である必要があります。](../code-quality/ca2123-override-link-demands-should-be-identical-to-base.md) | この規則は、メソッドをその基本メソッド (別の型のインターフェイスまたは仮想メソッド) とマッチングし、それぞれについてリンク確認要求を比較します。 この規則に違反すると、悪意のある呼び出し元が、保護されていないメソッドを呼び出すだけで、リンク確認要求を省略できます。 |
| CA2124 | [CA2124:ラップの脆弱性のある finally 句の外側を try します。](../code-quality/ca2124-wrap-vulnerable-finally-clauses-in-outer-try.md) | パブリック メソッドまたはプロテクト メソッドに try/finally ブロックが含まれています。 この finally ブロックはセキュリティの状態をリセットすると思われますが、それ自体が finally ブロックで囲まれていません。 |
| CA2126 | [CA 2126:型のリンク要求には、継承要求が必要です。](../code-quality/ca2126-type-link-demands-require-inheritance-demands.md) | シールされていないパブリックな型がリンク確認要求によって保護され、オーバーライド可能なメソッドを持っています。 その型またはメソッドが継承確認要求によって保護されていません。 |
| CA2127 | [CA 2136:メンバーには、透過性注釈の競合はありません。](../code-quality/ca2136-members-should-not-have-conflicting-transparency-annotations.md) | Critical コードは、100% 透過的なアセンブリで発生することはできません。 このルールは、型、フィールド、およびメソッド レベルですべての SecurityCritical 注釈の 100% の透過的なアセンブリを分析します。 |
| CA2128 |[CA2147:透過的メソッドは、セキュリティを使用しない可能性がありますアサート](../code-quality/ca2147-transparent-methods-may-not-use-security-asserts.md) | このルールは、すべてのメソッドとは 100% 透明または混合透過的/クリティカル、およびフラグをアサートの宣言的または強制的に使用するアセンブリ内の型を分析します。 |
| CA2129 | [CA 2140:透過的なコードは、セキュリティ上重要な項目を参照する必要があります。](../code-quality/ca2140-transparent-code-must-not-reference-security-critical-items.md) | SecurityTransparentAttribute でマークされたメソッドが、SecurityCritical とマークされたパブリックでないメンバーを呼び出しています。 この規則では、透過的/クリティカル混在のアセンブリ内のすべてのメソッドと型を分析し、透過的なコードからパブリックでないセキュリティ クリティカルなコードへの呼び出しのうち SecurityTreatAsSafe が適用されていないものにフラグが設定されます。 |
| CA2130 | [CA 2130:セキュリティ上重要な定数は透過的にする必要があります。](../code-quality/ca2130-security-critical-constants-should-be-transparent.md) | 実行時に検索の必要がない値がコンパイラのインライン定数に設定されているため、定数値に対して透過性は適用されません。 透過的なコードからは定数にアクセスできないとコード レビューアーが考えることがないよう、定数フィールドは透過的セキュリティなフィールドとして定義する必要があります。 |
| CA2131 | [CA 2131:セキュリティ クリティカルな型は型の等価性に参加できません。](../code-quality/ca2131-security-critical-types-may-not-participate-in-type-equivalence.md) | データ型は型の等価性に関与し、型自身、または型のメンバーあるいはフィールドが、SecurityCriticalAttribute 属性でマークされます。 この規則は、すべての重要な型、または型の等価性に関与する重要なメソッドあるいはフィールドが定義されたすべての型に対して適用されます。 こうした型が CLR によって検出されると、CLR では型が読み込まれず、実行時に TypeLoadException が発生します。 通常、この規則は、tlbimp やコンパイラによって型の等価性を実装するのではなく、ユーザーが手動で型の等価性を実装したときに適用されます。 |
| CA2132 | [CA2132:既定のコンス トラクターは、少なくとも基本型の既定のコンス トラクターと同程度に重要である必要があります。](../code-quality/ca2132-default-constructors-must-be-at-least-as-critical-as-base-type-default-constructors.md) |SecurityCriticalAttribute でマークされている型およびメンバーを Silverlight アプリケーション コードで使用することはできません。 セキュリティが重要な型やメンバーは、.NET Framework for Silverlight クラス ライブラリの信頼されているコードからのみ使用できます。 派生クラスにおけるパブリックな構築または保護された構築の透過性は、基本クラスと同程度以上である必要があるため、アプリケーション内のクラスを、SecurityCritical としてマークされたクラスから派生させることはできません。 |
| CA2133 | [CA2133:デリゲートは透過性の整合メソッドにバインドする必要があります。](../code-quality/ca2133-delegates-must-bind-to-methods-with-consistent-transparency.md) | この警告は、SecurityCriticalAttribute でマークされているデリゲートを、透過的メソッドまたは SecuritySafeCriticalAttribute でマークされているメソッドにバインドするメソッドに対して適用されます。 この警告は、透過的なデリゲートまたはセーフ クリティカルなデリゲートを、クリティカル メソッドにバインドするメソッドに対しても適用されます。 |
| CA2134 | [CA 2134:メソッドは基本メソッドをオーバーライドするときに透過性の整合性を保つ必要があります。](../code-quality/ca2134-methods-must-keep-consistent-transparency-when-overriding-base-methods.md) |この規則は、SecurityCriticalAttribute でマークされているメソッドが、透過的メソッドまたは SecuritySafeCriticalAttribute でマークされているメソッドをオーバーライドするときに適用されます。 また、透過的メソッドまたは SecuritySafeCriticalAttribute でマークされているメソッドが、SecurityCriticalAttribute でマークされているメソッドをオーバーライドした場合も、この規則が適用されます。 この規則は、仮想メソッドをオーバーライドする場合やインターフェイスを実装する場合に適用されます。 |
| CA2135 | [CA2135:レベル 2 のアセンブリは Linkdemand を含めることはできません。](../code-quality/ca2135-level-2-assemblies-should-not-contain-linkdemands.md) | LinkDemands は、レベル 2 のセキュリティ規則セットでは使用が非推奨とされます。 LinkDemands を使用して JIT コンパイル時にセキュリティを適用するのではなく、メソッド、型、およびフィールドに SecurityCriticalAttribute 属性を設定します。 |
| CA2136 | [CA 2136:メンバーには、透過性注釈の競合はありません。](../code-quality/ca2136-members-should-not-have-conflicting-transparency-annotations.md) | 透過性属性は、大きいスコープのコード要素から小さいスコープの要素に適用されます。 大きいスコープのコード要素の透過性属性は、最初の要素に含まれているコード要素の透過性属性よりも優先されます。 たとえば、SecurityCriticalAttribute 属性でマークされたクラスに SecuritySafeCriticalAttribute 属性でマークされたメソッドを含めることはできません。 |
| CA2137 | [CA 2137:透過的メソッドは、検証可能な IL のみを含める必要があります。](../code-quality/ca2137-transparent-methods-must-contain-only-verifiable-il.md) | メソッドに検証できないコードが含まれているか、メソッドから参照渡しで型が返されます。 この規則は、透過的セキュリティ コードが、検証できない MISL (Microsoft Intermediate Language) を実行しようとすると適用されます。 ただし、規則には完全な IL 検証ツールは含まれていないため、代わりにヒューリスティックを使用して、ほとんどの MSIL 検証違反が検出されます。 |
| CA2138 | [CA2138:透過的メソッドは、SuppressUnmanagedCodeSecurity 属性を持つメソッドを呼び出す必要がありますいません。](../code-quality/ca2138-transparent-methods-must-not-call-methods-with-the-suppressunmanagedcodesecurity-attribute.md) | 透過的セキュリティ メソッドは、SuppressUnmanagedCodeSecurityAttribute 属性でマークされているメソッドを呼び出します。 |
| CA2139 | [CA 2139:透過的メソッドは、HandleProcessCorruptingExceptions 属性を使用可能性があります。](../code-quality/ca2139-transparent-methods-may-not-use-the-handleprocesscorruptingexceptions-attribute.md) | この規則は、HandleProcessCorruptedStateExceptionsAttribute 属性を使用してプロセス破損状態例外を処理しようとする、すべての透過的メソッドに対して適用されます。 プロセス破損状態例外は、CLR バージョン 4.0 に分類される例外です (AccessViolationException など)。 HandleProcessCorruptedStateExceptionsAttribute 属性はセキュリティ クリティカルなメソッドでのみ使用できる属性で、透過的メソッドに適用された場合は無視されます。 |
| CA2140 | [CA 2140:透過的なコードは、セキュリティ上重要な項目を参照する必要があります。](../code-quality/ca2140-transparent-code-must-not-reference-security-critical-items.md) | SecurityCriticalAttribute 属性でマークされたコード要素は、セキュリティ上重要になります。 透過的なメソッドでセキュリティ上重要な要素を使用することはできません。 透過データ型でセキュリティ上重要な型を使用しようとすると、TypeAccessException、MethodAccessException、FieldAccessException のいずれかの例外が発生します。 |
| CA2141 |[CA2141: 透過的メソッドは、LinkDemand を満たしてはならない](../code-quality/ca2141-transparent-methods-must-not-satisfy-linkdemands.md) | 透過的セキュリティ メソッドは、APTCA でマークされていないアセンブリ内のメソッドを呼び出します。また、透過的セキュリティ メソッドは、データ型またはメソッドに対する LinkDemand の要件を満たします。 |
| CA2142 | [CA2142:LinkDemands を透過的なコードを保護する必要がありません。](../code-quality/ca2142-transparent-code-should-not-be-protected-with-linkdemands.md) | この規則は、アクセスするために LinkDemands を要求する透過的メソッドに対して適用されます。 透過的セキュリティ コードでは、操作のセキュリティ検証を行うことができないため、アクセス許可を要求できません。 |
| CA2143 | [CA 2143:透過的メソッドは、セキュリティ要求を使用しないでください。](../code-quality/ca2143-transparent-methods-should-not-use-security-demands.md) | 透過的セキュリティ コードでは、操作のセキュリティ検証を行うことができないため、アクセス許可を要求できません。 透過的セキュリティ コードは、フル アクセス要求を使用して、セキュリティ上の決定を行う必要があります。セーフ クリティカルなコードでは、透過的なコードを使用してフル アクセス要求を行うことはできません。 |
| CA2144 | [CA 2144:透過的なコードは、バイト配列からアセンブリを読み込めません](../code-quality/ca2144-transparent-code-should-not-load-assemblies-from-byte-arrays.md) | 透過的なコードはセキュリティ上重要な操作を実行できないため、透過的なコードのセキュリティ レビューは、クリティカル コードのセキュリティ レビューほど完全ではありません。 バイト配列から読み込まれるアセンブリは透過的なコード内で認識されない場合がありますが、監査を必要とする、クリティカルなコード、またはさらに重要であるセーフ クリティカルなコードがそのバイト配列に含まれる可能性があります。 |
| CA2145 | [CA2145:透過的なメソッドが、SuppressUnmanagedCodeSecurityAttribute で修飾されていない必要があります。](../code-quality/ca2145-transparent-methods-should-not-be-decorated-with-the-suppressunmanagedcodesecurityattribute.md) | SuppressUnmanagedCodeSecurityAttribute 属性で修飾されたメソッドには、それを呼び出すメソッドに対して適用される暗黙的な LinkDemand があります。 この LinkDemand では、呼び出し元のコードがセキュリティ クリティカルなコードである必要があります。 SuppressUnmanagedCodeSecurity を使用するメソッドに SecurityCriticalAttribute 属性を設定すると、メソッドの呼び出し元に対してこの要件がより明確になります。 |
| CA2146 | [CA2146:種類は、少なくとも、基本型およびインターフェイスと同程度に重要である必要があります。](../code-quality/ca2146-types-must-be-at-least-as-critical-as-their-base-types-and-interfaces.md) | 派生型に透過的セキュリティ属性が設定されていて、この属性が基本型または実装されたインターフェイスほど重要ではない場合に、この規則が適用されます。 クリティカルな基本型から派生したり、クリティカルなインターフェイスを実装したりできるのは、クリティカルなデータ型だけです。また、セーフ クリティカルな基本型から派生したり、セーフ クリティカルなインターフェイスを実装したりできるのは、クリティカルまたはセーフ クリティカルなデータ型だけです。 |
| CA2147 |[CA2147:透過的メソッドは、セキュリティを使用しない可能性がありますアサート](../code-quality/ca2147-transparent-methods-may-not-use-security-asserts.md) | SecurityTransparentAttribute とマークされたコードには、アサートに必要なアクセス許可が付与されません。 |
| CA2149 | [CA2149:透過的メソッドはネイティブ コードを呼び出す必要がありますいません。](../code-quality/ca2149-transparent-methods-must-not-call-into-native-code.md) | この規則は、P/Invoke などを使用してネイティブ コードを直接呼び出すすべての透過的メソッドに対して適用されます。 この規則に違反すると、レベル 2 の透過性モデルで MethodAccessException が発生し、レベル 1 の透過性モデルで UnmanagedCode に対するフル アクセス要求が発生します。 |
| CA2151 |[CA 2151:重要な型のフィールドはセキュリティ クリティカルなをする必要があります。](../code-quality/ca2151-fields-with-critical-types-should-be-security-critical.md) | セキュリティ クリティカルな型を使用するには、型を参照するコードがセキュリティ クリティカルであるか、セキュリティ セーフ クリティカルである必要があります。 これは、参照が間接的である場合にも当てはまります。 そのため、透過的セキュリティまたはセキュリティ セーフ クリティカルなフィールドが存在すると、透過的なコードはこのフィールドにアクセスできないので、紛らわしくなります。 |
| CA2200 | [CA 2200:スタックの詳細を保持するために再スローします。](../code-quality/ca2200-rethrow-to-preserve-stack-details.md) | 例外が再スローされ、その例外が throw ステートメントで明示的に指定されています。 throw ステートメントで例外を指定して例外が再スローされると、例外をスローした元のメソッドと現在のメソッドの間で呼び出されたメソッドの一覧は失われます。 |
| CA2201 | [CA2201:予約された例外の種類を発生させません](../code-quality/ca2201-do-not-raise-reserved-exception-types.md) | これにより、元のエラーの検出およびデバッグが困難になります。 |
| CA2202 | [CA 2202:オブジェクトを複数回破棄しません](../code-quality/ca2202-do-not-dispose-objects-multiple-times.md) |メソッドの実装に、同じオブジェクトに対して System.IDisposable.Dispose または Dispose と同等の操作 (たとえば、一部の型に対する Close() メソッドなど) を複数回呼び出すコード パスが含まれています。 |
| CA2204 | [CA2204:リテラルは正しく入力されなければなりません](../code-quality/ca2204-literals-should-be-spelled-correctly.md) | メソッド本体に含まれるリテラル文字列内に Microsoft スペル チェック ライブラリで認識されない語が 1 つ以上あります。 |
| CA2205 | [CA2205:Win32 API に相当するマネージドの使用します。](../code-quality/ca2205-use-managed-equivalents-of-win32-api.md) | オペレーティング システム呼び出しメソッドが定義されているし、同等の機能を持つメソッドですが、.NET Framework クラス ライブラリに記載されています。 |
| CA2207 | [CA2207:値型の静的フィールドのインラインを初期化します](../code-quality/ca2207-initialize-value-type-static-fields-inline.md) | 値型で明示的な静的コンストラクターを宣言しています。 この規則違反を修正するには、静的データが宣言されたとき、および静的コンストラクターを削除するときに、静的データをすべて初期化します。 |
| CA2208 |[CA2208:引数の例外を正しくインスタンス化します。](../code-quality/ca2208-instantiate-argument-exceptions-correctly.md) | ArgumentException またはそのクラスから派生した例外の種類の既定 (パラメーターなし) のコンストラクターに対して呼び出しが行われたか、ArgumentException またはそのクラスから派生した例外の種類のパラメーター付きのコンストラクターに不適切な文字列型の引数が渡されました。 |
| CA2210 |[CA 2210:アセンブリが有効な厳密な名前](../code-quality/ca2210-assemblies-should-have-valid-strong-names.md) | 厳密な名前によって、改ざんされたアセンブリを、クライアントが無意識のうちに読み込む問題を防ぐことができます。 厳密な名前のないアセンブリが配置される状況は、限定されます。 適切に署名されていないアセンブリを共有または配布すると、アセンブリが改ざんされる場合、共通言語ランタイムでアセンブリを読み込むことができない場合、またはユーザーのコンピューターで検証を無効にする必要がある場合などの問題が考えられます。 |
| CA2211 |[CA 2211:非定数フィールドを表示することはできません。](../code-quality/ca2211-non-constant-fields-should-not-be-visible.md) | 定数でも読み取り専用でもない静的フィールドは、スレッド セーフではありません。 このようなフィールドへのアクセスは、慎重に制御してください。また、クラス オブジェクトへのアクセスを同期するには、高度なプログラミング技術が必要です。 |
| CA2212 | [CA2212:サービス コンポーネントを webmethod に設定をマークしないでください。](../code-quality/ca2212-do-not-mark-serviced-components-with-webmethod.md) |System.EnterpriseServices.ServicedComponent から継承された型のメソッドが、System.Web.Services.WebMethodAttribute でマークされています。 WebMethodAttribute と ServicedComponent メソッドは、コンテキストおよびトランザクション フローの動作および要件が衝突するため、状況によっては正常に動作しません。 |
| CA2213 | [CA2213: 破棄可能なフィールドは破棄されなければなりません](../code-quality/ca2213-disposable-fields-should-be-disposed.md) | System.IDisposable を実装する型が、IDisposable も実装する型を持つフィールドを宣言しています。 このフィールドの Dispose メソッドは、宣言する型の Dispose メソッドから呼び出されていません。 |
| CA2214 | [CA 2214:コンス トラクターのオーバーライド可能なメソッドを呼び出しません](../code-quality/ca2214-do-not-call-overridable-methods-in-constructors.md) | コンストラクターから仮想メソッドを呼び出すと、メソッドを呼び出すインスタンスのコンストラクターが実行されないことがあります。 |
| CA2215 | [CA2215:Dispose メソッドが基底クラス dispose を呼び出す必要があります。](../code-quality/ca2215-dispose-methods-should-call-base-class-dispose.md) | 型が、破棄できる型から継承している場合、使用している Dispose メソッド内から基本型の Dispose メソッドを呼び出す必要があります。 |
| CA2216 |[CA 2216:破棄可能な型はファイナライザーを宣言する必要があります。](../code-quality/ca2216-disposable-types-should-declare-finalizer.md) | System.IDisposable を実装し、アンマネージ リソースの使用を提案するフィールドが含まれる型が、Object.Finalize で記述されているようにファイナライザーを実装していません。 |
| CA2217 | [CA2217:FlagsAttribute で列挙をマークしないでください。](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md) |外部から参照できる列挙型が FlagsAttribute でマークされ、その列挙型に、2 の累乗でもなく、その列挙型で定義されている他の値の組み合わせでもない値が 1 つ以上含まれています。 |
| CA2218 |[CA2218:Equals をオーバーライドの GetHashCode をオーバーライドします。](../code-quality/ca2218-override-gethashcode-on-overriding-equals.md) | GetHashCode は、現在のインスタンスに基づいて、ハッシュ アルゴリズムとデータ構造 (ハッシュ テーブルなど) に適した値を返します。 同じ型で等値の 2 つのオブジェクトによって同じハッシュ コードが返される必要があります。 |
| CA2219 | [CA2219:Exception 句に例外を発生させません](../code-quality/ca2219-do-not-raise-exceptions-in-exception-clauses.md) | finally 句または fault 句で例外が発生すると、アクティブな例外が新しい例外によって隠されます。 filter 句で例外が発生すると、ランタイムがその例外を暗黙的にキャッチします。 これにより、元のエラーの検出およびデバッグが困難になります。 |
| CA2220 | [CA 2220:ファイナライザーは基本クラスのファイナライザーを呼び出す必要があります。](../code-quality/ca2220-finalizers-should-call-base-class-finalizer.md) | 終了処理は、継承の階層構造を使用して反映する必要があります。 これを確実に行うには、型が型の Finalize メソッドで基本クラスの Finalize メソッドを呼び出す必要があります。 |
| CA2221 |[CA2221:ファイナライザーは保護する必要があります。](../code-quality/ca2221-finalizers-should-be-protected.md) | ファイナライザーは、ファミリ アクセス修飾子を使用する必要があります。 |
| CA2222 | [CA2222:継承されたメンバーの可視性を縮小しません](../code-quality/ca2222-do-not-decrease-inherited-member-visibility.md) |継承メンバーのアクセス修飾子は変更しないでください。 継承メンバーをプライベートに変更しても、呼び出し元はメソッドの基本クラスの実装にアクセスできます。 |
| CA2223 | [CA2223:メンバーが複数の戻り値の型が異なる必要があります。](../code-quality/ca2223-members-should-differ-by-more-than-return-type.md) | 共通言語ランタイムでは、戻り値の型以外は同じであるメンバーの区別に戻り値の型を使用することが許可されていますが、この機能は共通言語仕様ではなく、.NET プログラミング言語の共通機能でもありません。 |
| CA2224 | [CA2224:オーバー ロードする演算子 equals で equals をオーバーライド](../code-quality/ca2224-override-equals-on-overloading-operator-equals.md) | パブリック型で等値演算子が実装されていますが、Object.Equals がオーバーライドされていません。 |
| CA2225 | [CA2225:演算子のオーバー ロード名前付けされた代替](../code-quality/ca2225-operator-overloads-have-named-alternates.md) |演算子のオーバーロードが検出され、予想される名前の代替メソッドが検出されませんでした。 名前付きの代替メンバーによって、演算子と同じ機能へアクセスできるようになります。また、演算子のオーバーロードをサポートしていない言語でプログラミングする場合でも、その代替メンバーを使用できます。 |
| CA2226 | [CA2226:演算子は対称型オーバー ロードである必要があります。](../code-quality/ca2226-operators-should-have-symmetrical-overloads.md) | 型で等値演算子または非等値演算子を実装し、逆の働きをする演算子を実装していません。 |
| CA2227 |[CA2227:コレクションのプロパティは読み取り専用にします。](../code-quality/ca2227-collection-properties-should-be-read-only.md) |書き込み可能なコレクション プロパティにより、ユーザーはコレクションを異なるコレクションで置換できます。 読み取り専用プロパティは、コレクションを置換できないようにしますが、個別のメンバーが設定されることは回避できません。 |
| CA2228 | [CA2228:未公開のリソース形式を出荷しません](../code-quality/ca2228-do-not-ship-unreleased-resource-formats.md) | .NET Framework のプレリリース バージョンを使用してビルドされたリソース ファイルは、サポートされているバージョンの .NET Framework で使用できるしない場合があります。 |
| CA2229 | [CA2229: シリアル化コンストラクターを実装します](../code-quality/ca2229-implement-serialization-constructors.md) | この規則違反を修正するには、シリアル化コンストラクターを実装します。 シールされたクラスの場合、コンストラクターをプライベートにするか、プロテクトにします。 |
| CA2230 | [CA2230:可変個の引数に対して param を使用します。](../code-quality/ca2230-use-params-for-variable-arguments.md) | パブリック型またはプロテクト型に、params キーワードではなく VarArgs 呼び出し規則を使用するパブリック メソッドまたはプロテクト メソッドが含まれています。 |
| CA2231 | [CA2231: ValueType.Equals のオーバーライドで、演算子 equals をオーバーロードします](../code-quality/ca2231-overload-operator-equals-on-overriding-valuetype-equals.md) | 値型は、Object.Equals をオーバーライドしていますが、等値演算子を実装していません。 |
| CA2232 | [CA2232:Mark の Windows フォームのエントリ ポイントを stathread に設定します](../code-quality/ca2232-mark-windows-forms-entry-points-with-stathread.md) | STAThreadAttribute は、アプリケーションの COM スレッド処理モデルがシングルスレッド アパートメントであることを示します。 この属性は、Windows フォームを使用するすべてのアプリケーションのエントリ ポイントに指定する必要があります。省略すると、Windows コンポーネントが正常に機能しないことがあります。 |
| CA2233 |[CA2233:操作はオーバーフローできません。](../code-quality/ca2233-operations-should-not-overflow.md) | 算術演算を実行する前にオペランドを検証してください。 これにより、演算結果が関連するデータ型で使用できる値の範囲を超えないことを確認できます。 |
| CA2234 | [CA2234:文字列の代わりに System.Uri オブジェクトを渡します](../code-quality/ca2234-pass-system-uri-objects-instead-of-strings.md) | "uri"、"URI"、"urn"、"URN"、"url"、または "URL" という名前を持つ文字列パラメーターが指定されているメソッドに対して、呼び出しが行われました。 そのメソッドの型宣言に対応するメソッドのオーバーロードが存在し、それに対して System.Uri パラメーターが指定されています。 |
| CA2235 | [CA2235:すべてのシリアル化不可能なフィールドをマークします。](../code-quality/ca2235-mark-all-non-serializable-fields.md) | シリアル化できない型のインスタンス フィールドが、シリアル化できる型で宣言されています。 |
| CA2236 | [CA2236:ISerializable 型の基本クラス メソッドを呼び出す](../code-quality/ca2236-call-base-class-methods-on-iserializable-types.md) | この規則違反を修正するには、基本型の GetObjectData メソッドまたはシリアル化コンストラクターを、対応する派生型のメソッドまたはコンストラクターから呼び出します。 |
| CA2237 | [CA2237:ISerializable 型を serializableattribute に設定します](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md) | 型が共通言語ランタイムでシリアル化できると認識されるようにするには、型を SerializableAttribute 属性でマークする必要があります。型が ISerializable インターフェイスの実装を通じてカスタムのシリアル化ルーチンを使用している場合でも、マークする必要があります。 |
| CA2238 |[CA2238:シリアル化メソッドを正しく実装します。](../code-quality/ca2238-implement-serialization-methods-correctly.md) | シリアル化イベントを処理するメソッドに、適切なシグネチャ、戻り値の型、または参照範囲がありません。 |
| CA2239 | [CA2239:オプションのフィールドに逆シリアル化メソッドを提供します。](../code-quality/ca2239-provide-deserialization-methods-for-optional-fields.md) | 型に System.Runtime.Serialization.OptionalFieldAttribute 属性でマークされているフィールドがあり、その型に逆シリアル化のイベント処理メソッドがありません。 |
| CA2240 | [CA2240:ISerializable を正しく実装します。](../code-quality/ca2240-implement-iserializable-correctly.md) | この規則違反を修正するには、GetObjectData メソッドを外部から参照できるようにし、オーバーライドできるようにします。また、すべてのインスタンス フィールドをシリアル化プロセスに含めるか、NonSerializedAttribute 属性で明示的にマークします。 |
| CA2241 | [CA2241:書式指定メソッドに正しい引数を指定します。](../code-quality/ca2241-provide-correct-arguments-to-formatting-methods.md) | System.String.Format に渡される引数 format に、各オブジェクトの引数に対応する書式指定項目が含まれていません (その逆も考えられます)。 |
| CA2242 |[CA2242:NaN に対して正しくテストします](../code-quality/ca2242-test-for-nan-correctly.md) | この式が Single.Nan または Double.Nan に対して値をテストしています。 値をテストするには、Single.IsNan(Single) または Double.IsNan(Double) を使用します。 |
| CA2243 |[CA2243:属性文字列リテラルは、正しく解析する必要があります。](../code-quality/ca2243-attribute-string-literals-should-parse-correctly.md) | 属性のリテラル文字列パラメーターが URL、GUID、またはバージョンとして正しく解析されません。 |
| CA5122 | [CA5122 P/Invoke 宣言をセーフ クリティカルにしないでください](../code-quality/ca5122-p-invoke-declarations-should-not-be-safe-critical.md) | メソッドは、セキュリティに対する配慮が必要な操作を行うときは SecuritySafeCritical としてマークされますが、透過的なコードによって使用される場合も安全です。 透過的なコードは、P/Invoke を通じてネイティブ コードを直接呼び出すことはありません。 そのため、P/Invoke をセキュリティ セーフ クリティカルとしてマークしても、透過的なコードはそれを呼び出すことができず、セキュリティ分析の際に紛らわしくなります。 |