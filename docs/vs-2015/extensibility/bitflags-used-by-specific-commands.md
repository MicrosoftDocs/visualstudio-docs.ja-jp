---
title: 特定のコマンドで使用されるビットフラグ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, bitflags used by specific commands
ms.assetid: 37969977-6f7d-45c9-ba03-1306ae71f5d1
caps.latest.revision: 25
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 43dc083812bc172fe4a9f80335742b3faab2e1f4
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58975145"
---
# <a name="bitflags-used-by-specific-commands"></a>特定のコマンドで使用されるビットフラグ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

1 つの値で 1 つ以上のビットを設定して、さまざまなソース管理プラグイン API の関数の動作を変更できます。 これらの値は、ビットフラグと呼ばれます。 ソース管理プラグイン API によって使用されるビットフラグのさまざまな詳細についてはここでは、それらを使用する関数によってグループ化します。  
  
## <a name="checked-out-flag"></a>チェック アウト フラグ  
 いずれかのこのフラグを設定することができます、 [SccAdd](../extensibility/sccadd-function.md)または[SccCheckin](../extensibility/scccheckin-function.md)します。  
  
|フラグ|[値]|説明|  
|----------|-----------|-----------------|  
|`SCC_KEEP_CHECKEDOUT`|0x1000|ファイルをチェック アウトしてください。|  
  
## <a name="add-flags"></a>フラグを追加します。  
 これらのフラグを使って、 [SccAdd](../extensibility/sccadd-function.md)します。  
  
|フラグ|[値]|説明|  
|----------|-----------|-----------------|  
|`SCC_FILETYPE_AUTO`|0x00|ソース管理プラグインは、ファイルがテキストかバイナリかどうかを自動的に検出するために必要です。|  
|`SCC_FILETYPE_TEXT`|0x01|ファイルの種類は、テキストです。|  
|`SCC_FILETYPE_BINARY`|0x04|ファイルの種類はバイナリです。 **注:** `SCC_FILETYPE_TEXT`と`SCC_FILETYPE_BINARY`フラグが相互に排他的です。 1 つだけ、またはどちらも設定します。|  
|`SCC_ADD_STORELATEST`|0x02|最新のバージョンのみ (デルタではありません) を格納します。|  
  
## <a name="diff-flags"></a>Diff フラグ  
 [SccDiff](../extensibility/sccdiff-function.md)これらのフラグを使用して、diff 操作のスコープを定義します。 `SCC_DIFF_QD_xxx`フラグが相互に排他的です。 いずれかのファイルが指定されている場合、視覚的なフィードバックはありませんを指定します。 "クイック diff"で (QD) プラグインによって決定されないファイルが異なる場合のみです。 これらのフラグを指定されていない場合、"visual diff"が行われます。詳細なファイルの相違点が計算され、表示されます。 要求された QD がサポートされていない場合、[次へ] の最適なものには、プラグインのことが移動します。 たとえば、IDE、チェックサムを要求するプラグインがサポートしていない場合は、プラグインは完全な内容を確認 (まだより速く視覚的に表示) します。  
  
|フラグ|[値]|説明|  
|----------|-----------|-----------------|  
|`SCC_DIFF_IGNORECASE`|0x0002|大文字小文字の違いを無視します。|  
|`SCC_DIFF_IGNORESPACE`|0x0004|空白の相違を無視します。 **注:**`SCC_DIFF_IGNORECASE`と`SCC_DIFF_IGNORESPACE`フラグは省略可能なビットフラグします。|  
|`SCC_DIFF_QD_CONTENTS`|0x0010|ファイルの内容全体を比較することによって QD します。|  
|`SCC_DIFF_QD_CHECKSUM`|0x0020|チェックサムによって QD します。|  
|`SCC_DIFF_QD_TIME`|0x0040|ファイルの日付/時刻スタンプによって QD します。|  
|`SCC_DIFF_QUICK_DIFF`|0x0070|これは、すべての QD ビットフラグを確認するために使用するマスクです。 関数に渡すことはできません次の 3 つの QD ビットフラグは相互に排他的です。 QD には、UI の表示を常に意味するものはありません。|  
  
## <a name="populatelist-flag"></a>PopulateList フラグ  
 このフラグを使用して、 [SccPopulateList](../extensibility/sccpopulatelist-function.md)で、`fOptions`パラメーター。  
  
|フラグ|[値]|説明|  
|----------|-----------|-----------------|  
|`SCC_PL_DIR`|0x00000001L|IDE がファイルではなく、ディレクトリを渡すことです。|  
  
## <a name="populatedirlist-flags"></a>PopulateDirList フラグ  
 これらのフラグを使って、 [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)で、`fOptions`パラメーター。  
  
|オプションの値|[値]|説明|  
|------------------|-----------|-----------------|  
|SCC_PDL_ONELEVEL|0x0000|(これは、既定値) のディレクトリのディレクトリの 1 つだけのレベルを確認します。|  
|SCC_PDL_RECURSIVE|0x0001|再帰的には、指定された各ディレクトリの下のすべてのディレクトリを確認します。|  
|SCC_PDL_INCLUDEFILES|0x0002|検査プロセスで ファイル名が含まれます。|  
  
## <a name="openproject-flags"></a>プロジェクトを開くフラグ  
 これらのフラグを使って、 [SccOpenProject](../extensibility/sccopenproject-function.md)で、`dwFlags`パラメーター。  
  
|オプションの値|[値]|説明|  
|------------------|-----------|-----------------|  
|SCC_OP_CREATEIFNEW|0x00000001L|ソース管理にプロジェクトが存在しない場合は、それを作成します。 このフラグが設定されていない場合は、プロジェクトを作成するには、ユーザーを求める (しない限り、`SCC_OP_SILENTOPEN`フラグを指定)。|  
|SCC_OP_SILENTOPEN|0x00000002L|プロジェクトを作成するユーザーに確認しません。戻り値`SCC_E_UNKNOWNPROJECT`します。|  
  
## <a name="get-flags"></a>フラグを取得します。  
 これらのフラグを使って、 [SccGet](../extensibility/sccget-function.md)と[SccCheckout](../extensibility/scccheckout-function.md)します。  
  
|フラグ|[値]|説明|  
|----------|-----------|-----------------|  
|`SCC_GET_ALL`|0x00000001L|IDE は、ディレクトリ、ファイルではなく渡すことは。これらのディレクトリ内のすべてのファイルを取得します。|  
|`SCC_GET_RECURSIVE`|0x00000002L|IDE では、ディレクトリを渡します。これらのディレクトリとそのすべてのサブディレクトリを取得します。|  
  
## <a name="noption-values"></a>nOption 値  
 これらのフラグを使って、 [SccSetOption](../extensibility/sccsetoption-function.md)で、`nOption`パラメーター。  
  
|フラグ|[値]|説明|  
|----------|-----------|-----------------|  
|`SCC_OPT_EVENTQUEUE`|0x00000001L|イベント キューの状態を設定します。|  
|`SCC_OPT_USERDATA`|0x00000002L|ユーザーのデータを指定`SCC_OPT_NAMECHANGEPFN`します。|  
|`SCC_OPT_HASCANCELMODE`|0x00000003L|IDE がキャンセルを処理できます。|  
|`SCC_OPT_NAMECHANGEPFN`|0x00000004L|名前の変更についてコールバックを設定します。|  
|`SCC_OPT_SCCCHECKOUTONLY`|0x00000005L|ソース管理のプラグイン UI チェック アウトを無効にし、作業ディレクトリを設定しないでください。|  
|`SCC_OPT_SHARESUBPROJ`|0x00000006L|作業ディレクトリを指定するソース管理システムから追加します。 直接の子孫である場合は、関連付けられているプロジェクトに共有しようとしてください。|  
  
## <a name="dwval-bitflags"></a>dwVal ビットフラグ  
 これらのフラグを使って、 [SccSetOption](../extensibility/sccsetoption-function.md)で、`dwVal`パラメーター。  
  
|フラグ|[値]|説明|使用される`nOption`値|  
|----------|-----------|-----------------|-----------------------------|  
|`SCC_OPT_EQ_DISABLE`|0x00L|イベント キューのアクティビティを中断します。|`SCC_OPT_EVENTQUEUE`|  
|`SCC_OPT_EQ_ENABLE`|0x01L|イベント キューのログ記録を有効にします。|`SCC_OPT_EVENTQUEUE`|  
|`SCC_OPT_HCM_NO`|0L|(既定値)[キャンセル] モードがありません。プラグインする必要があります指定が必要な場合。|`SCC_OPT_HASCANCELMODE`|  
|`SCC_OPT_HCM_YES`|1L|IDE では、キャンセルを処理します。|`SCC_OPT_HASCANCELMODE`|  
|`SCC_OPT_SCO_NO`|0L|(既定値)プラグイン UI からチェック アウトするには、[ok]作業ディレクトリが設定されます。|`SCC_OPT_SCCCHECKOUTONLY`|  
|`SCC_OPT_SCO_YES`|1L|ないプラグイン UI チェック アウト、作業ディレクトリがありません。|`SCC_OPT_SCCCHECKOUTONLY`|  
  
## <a name="see-also"></a>関連項目  
 [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
