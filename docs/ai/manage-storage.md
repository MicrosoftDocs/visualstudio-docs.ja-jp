---
ms.technology: vs-ai-tools
ms.openlocfilehash: b941d0ba55c540de4bda1cb0f9c4ed18ceab524f
ms.sourcegitcommit: 8cbe6b38b810529a6c364d0f1918e5c71dee2c68
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/28/2018
---
# <a name="browse-storage-to-upload-data-or-download-models-and-logs"></a>データのアップロードまたはモデルとログのダウンロードを行うストレージを参照する

リモート マシンまたは Azure のファイル共有ですべての記憶域を参照して、データのアップロードまたはモデルとログのダウンロードを有効にすることができます。 または、特定のジョブのログ出力およびジョブ出力にアクセスする場合は、ジョブ ブラウザーからでもアクセスすることができます。

## <a name="to-access-all-data-on-the-remote-machine-or-file-share"></a>リモート マシンまたはファイル共有上のすべてのデータにアクセスするには
1. **サーバー エクスプローラー**を開きます。
2. リモート マシンまたはバッチ AI 計算コンテキストを展開します。
3. **[ストレージ]** を右クリックし、**[参照]** をクリックします。

    ![storage](media\manage-storage\browse-storage.png)

## <a name="to-access-job-specific-data-on-the-remote-machine-or-file-share"></a>リモート マシンまたはファイル共有上にあるジョブ固有のデータにアクセスするには
1. [[ジョブ履歴]](job-details.md) を開きます。
2. ジョブを選択します。
3. **[作業フォルダー]** をクリックします。あるいは、これらの重要なログ ファイルにすばやくアクセスするために [Stdout] または [Stderr] をクリックします。

    ![storage](media\manage-storage\job-workingfolder.png)
