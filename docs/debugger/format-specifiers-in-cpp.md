---
title: デバッガーでの書式指定子 (C++) | Microsoft Docs
description: 書式指定子を使用すると、[ウォッチ] ウィンドウ、[自動変数] ウィンドウ、または [ローカル] ウィンドウに表示される値の書式を変更できます。 この記事では、使用方法の詳細について説明します。
ms.custom: SEO-VS-2020
ms.date: 3/11/2019
ms.topic: conceptual
f1_keywords:
- vs.debug
dev_langs:
- C++
helpviewer_keywords:
- QuickWatch dialog box, format specifiers in C++
- variables [debugger], watch variable symbols
- symbols, watch variable formatting
- QuickWatch dialog box, using format specifiers
- expressions [C++], format specifiers
- specifiers, watch variable format
- specifiers
- Watch window, format specifiers in C++
- watch variable symbols
- format specifiers, debugger
- debugger, format specifiers recognized by
ms.assetid: 0f6f3b7c-ce2c-4b4d-b14f-7589dbed5444
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- cplusplus
ms.openlocfilehash: 868c02091814fe49ea0224190c7d205e8b67c42b
ms.sourcegitcommit: 4b2b6068846425f6964c1fd867370863fc4993ce
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/12/2021
ms.locfileid: "112042978"
---
# <a name="format-specifiers-for-c-in-the-visual-studio-debugger"></a>Visual Studio デバッガーでの書式指定子 (C++)

書式指定子を使用して、 **[ウォッチ]** 、 **[自動変数]** 、 **[ローカル]** の各ウィンドウに表示される値の書式を変更することができます。

また、 **[イミディエイト]** ウィンドウ、 **[コマンド]** ウィンドウ、[トレースポイント](../debugger/using-breakpoints.md#BKMK_Print_to_the_Output_window_with_tracepoints)、ソースのウィンドウでも、書式指定子を使用できます。 これらのウィンドウで式の上にカーソルを合わせると、結果が [[データヒント]](../debugger/view-data-values-in-data-tips-in-the-code-editor.md) に表示されます。 [データヒント] の表示には、書式指定子が反映されます。

> [!NOTE]
> Visual Studio のネイティブ デバッガーが新しいデバッグ エンジンに変更されたときに、新しい書式指定子がいくつか追加され、古いものがいくつか削除されました。 C++/CLI で相互運用 (ネイティブ コードとマネージド コードの混合) をデバッグする場合は、以前のデバッガーが引き続き使用されます。

## <a name="set-format-specifiers"></a>書式指定子の設定

次のコード例を使用します。

```C++
int main() {
    int my_var1 = 0x0065;
    int my_var2 = 0x0066;
    int my_var3 = 0x0067;
}
```

デバッグ中に `my_var1` 変数を **ウォッチ** ウィンドウに追加します ( **[デバッグ]**  >  **[Windows]**  >  **[ウォッチ]**  >  **[ウォッチ 1]** )。 次に、変数を右クリックし、 **[16 進数で表示]** を選択します。 これで、**ウォッチ** ウィンドウに値 0x0065 が示されます。 この値を整数ではなく文字として表示するには、最初に右クリックして **[16 進数で表示]** を選択解除します。 次に、文字書式指定子 **, c** を、 **[Name]** 列の変数名の後に追加します。 **[Value]** 列に **101 'e'** が表示されるようになります。

![Visual Studio のウォッチ ウィンドウのスクリーンショット。値が 101 'e' で型が int の my_var1.c を示す 1 行が選択されています。](../debugger/media/watchformatcplus1.png)

::: moniker range=">= vs-2019" 
**ウォッチ** ウィンドウの値にコンマ (,) を追加することで、使用できる書式指定子の一覧を表示して選択できます。 

![WatchFormatSpecDropdown](../debugger/media/vs-2019/format-specs-cpp.png "FormatSpecCpp")

::: moniker-end

## <a name="format-specifiers"></a><a name="BKMK_Visual_Studio_2012_format_specifiers"></a> 書式指定子

次の表で、Visual Studio で使用できる書式指定子を説明します。 太字で示されている指定子は、新しいデバッガーでのみサポートされており、C++/CLI を使用した相互運用機能デバッグではサポートされていません。

::: moniker range=">= vs-2019" 

|指定子|形式|元の [ウォッチ] の値|表示される値|
|---------------|------------|--------------------------|---------------------|
|d|10 進整数|0x00000066|102|
|o|符号なし 8 進整数。|0x00000066|000000000146|
|x<br /><br /> **h**|16 進整数|102|0xcccccccc|
|x<br /><br /> **H**|16 進整数|102|0xcccccccc|
|xb<br /><br /> **hb**|16 進数の整数 (先頭 0x なし)|102|cccccccc|
|Xb<br /><br /> **Hb**|16 進数の整数 (先頭 0x なし)|102|CCCCCCCC|
|b|符号なし 2 進整数|25|0b00000000000000000000000000011001|
|bb|符号なし 2 進整数 (先頭 0b なし)|25|00000000000000000000000000011001|
|e|指数表記|25000000|2.500000e+07|
|G|指数表記と浮動小数点のうちの短い方|25000000|2.5e+07|
|c|単一文字|0x0065|101 'e'|
|s|const char* 文字列 (引用符あり)|\<location> "hello world"|"hello world"|
|**sb**|const char* 文字列 (引用符なし)|\<location> "hello world"|hello world|
|s8|UTF-8 文字列|\<location> "This is a UTF-8 coffee cup â˜•"|"This is a UTF-8 coffee cup ☕"|
|**s8b**|UTF-8 文字列 (引用符なし)|\<location> "hello world"|hello world|
|su|Unicode (UTF-16 エンコード) 文字列 (引用符あり)|\<location> L"hello world"|L"hello world"<br /><br /> u"hello world"|
|sub|Unicode (UTF-16 エンコード) 文字列 (引用符なし)|\<location> L"hello world"|hello world|
|bstr|BSTR バイナリ文字列 (引用符あり)|\<location> L"hello world"|L"hello world"|
|env|環境ブロック (2 つの null で終了する文字列)|\<location> L"=::=::\\\\"|L"=::=::\\\\\\0=C:=C:\\\\windows\\\\system32\\0ALLUSERSPROFILE=...|
|**s32**|UTF-32 文字列 (引用符あり)|\<location> U"hello world"|u"hello world"|
|**s32b**|UTF-32 文字列 (引用符なし)|\<location> U"hello world"|hello world|
|**en**|enum|Saturday(6)|土曜日|
|**hv**|ポインター型。検査されるポインター値が配列のヒープ割り当ての結果であることを意味します (たとえば、 `new int[3]`)。|\<location>{\<first member>}|\<location>{\<first member>, \<second member>, ...}|
|**na**|オブジェクトのポインターのメモリ アドレスを非表示にします。|\<location>, {member=value...}|{member=value...}|
|**nd**|基底クラスの情報だけを表示し、派生クラスは無視します。|`(Shape*) square` には基底クラスおよび派生クラスの情報が含まれます。|基底クラスの情報だけを表示します。|
|hr|HRESULT または Win32 エラー コード。 この指定子は、デバッガーによって自動的にデコードされるため、HRESULT では不要になりました。|S_OK|S_OK|
|wc|Windows クラス フラグ|0x0010|WC_DEFAULTCHAR|
|wm|Windows メッセージ番号|16|WM_CLOSE|
|nr|"未加工ビュー" 項目の抑制|
|nvo|数値に対してのみ "未加工ビュー" 項目を表示する|
|!|データ型の表示カスタマイズをすべて無視した、未処理の書式。|\<customized representation>|4|
|ハンドル|win32 ハンドルに関する情報を表示します|0x000000000000009c| スレッド ID など、ハンドルに関する有用な情報を表示します。 |

::: moniker-end

::: moniker range="vs-2017" 

|指定子|形式|元の [ウォッチ] の値|表示される値|
|---------------|------------|--------------------------|---------------------|
|d|10 進整数|0x00000066|102|
|o|符号なし 8 進整数。|0x00000066|000000000146|
|x<br /><br /> **h**|16 進整数|102|0xcccccccc|
|x<br /><br /> **H**|16 進整数|102|0xcccccccc|
|c|単一文字|0x0065, c|101 'e'|
|s|const char* 文字列 (引用符あり)|\<location> "hello world"|"hello world"|
|**sb**|const char* 文字列 (引用符なし)|\<location> "hello world"|hello world|
|s8|UTF-8 文字列|\<location> "This is a UTF-8 coffee cup â˜•"|"This is a UTF-8 coffee cup ☕"|
|**s8b**|UTF-8 文字列 (引用符なし)|\<location> "hello world"|hello world|
|su|Unicode (UTF-16 エンコード) 文字列 (引用符あり)|\<location> L"hello world"|L"hello world"<br /><br /> u"hello world"|
|sub|Unicode (UTF-16 エンコード) 文字列 (引用符なし)|\<location> L"hello world"|hello world|
|bstr|BSTR バイナリ文字列 (引用符あり)|\<location> L"hello world"|L"hello world"|
|env|環境ブロック (2 つの null で終了する文字列)|\<location> L"=::=::\\\\"|L"=::=::\\\\\\0=C:=C:\\\\windows\\\\system32\\0ALLUSERSPROFILE=...|
|**s32**|UTF-32 文字列 (引用符あり)|\<location> U"hello world"|u"hello world"|
|**s32b**|UTF-32 文字列 (引用符なし)|\<location> U"hello world"|hello world|
|**en**|enum|Saturday(6)|土曜日|
|**hv**|ポインター型。検査されるポインター値が配列のヒープ割り当ての結果であることを意味します (たとえば、 `new int[3]`)。|\<location>{\<first member>}|\<location>{\<first member>, \<second member>, ...}|
|**na**|オブジェクトのポインターのメモリ アドレスを非表示にします。|\<location>, {member=value...}|{member=value...}|
|**nd**|基底クラスの情報だけを表示し、派生クラスは無視します。|`(Shape*) square` には基底クラスおよび派生クラスの情報が含まれます。|基底クラスの情報だけを表示します。|
|hr|HRESULT または Win32 エラー コード。 この指定子は、デバッガーによって自動的にデコードされるため、HRESULT では不要になりました。|S_OK|S_OK|
|wc|Windows クラス フラグ|0x0010|WC_DEFAULTCHAR|
|wm|Windows メッセージ番号|16|WM_CLOSE|
|!|データ型の表示カスタマイズをすべて無視した、未処理の書式。|\<customized representation>|4|

::: moniker-end

> [!NOTE]
> **hv** 書式指定子が存在する場合、デバッガーはバッファーの長さを判断してその要素の数を表示しようと試みます。 デバッガーは配列の正確なバッファー サイズを常に判断できるとは限らないため、可能な場合には必ずサイズ指定子 `(pBuffer,[bufferSize])` を使用してください。 **hv** 書式指定子は、バッファー サイズをすぐに利用できない場合に役立ちます。

### <a name="size-specifiers-for-pointers-as-arrays"></a><a name="BKMK_Size_specifiers_for_pointers_as_arrays_in_Visual_Studio_2012"></a> 配列としてのポインターのサイズ指定子

オブジェクトに対するポインターを配列として表示する場合、整数または式で配列要素数を指定できます。

|指定子|形式|元の [ウォッチ] の値|表示される値|
|---------------|------------|---------------------------|---------------------|
|n|10 進数または **16 進数** の整数|pBuffer,[32]<br /><br /> pBuffer, **[0x20]**|`pBuffer` を 32 要素の配列として表示します。|
|**[exp]**|整数に評価される有効な C++ 式|pBuffer,[bufferSize]|pBuffer を `bufferSize` 要素の配列として表示します。|
|**expand(n)**|整数に評価される有効な C++ 式|pBuffer, expand(2)|`pBuffer` の 3 番目の要素を表示します。|

## <a name="format-specifiers-for-interop-debugging-with-ccli"></a><a name="BKMK_Format_specifiers_for_interop_debugging_and_C___edit_and_continue"></a> C++/CLI での相互運用機能デバッグ用の書式指定子

**太字** で示されている指定子は、ネイティブおよび C++/CLI コードをデバッグする場合にのみサポートされます。 これには、[マネージド互換モード](../debugger/general-debugging-options-dialog-box.md)を使用して指定されたレガシ デバッガーが必要です。

|指定子|形式|元の [ウォッチ] の値|表示される値|
|---------------|------------|--------------------------|---------------------|
|**d**<br /><br />**i**|符号付き 10 進整数。|0xF000F065|-268373915|
|**u**|符号なし 10 進整数。|0x0065|101|
|o|符号なし 8 進整数。|0xF065|0170145|
|x<br /><br />x|16 進整数|61541|0x0000f065|
|**l**<br /><br />**h**|d、i、u、o、x、X の long 型または short 型のプレフィックス。|00406042|0x0c22|
|**f**|符号付き浮動小数点数値。|(3./2.), f|1.500000|
|**e**|符号付き指数表記。|(3.0/2.0)|1.500000e+000|
|**g**|符号付き浮動小数点数値または符号付き指数表記の<br/> 短い方|(3.0/2.0)|1.5|
|c|単一文字|\<location>|101 'e'|
|s|const char* (引用符あり)|\<location>|"hello world"|
|su|const wchar_t*<br /><br /> const char16_t\* (引用符あり)|\<location>|L"hello world"|
|sub|const wchar_t*<br /><br /> const char16_t\*|\<location>|hello world|
|s8|const char* (引用符あり)|\<location>|"hello world"|
|hr|HRESULT または Win32 エラー コード。<br/>この指定子は、デバッガーによって自動的にデコードされるため、HRESULT では不要になりました。|S_OK|S_OK|
|wc|Windows クラス フラグ|0x00000040,|WC_DEFAULTCHAR|
|wm|Windows メッセージ番号|0x0010|WM_CLOSE|
|!|データ型の表示カスタマイズをすべて無視した、未処理の書式|\<customized representation>|4|

### <a name="format-specifiers-for-memory-locations-in-interop-debugging-with-ccli"></a><a name="BKMK_Format_specifiers_memory_locations_in_interop_debugging_and_C___edit_and_continue"></a> C++/CLI での相互運用機能デバッグでのメモリ位置の書式指定子

メモリ位置を表すために使われる書式シンボルを次の表に示します。 メモリ位置指定子は、任意の値、または位置を評価する式に使用できます。

**太字** で示されている指定子は、ネイティブおよび C++/CLI コードをデバッグする場合にのみサポートされます。 これには、[マネージド互換モード](../debugger/general-debugging-options-dialog-box.md)を使用して指定されたレガシ デバッガーが必要です。

|シンボル|形式|元の [ウォッチ] の値|表示される値|
|------------|------------|--------------------------|---------------------|
|**ma**|64 ASCII 文字。|0x0012ffac|0x0012ffac .4...0...".0W&.......1W&.0.:W..1...."..1.JO&.1.2.."..1...0y....1|
|**m**|16 バイトの 16 進数。16 文字の ASCII 文字が続きます。|0x0012ffac|0x0012ffac B3 34 CB 00 84 30 94 80 FF 22 8A 30 57 26 00 00 .4...0...".0W&amp;.|
|**mb**|16 バイトの 16 進数。16 文字の ASCII 文字が続きます。|0x0012ffac|0x0012ffac B3 34 CB 00 84 30 94 80 FF 22 8A 30 57 26 00 00 .4...0...".0W&amp;.|
|**mw**|8 ワード。|0x0012ffac|0x0012ffac 34B3 00CB 3084 8094 22FF 308A 2657 0000|
|**md**|4 ダブルワード。|0x0012ffac|0x0012ffac 00CB34B3 80943084 308A22FF 00002657|
|**mq**|2 クワドワード。|0x0012ffac|0x0012ffac 7ffdf00000000000 5f441a790012fdd4|
|**mu**|2 バイト文字 (Unicode)|0x0012ffac|0x0012ffac 8478 77f4 ffff ffff 0000 0000 0000 0000|

### <a name="size-specifier-for-pointers-as-arrays-in-interop-debugging-with-ccli"></a><a name="BKMK_Size_specifier_for_pointers_as_arrays_in_interop_debugging_and_C___edit_and_continue"></a> C++/CLI での相互運用機能デバッグでの配列としてのポインターのサイズ指定子

オブジェクトに対するポインターを配列として表示する場合、整数で配列要素数を指定できます。

|指定子|形式|正規表現|表示される値|
|---------------|------------|----------------|---------------------|
|n|10 進整数|pBuffer[32]|`pBuffer` を 32 要素の配列として表示します。|
