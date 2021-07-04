---
description: この関数は、ソース管理システムで現在のファイル (ローカル ディスク上) と最後にチェックインされたバージョンとの差異を表示します (または必要に応じて差異の有無の確認のみを行います)。
title: SccDiff 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccDiff
helpviewer_keywords:
- SccDiff function
ms.assetid: d49bc8c5-f631-4153-9d3c-feb3564da305
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 484d8b5e988ede9b50099e3c0376f2c3afce8317
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904657"
---
# <a name="sccdiff-function"></a>SccDiff 関数
この関数は、ソース管理システムで現在のファイル (ローカル ディスク上) と最後にチェックインされたバージョンとの差異を表示します (または必要に応じて差異の有無の確認のみを行います)。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccDiff(
   LPVOID    pvContext,
   HWND      hWnd,
   LPCSTR    lpFileName,
   LONG      fOptions,
   LPCMDOPTS pvOptions
);
```

### <a name="parameters"></a>パラメーター
 pvContext

[入力] ソース管理プラグインのコンテキスト構造体。

 hWnd

[入力] ソース管理プラグインが、提供するすべてのダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 lpFileName

[入力] 差異が要求されるファイルの名前。

 fOptions

[入力] コマンド フラグ。 詳細については、「解説」を参照してください。

 pvOptions

[入力] ソース管理プラグイン固有のオプション。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値が返されることが予期されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|作業コピーとサーバー バージョンは同一です。|
|SCC_I_FILESDIFFERS|作業コピーは、ソース管理下のバージョンとは異なります。|
|SCC_I_RELOADFILE|ファイルまたはプロジェクトを再度読み込む必要があります。|
|SCC_E_FILENOTCONTROLLED|ファイルはソース管理されていません。|
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作の実行が許可されていません。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセス中に問題が発生しました。ネットワークまたは競合の問題が原因になっている可能性があります。 再試行することをお勧めします。|
|SCC_E_NONSPECIFICERROR|不特定のエラーです。ファイルの差異は取得されませんでした。|
|SCC_E_FILENOTEXIST|ローカル ファイルが見つかりませんでした。|

## <a name="remarks"></a>解説
 この関数は、2 つの異なる目的を果たします。 既定では、ファイルに対する変更の一覧が表示されます。 ソース管理プラグインは、選択した形式で独自のウィンドウを開き、ディスク上のユーザーのファイルと、ソース管理下にあるファイルの最新バージョンとの差異を表示します。

 または、IDE で、単にファイルが変更されたかどうかを判断する必要がある場合があります。 たとえば、IDE では、ユーザーに通知することなくファイルをチェックアウトしても安全かどうかを判断する必要がある場合があります。 その場合は、IDE によって `SCC_DIFF_CONTENTS` フラグが渡されます。 ソース管理プラグインでは、ソース管理下にあるファイルに対してディスク上のファイルをバイト単位でチェックし、ユーザーに何も表示せずに 2 つのファイルが異なるかどうかを示す値を返す必要があります。

 パフォーマンスを最適化するために、ソース管理プラグインでは、`SCC_DIFF_CONTENTS` によって要求されるバイト単位の比較ではなく、チェックサムまたはタイムスタンプに基づく代替策を使用する場合があります。この形式の比較は明らかに高速ですが、信頼性は低くなります。 すべてのソース管理システムでこれらの代替の比較方法がサポートされるとは限りません。また、プラグインでコンテンツ比較へのフォールバックが必要になる場合があります。 すべてのソース管理プラグインで、少なくともコンテンツ比較をサポートしている必要があります。

> [!NOTE]
> クイック差分フラグは相互に排他的です。 フラグを渡さないことは有効ですが、複数を同時に渡すことは有効ではありません。 すべてのフラグを組み合わせたマスクである `SCC_DIFF_QUICK_DIFF` は、テストに使用できますが、パラメーターとしては渡さないようにする必要があります。

|`fOption`|説明|
|---------------|-------------|
|SCC_DIFF_IGNORECASE|大文字と小文字を区別しない比較 (クイックまたはビジュアルな差異に使用できます)。|
|SCC_DIFF_IGNORESPACE|空白を無視します (クイックまたはビジュアルな差異に使用できます)。|
|SCC_DIFF_QD_CONTENTS|ファイルをバイト単位で自動的に比較します。|
|SCC_DIFF_QD_CHECKSUM|サポートされている場合は、チェックサムを使用してファイルを自動的に比較します。 サポートされていない場合は、コンテンツの比較にフォールバックします。|
|SCC_DIFF_QD_TIME|サポートされている場合は、タイムスタンプを使用してファイルを自動的に比較します。 サポートされていない場合は、コンテンツの比較にフォールバックします。|

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
