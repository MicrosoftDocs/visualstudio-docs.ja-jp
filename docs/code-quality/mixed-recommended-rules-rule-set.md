---
title: "\"混合推奨規則\" 規則セット"
ms.date: 11/04/2016
description: Visual Studio の "混合推奨規則" 規則セットについて説明します。 共通言語ランタイムをサポートする C++ プロジェクトのルールの説明をご覧ください。
ms.custom: SEO-VS-2020
ms.topic: reference
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 7897799e631aad1005d4300e811f8209adb8281d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99859776"
---
# <a name="mixed-recommended-rules-rule-set"></a>"混合推奨規則" 規則セット

Microsoft の混合推奨規則は、共通言語ランタイムをサポートする C++ プロジェクトの最も一般的で重大な問題 (潜在的なセキュリティ ホールやアプリケーションのクラッシュ、その他の重要な論理エラーや設計エラーなど) に関するものです。 この規則セットには、"[混合推奨規則](mixed-minimum-rules-rule-set.md)" 規則セット内のすべての規則が含まれます。

共通言語ランタイムをサポートする C++ プロジェクトにカスタムの規則セットを作成する場合は、この規則セットを含めます。

|ルール|説明|
|----------|-----------------|
|[C6001](/cpp/code-quality/c6001)|初期化されていないメモリの使用|
|[C6011](/cpp/code-quality/c6011)|Null ポインターの逆参照|
|[C6029](/cpp/code-quality/c6029)|未確認の値の使用|
|[C6031](/cpp/code-quality/c6031)|戻り値の無視|
|[C6053](/cpp/code-quality/c6053)|呼び出しの 0 での終了|
|[C6054](/cpp/code-quality/c6054)|0 での終了がない|
|[C6059](/cpp/code-quality/c6059)|不適切な連結|
|[C6063](/cpp/code-quality/c6063)|Format 関数への文字列引数がない|
|[C6064](/cpp/code-quality/c6064)|Format 関数への整数引数がない|
|[C6066](/cpp/code-quality/c6066)|Format 関数へのポインター引数がない|
|[C6067](/cpp/code-quality/c6067)|Format 関数への文字列ポインター引数がない|
|[C6101](/cpp/code-quality/c6101)|初期化されていないメモリを返す|
|[C6200](/cpp/code-quality/c6200)|インデックスがバッファーの最大値を超過|
|[C6201](/cpp/code-quality/c6201)|インデックスがスタック バッファーの最大値を超過|
|[C6214](/cpp/code-quality/c6214)|HRESULT から BOOL への無効なキャスト|
|[C6215](/cpp/code-quality/c6215)|BOOL から HRESULT への無効なキャスト|
|[C6216](/cpp/code-quality/c6216)|BOOL から HRESULT へのコンパイラ挿入された無効なキャスト|
|[C6217](/cpp/code-quality/c6217)|NOT での無効な HRESULT テスト|
|[C6220](/cpp/code-quality/c6220)|-1 との無効な HRESULT 比較|
|[C6226](/cpp/code-quality/c6226)|-1 への無効な HRESULT 代入|
|[C6230](/cpp/code-quality/c6230)|ブール値としての無効な HRESULT 使用|
|[C6235](/cpp/code-quality/c6235)|0 でない定数と論理 Or|
|[C6236](/cpp/code-quality/c6236)|論理 Or と 0 でない定数|
|[C6237](/cpp/code-quality/c6237)|0 と論理 And での副作用の消失|
|[C6242](/cpp/code-quality/c6242)|ローカル アンワインドの強制|
|[C6248](/cpp/code-quality/c6248)|Null DACL の作成|
|[C6250](/cpp/code-quality/c6250)|解放されていないアドレス記述子|
|[C6255](/cpp/code-quality/c6255)|Alloca の保護されていない使用|
|[C6258](/cpp/code-quality/c6258)|TerminateThread の使用|
|[C6259](/cpp/code-quality/c6259)|ビットごとの Or で制限される Switch で実行されないコード|
|[C6260](/cpp/code-quality/c6260)|バイト算術の使用|
|[C6262](/cpp/code-quality/c6262)|過剰なスタック使用|
|[C6263](/cpp/code-quality/c6263)|ループでの Alloca の使用|
|[C6268](/cpp/code-quality/c6268)|キャストでのかっこの不足|
|[C6269](/cpp/code-quality/c6269)|ポインターの逆参照の無視|
|[C6270](/cpp/code-quality/c6270)|Format 関数への Float 引数がない|
|[C6271](/cpp/code-quality/c6271)|Format 関数への余分な引数|
|[C6272](/cpp/code-quality/c6272)|Format 関数への Float でない引数|
|[C6273](/cpp/code-quality/c6273)|Format 関数への整数でない引数|
|[C6274](/cpp/code-quality/c6274)|Format 関数への文字でない引数|
|[C6276](/cpp/code-quality/c6276)|無効な文字列のキャスト|
|[C6277](/cpp/code-quality/c6277)|無効な CreateProcess 呼び出し|
|[C6278](/cpp/code-quality/c6278)|配列の New とスカラーの Delete の不一致|
|[C6279](/cpp/code-quality/c6279)|スカラーの New と配列の Delete の不一致|
|[C6280](/cpp/code-quality/c6280)|メモリの割り当てと解放の不一致|
|[C6281](/cpp/code-quality/c6281)|ビットごとの関係の優先順位|
|[C6282](/cpp/code-quality/c6282)|代入をテストに置き換え|
|[C6283](/cpp/code-quality/c6283)|プリミティブな配列の New とスカラーの Delete の不一致|
|[C6284](/cpp/code-quality/c6284)|Format 関数への無効なオブジェクト引数|
|[C6285](/cpp/code-quality/c6285)|定数の論理 Or|
|[C6286](/cpp/code-quality/c6286)|0 でない論理 Or での副作用の消失|
|[C6287](/cpp/code-quality/c6287)|冗長テスト|
|[C6288](/cpp/code-quality/c6288)|論理 And での相互包括は False|
|[C6289](/cpp/code-quality/c6289)|論理 Or での相互排他は True|
|[C6290](/cpp/code-quality/c6290)|論理 Not とビットごとの And の優先順位|
|[C6291](/cpp/code-quality/c6291)|論理 Not とビットごとの Or の優先順位|
|[C6292](/cpp/code-quality/c6292)|ループ カウントの最大値超過|
|[C6293](/cpp/code-quality/c6293)|ループ カウントの最小値未満|
|[C6294](/cpp/code-quality/c6294)|ループ本体が実行されない|
|[C6295](/cpp/code-quality/c6295)|無限ループ|
|[C6296](/cpp/code-quality/c6296)|ループが 1 度だけ実行される|
|[C6297](/cpp/code-quality/c6297)|シフトの結果がより大きいサイズにキャストされる|
|[C6299](/cpp/code-quality/c6299)|ビット フィールドとブール値の比較|
|[C6302](/cpp/code-quality/c6302)|Format 関数への無効な文字列引数|
|[C6303](/cpp/code-quality/c6303)|Format 関数への無効なワイド文字列引数|
|[C6305](/cpp/code-quality/c6305)|サイズと数の使用の不一致|
|[C6306](/cpp/code-quality/c6306)|不適切な変数引数の関数呼び出し|
|[C6308](/cpp/code-quality/c6308)|Realloc のリーク|
|[C6310](/cpp/code-quality/c6310)|無効な例外フィルター定数|
|[C6312](/cpp/code-quality/c6312)|Exception Continue Execution ループ|
|[C6314](/cpp/code-quality/c6314)|ビットごとの Or の優先順位|
|[C6317](/cpp/code-quality/c6317)|否定と補数の不可|
|[C6318](/cpp/code-quality/c6318)|Exception Continue Search|
|[C6319](/cpp/code-quality/c6319)|コンマによる無視|
|[C6324](/cpp/code-quality/c6324)|文字列比較でない文字列コピー|
|[C6328](/cpp/code-quality/c6328)|引数の型の不一致の可能性|
|[C6331](/cpp/code-quality/c6331)|VirtualFree の無効なフラグ|
|[C6332](/cpp/code-quality/c6332)|VirtualFree の無効なパラメーター|
|[C6333](/cpp/code-quality/c6333)|VirtualFree の無効なサイズ|
|[C6335](/cpp/code-quality/c6335)|プロセス ハンドルのリーク|
|[C6381](/cpp/code-quality/c6381)|シャットダウン情報がない|
|[C6383](/cpp/code-quality/c6383)|要素数とバイト数のバッファー オーバーラン|
|[C6384](/cpp/code-quality/c6384)|ポインターのサイズの除算|
|[C6385](/cpp/code-quality/c6385)|読み取りのオーバーラン|
|[C6386](/cpp/code-quality/c6386)|書き込みのオーバーラン|
|[C6387](/cpp/code-quality/c6387)|無効なパラメーター値|
|[C6388](/cpp/code-quality/c6388)|無効なパラメーター値|
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
|[C6995](/cpp/code-quality/c6995)|XML ログ ファイルを保存できませんでした|
|[C26100](/cpp/code-quality/c26100)|競合状態|
|[C26101](/cpp/code-quality/c26101)|適切なインタロック操作の使用の失敗|
|[C26110](/cpp/code-quality/c26110)|呼び出し元でのロックの保持の失敗|
|[C26111](/cpp/code-quality/c26111)|呼び出し元でのロックの解放の失敗|
|[C26112](/cpp/code-quality/c26112)|呼び出し元がロックを保持できない|
|[C26115](/cpp/code-quality/c26115)|ロックの解放の失敗|
|[C26116](/cpp/code-quality/c26116)|ロックの取得または保持の失敗|
|[C26117](/cpp/code-quality/c26117)|保持されていないロックの解放|
|[C26140](/cpp/code-quality/c26140)|コンカレンシー SAL 注釈のエラーです|
|[C28020](/cpp/code-quality/c28020)|式はこの呼び出しで true ではありません|
|[C28021](/cpp/code-quality/c28021)|注釈が付けられているパラメーターはポインターである必要があります|
|[C28022](/cpp/code-quality/c28022)|この関数の関数クラスが、定義に使用された typedef の関数クラスと一致しません。|
|[C28023](/cpp/code-quality/c28023)|割り当てられているか、または渡されている関数には、少なくとも 1 つのクラスに対する \_Function\_class\_ 注釈が必要です|
|[C28024](/cpp/code-quality/c28024)|割り当てられている関数ポインターが関数クラスで注釈を付けられています。これは関数クラス一覧には含まれません。|
|[C28039](/cpp/code-quality/c28039)|実パラメーターの型は、型と完全に一致する必要があります|
|[C28112](/cpp/code-quality/c28112)|Interlocked 関数経由でアクセスされる変数には、必ず Interlocked 関数経由でアクセスする必要があります。|
|[C28113](/cpp/code-quality/c28113)|Interlocked 関数経由でローカル変数にアクセスしています|
|[C28125](/cpp/code-quality/c28125)|関数は try/except ブロック内から呼び出される必要があります|
|[C28137](/cpp/code-quality/c28137)|変数の引数は、(リテラル) 定数である必要があります|
|[C28138](/cpp/code-quality/c28138)|定数の引数は、変数である必要があります|
|[C28159](/cpp/code-quality/c28159)|代わりに別の関数を使用することを検討してください。|
|[C28160](/cpp/code-quality/c28160)|エラーの注釈|
|[C28163](/cpp/code-quality/c28163)|関数を try/except ブロック内から呼び出さないでください|
|[C28164](/cpp/code-quality/c28164)|引数は、ポインターへのポインターではなく、オブジェクトへのポインターが予期される関数に渡されています|
|[C28182](/cpp/code-quality/c28182)|Null ポインターの逆参照 このポインターは、もう 1 つのポインターと同じ Null 値を持ちます。|
|[C28183](/cpp/code-quality/c28183)|引数は 1 つの値である可能性があり、ポインターで見つかった値のコピーです|
|[C28193](/cpp/code-quality/c28193)|変数は検証が必要な値を保持しています|
|[C28196](/cpp/code-quality/c28196)|要件が満たされていません (式は true に評価されません)|
|[C28202](/cpp/code-quality/c28202)|静的でないメンバーへの参照が正しくありません|
|[C28203](/cpp/code-quality/c28203)|クラス メンバーへのあいまいな参照です。|
|[C28205](/cpp/code-quality/c28205)|\_Success\_ または \_On\_failure\_ が無効なコンテキスト内で使用されています|
|[C28206](/cpp/code-quality/c28206)|左側のオペランドは構造体をポイントするため、'-> ' を使用します|
|[C28207](/cpp/code-quality/c28207)|左側のオペランドは構造体であるため、'.' を使用します|
|[C28209](/cpp/code-quality/c28209)|シンボルの宣言に競合する宣言が含まれています|
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
|[C28244](/cpp/code-quality/c28244)|関数に対する注釈には、解析不能なパラメーター/外部注釈が含まれています|
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
|[C28306](/cpp/code-quality/c28306)|パラメーターの注釈は使用されなくなりました|
|[C28307](/cpp/code-quality/c28307)|パラメーターの注釈は使用されなくなりました|
|[C28350](/cpp/code-quality/c28350)|注釈には、条件付きで適用できない状況の説明が表示されます。|
|[C28351](/cpp/code-quality/c28351)|注釈には、動的な値 (変数) が使用できない条件が記述されています。|
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