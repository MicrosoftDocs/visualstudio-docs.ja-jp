---
title: '方法: ビルドからプロジェクトを除外する'
ms.date: 11/04/2016
ms.technology: vs-ide-compile
ms.topic: conceptual
ms.assetid: 17a837ca-5db9-46cd-b5a7-b14ad1d2c47d
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a19c49482c45aa0a3cf5d7cb33eb106adb65b83b
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "76114803"
---
# <a name="how-to-exclude-projects-from-a-build"></a>方法: ビルドからプロジェクトを除外する

ソリューションをビルドするために、含まれるすべてのプロジェクトをビルドする必要はありません。 たとえば、ビルドを中断するプロジェクトを除外できます。 その後、問題の調査と対処を行ってからプロジェクトをビルドすることができます。

次の方法を実行することでプロジェクトを除外できます。

- アクティブなソリューション構成からプロジェクトを一時的に削除する。

- 対象プロジェクトを含まないソリューション構成を作成する。

詳しくは、「[ビルド構成について](../ide/understanding-build-configurations.md)」をご覧ください。

## <a name="to-temporarily-remove-a-project-from-the-active-solution-configuration"></a>アクティブなソリューション構成からプロジェクトを一時的に削除するには

1. メニュー バーで **[ビルド]**  >  **[構成マネージャー]** の順に選択します。

2. **[プロジェクトのコンテキスト]** テーブルで、ビルドから除外するプロジェクトを見つけます。

3. プロジェクトの **[ビルド]** 列で、チェック ボックスをオフにします。

4. **[閉じる]** を選択し、ソリューションをリビルドします。

## <a name="to-create-a-solution-configuration-that-excludes-a-project"></a>プロジェクトを除外するソリューション構成を作成するには

1. メニュー バーで **[ビルド]**  >  **[構成マネージャー]** の順に選択します。

2. **[アクティブ ソリューション構成]** 一覧の **[\<新規作成>]** を選択します。

3. **[名前]** ボックスに、ソリューション構成の名前を入力します。

4. **[設定のコピー元]** ボックスの一覧で、新しい構成のベースにするソリューション構成 ( **[デバッグ]** など) を選択し、 **[OK]** を選択します。

5. **[構成マネージャー]** ダイアログ ボックスで、除外するプロジェクトの **[ビルド]** 列のチェック ボックスをオフにし、 **[閉じる]** を選択します。

6. **[標準]** ツール バーで、 **[ソリューション構成]** ボックスのアクティブな構成が、新しいソリューション構成であることを確認します。

7. メニュー バーから、 **[ビルド]**  >  **[ソリューションのリビルド]** の順に選びます。

## <a name="skipped-projects"></a>スキップされたプロジェクト

ビルド中にプロジェクトがスキップされる場合があります。これらのプロジェクトは最新ではないか、構成から除外されているためです。 Visual Studio では、MSBuild を使用してプロジェクトをビルドします。 ファイルのタイムスタンプから判断して、出力が入力よりも古い場合、MSBuild はターゲットのみをビルドします。 強制的にリビルドするには、コマンド **[ビルド]**  >  **[ソリューションのリビルド]** を使用します。

Visual Studio の **[出力]** ウィンドウの **[ビルド]** ペインでは、最新であったプロジェクトの数、正常にビルドされた数、失敗した数、スキップされた数が報告されます。 スキップされた数に、最新だったためにビルドされなかったプロジェクトは含まれません。 アクティブな構成から除外されたプロジェクトは、ビルド時にスキップされます。 ビルド出力には、プロジェクトがスキップされることを示すメッセージが表示されます。

```output
2>------ Skipped Build: Project: ConsoleApp2, Configuration: Debug x86 ------
2>Project not selected to build for this solution configuration
```

プロジェクトがスキップされた理由を確認するには、アクティブな構成 (前の例では `Debug x86`) を見つけ、 **[ビルド]**  >  **[構成マネージャー]** を選択します。 この記事で説明されているように、構成ごとにスキップされるプロジェクトを表示または変更できます。

## <a name="see-also"></a>参照

- [ビルド構成について](../ide/understanding-build-configurations.md)
- [方法: 構成を作成および編集する](../ide/how-to-create-and-edit-configurations.md)
- [方法: 複数の構成を同時にビルドする](../ide/how-to-build-multiple-configurations-simultaneously.md)
