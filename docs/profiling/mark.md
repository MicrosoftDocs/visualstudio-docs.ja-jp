---
title: Mark | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 1d72cef3-bb09-4bbb-8864-6ea0ab623ff9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 440401f8c46a3920fce6c8e0d29f630a24103f65
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62999989"
---
# <a name="mark"></a>Mark
*VSPerfCmd.exe* の **Mark** オプションは、プロファイル データ ファイルに指定した情報を挿入します。 マークは個別の VSPerfReport レポートまたはプロファイラー UI のマーク レポート ビューに一覧表示できます。 **Mark** を使用して、レポートおよびビュー フィルターの開始点と終了点を指定できます。

 コマンド ラインで指定するオプションは **Mark** オプションのみにする必要があります。

## <a name="syntax"></a>構文

```cmd
VSPerfCmd.exe /Mark:MarkID,[MarkName]
```

#### <a name="parameters"></a>パラメーター
 `MarkID` プロファイラー ビューおよびレポートにマーク ID として一覧表示される、ユーザー定義の整数。 `MarkID` は一意である必要はありません。

 `MarkName` (省略可能) プロファイラー ビューおよびレポートにマーク名として一覧表示される、ユーザー定義の文字列。 `MarkName` が指定されていない場合、マーク一覧のマーク名フィールドは空になります。 スペースやスラッシュ ("/") を含む文字列は引用符で囲みます。

## <a name="example"></a>例
 この例では、ID が 123 でマーク名が "TestMark" というマークを挿入します。

```cmd
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp
VSPerfCmd.exe /Launch:TestApp.exe
VSPerfCmd.exe /Mark:123,TestMark
```

## <a name="see-also"></a>関連項目
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [スタンドアロン アプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)