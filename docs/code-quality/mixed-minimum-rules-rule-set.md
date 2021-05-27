---
title: "\"混合最小規則\" 規則セット"
ms.date: 11/04/2016
description: Visual Studio の "混合最小規則" 規則セットについて説明します。 共通言語ランタイムをサポートする C++ プロジェクトの規則の説明をご覧ください。
ms.custom: SEO-VS-2020
ms.topic: reference
ms.assetid: bc8df61c-19af-40ab-a871-315807e5f4bf
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 54ba61f3d4f82a5db25d0079193955a5569afa8a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99867881"
---
# <a name="mixed-minimum-rules-rule-set"></a>"混合最小規則" 規則セット

Microsoft 混合最小規則は、共通言語ランタイムをサポートする C++ プロジェクトの最も重大な問題 (潜在的なセキュリティ ホールやアプリケーションのクラッシュなど) に関するものです。

共通言語ランタイムをサポートする C++ プロジェクトにカスタムの規則セットを作成する場合は、この規則セットを含めます。

|ルール|説明|
|----------|-----------------|
|[C6001](/cpp/code-quality/c6001)|初期化されていないメモリの使用|
|[C6011](/cpp/code-quality/c6011)|Null ポインターの逆参照|
|[C6029](/cpp/code-quality/c6029)|未確認の値の使用|
|[C6053](/cpp/code-quality/c6053)|呼び出しの 0 での終了|
|[C6059](/cpp/code-quality/c6059)|不適切な連結|
|[C6063](/cpp/code-quality/c6063)|Format 関数への文字列引数がない|
|[C6064](/cpp/code-quality/c6064)|Format 関数への整数引数がない|
|[C6066](/cpp/code-quality/c6066)|Format 関数へのポインター引数がない|
|[C6067](/cpp/code-quality/c6067)|Format 関数への文字列ポインター引数がない|
|[C6101](/cpp/code-quality/c6101)|初期化されていないメモリを返す|
|[C6200](/cpp/code-quality/c6200)|インデックスがバッファーの最大値を超過|
|[C6201](/cpp/code-quality/c6201)|インデックスがスタック バッファーの最大値を超過|
|[C6270](/cpp/code-quality/c6270)|Format 関数への Float 引数がない|
|[C6271](/cpp/code-quality/c6271)|Format 関数への余分な引数|
|[C6272](/cpp/code-quality/c6272)|Format 関数への Float でない引数|
|[C6273](/cpp/code-quality/c6273)|Format 関数への整数でない引数|
|[C6274](/cpp/code-quality/c6274)|Format 関数への文字でない引数|
|[C6276](/cpp/code-quality/c6276)|無効な文字列のキャスト|
|[C6277](/cpp/code-quality/c6277)|無効な CreateProcess 呼び出し|
|[C6284](/cpp/code-quality/c6284)|Format 関数への無効なオブジェクト引数|
|[C6290](/cpp/code-quality/c6290)|論理 Not とビットごとの And の優先順位|
|[C6291](/cpp/code-quality/c6291)|論理 Not とビットごとの Or の優先順位|
|[C6302](/cpp/code-quality/c6302)|Format 関数への無効な文字列引数|
|[C6303](/cpp/code-quality/c6303)|Format 関数への無効なワイド文字列引数|
|[C6305](/cpp/code-quality/c6305)|サイズと数の使用の不一致|
|[C6306](/cpp/code-quality/c6306)|不適切な変数引数の関数呼び出し|
|[C6328](/cpp/code-quality/c6328)|引数の型の不一致の可能性|
|[C6385](/cpp/code-quality/c6385)|読み取りのオーバーラン|
|[C6386](/cpp/code-quality/c6386)|書き込みのオーバーラン|
|[C6387](/cpp/code-quality/c6387)|無効なパラメーター値|
|[C6500](/cpp/code-quality/c6500)|無効な属性プロパティ|
|[C6501](/cpp/code-quality/c6501)|属性プロパティ値の競合|
|[C6503](/cpp/code-quality/c6503)|参照は Null にはできない|
|[C6504](/cpp/code-quality/c6504)|非ポインターでの Null|
|[C6505](/cpp/code-quality/c6505)|Void での MustCheck|
|[C6506](/cpp/code-quality/c6506)|非ポインターまたは配列でのバッファー サイズ|
|[C6508](/cpp/code-quality/c6508)|定数での書き込みアクセス|
|[C6509](/cpp/code-quality/c6509)|前提条件で使用される Return|
|[C6510](/cpp/code-quality/c6510)|非ポインターでの Null 終了|
|[C6511](/cpp/code-quality/c6511)|MustCheck は Yes または No でなければならない|
|[C6513](/cpp/code-quality/c6513)|バッファー サイズのない要素サイズ|
|[C6514](/cpp/code-quality/c6514)|バッファー サイズが配列サイズを超過|
|[C6515](/cpp/code-quality/c6515)|非ポインターでのバッファー サイズ|
|[C6516](/cpp/code-quality/c6516)|属性にプロパティがない|
|[C6517](/cpp/code-quality/c6517)|読み取り可能でないバッファーでの有効なサイズ|
|[C6518](/cpp/code-quality/c6518)|書き込み可能でないバッファーでの書き込み可能サイズ|
|[C6522](/cpp/code-quality/c6522)|無効なサイズの文字列型|
|[C6525](/cpp/code-quality/c6525)|無効なサイズの到達不能な場所の文字列|
|[C6527](/cpp/code-quality/c6527)|無効な注釈です: 'NeedsRelease' プロパティは、void 型の値では使用できません|
|[C6530](/cpp/code-quality/c6530)|認識されない書式指定文字列スタイル|
|[C6540](/cpp/code-quality/c6540)|この関数で属性注釈を使用すると、既存の __declspec 注釈がすべて無効となります|
|[C6551](/cpp/code-quality/c6551)|無効なサイズ指定です: 式が解析可能ではありません|
|[C6552](/cpp/code-quality/c6552)|無効な Deref= または Notref= です: 式が解析可能ではありません|
|[C6701](/cpp/code-quality/c6701)|値が有効な Yes/No/Maybe 値ではありません|
|[C6702](/cpp/code-quality/c6702)|値が文字列値ではありません|
|[C6703](/cpp/code-quality/c6703)|値が数値ではありません|
|[C6704](/cpp/code-quality/c6704)|予期しない注釈式エラーです|
|[C6705](/cpp/code-quality/c6705)|想定した注釈の引数の数が、実際の注釈の引数の数と一致しません|
|[C6706](/cpp/code-quality/c6706)|注釈に対する、予期しない注釈エラーです|
|[C28021](/cpp/code-quality/c28021)|注釈が付けられているパラメーターはポインターである必要があります|
|[C28182](/cpp/code-quality/c28182)|Null ポインターの逆参照 このポインターは、もう 1 つのポインターと同じ Null 値を持ちます。|
|[C28202](/cpp/code-quality/c28202)|静的でないメンバーへの参照が正しくありません|
|[C28203](/cpp/code-quality/c28203)|クラス メンバーへのあいまいな参照です。|
|[C28205](/cpp/code-quality/c28205)|\_Success\_ または \_On\_failure\_ が無効なコンテキスト内で使用されています|
|[C28206](/cpp/code-quality/c28206)|左側のオペランドは構造体をポイントするため、'-> ' を使用します|
|[C28207](/cpp/code-quality/c28207)|左側のオペランドは構造体であるため、'.' を使用します|
|[C28210](/cpp/code-quality/c28210)|__on_failure コンテキストの注釈を明示的なプリ コンテキストに含めることはできません|
|[C28211](/cpp/code-quality/c28211)|SAL_context には静的コンテキスト名が必要です|
|[C28212](/cpp/code-quality/c28212)|注釈にはポインター式が必要です|
|[C28213](/cpp/code-quality/c28213)|\_Use\_decl\_annotations\_ 注釈は、変更、先行する宣言なしで、参照に使用される必要があります。|
|[C28214](/cpp/code-quality/c28214)|属性パラメーター名は、p1...p9 である必要があります|
|[C28215](/cpp/code-quality/c28215)|typefix は、既に typefix のあるパラメーターには適用できません|
|[C28216](/cpp/code-quality/c28216)|checkReturn 注釈は、特定の関数パラメーターの事後条件にのみ適用されます。|
|[C28217](/cpp/code-quality/c28217)|関数について、注釈へのパラメーター数がファイルで検出されたものと一致しません|
|[C28218](/cpp/code-quality/c28218)|関数パラメーターについて、注釈のパラメーターがファイルで検出されたものと一致しません|
|[C28219](/cpp/code-quality/c28219)|注釈 (注釈のパラメーター) には列挙型のメンバーが必要です|
|[C28220](/cpp/code-quality/c28220)|注釈 (注釈のパラメーター) には整数式が必要です|
|[C28221](/cpp/code-quality/c28221)|注釈のパラメーターには文字列式が必要です|
|[C28222](/cpp/code-quality/c28222)|注釈には __yes、\__no、または \__maybe が必要です|
|[C28223](/cpp/code-quality/c28223)|注釈に必要なトークン/識別子、パラメーターがありません|
|[C28224](/cpp/code-quality/c28224)|注釈にはパラメーターが必要です|
|[C28225](/cpp/code-quality/c28225)|注釈に正しい数の必須パラメーターがありません|
|[C28226](/cpp/code-quality/c28226)|注釈は、PrimOp (現在の宣言内) になることもできません|
|[C28227](/cpp/code-quality/c28227)|注釈は、PrimOp (前の宣言を参照) になることもできません|
|[C28228](/cpp/code-quality/c28228)|注釈パラメーター: 注釈内で型を使用することはできません|
|[C28229](/cpp/code-quality/c28229)|注釈はパラメーターをサポートしません|
|[C28230](/cpp/code-quality/c28230)|パラメーターの型にはメンバーがありません。|
|[C28231](/cpp/code-quality/c28231)|注釈は配列でのみ有効です|
|[C28232](/cpp/code-quality/c28232)|pre、post、または deref は注釈に適用されません|
|[C28233](/cpp/code-quality/c28233)|pre、post、または deref はブロックに適用されます|
|[C28234](/cpp/code-quality/c28234)|_at 式は現在の関数に適用されません|
|[C28235](/cpp/code-quality/c28235)|関数は注釈として独立できません|
|[C28236](/cpp/code-quality/c28236)|注釈は式内で使用できません|
|[C28237](/cpp/code-quality/c28237)|パラメーターの注釈は、もうサポートされていません|
|[C28238](/cpp/code-quality/c28238)|パラメーターの注釈には、複数の値、stringValue、および longValue が含まれています。 paramn=xxx を使用してください|
|[C28239](/cpp/code-quality/c28239)|パラメーターの注釈には、両方の値、stringValue、または longValue、さらに paramn=xxx が含まれます。 paramn=xxx のみを使用してください|
|[C28240](/cpp/code-quality/c28240)|パラメーターの注釈は、param2 を含みますが param1 は含みません|
|[C28241](/cpp/code-quality/c28241)|パラメーターの関数の注釈は認識されません|
|[C28243](/cpp/code-quality/c28243)|パラメーターの関数の注釈には、注釈が付けられた実際の型に許可された数よりも多くの逆参照が必要です|
|[C28245](/cpp/code-quality/c28245)|関数に対する注釈は、非メンバー関数上で 'this' に注釈を付けます。|
|[C28246](/cpp/code-quality/c28246)|関数に対するパラメーターの注釈が、パラメーターの型に一致しません|
|[C28250](/cpp/code-quality/c28250)|関数に対する一貫性のない注釈: 前のインスタンスにはエラーが含まれます。|
|[C28251](/cpp/code-quality/c28251)|関数に対する一貫性のない注釈: 前のインスタンスにはエラーが含まれます。|
|[C28252](/cpp/code-quality/c28252)|関数に対する一貫性のない注釈: パラメーターは、このインスタンスについて他の注釈を含みます。|
|[C28253](/cpp/code-quality/c28253)|関数に対する一貫性のない注釈: パラメーターは、このインスタンスについて他の注釈を含みます。|
|[C28254](/cpp/code-quality/c28254)|dynamic_cast<>() は、注釈ではサポートされません|
|[C28262](/cpp/code-quality/c28262)|注釈での構文エラーが関数の注釈で見つかりました|
|[C28263](/cpp/code-quality/c28263)|条件付き注釈での構文エラーが、組み込みの注釈で見つかりました|
|[C28267](/cpp/code-quality/c28267)|注釈での構文エラーが、関数の注釈で見つかりました。|
|[C28272](/cpp/code-quality/c28272)|検査中の関数とパラメーターに対する注釈に関数宣言との一貫性がありません|
|[C28273](/cpp/code-quality/c28273)|関数について、手がかりには関数宣言との一貫性がありません。|
|[C28275](/cpp/code-quality/c28275)|\_Macro\_value\_ のパラメーターは null です|
|[C28279](/cpp/code-quality/c28279)|シンボルについて、'begin' はありましたが、対応する 'end' がありません|
|[C28280](/cpp/code-quality/c28280)|シンボルについて、'end' はありましたが、対応する 'begin' がありません|
|[C28282](/cpp/code-quality/c28282)|書式指定文字列は、前提条件の中に存在する必要があります|
|[C28285](/cpp/code-quality/c28285)|関数について、パラメーターに構文エラーがあります|
|[C28286](/cpp/code-quality/c28286)|関数について、構文エラーが最後の近くにあります|
|[C28287](/cpp/code-quality/c28287)|関数について、\_At\_() 注釈 (認識されないパラメーター名) に構文エラーがあります|
|[C28288](/cpp/code-quality/c28288)|関数について、\_At\_() 注釈 (無効のパラメーター名) に構文エラーがあります|
|[C28289](/cpp/code-quality/c28289)|関数について: ReadableTo または WritableTo には、パラメーターとして limit-spec がありませんでした|
|[C28290](/cpp/code-quality/c28290)|関数の注釈は、実際のパラメーターの数より多い外部参照を含みます|
|[C28291](/cpp/code-quality/c28291)|deref レベル 0 での post null/notnull は、関数に対して意味がありません。|
|[C28300](/cpp/code-quality/c28300)|演算子に対する互換性のない型の、式のオペランドです|
|[C28301](/cpp/code-quality/c28301)|関数の最初の宣言に対して注釈がありません。|
|[C28302](/cpp/code-quality/c28302)|余分な \_Deref\_ 演算子が注釈に見つかりました。|
|[C28303](/cpp/code-quality/c28303)|あいまいな \_Deref\_ 演算子が注釈に見つかりました。|
|[C28304](/cpp/code-quality/c28304)|不適切に設定された \_Notref\_ 演算子がトークンに適用されました。|
|[C28305](/cpp/code-quality/c28305)|トークンの解析中にエラーが発生しました。|
|[C28350](/cpp/code-quality/c28350)|注釈には、条件付きで適用できない状況の説明が表示されます。|
|[C28351](/cpp/code-quality/c28351)|注釈には、動的な値 (変数) が使用できない条件が記述されています。|
|[CA1001](/dotnet/fundamentals/code-analysis/quality-rules/ca1001)|破棄可能なフィールドを所有する型は、破棄可能でなければなりません|
|[CA1821](/dotnet/fundamentals/code-analysis/quality-rules/ca1821)|空のファイナライザーを削除します|
|[CA2213](/dotnet/fundamentals/code-analysis/quality-rules/ca2213)|破棄可能なフィールドは破棄されなければなりません|
|[CA2231](/dotnet/fundamentals/code-analysis/quality-rules/ca2231)|ValueType.Equals のオーバーライドで、演算子 equals をオーバーロードします|