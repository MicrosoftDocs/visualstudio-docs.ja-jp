---
title: Visual Studio でのテスト用の診断データ アダプターの作成
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- Diagnostic Data Adapter [Visual Studio ALM]
- Diagnostic Data Adapter
ms.assetid: b0b53fae-7007-4ad9-a604-21685937622f
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: a12cac4e3a0c7144fd2e2cca2044ad416ac966d0
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
ms.locfileid: "31964952"
---
# <a name="create-a-diagnostic-data-adapter-to-collect-custom-data-or-affect-a-test-machine"></a>診断データ アダプターを作成してカスタム データを収集する、またはテスト コンピューターに影響を与える

独自の診断データ アダプターを作成してテストの実行時のデータを収集することや、テストの一環としてテスト コンピューターに影響を与えることが必要になる場合があります。 たとえば、テスト中のアプリケーションによって作成されるログ ファイルを収集し、これをテスト結果にアタッチする場合、またはコンピューターの残りのディスク容量が限られている状態でテストを実行する場合があります。 Visual Studio Enterprise に用意されている API を使用すると、テストの実行中の特定時点にタスクを実行するコードを記述できます。 たとえば、テストの実行の開始時、個別のテストの実行の前後、テストの実行の完了時にタスクを実行できます。

構成設定ファイルを使用して、カスタム診断データ アダプターに既定の入力を渡すことができます。 たとえば、収集してテスト結果にアタッチするファイルの場所、またはシステムの残りのディスク容量についての情報を指定できます。 このデータは、作成するテストの設定ごとに構成できます。 これは、Microsoft Test Manager に用意されている既定のエディターを使用して表示および編集できるほか、エディターとして使用する独自のユーザー コントロールを作成することもできます。 エディターでアダプター構成に加えたすべての変更はテストの設定と共に保存されます。

Visual Studio からテストを実行する場合は、これらのテスト設定をアクティブとして設定する必要があります。 テスト設定の詳細については、「[Collect Diagnostic Information Using Test Settings](../test/collect-diagnostic-information-using-test-settings.md)」(テスト設定を使用して診断情報を収集する) を参照してください。

## <a name="tasks"></a>[タスク]

 診断データ アダプターを作成するには、次のトピックを参照してください。

|[タスク]|関連するトピック|
|-----------|-----------------------|
|**診断データ アダプターを作成する:** クラス ライブラリを作成して診断データ アダプターを作成し、次に診断データ アダプターの API を使用して、目的の情報を収集したり、テストの実行に使用するテスト システムに影響を与えたりします。|-   [方法: 診断データ アダプターを作成する](../test/how-to-create-a-diagnostic-data-adapter.md)|
|**カスタム診断データ アダプターをインストールする:** 自分または他のユーザーが作成した診断データ アダプターを適切なディレクトリにコピーすることにより、カスタム診断データ アダプターをインストールできます。|-   [方法: カスタム診断データ アダプターをインストールする](../test/how-to-install-a-custom-diagnostic-data-adapter.md)|
|**テストの実行時に使用するカスタム診断データ アダプターを選択する:** テストの設定で使用する診断データ アダプターを選択することにより、テストの実行時に使用するアダプターを指定できます。|-   [テスト中の診断データの収集 (VSTS)](/vsts/manual-test/collect-diagnostic-data)<br />-   [手動テストでの診断データの収集 (VSTS)](/vsts/manual-test/mtm/collect-more-diagnostic-data-in-manual-tests)|
|**診断データ アダプターによって実行するアクションを構成する:** 特定のテストの設定における診断データ アダプターのアクションを制御するための設定を構成できます。|-   [方法: 診断データ アダプター用のデータのカスタム エディターを作成する](../test/how-to-create-a-custom-editor-for-data-for-your-diagnostic-data-adapter.md)|

## <a name="see-also"></a>関連項目

- [診断データ アダプター作成用のサンプル プロジェクト](../test/sample-project-for-creating-a-diagnostic-data-adapter.md)
- [テスト設定を使用して診断情報を収集する](../test/collect-diagnostic-information-using-test-settings.md)