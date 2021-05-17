---
title: 式エバリュエーターの登録 |Microsoft Docs
description: 式エバリュエーターが、Windows COM 環境と Visual Studio の両方を備えたクラス ファクトリとして自身を登録する方法を説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluators, registering
ms.assetid: 236be234-e05f-4ad8-9200-24ce51768ecf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3cf6998a9dd8bc521d8d5c7b8bd3e598e9a4e3bc
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070649"
---
# <a name="register-an-expression-evaluator"></a>式エバリュエーターを登録する
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)に関する記事と[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

 式エバリュエーター (EE) は、Windows COM 環境と Visual Studio の両方を備えたクラス ファクトリとして自身を登録する必要があります。 EE は DLL として設定されるため、どちらのエンティティによって EE がインスタンス化されるかに応じて、デバッグエンジン (DE) アドレス空間または Visual Studio アドレス空間に挿入されます。

## <a name="managed-code-expression-evaluator"></a>マネージド コード式エバリュエーター
 マネージド コード EE はクラス ライブラリとして実装されます。このライブラリは、COM 環境にそれ自体を登録する DLL、*regpkg.exe* であり、通常、VSIP プログラムの呼び出しによって開始されます。 COM 環境のレジストリ キーを書き込む実際のプロセスは、自動的に処理されます。

 メイン クラスのメソッドは <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute> でマークされます。これは、DLL が COM に登録されているときにメソッドが呼び出されることを示します。 この登録方法は、多くの場合、`RegisterClass` と呼ばれ、Visual Studio に DLL を登録するタスクを実行します。 対応する `UnregisterClass` (<xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute> でマークされた) は、DLL がアンインストールされると、`RegisterClass` の効果を元に戻します。
同じレジストリ エントリが、アンマネージド コードで記述された EE に対して作成されます。唯一の違いは、`SetEEMetric` など、作業を行うためのヘルパー関数がないことです。 登録と登録解除のプロセスの例を次に示します。

### <a name="example"></a>例
 次の関数は、マネージド コード EE が Visual Studio に自身を登録および登録解除する方法を示しています。

```csharp
namespace EEMC
{
    [GuidAttribute("462D4A3D-B257-4AEE-97CD-5918C7531757")]
    public class EEMCClass : IDebugExpressionEvaluator
    {
        #region Register and unregister.
        private static Guid guidMycLang = new Guid("462D4A3E-B257-4AEE-97CD-5918C7531757");
        private static string languageName = "MyC";
        private static string eeName = "MyC Expression Evaluator";

        private static Guid guidMicrosoftVendor = new Guid("994B45C4-E6E9-11D2-903F-00C04FA302A1");
        private static Guid guidCOMPlusOnlyEng = new Guid("449EC4CC-30D2-4032-9256-EE18EB41B62B");
        private static Guid guidCOMPlusNativeEng = new Guid("92EF0900-2251-11D2-B72E-0000F87572EF");

        /// <summary>
        /// Register the expression evaluator.
        /// Set "project properties/configuration properties/build/register for COM interop" to true.
        /// </summary>
         [ComRegisterFunctionAttribute]
        public static void RegisterClass(Type t)
        {
            // Get Visual Studio version (set by regpkg.exe)
            string hive = Environment.GetEnvironmentVariable("EnvSdk_RegKey");
            string s = @"SOFTWARE\Microsoft\VisualStudio\"
                        + hive
                        + @"\AD7Metrics\ExpressionEvaluator";

            RegistryKey rk = Registry.LocalMachine.CreateSubKey(s);
            if (rk == null)  return;

            rk = rk.CreateSubKey(guidMycLang.ToString("B"));
            rk = rk.CreateSubKey(guidMicrosoftVendor.ToString("B"));
            rk.SetValue("CLSID", t.GUID.ToString("B"));
            rk.SetValue("Language", languageName);
            rk.SetValue("Name", eeName);

            rk = rk.CreateSubKey("Engine");
            rk.SetValue("0", guidCOMPlusOnlyEng.ToString("B"));
            rk.SetValue("1", guidCOMPlusNativeEng.ToString("B"));
        }
        /// <summary>
        /// Unregister the expression evaluator.
        /// </summary>
         [ComUnregisterFunctionAttribute]
        public static void UnregisterClass(Type t)
        {
            // Get Visual Studio version (set by regpkg.exe)
            string hive = Environment.GetEnvironmentVariable("EnvSdk_RegKey");
            string s = @"SOFTWARE\Microsoft\VisualStudio\"
                        + hive
                        + @"\AD7Metrics\ExpressionEvaluator\"
                        + guidMycLang.ToString("B");
            RegistryKey key = Registry.LocalMachine.OpenSubKey(s);
            if (key != null)
            {
                key.Close();
                Registry.LocalMachine.DeleteSubKeyTree(s);
            }
        }
    }
}
```

## <a name="unmanaged-code-expression-evaluator"></a>アンマネージド コード式エバリュエーター
 EE DLL は、Visual Studio だけでなく、COM 環境にも自身を登録する `DllRegisterServer` 関数を実装しています。

> [!NOTE]
> MyCEE コード サンプル レジストリ コードは、EnVSDK\MyCPkgs\MyCEE の下にインストールされた VSIP 内にあるファイル *dllentry.cpp* にあります。

### <a name="dll-server-process"></a>DLL サーバー プロセス
 EE を登録すると、DLL サーバーは以下を行います。

1. 通常の COM 規約に従って、自身のクラス ファクトリ `CLSID` を登録します。

2. ヘルパー関数 `SetEEMetric` を呼び出して、次の表に示す EE メトリックを Visual Studio に登録します。 次のように指定された関数 `SetEEMetric` とメトリックは、*dbgmetric.lib* ライブラリの一部です。 詳細については、「[デバッグ用 SDK ヘルパー](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)」を参照してください。

    |メトリック|説明|
    |------------|-----------------|
    |`metricCLSID`|EE クラス ファクトリの `CLSID`|
    |`metricName`|表示可能な文字列としての EE の名前|
    |`metricLanguage`|EE による評価の対象となる言語の名前|
    |`metricEngine`|この EE で動作するデバッグ エンジン (DE) の `GUID`|

    > [!NOTE]
    > `metricLanguage``GUID` は、言語を名前で識別しますが、言語を選択するのは、`SetEEMetric` への `guidLang` 引数です。 コンパイラは、デバッグ情報ファイルを生成するときに、適切な `guidLang` を記述して、どの EE を使用するかを DE に認識させる必要があります。 通常、DE はシンボル プロバイダーにこの言語 `GUID` を要求します。この言語は、デバッグ情報ファイルに格納されます。

3. HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\*X.Y* の下にキーを作成して Visual Studio に登録 します。ここで、*X.Y* は、登録先の Visual Studio のバージョンです。

### <a name="example"></a>例
 次の関数は、アンマネージド コード (C++) EE が Visual Studio に自身を登録および登録解除する方法を示しています。

```cpp
/*---------------------------------------------------------
  Registration
-----------------------------------------------------------*/
#ifndef LREGKEY_VISUALSTUDIOROOT
    #define LREGKEY_VISUALSTUDIOROOT L"Software\\Microsoft\\VisualStudio\\8.0"
#endif

static HRESULT RegisterMetric( bool registerIt )
{
    // check where we should register
    const ULONG cchBuffer = _MAX_PATH;
    WCHAR wszRegistrationRoot[cchBuffer];
    DWORD cchFreeBuffer = cchBuffer - 1;
    wcscpy(wszRegistrationRoot, LREGKEY_VISUALSTUDIOROOT_NOVERSION);
    wcscat(wszRegistrationRoot, L"\\");

    // this is Environment SDK specific
    // we check for  EnvSdk_RegKey environment variable to
    // determine where to register
    DWORD cchDefRegRoot = lstrlenW(LREGKEY_VISUALSTUDIOROOT_NOVERSION) + 1;
    cchFreeBuffer = cchFreeBuffer - cchDefRegRoot;
    DWORD cchEnvVarRead = GetEnvironmentVariableW(
        /* LPCTSTR */ L"EnvSdk_RegKey", // environment variable name
        /* LPTSTR  */ &wszRegistrationRoot[cchDefRegRoot],// buffer for variable value
        /* DWORD   */ cchFreeBuffer);// size of buffer
    if (cchEnvVarRead >= cchFreeBuffer)
        return E_UNEXPECTED;
    // If the environment variable does not exist then we must use
    // LREGKEY_VISUALSTUDIOROOT which has the version number.
    if (0 == cchEnvVarRead)
        wcscpy(wszRegistrationRoot, LREGKEY_VISUALSTUDIOROOT);

    if (registerIt)
    {
        SetEEMetric(guidMycLang,
                    guidMicrosoftVendor,
                    metricCLSID,
                    CLSID_MycEE,
                    wszRegistrationRoot );
        SetEEMetric(guidMycLang,
                    guidMicrosoftVendor,
                    metricName,
                    GetString(IDS_INFO_MYCDESCRIPTION),
                    wszRegistrationRoot );
        SetEEMetric(guidMycLang,
                    guidMicrosoftVendor,
                    metricLanguage, L"MyC",
                    wszRegistrationRoot);

        GUID engineGuids[2];
        engineGuids[0] = guidCOMPlusOnlyEng;
        engineGuids[1] = guidCOMPlusNativeEng;
        SetEEMetric(guidMycLang,
                    guidMicrosoftVendor,
                    metricEngine,
                    engineGuids,
                    2,
                    wszRegistrationRoot);
    }
    else
    {
        RemoveEEMetric( guidMycLang,
                        guidMicrosoftVendor,
                        metricCLSID,
                        wszRegistrationRoot);
        RemoveEEMetric( guidMycLang,
                        guidMicrosoftVendor,
                        metricName,
                        wszRegistrationRoot );
        RemoveEEMetric( guidMycLang,
                        guidMicrosoftVendor,
                        metricLanguage,
                        wszRegistrationRoot );
        RemoveEEMetric( guidMycLang,
                        guidMicrosoftVendor,
                        metricEngine,
                        wszRegistrationRoot );
    }

    return S_OK;
}
```

## <a name="see-also"></a>関連項目
- [CLR 式エバリュエーターの記述](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
- [デバッグ用 SDK ヘルパー](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
