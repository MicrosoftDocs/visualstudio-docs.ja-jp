---
title: カウンター | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: aa4b4cdb-e6ea-433a-9579-56f3785e1385
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 16a16e76e2556549f428e1ef6554a3ff2c2a29ab
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2019
ms.locfileid: "53835371"
---
# <a name="counter"></a>カウンター
**Counter** オプションは、プロセッサ (ハードウェア) のパフォーマンス カウンターからデータを収集します。  
  
- サンプリング プロファイリング メソッドを使っているときは、**Counter** でオンチップ パフォーマンス カウンターと、サンプリング間隔として使うカウンター イベントの数を指定します。 サンプリングを使っているときは、指定できるカウンターは 1 つだけです。  
  
- インストルメンテーション プロファイリング メソッドを使っているときは、前回と今回の収集イベントの間に発生したカウンター イベントの数が、プロファイラー レポートでは独立したフィールドとして表示されます。 インストルメンテーションを使っている場合は、複数の **Counter** オプションを指定できます。  
  
  プロセッサの種類ごとに、ハードウェア パフォーマンス カウンターの固有のセットがあります。 プロファイラーでは、ほぼすべてのプロセッサに共通する汎用パフォーマンス カウンターのセットが定義されています。 コンピューターの汎用カウンターおよびプロセッサ固有カウンターの一覧を見るには、VSPerfCmd **QueryCounters** コマンドを使ってください。  
  
## <a name="syntax"></a>構文  
  
```cmd  
VSPerfCmd.exe {/Launch:AppName | /Attach PID} /Counter:Name[,Reload[,FriendlyName]][Options]  
```  
  
```cmd  
VSPerfCmd.exe /Start:Method /Counter:Name[,Reload[,FriendlyName]][/Counter:Name[,Reload[,FriendlyName]]][Options]  
```  
  
#### <a name="parameters"></a>パラメーター  
 `Name`  
 カウンターの名前。 コンピューターで使用可能なカウンターの名前の一覧を表示するには、VSPerfCmd.exe の **/QueryCounters** オプションを使ってください。  
  
 `Reload`  
 サンプリング間隔におけるカウンター イベントの数。 インストルメンテーション メソッドでは使わないでください。  
  
 `FriendlyName`  
 (省略可能) プロファイラーのレポートおよびビューの列見出しで `Name` の代わりに使う文字列。  
  
## <a name="required-options"></a>必須オプション  
 Counter オプションは、次のいずれかのオプションと併用することだけが可能です。  
  
 **Start:** `Trace`  
 インストルメンテーション メソッドを使うようにプロファイラーを初期化します。  
  
 **Launch:** `AppName`  
 指定したアプリケーションとプロファイラーを開始します。 プロファイラーは、サンプリング メソッドを使うように初期化する必要があります。  
  
 **Attach:** `PID`  
 プロファイラーを開始し、プロセス ID で指定したプロセスにアタッチします。 プロファイラーは、サンプリング メソッドを使うように初期化する必要があります。  
  
## <a name="example"></a>例  
 サンプリング メソッドの例では、汎用プロファイラー カウンター NonHaltedCycles が 1000 回発生するごとにアプリケーションをサンプリングする方法を示します。  
  
 インストルメンテーション メソッドの例では、L2InstructionFetches カウンター イベントを収集するようにプロファイラーを初期化する方法を示します。 L2InstructionFetches というカウンター名はプロセッサに固有です。  
  
```cmd  
; Sample Method Example  
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp  
VSPerfCmd.exe /Launch:TestApp.exe /Counter:NonHaltedCycles,1000,"Non-Halted Cycles"  
  
;INSTRUMENTATION METHOD EXAMPLE  
VSPerfCmd.exe /Start:Trace /Output:TestApp.exe.vsp /Counter:L2InstructionFetches,,"L2 Cache Instruction Fetches"  
```  
  
## <a name="see-also"></a>関連項目  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [スタンドアロン アプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)