---
title: FxCop 規則のポートの状態
ms.date: 05/21/2019
description: Visual Studio で .NET analyzer に移植された静的コード分析規則について説明します。 移植された更新プログラムに関する移植されたルールとリソースを表示します。
ms.custom: SEO-VS-2020
ms.topic: reference
helpviewer_keywords:
- fxcop rules
- .NET analyzers, ported rules
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: dde5a3d8ccf5557905395ee03d108e995ecffe7e
ms.sourcegitcommit: 967c2f8c1b3f805cf42c0246389517689d971b53
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96039576"
---
# <a name="fxcop-rule-port-status"></a>Fxcop 規則のポートの状態

以前に Visual Studio で静的コード分析を使用していた場合は、現在の実装で [.net アナライザー](install-net-analyzers.md)として使用できる規則を確認できます。 このページには、移植されたルールの一覧が表示されます。 移植されていないルール、およびそれらに移植する計画があるかどうかについては、「 [unported 規則](fxcop-unported-rules.md) 」を参照してください。

## <a name="ported-rules"></a>移植された規則

Roslyn アナライザーリポジトリの自動生成された [ドキュメントページ](https://github.com/dotnet/roslyn-analyzers/blob/master/src/NetAnalyzers/Microsoft.CodeAnalysis.NetAnalyzers.md) には、roslyn アナライザーに移植されたルールの最新の一覧が含まれています。 このページには、規則が既定で有効になっているかどうかや、関連付けられている *コード修正プログラム* があるかどうかなどの追加情報も含まれています。 ([コード修正](../ide/quick-actions.md) は、Visual Studio の電球アイコンメニューで使用できるワンクリック修正です)。

このページの日付のとき、 [.net アナライザー](install-net-analyzers.md) に移植された FxCop 規則の一覧には次のものが含まれます。

ルールの ID | タイトル
--------|---------
[CA1000](/dotnet/fundamentals/code-analysis/quality-rules/ca1000) | ジェネリック型の静的メンバーを宣言しません
[CA1001](/dotnet/fundamentals/code-analysis/quality-rules/ca1001) | 破棄可能なフィールドを所有する型は、破棄可能でなければなりません
[CA1002](/dotnet/fundamentals/code-analysis/quality-rules/ca1002) | ジェネリック リストを公開しません
[CA1003](/dotnet/fundamentals/code-analysis/quality-rules/ca1003) | 汎用イベント ハンドラーのインスタンスを使用します
[CA1005](/dotnet/fundamentals/code-analysis/quality-rules/ca1005) | ジェネリック型でパラメーターを使用しすぎないでください
[CA1008](/dotnet/fundamentals/code-analysis/quality-rules/ca1008) | Enums は 0 値を含んでいなければなりません
[CA1010](/dotnet/fundamentals/code-analysis/quality-rules/ca1010) | コレクションは、ジェネリック インターフェイスを実装しなければなりません
[CA1012](/dotnet/fundamentals/code-analysis/quality-rules/ca1012) | 抽象型にはコンストラクターを含めません
[CA1014](/dotnet/fundamentals/code-analysis/quality-rules/ca1014) | アセンブリを CLSCompliant にマークします
[CA1016](/dotnet/fundamentals/code-analysis/quality-rules/ca1016) | アセンブリのバージョンをアセンブリにマークする
[CA1017](/dotnet/fundamentals/code-analysis/quality-rules/ca1017) | アセンブリに ComVisible を設定します
[CA1018](/dotnet/fundamentals/code-analysis/quality-rules/ca1018) | 属性を AttributeUsageAttribute に設定します
[CA1019](/dotnet/fundamentals/code-analysis/quality-rules/ca1019) | 属性引数にアクセサーを定義します
[CA1021](/dotnet/fundamentals/code-analysis/quality-rules/ca1021) | out パラメーターを使用しません
[CA1024](/dotnet/fundamentals/code-analysis/quality-rules/ca1024) | 適切な場所にプロパティを使用します
[CA1027](/dotnet/fundamentals/code-analysis/quality-rules/ca1027) | 列挙型を FlagsAttribute に設定します
[CA1028](/dotnet/fundamentals/code-analysis/quality-rules/ca1028) | 列挙ストレージは Int32 でなければなりません
[CA1030](/dotnet/fundamentals/code-analysis/quality-rules/ca1030) | 適切な場所にイベントを使用します
[CA1031](/dotnet/fundamentals/code-analysis/quality-rules/ca1031) | 一般的な例外の種類はキャッチしません
[CA1032](/dotnet/fundamentals/code-analysis/quality-rules/ca1032) | 標準例外コンストラクターを実装します
[CA1033](/dotnet/fundamentals/code-analysis/quality-rules/ca1033) | インターフェイス メソッドは、子型によって呼び出し可能でなければなりません
[CA1034](/dotnet/fundamentals/code-analysis/quality-rules/ca1034) | 入れ子にされた型を参照可能にすることはできません
[CA1036](/dotnet/fundamentals/code-analysis/quality-rules/ca1036) | 比較可能な型でメソッドをオーバーライドします
[CA1040](/dotnet/fundamentals/code-analysis/quality-rules/ca1040) | 空のインターフェイスは使用しません
[CA1041](/dotnet/fundamentals/code-analysis/quality-rules/ca1041) | ObsoleteAttribute メッセージを指定します
[CA1043](/dotnet/fundamentals/code-analysis/quality-rules/ca1043) | インデクサーに整数または文字列引数を使用する
[CA1044](/dotnet/fundamentals/code-analysis/quality-rules/ca1044) | プロパティを書き込み専用にすることはできません
[CA1045](/dotnet/fundamentals/code-analysis/quality-rules/ca1045) | 型を参照によって渡しません
[CA1046](/dotnet/fundamentals/code-analysis/quality-rules/ca1046) | 参照型で、演算子 equals をオーバーロードしないでください
[CA1047](/dotnet/fundamentals/code-analysis/quality-rules/ca1047) | シールド型の保護されたメンバーを宣言しません
[CA1050](/dotnet/fundamentals/code-analysis/quality-rules/ca1050) | 名前空間で型を宣言します
[CA1051](/dotnet/fundamentals/code-analysis/quality-rules/ca1051) | 参照可能なインスタンス フィールドを宣言しません
[CA1052](/dotnet/fundamentals/code-analysis/quality-rules/ca1052) | 静的ホルダー型は static または NotInheritable である必要があります
[CA1053](/dotnet/fundamentals/code-analysis/quality-rules/ca1053) | 静的ホルダー型にコンストラクターを含めることはできません (CA1053 は .NET アナライザーの [CA1052](/dotnet/fundamentals/code-analysis/quality-rules/ca1052) の一部です)
[CA1054](/dotnet/fundamentals/code-analysis/quality-rules/ca1054) | Uri パラメーターを文字列にすることはできません
[CA1055](/dotnet/fundamentals/code-analysis/quality-rules/ca1055) | Uri 戻り値を文字列にすることはできません
[CA1056](/dotnet/fundamentals/code-analysis/quality-rules/ca1056) | Uri プロパティを文字列にすることはできません
[CA1058](/dotnet/fundamentals/code-analysis/quality-rules/ca1058) | 型は、一定の基本型を拡張することはできません
[CA1060](/dotnet/fundamentals/code-analysis/quality-rules/ca1060) | Pinvokes をネイティブメソッドクラスに移動する
[CA1061](/dotnet/fundamentals/code-analysis/quality-rules/ca1061) | 基底クラス メソッドを非表示にしません
[CA1062](/dotnet/fundamentals/code-analysis/quality-rules/ca1062) | パブリック メソッドの引数の検証
[CA1063](/dotnet/fundamentals/code-analysis/quality-rules/ca1063) | IDisposable を正しく実装する
[CA1064](/dotnet/fundamentals/code-analysis/quality-rules/ca1064) | 例外は public として設定する必要があります
[CA1065](/dotnet/fundamentals/code-analysis/quality-rules/ca1065) | 予期しない場所に例外を発生させません
[CA1066](/dotnet/fundamentals/code-analysis/quality-rules/ca1066) | Type {0} は Equals をオーバーライドするため、IEquatable を実装しなければなりませ \<T> ん
[CA1067](/dotnet/fundamentals/code-analysis/quality-rules/ca1067) | IEquatable を実装するときに、Object.equals (object) をオーバーライドします。\<T>
[CA1303](/dotnet/fundamentals/code-analysis/quality-rules/ca1303) | ローカライズされるパラメーターとしてリテラルを渡さない
[CA1304](/dotnet/fundamentals/code-analysis/quality-rules/ca1304) | CultureInfo を指定します
[CA1305](/dotnet/fundamentals/code-analysis/quality-rules/ca1305) | IFormatProvider を指定します
[CA1307](/dotnet/fundamentals/code-analysis/quality-rules/ca1307) | 意味を明確にするための StringComparison の指定
[CA1308](/dotnet/fundamentals/code-analysis/quality-rules/ca1308) | 文字列を大文字に標準化します
[CA1309](/dotnet/fundamentals/code-analysis/quality-rules/ca1309) | 序数の文字列比較を使用する
[CA1401](/dotnet/fundamentals/code-analysis/quality-rules/ca1401) | P/Invoke は参照可能であることはできません
[CA1501](/dotnet/fundamentals/code-analysis/quality-rules/ca1501) | 継承を使用しすぎないでください
[CA1502](/dotnet/fundamentals/code-analysis/quality-rules/ca1502) | メソッドの実装を複雑にしすぎないでください
[CA1505](/dotnet/fundamentals/code-analysis/quality-rules/ca1505) | メンテナンスできないコードを使用しないでください
[CA1506](/dotnet/fundamentals/code-analysis/quality-rules/ca1506) | クラス結合度を大きくしすぎないでください
[CA1700](/dotnet/fundamentals/code-analysis/quality-rules/ca1700) | 列挙型値に 'Reserved' という名前を指定しません
[CA1707](/dotnet/fundamentals/code-analysis/quality-rules/ca1707) | 識別子はアンダースコアを含むことはできません
[CA1708](/dotnet/fundamentals/code-analysis/quality-rules/ca1708) | 識別子は、大文字と小文字の区別以外にも相違していなければなりません
[CA1710](/dotnet/fundamentals/code-analysis/quality-rules/ca1710) | 識別子は、正しいサフィックスを含んでいなければなりません
[CA1711](/dotnet/fundamentals/code-analysis/quality-rules/ca1711) | 識別子は、不適切なサフィックスを含むことはできません
[CA1712](/dotnet/fundamentals/code-analysis/quality-rules/ca1712) | 列挙型値を型名のプレフィックスにしません
[CA1713](/dotnet/fundamentals/code-analysis/quality-rules/ca1713) | イベントは、before または after プレフィックスを含むことはできません
[CA1714](/dotnet/fundamentals/code-analysis/quality-rules/ca1714) | フラグ列挙型は、複数形の名前を含んでいなければなりません
[CA1715](/dotnet/fundamentals/code-analysis/quality-rules/ca1715) | 識別子は正しいプレフィックスを含んでいなければなりません
[CA1716](/dotnet/fundamentals/code-analysis/quality-rules/ca1716) | 識別子はキーワードと同一にすることはできません
[CA1717](/dotnet/fundamentals/code-analysis/quality-rules/ca1717) | FlagsAttribute 列挙型のみが複数形の名前を含んでいなければなりません
[CA1720](/dotnet/fundamentals/code-analysis/quality-rules/ca1720) | 識別子に型名が含まれています
[CA1721](/dotnet/fundamentals/code-analysis/quality-rules/ca1721) | プロパティ名は get メソッドと同一にすることはできません
[CA1724](/dotnet/fundamentals/code-analysis/quality-rules/ca1724) | 型名を名前空間と一致させることはできません
[CA1725](/dotnet/fundamentals/code-analysis/quality-rules/ca1725) | パラメーター名は基本宣言と同一でなければなりません
[CA1801](/dotnet/fundamentals/code-analysis/quality-rules/ca1801) | 使用されていないパラメーターの確認
[CA1802](/dotnet/fundamentals/code-analysis/quality-rules/ca1802) | 適切な場所にリテラルを使用する
[CA1805](/dotnet/fundamentals/code-analysis/quality-rules/ca1805) | 不必要に初期化しない
[CA1806](/dotnet/fundamentals/code-analysis/quality-rules/ca1806) | メソッドの結果を無視しない
[CA1810](/dotnet/fundamentals/code-analysis/quality-rules/ca1810) | 参照型の静的フィールドをインラインで初期化します
[CA1812](/dotnet/fundamentals/code-analysis/quality-rules/ca1812) | インスタンス化されていない内部クラスを使用しません
[CA1813](/dotnet/fundamentals/code-analysis/quality-rules/ca1813) | アンシールド属性を使用しません
[CA1814](/dotnet/fundamentals/code-analysis/quality-rules/ca1814) | 複数次元の配列ではなくジャグ配列を使用します
[CA1815](/dotnet/fundamentals/code-analysis/quality-rules/ca1815) | equals および operator equals を値型でオーバーライドします
[CA1816](/dotnet/fundamentals/code-analysis/quality-rules/ca1816) | Dispose メソッドは Gc.suppressfinalize を呼び出す必要があります
[CA1819](/dotnet/fundamentals/code-analysis/quality-rules/ca1819) | プロパティは、配列を返すことはできません
[CA1820](/dotnet/fundamentals/code-analysis/quality-rules/ca1820) | 文字列の長さを使用して空の文字列をテストします
[CA1821](/dotnet/fundamentals/code-analysis/quality-rules/ca1821) | 空のファイナライザーの削除
[CA1822](/dotnet/fundamentals/code-analysis/quality-rules/ca1822) | メンバーを static に設定します
[CA1823](/dotnet/fundamentals/code-analysis/quality-rules/ca1823) | 使用されていないプライベート フィールドを使用しません
[CA1824](/dotnet/fundamentals/code-analysis/quality-rules/ca1824) | アセンブリを NeutralResourcesLanguageAttribute に設定します
[CA1825](/dotnet/fundamentals/code-analysis/quality-rules/ca1825) | 長さ0の配列を割り当てないようにします。
[CA2000](/dotnet/fundamentals/code-analysis/quality-rules/ca2000) | スコープを失う前にオブジェクトを破棄
[CA2002](/dotnet/fundamentals/code-analysis/quality-rules/ca2002) | 弱い ID を伴うオブジェクト上でロックしません
[CA2100](/dotnet/fundamentals/code-analysis/quality-rules/ca2100) | SQL クエリのセキュリティ脆弱性を確認
[CA2101](/dotnet/fundamentals/code-analysis/quality-rules/ca2101) | P/Invoke 文字列引数に対してマーシャリングを指定します
[CA2109](/dotnet/fundamentals/code-analysis/quality-rules/ca2109) | 表示するイベント ハンドラーを確認します
[CA2119](/dotnet/fundamentals/code-analysis/quality-rules/ca2119) | プライベート インターフェイスを満たすメソッドをシールします
[CA2153](/dotnet/fundamentals/code-analysis/quality-rules/ca2153) | 破損状態の例外をキャッチしない
[CA2200](/dotnet/fundamentals/code-analysis/quality-rules/ca2200) | スタックの詳細を保持するために再スローします。
[CA2201](/dotnet/fundamentals/code-analysis/quality-rules/ca2201) | 予約された例外の種類を発生させません
[CA2207](/dotnet/fundamentals/code-analysis/quality-rules/ca2207) | 値型のスタティック フィールドのインラインを初期化します
[CA2208](/dotnet/fundamentals/code-analysis/quality-rules/ca2208) | 引数の例外を正しくインスタンス化します
[CA2211](/dotnet/fundamentals/code-analysis/quality-rules/ca2211) | 非定数フィールドは表示されません
[CA2213](/dotnet/fundamentals/code-analysis/quality-rules/ca2213) | 破棄可能なフィールドは破棄されなければなりません
[CA2214](/dotnet/fundamentals/code-analysis/quality-rules/ca2214) | コンストラクターのオーバーライド可能なメソッドを呼び出しません
[CA2215](/dotnet/fundamentals/code-analysis/quality-rules/ca2215) | Dispose メソッドが基底クラスの Dispose を呼び出す必要があります
[CA2216](/dotnet/fundamentals/code-analysis/quality-rules/ca2216) | 破棄可能な型はファイナライザーを宣言しなければなりません
[CA2217](/dotnet/fundamentals/code-analysis/quality-rules/ca2217) | 列挙型を FlagsAttribute に設定しません
[CA2219](/dotnet/fundamentals/code-analysis/quality-rules/ca2219) | Finally 句で例外を発生させない
[CA2225](/dotnet/fundamentals/code-analysis/quality-rules/ca2225) | 演算子オーバーロードには名前付けされた代替が存在します
[CA2226](/dotnet/fundamentals/code-analysis/quality-rules/ca2226) | 演算子は対称型オーバーロードを含まなければなりません
[CA2227](/dotnet/fundamentals/code-analysis/quality-rules/ca2227) | Collection プロパティは読み取り専用でなければなりません
[CA2229](/dotnet/fundamentals/code-analysis/quality-rules/ca2229) | シリアル化コンストラクターを実装します
[CA2231](/dotnet/fundamentals/code-analysis/quality-rules/ca2231) | 値型 Equals のオーバーライドで、演算子 equals をオーバーロードします
[CA2234](/dotnet/fundamentals/code-analysis/quality-rules/ca2234) | 文字列ではなくシステム uri オブジェクトを渡す
[CA2235](/dotnet/fundamentals/code-analysis/quality-rules/ca2235) | すべてのシリアル化不可能なフィールドを設定します
[CA2237](/dotnet/fundamentals/code-analysis/quality-rules/ca2237) | ISerializable 型を Serializable に設定します
[CA2241](/dotnet/fundamentals/code-analysis/quality-rules/ca2241) | 書式設定メソッドに正しい引数を提供
[CA2242](/dotnet/fundamentals/code-analysis/quality-rules/ca2242) | NaN に対して正しくテストします
[CA2243](/dotnet/fundamentals/code-analysis/quality-rules/ca2243) | 属性文字列リテラルは、正しく解析する必要があります
[CA2300](/dotnet/fundamentals/code-analysis/quality-rules/ca2300) | 安全ではないデシリアライザー BinaryFormatter を使用しないでください
[CA2301](/dotnet/fundamentals/code-analysis/quality-rules/ca2301) | 最初に BinaryFormatter.Binder を設定しないで BinaryFormatter.Deserialize を呼び出さないでください
[CA2302](/dotnet/fundamentals/code-analysis/quality-rules/ca2302) | BinaryFormatter.Deserialize を呼び出す前に BinaryFormatter.Binder が設定されていることを確認します
[CA2305](/dotnet/fundamentals/code-analysis/quality-rules/ca2305) | 安全ではないデシリアライザー LosFormatter を使用しないでください
[CA2310](/dotnet/fundamentals/code-analysis/quality-rules/ca2310) | 安全ではないデシリアライザー NetDataContractSerializer を使用しないでください
[CA2311](/dotnet/fundamentals/code-analysis/quality-rules/ca2311) | 最初に NetDataContractSerializer.Binder を設定しないで逆シリアル化しないでください
[CA2312](/dotnet/fundamentals/code-analysis/quality-rules/ca2312) | NetDataContractSerializer.Binder を設定してから逆シリアル化してください
[CA2315](/dotnet/fundamentals/code-analysis/quality-rules/ca2315) | 安全ではないデシリアライザー ObjectStateFormatter を使用しないでください
[CA2321](/dotnet/fundamentals/code-analysis/quality-rules/ca2321) | SimpleTypeResolver を使って JavaScriptSerializer で逆シリアル化しないでください
[CA2322](/dotnet/fundamentals/code-analysis/quality-rules/ca2322) | 逆シリアル化する前に JavaScriptSerializer が SimpleTypeResolver によって初期化されていないことを確認してください
[CA3001](/dotnet/fundamentals/code-analysis/quality-rules/ca3001) | SQL インジェクションの脆弱性のコード レビュー
[CA3002](/dotnet/fundamentals/code-analysis/quality-rules/ca3002) | XSS の脆弱性のコード レビュー
[CA3003](/dotnet/fundamentals/code-analysis/quality-rules/ca3003) | ファイル パス インジェクションの脆弱性のコード レビュー
[CA3004](/dotnet/fundamentals/code-analysis/quality-rules/ca3004) | 情報漏えいの脆弱性のコード レビュー
[CA3005](/dotnet/fundamentals/code-analysis/quality-rules/ca3005) | LDAP インジェクションの脆弱性のコード レビュー
[CA3006](/dotnet/fundamentals/code-analysis/quality-rules/ca3006) | プロセス コマンド インジェクションの脆弱性のコード レビュー
[CA3007](/dotnet/fundamentals/code-analysis/quality-rules/ca3007) | オープン リダイレクトの脆弱性のコード レビュー
[CA3008](/dotnet/fundamentals/code-analysis/quality-rules/ca3008) | XPath インジェクションの脆弱性のコード レビュー
[CA3009](/dotnet/fundamentals/code-analysis/quality-rules/ca3009) | XML インジェクションの脆弱性のコード レビュー
[CA3010](/dotnet/fundamentals/code-analysis/quality-rules/ca3010) | XAML インジェクションの脆弱性のコード レビュー
[CA3011](/dotnet/fundamentals/code-analysis/quality-rules/ca3011) | DLL インジェクションの脆弱性のコード レビュー
[CA3012](/dotnet/fundamentals/code-analysis/quality-rules/ca3012) | RegEx インジェクションの脆弱性のコード レビュー
[CA3061](/dotnet/fundamentals/code-analysis/quality-rules/ca3061) | URL でスキーマを追加しない
[CA3075](/dotnet/fundamentals/code-analysis/quality-rules/ca3075) | XML での DTD 処理が安全ではありません
[CA3076](/dotnet/fundamentals/code-analysis/quality-rules/ca3076) | 安全ではない XSLT スクリプトの処理。
[CA3077](/dotnet/fundamentals/code-analysis/quality-rules/ca3077) | API 設計、XmlDocument、XmlTextReader で安全ではない処理
[CA3147](/dotnet/fundamentals/code-analysis/quality-rules/ca3147) | アンチ偽造トークンを検証する動詞ハンドラーをマークします
[CA5350](/dotnet/fundamentals/code-analysis/quality-rules/ca5350) | 脆弱な暗号アルゴリズムを使用しないでください
[CA5351](/dotnet/fundamentals/code-analysis/quality-rules/ca5351) | 破損した暗号アルゴリズムを使用しない
[CA5358](/dotnet/fundamentals/code-analysis/quality-rules/ca5358) | 安全ではない暗号モードを使用しないでください
CA5359 | 証明書の検証を無効にしない
CA5360 | 逆シリアル化で危険なメソッドを呼び出さないでください
[CA5361](/dotnet/fundamentals/code-analysis/quality-rules/ca5361) | 強力な暗号の SChannel 使用を無効にしない
CA5362 | Serializable クラスの Self を参照しない
[CA5363](/dotnet/fundamentals/code-analysis/quality-rules/ca5363) | 要求の検証を無効にしない
[CA5364](/dotnet/fundamentals/code-analysis/quality-rules/ca5364) | 非推奨のセキュリティプロトコルを使用しない
CA5365 | HTTP ヘッダーチェックを無効にしない
CA5366 | DataSet に XmlReader を使用する Xml の読み取り
CA5367 | ポインターフィールドを持つ型をシリアル化しない
CA5368 | ページから派生したクラスの ViewStateUserKey を設定する
[CA5369](/dotnet/fundamentals/code-analysis/quality-rules/ca5369) | 逆シリアル化に XmlReader を使用する
[CA5370](/dotnet/fundamentals/code-analysis/quality-rules/ca5370) | 読み取りの検証に XmlReader を使用する
[CA5371](/dotnet/fundamentals/code-analysis/quality-rules/ca5371) | スキーマ読み取りに XmlReader を使用する
[CA5372](/dotnet/fundamentals/code-analysis/quality-rules/ca5372) | Xpath ドキュメントに XmlReader を使用する
[CA5373](/dotnet/fundamentals/code-analysis/quality-rules/ca5373) | 廃止されたキー派生関数を使用しません
CA5374 | XslTransform を使用しない
CA5375 | アカウントを使用しない Shared Access Signature
CA5376 | SharedAccessProtocol HttpsOnly を使用する
CA5377 | コンテナーレベルのアクセスポリシーを使用する
[CA5378](/dotnet/fundamentals/code-analysis/quality-rules/ca5378) | ServicePointManagerSecurityProtocols を無効にしません
CA5379 | 弱いキー派生関数アルゴリズムを使用しない
CA9999 | アナライザーのバージョンが一致しません

## <a name="see-also"></a>関連項目

- [.NET analyzer の規則](https://github.com/dotnet/roslyn-analyzers/blob/master/src/NetAnalyzers/Microsoft.CodeAnalysis.NetAnalyzers.md)
