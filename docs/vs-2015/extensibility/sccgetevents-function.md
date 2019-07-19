---
title: SccGetEvents 関数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccGetEvents
helpviewer_keywords:
- SccGetEvents function
ms.assetid: 32f8147d-6dcc-465e-b07b-42da5824f9b0
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d975570334aeab7c6709db92f3240a8e8d06b131
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68200113"
---
# <a name="sccgetevents-function"></a>SccGetEvents 関数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

この関数は、キューに置かれた状態のイベントを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
SCCRTN SccGetEvents (  
   LPVOID pvContext,  
   LPSTR  lpFileName,  
   LPLONG lpStatus,  
   LPLONG pnEventsRemaining  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 pvContext  
 [in]ソース管理プラグイン コンテキスト構造体。  
  
 lpFileName  
 [入力、出力]ソース管理プラグインが (最大 _MAX_PATH 文字) 返されたファイル名を格納するバッファー。  
  
 lpStatus  
 [入力、出力]ステータス コードを返します (を参照してください[ファイルの状態コード](../extensibility/file-status-code-enumerator.md)使用可能な値)。  
  
 pnEventsRemaining  
 [入力、出力]この呼び出しの後にキューに残ってエントリの数を返します。 呼び出し元を呼び出すことがこの数値が大きい場合、 [SccQueryInfo](../extensibility/sccqueryinfo-function.md)情報を一度にすべてを取得します。  
  
## <a name="return-value"></a>戻り値  
 この関数のソース管理プラグイン実装は、次の値のいずれかを返すが必要です。  
  
|[値]|説明|  
|-----------|-----------------|  
|SCC_OK|成功したイベントを取得します。|  
|SCC_E_OPNOTSUPPORTED|この関数はサポートされません。|  
|SCC_E_NONSPECIFICERROR|不特定のエラーです。|  
  
## <a name="remarks"></a>Remarks  
 この関数は加えられていないかどうか、ソース管理下にあるファイルのステータスの更新を表示するアイドル状態の処理中に呼び出されます。 ソース管理プラグインが把握しているすべてのファイルの状態を維持し、変更されるたびに状態が記載されています、プラグインによって状態と関連付けられているファイルは、キューに格納されます。 ときに`SccGetEvents`を呼び出すと、上部、キューの要素が取得され、返されます。 この関数は以前にキャッシュされた情報のみを返すに制限し、非常に高速ターンアラウンド (なし、ディスクの読み取りが、ソース管理システムの状態を求める); 必要があります。それ以外の場合、IDE のパフォーマンスが低下する開始します。  
  
 レポートにステータスの更新がない場合は、ソース管理プラグインは空の文字列を指すバッファーに格納`lpFileName`します。 それ以外の場合、プラグインの完全なパスの名前を格納、ファイルには、状態情報が変更された適切な状態コードを返します (に記載された値の 1 つ[ファイルの状態コード](../extensibility/file-status-code-enumerator.md))。  
  
## <a name="see-also"></a>関連項目  
 [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)   
 [ファイルの状態コード](../extensibility/file-status-code-enumerator.md)
