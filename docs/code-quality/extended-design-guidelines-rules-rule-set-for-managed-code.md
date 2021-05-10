---
title: マネージド コードの "拡張デザイン ガイドライン規則" 規則セット
ms.date: 11/04/2016
description: Visual Studio の "拡張デザイン ガイドライン規則" 規則セットについて説明します。これは、使いやすさと保守容易性に重点を置いています。 規則の説明を示します。
ms.custom: SEO-VS-2020
ms.topic: reference
ms.assetid: a338caf2-b75d-4f23-a0f9-3024fa0bceac
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 3555014113f84a5e21f21d1ab7d9a658e2c9aa6c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99860335"
---
# <a name="extended-design-guidelines-rules-rule-set-for-managed-code"></a>マネージド コードの "拡張デザイン ガイドライン規則" 規則セット

Microsoft "拡張デザイン ガイドライン規則" 規則セットは、基本デザイン ガイドライン規則を拡張して、使いやすさと保守容易性に関して報告される問題の検出範囲を最大化します。 特に、命名に関するガイドラインに重点が置かれています。 プロジェクトにライブラリ コードが含まれる場合や、最高レベルの基準を適用して、保守が容易なコードを記述する場合は、この規則セットの使用を検討してください。

拡張デザイン ガイドライン規則には、"[基本デザイン ガイドライン規則](../code-quality/basic-design-guideline-rules-rule-set-for-managed-code.md)" 規則セットのすべての規則が含まれます。この規則セットには、"[推奨されるマネージド規則](../code-quality/managed-recommended-rules-rule-set-for-managed-code.md)" 規則セットの規則が含まれます。

次の表では、Microsoft "拡張デザイン ガイドライン規則" 規則セットのすべての規則について説明します。

|ルール|説明|
|----------|-----------------|
|[CA1001](/dotnet/fundamentals/code-analysis/quality-rules/ca1001)|破棄可能なフィールドを所有する型は、破棄可能でなければなりません|
|[CA1009](../code-quality/ca1009.md)|イベント ハンドラーを正しく宣言します|
|[CA1016](/dotnet/fundamentals/code-analysis/quality-rules/ca1016)|アセンブリに AssemblyVersionAttribute を設定します|
|[CA1033](/dotnet/fundamentals/code-analysis/quality-rules/ca1033)|インターフェイス メソッドは、子型によって呼び出し可能でなければなりません|
|[CA1049](../code-quality/ca1049.md)|ネイティブ リソースを所有する型は、破棄可能でなければなりません|
|[CA1060](/dotnet/fundamentals/code-analysis/quality-rules/ca1060)|P/Invoke を NativeMethods クラスに移動します|
|[CA1061](/dotnet/fundamentals/code-analysis/quality-rules/ca1061)|基底クラス メソッドを非表示にしません|
|[CA1063](/dotnet/fundamentals/code-analysis/quality-rules/ca1063)|IDisposable を正しく実装します|
|[CA1065](/dotnet/fundamentals/code-analysis/quality-rules/ca1065)|予期しない場所に例外を発生させません|
|[CA1301](../code-quality/ca1301.md)|重複するアクセラレータを使用しません|
|[CA1400](../code-quality/ca1400.md)|P/Invoke エントリ ポイントは存在しなければなりません|
|[CA1401](/dotnet/fundamentals/code-analysis/quality-rules/ca1401)|P/Invoke は参照可能であることはできません|
|[CA1403](../code-quality/ca1403.md)|Auto 配置の型を COM 参照可能にすることはできません|
|[CA1404](../code-quality/ca1404.md)|P/Invoke の直後に GetLastError を呼び出します|
|[CA1405](../code-quality/ca1405.md)|COM 参照可能な型の基本型は COM 参照可能でなければなりません|
|[CA1410](../code-quality/ca1410.md)|COM 登録メソッドは一致しなければなりません|
|[CA1415](../code-quality/ca1415.md)|P/Invoke を正しく宣言します|
|[CA1821](/dotnet/fundamentals/code-analysis/quality-rules/ca1821)|空のファイナライザーを削除します|
|[CA1900](../code-quality/ca1900.md)|値型フィールドはポータブルでなければなりません|
|[CA1901](../code-quality/ca1901.md)|P/Invoke 宣言はポータブルでなければなりません|
|[CA2002](/dotnet/fundamentals/code-analysis/quality-rules/ca2002)|弱い ID を伴うオブジェクト上でロックしません|
|[CA2100](/dotnet/fundamentals/code-analysis/quality-rules/ca2100)|SQL クエリのセキュリティ脆弱性を確認|
|[CA2101](/dotnet/fundamentals/code-analysis/quality-rules/ca2101)|P/Invoke 文字列引数に対してマーシャリングを指定します|
|[CA2108](../code-quality/ca2108.md)|値型での宣言セキュリティを確認します|
|[CA2111](../code-quality/ca2111.md)|ポインターは参照可能にすることはできません|
|[CA2112](../code-quality/ca2112.md)|セキュリティで保護された型はフィールドを公開してはなりません|
|[CA2114](../code-quality/ca2114.md)|メソッド セキュリティは型のスーパーセットでなければなりません|
|[CA2116](../code-quality/ca2116.md)|APTCA メソッドは APTCA メソッドのみを呼び出すことができます|
|[CA2117](../code-quality/ca2117.md)|APTCA 型は APTCA 基本型のみを拡張することができます|
|[CA2122](../code-quality/ca2122.md)|リンク要求を含むメソッドを間接的に公開しません|
|[CA2123](../code-quality/ca2123.md)|オーバーライドのリンク要求はベースと同一でなければなりません|
|[CA2124](../code-quality/ca2124.md)|脆弱性のある finally 句を外側の try でラップします|
|[CA2126](../code-quality/ca2126.md)|型のリンク要求には継承要求が必要です|
|[CA2131](../code-quality/ca2131.md)|セキュリティ上重要な型は型等価性に参加してはならない|
|[CA2132](../code-quality/ca2132.md)|既定のコンストラクターは、基本型の既定コンストラクターと同程度以上、重要であることが必要|
|[CA2133](../code-quality/ca2133.md)|デリゲートは透過性の整合がとれたメソッドにバインドする必要がある|
|[CA2134](../code-quality/ca2134.md)|メソッドは、基本メソッドをオーバーライドしている場合、透過性の整合性を保つ必要がある|
|[CA2137](../code-quality/ca2137.md)|透過的メソッドは、検証可能な IL のみを含まなければならない|
|[CA2138](../code-quality/ca2138.md)|透過的メソッドは、SuppressUnmanagedCodeSecurity 属性を持つメソッドを呼び出してはならない|
|[CA2140](../code-quality/ca2140.md)|透過的コードは、セキュリティ上重要な項目を参照してはならない|
|[CA2141](../code-quality/ca2141.md)|透過的メソッドは LinkDemand を満たしてはならない|
|[CA2146](../code-quality/ca2146.md)|型は、基本型およびインターフェイスと同程度以上、重要でなければならない|
|[CA2147](../code-quality/ca2147.md)|透過コードは、セキュリティ アサートを使用してはならない|
|[CA2149](../code-quality/ca2149.md)|透過的メソッドは、ネイティブ コード内に呼び出しを行ってはならない|
|[CA2200](/dotnet/fundamentals/code-analysis/quality-rules/ca2200)|スタック詳細を保持するために再度スローします|
|[CA2202](../code-quality/ca2202.md)|オブジェクトを複数回破棄しない|
|[CA2207](/dotnet/fundamentals/code-analysis/quality-rules/ca2207)|値型のスタティック フィールドのインラインを初期化します|
|[CA2212](../code-quality/ca2212.md)|サービス コンポーネントを WebMethod に設定しません|
|[CA2213](/dotnet/fundamentals/code-analysis/quality-rules/ca2213)|破棄可能なフィールドは破棄されなければなりません|
|[CA2214](/dotnet/fundamentals/code-analysis/quality-rules/ca2214)|コンストラクターのオーバーライド可能なメソッドを呼び出しません|
|[CA2216](/dotnet/fundamentals/code-analysis/quality-rules/ca2216)|破棄可能な型はファイナライザーを宣言しなければなりません|
|[CA2220](../code-quality/ca2220.md)|ファイナライザーは基底クラスのファイナライザーを呼び出さなければなりません|
|[CA2229](/dotnet/fundamentals/code-analysis/quality-rules/ca2229)|シリアル化コンストラクターを実装します|
|[CA2231](/dotnet/fundamentals/code-analysis/quality-rules/ca2231)|ValueType.Equals のオーバーライドで、演算子 equals をオーバーロードします|
|[CA2232](../code-quality/ca2232.md)|Windows フォームのエントリ ポイントを STAThread に設定します|
|[CA2235](/dotnet/fundamentals/code-analysis/quality-rules/ca2235)|すべてのシリアル化不可能なフィールドを設定します|
|[CA2236](../code-quality/ca2236.md)|ISerializable 型で基底クラス メソッドを呼び出します|
|[CA2237](/dotnet/fundamentals/code-analysis/quality-rules/ca2237)|ISerializable 型を SerializableAttribute に設定します|
|[CA2238](../code-quality/ca2238.md)|シリアル化メソッドを正しく実装します|
|[CA2240](../code-quality/ca2240.md)|ISerializable を正しく実装します|
|[CA2241](/dotnet/fundamentals/code-analysis/quality-rules/ca2241)|書式設定メソッドに正しい引数を提供|
|[CA2242](/dotnet/fundamentals/code-analysis/quality-rules/ca2242)|NaN に対して正しくテストします|
|[CA1000](/dotnet/fundamentals/code-analysis/quality-rules/ca1000)|ジェネリック型の静的メンバーを宣言しません|
|[CA1002](/dotnet/fundamentals/code-analysis/quality-rules/ca1002)|ジェネリック リストを公開しません|
|[CA1003](/dotnet/fundamentals/code-analysis/quality-rules/ca1003)|汎用イベント ハンドラーのインスタンスを使用します|
|[CA1004](../code-quality/ca1004.md)|ジェネリック メソッドは型パラメーターを指定しなければなりません|
|[CA1005](/dotnet/fundamentals/code-analysis/quality-rules/ca1005)|ジェネリック型でパラメーターを使用しすぎないでください|
|[CA1006](../code-quality/ca1006.md)|ジェネリック型をメンバー シグネチャ内で入れ子にしません|
|[CA1007](../code-quality/ca1007.md)|適切な場所にジェネリックを使用します|
|[CA1008](/dotnet/fundamentals/code-analysis/quality-rules/ca1008)|Enums は 0 値を含んでいなければなりません|
|[CA1010](/dotnet/fundamentals/code-analysis/quality-rules/ca1010)|コレクションは、ジェネリック インターフェイスを実装しなければなりません|
|[CA1011](../code-quality/ca1011.md)|基本型をパラメーターとして渡すことを考慮します|
|[CA1012](/dotnet/fundamentals/code-analysis/quality-rules/ca1012)|抽象型にはコンストラクターを含めません|
|[CA1013](../code-quality/ca1013.md)|オーバーロードする加算および減算で、演算子 equals をオーバーロードします|
|[CA1014](/dotnet/fundamentals/code-analysis/quality-rules/ca1014)|アセンブリに CLSCompliantAttribute を設定します|
|[CA1017](/dotnet/fundamentals/code-analysis/quality-rules/ca1017)|アセンブリに ComVisibleAttribute を設定します|
|[CA1018](/dotnet/fundamentals/code-analysis/quality-rules/ca1018)|属性を AttributeUsageAttribute に設定します|
|[CA1019](/dotnet/fundamentals/code-analysis/quality-rules/ca1019)|属性引数にアクセサーを定義します|
|[CA1023](../code-quality/ca1023.md)|インデクサーを多次元にすることはできません|
|[CA1024](/dotnet/fundamentals/code-analysis/quality-rules/ca1024)|適切な場所にプロパティを使用します|
|[CA1025](../code-quality/ca1025.md)|反復する引数を params 配列で置き換えます|
|[CA1026](../code-quality/ca1026.md)|既定パラメーターを使用することはできません|
|[CA1027](/dotnet/fundamentals/code-analysis/quality-rules/ca1027)|列挙型を FlagsAttribute に設定します|
|[CA1028](/dotnet/fundamentals/code-analysis/quality-rules/ca1028)|列挙ストレージは Int32 でなければなりません|
|[CA1030](/dotnet/fundamentals/code-analysis/quality-rules/ca1030)|適切な場所にイベントを使用します|
|[CA1031](/dotnet/fundamentals/code-analysis/quality-rules/ca1031)|一般的な例外の種類はキャッチしません|
|[CA1032](/dotnet/fundamentals/code-analysis/quality-rules/ca1032)|標準例外コンストラクターを実装します|
|[CA1034](/dotnet/fundamentals/code-analysis/quality-rules/ca1034)|入れ子にされた型を参照可能にすることはできません|
|[CA1035](../code-quality/ca1035.md)|ICollection の実装は、厳密に型指定されたメンバーを含んでいます|
|[CA1036](/dotnet/fundamentals/code-analysis/quality-rules/ca1036)|比較可能な型でメソッドをオーバーライドします|
|[CA1038](../code-quality/ca1038.md)|列挙子は厳密に型指定されていなければなりません|
|[CA1039](../code-quality/ca1039.md)|リストは厳密に型指定されています|
|[CA1041](/dotnet/fundamentals/code-analysis/quality-rules/ca1041)|ObsoleteAttribute メッセージを指定します|
|[CA1043](/dotnet/fundamentals/code-analysis/quality-rules/ca1043)|インデクサーには整数または文字列引数を使用します|
|[CA1044](/dotnet/fundamentals/code-analysis/quality-rules/ca1044)|プロパティを書き込み専用にすることはできません|
|[CA1046](/dotnet/fundamentals/code-analysis/quality-rules/ca1046)|参照型で、演算子 equals をオーバーロードしないでください|
|[CA1047](/dotnet/fundamentals/code-analysis/quality-rules/ca1047)|シールド型の保護されたメンバーを宣言しません|
|[CA1048](../code-quality/ca1048.md)|シールド型の仮想メンバーを宣言しません|
|[CA1050](/dotnet/fundamentals/code-analysis/quality-rules/ca1050)|名前空間で型を宣言します|
|[CA1051](/dotnet/fundamentals/code-analysis/quality-rules/ca1051)|参照可能なインスタンス フィールドを宣言しません|
|[CA1052](/dotnet/fundamentals/code-analysis/quality-rules/ca1052)|スタティック ホルダー型はシールドされていなければなりません|
|[CA1053](/dotnet/fundamentals/code-analysis/quality-rules/ca1053)|スタティック ホルダー型はコンストラクターを含むことはできません|
|[CA1054](/dotnet/fundamentals/code-analysis/quality-rules/ca1054)|URI パラメーターを文字列にすることはできません|
|[CA1055](/dotnet/fundamentals/code-analysis/quality-rules/ca1055)|URI 戻り値を文字列にすることはできません|
|[CA1056](/dotnet/fundamentals/code-analysis/quality-rules/ca1056)|URI プロパティを文字列にすることはできません|
|[CA1057](../code-quality/ca1057.md)|文字列 URI オーバーロードが、System.Uri オーバーロードを呼び出します|
|[CA1058](/dotnet/fundamentals/code-analysis/quality-rules/ca1058)|型は、一定の基本型を拡張することはできません|
|[CA1059](../code-quality/ca1059.md)|メンバーは特定の具象型を公開できません|
|[CA1064](/dotnet/fundamentals/code-analysis/quality-rules/ca1064)|例外は public として設定する必要があります|
|[CA1500](../code-quality/ca1500.md)|変数名はフィールド名と同一にすることはできません|
|[CA1502](/dotnet/fundamentals/code-analysis/quality-rules/ca1502)|メソッドの実装を複雑にしすぎないでください|
|[CA1708](/dotnet/fundamentals/code-analysis/quality-rules/ca1708)|識別子は、大文字と小文字の区別以外にも相違していなければなりません|
|[CA1716](/dotnet/fundamentals/code-analysis/quality-rules/ca1716)|識別子はキーワードと同一にすることはできません|
|[CA1801](/dotnet/fundamentals/code-analysis/quality-rules/ca1801)|使用されていないパラメーターの確認|
|[CA1804](../code-quality/ca1804.md)|使用されていないローカルを削除します|
|[CA1809](../code-quality/ca1809.md)|ローカルを使用しすぎないでください|
|[CA1810](/dotnet/fundamentals/code-analysis/quality-rules/ca1810)|参照型の静的フィールドをインラインで初期化します|
|[CA1811](../code-quality/ca1811.md)|呼び出されていないプライベート コードを使用しません|
|[CA1812](/dotnet/fundamentals/code-analysis/quality-rules/ca1812)|インスタンス化されていない内部クラスを使用しません|
|[CA1813](/dotnet/fundamentals/code-analysis/quality-rules/ca1813)|アンシールド属性を使用しません|
|[CA1814](/dotnet/fundamentals/code-analysis/quality-rules/ca1814)|複数次元の配列ではなくジャグ配列を使用します|
|[CA1815](/dotnet/fundamentals/code-analysis/quality-rules/ca1815)|equals および operator equals を値型でオーバーライドします|
|[CA1819](/dotnet/fundamentals/code-analysis/quality-rules/ca1819)|プロパティは、配列を返すことはできません|
|[CA1820](/dotnet/fundamentals/code-analysis/quality-rules/ca1820)|文字列の長さを使用して空の文字列をテストします|
|[CA1822](/dotnet/fundamentals/code-analysis/quality-rules/ca1822)|メンバーを static に設定します|
|[CA1823](/dotnet/fundamentals/code-analysis/quality-rules/ca1823)|使用されていないプライベート フィールドを使用しません|
|[CA2201](/dotnet/fundamentals/code-analysis/quality-rules/ca2201)|予約された例外の種類を発生させません|
|[CA2205](../code-quality/ca2205.md)|Win32 API に相当するマネージド API を使用します|
|[CA2208](/dotnet/fundamentals/code-analysis/quality-rules/ca2208)|引数の例外を正しくインスタンス化します|
|[CA2211](/dotnet/fundamentals/code-analysis/quality-rules/ca2211)|非定数フィールドは表示されません|
|[CA2217](/dotnet/fundamentals/code-analysis/quality-rules/ca2217)|列挙型を FlagsAttribute に設定しません|
|[CA2219](/dotnet/fundamentals/code-analysis/quality-rules/ca2219)|exception 句に例外を発生させないでください|
|[CA2221](../code-quality/ca2221.md)|ファイナライザーは保護されなければなりません|
|[CA2222](../code-quality/ca2222.md)|継承されたメンバーの参照範囲を縮小しません|
|[CA2223](../code-quality/ca2223.md)|メンバーは、戻り値の型以外にも異なる点がなければなりません|
|[CA2224](../code-quality/ca2224.md)|オーバーロードする演算子 equals で Equals をオーバーライドします|
|[CA2225](/dotnet/fundamentals/code-analysis/quality-rules/ca2225)|演算子オーバーロードには名前付けされた代替が存在します|
|[CA2226](/dotnet/fundamentals/code-analysis/quality-rules/ca2226)|演算子は対称型オーバーロードを含まなければなりません|
|[CA2227](/dotnet/fundamentals/code-analysis/quality-rules/ca2227)|Collection プロパティは読み取り専用でなければなりません|
|[CA2230](../code-quality/ca2230.md)|可変引数に対して param を使用します|
|[CA2234](/dotnet/fundamentals/code-analysis/quality-rules/ca2234)|文字列の代わりに System.Uri オブジェクトを渡します|
|[CA2239](../code-quality/ca2239.md)|省略可能なフィールドに、逆シリアル化メソッドを指定します|
|[CA1020](../code-quality/ca1020.md)|型をほとんど含まない名前空間を使用しません|
|[CA1021](/dotnet/fundamentals/code-analysis/quality-rules/ca1021)|out パラメーターを使用しません|
|[CA1040](/dotnet/fundamentals/code-analysis/quality-rules/ca1040)|空のインターフェイスは使用しません|
|[CA1045](/dotnet/fundamentals/code-analysis/quality-rules/ca1045)|型を参照によって渡しません|
|[CA1062](/dotnet/fundamentals/code-analysis/quality-rules/ca1062)|パブリック メソッドの引数の検証|
|[CA1501](/dotnet/fundamentals/code-analysis/quality-rules/ca1501)|継承を使用しすぎないでください|
|[CA1504](../code-quality/ca1504.md)|紛らわしいフィールド名を確認します|
|[CA1505](/dotnet/fundamentals/code-analysis/quality-rules/ca1505)|メンテナンスできないコードを使用しないでください|
|[CA1506](/dotnet/fundamentals/code-analysis/quality-rules/ca1506)|クラス結合度を大きくしすぎないでください|
|[CA1700](/dotnet/fundamentals/code-analysis/quality-rules/ca1700)|列挙型値に 'Reserved' という名前を指定しません|
|[CA1701](../code-quality/ca1701.md)|リソース文字列の複合語は、大文字と小文字を正しく区別しなければなりません|
|[CA1702](../code-quality/ca1702.md)|複合語では、大文字と小文字が正しく区別されなければなりません|
|[CA1703](../code-quality/ca1703.md)|リソース文字列は正しく入力されなければなりません|
|[CA1704](../code-quality/ca1704.md)|識別子は正しく入力されなければなりません|
|[CA1707](/dotnet/fundamentals/code-analysis/quality-rules/ca1707)|識別子はアンダースコアを含むことはできません|
|[CA1709](../code-quality/ca1709.md)|識別子では、大文字と小文字が正しく区別されなければなりません|
|[CA1710](/dotnet/fundamentals/code-analysis/quality-rules/ca1710)|識別子は、正しいサフィックスを含んでいなければなりません|
|[CA1711](/dotnet/fundamentals/code-analysis/quality-rules/ca1711)|識別子は、不適切なサフィックスを含むことはできません|
|[CA1712](/dotnet/fundamentals/code-analysis/quality-rules/ca1712)|列挙型値を型名のプレフィックスにしません|
|[CA1713](/dotnet/fundamentals/code-analysis/quality-rules/ca1713)|イベントは、before または after プレフィックスを含むことはできません|
|[CA1714](/dotnet/fundamentals/code-analysis/quality-rules/ca1714)|フラグ列挙型は、複数形の名前を含んでいなければなりません|
|[CA1715](/dotnet/fundamentals/code-analysis/quality-rules/ca1715)|識別子は正しいプレフィックスを含んでいなければなりません|
|[CA1717](/dotnet/fundamentals/code-analysis/quality-rules/ca1717)|FlagsAttribute 列挙型のみが複数形の名前を含んでいなければなりません|
|[CA1719](../code-quality/ca1719.md)|パラメーター名はメンバー名と同一にすることはできません|
|[CA1720](/dotnet/fundamentals/code-analysis/quality-rules/ca1720)|識別子には型名を含めないでください|
|[CA1721](/dotnet/fundamentals/code-analysis/quality-rules/ca1721)|プロパティ名は get メソッドと同一にすることはできません|
|[CA1722](../code-quality/ca1722.md)|識別子は不適切なプレフィックスを含むことはできません|
|[CA1724](/dotnet/fundamentals/code-analysis/quality-rules/ca1724)|型名は名前空間と同一にすることはできません|
|[CA1725](/dotnet/fundamentals/code-analysis/quality-rules/ca1725)|パラメーター名は基本宣言と同一でなければなりません|
|[CA1726](../code-quality/ca1726.md)|適切な用語を使用します|
|[CA2204](../code-quality/ca2204.md)|リテラルに正しいスペルを要求|
