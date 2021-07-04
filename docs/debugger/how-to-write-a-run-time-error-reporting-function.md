---
title: ランタイム エラー レポート関数を記述する | Microsoft Docs
description: Visual Studio でのカスタム ランタイム エラー レポート関数の作成の例を示します。 _CrtDbgReportW と同じ宣言を指定し、値 1 を返す必要があります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- run-time errors, reporting functions
- reporting function
ms.assetid: 989bf312-5038-44f3-805f-39a34d18760e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6ff82afdfda8af746533f07f21d330c359a1618c
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112385138"
---
# <a name="how-to-write-a-run-time-error-reporting-function-c"></a>方法: ランタイム エラー レポート関数を記述する (C++)
ランタイム エラーのカスタム レポート関数には、`_CrtDbgReportW` と同じ宣言を使用する必要があります。 デバッガーへの戻り値は 1 です。

次の例は、カスタム レポート関数の定義方法を示しています。

## <a name="example-1"></a>例 1

```cpp
#include <stdio.h>
int errorhandler = 0;
void configureMyErrorFunc(int i)
{
    errorhandler = i;
}

int MyErrorFunc(int errorType, const wchar_t *filename,
                int linenumber, const wchar_t *moduleName,
                const wchar_t *format, ...)
{
    switch (errorhandler)
    {
    case 0:
    case 1:
        wprintf(L"Error type %d at %s line %d in %s",
                errorType, filename, linenumber, moduleName);
        break;
    case 2:
    case 3:
        fprintf(stderr, "Error type");
        break;
    }

    return 1;
}
```

## <a name="example-2"></a>例 2
次の例は、より複雑なカスタム レポート関数を示しています。 この例では、switch ステートメントによって、各種のエラーが `reportType` の `_CrtDbgReportW` パラメーターの定義に従って処理されます。 `_CrtDbgReportW` を置き換えるため、`_CrtSetReportMode` は使用できません。 関数では、出力を処理する必要があります。 この関数の最初の可変個の引数には、ランタイム エラー番号を使用します。 詳細については、「[_RTC_SetErrorType](/cpp/c-runtime-library/reference/rtc-seterrortype)」を参照してください。

```cpp
#include <windows.h>
#include <stdarg.h>
#include <rtcapi.h>
#include <malloc.h>
#pragma runtime_checks("", off)
int Catch_RTC_Failure(int errType, const wchar_t *file, int line,
                      const wchar_t *module, const wchar_t *format, ...)
{
    // Prevent re-entrance.
    static long running = 0;
    while (InterlockedExchange(&running, 1))
        Sleep(0);
    // Now, disable all RTC failures.
    int numErrors = _RTC_NumErrors();
    int *errors=(int*)_alloca(numErrors);
    for (int i = 0; i < numErrors; i++)
        errors[i] = _RTC_SetErrorType((_RTC_ErrorNumber)i, _RTC_ERRTYPE_IGNORE);

    // First, get the rtc error number from the var-arg list.
    va_list vl;
    va_start(vl, format);
    _RTC_ErrorNumber rtc_errnum = va_arg(vl, _RTC_ErrorNumber);
    va_end(vl);

    wchar_t buf[512];
    const char *err = _RTC_GetErrDesc(rtc_errnum);
    swprintf_s(buf, 512, L"%S\nLine #%d\nFile:%s\nModule:%s",
        err,
        line,
        file ? file : L"Unknown",
        module ? module : L"Unknown");
    int res = (MessageBox(NULL, buf, L"RTC Failed...", MB_YESNO) == IDYES) ? 1 : 0;
    // Now, restore the RTC errortypes.
    for(int i = 0; i < numErrors; i++)
        _RTC_SetErrorType((_RTC_ErrorNumber)i, errors[i]);
    running = 0;
    return res;
}
#pragma runtime_checks("", restore)
```

## <a name="example-3"></a>例 3
`_RTC_SetErrorFuncW` の代わりにカスタム関数を組み込むには、`_CrtDbgReportW` を使用します。 詳細については、「[_RTC_SetErrorFuncW](/cpp/c-runtime-library/reference/rtc-seterrorfuncw)」を参照してください。 `_RTC_SetErrorFuncW` の戻り値は、直前のレポート関数であり、必要に応じて保存して復元できます。

```cpp
#include <rtcapi.h>
int main()
{
    _RTC_error_fnW oldfunction, newfunc;
    oldfunction = _RTC_SetErrorFuncW(&MyErrorFunc);
    // Run some code.
    newfunc = _RTC_SetErrorFuncW(oldfunction);
    // newfunc == &MyErrorFunc;
    // Run some more code.
}
```

## <a name="see-also"></a>関連項目
[ネイティブ ランタイム チェックのカスタマイズ](../debugger/native-run-time-checks-customization.md)
