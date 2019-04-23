---
title: 単体テスト プロジェクトを作成する | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: a608bfba-1a43-4a60-b73a-1fe53ef58098
caps.latest.revision: 10
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: ca472a8db08f337d873f0e43475a9231f2999b13
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60096622"
---
# <a name="create-a-unit-test-project"></a>単体テスト プロジェクトを作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

単体テストでは、多くの場合、テスト対象のコードの構造を再現します。 たとえば、製品のコード プロジェクトごとに単体テスト プロジェクトを作成します。 テスト プロジェクトは本稼働コードと同じソリューションに置くことも、別個のソリューションに置くこともできます。 1 つのソリューションに複数の単体テスト プロジェクトを置くこともできます。  
  
> [!NOTE]
>  ネイティブ コードの単体テストの場所とテスト プロジェクトの構造は、このトピックの説明にある構造とは異なっていても構いません。 詳細については、「[既存の C++ アプリケーションへの単体テストの追加](../test/unit-testing-existing-cpp-applications-with-test-explorer.md)」を参照してください。  
  
## <a name="to-create-a-unit-test-project"></a>単体テスト プロジェクトを作成するには:  
  
1. **[ファイル]** メニューの **[新規作成]** をクリックし、 **[プロジェクト]** をクリックします (キーボード: Ctrl + Shift + N)。  
  
2. [新しいプロジェクト] ダイアログ ボックスで、**[インストール済み]** ノードを展開して、テスト プロジェクトで使用する言語を選択し、**[テスト]** をクリックします。  
  
3. Microsoft 単体テスト フレームワークの 1 つを使用するには、プロジェクト テンプレートの一覧から **[単体テスト プロジェクト]** を選択します。 それ以外の場合は、使用する単体テスト フレームワークのプロジェクト テンプレートを選択します。 この例の Accounts プロジェクトをテストするために、プロジェクトの名前を AccountsTests に設定します。  
  
4. 単体テスト プロジェクトに、テスト対象のコードへの参照を追加します。  同じソリューションのコード プロジェクトへの参照を作成する方法は次のようになります。  
  
    1. ソリューション エクスプローラーでプロジェクトを選択します。  
  
    2. **[プロジェクト]** メニューの **[参照の追加]** をクリックします。  
  
    3. [参照マネージャー] ダイアログ ボックスで、**[ソリューション]** ノードを開き、**[プロジェクト]** を選択します。 コード プロジェクトの名前を選択し、ダイアログ ボックスを閉じます。  
  
5. テストするコードが別の場所にある場合、「[プロジェクト内の参照の管理](../ide/managing-references-in-a-project.md)」を参照してください。  
  
## <a name="next-steps"></a>次の手順  
 **単体テストの記述**  
  
 次のいずれかのセクションを参照してください。  
  
- [マネージド コード用の Microsoft 単体テスト フレームワークを使用した .NET Framework 用単体テストの記述](../test/writing-unit-tests-for-the-dotnet-framework-with-the-microsoft-unit-test-framework-for-managed-code.md)  
  
- [C++ 用の Microsoft 単体テスト フレームワークを使用した C++ 用単体テストの記述](../test/writing-unit-tests-for-c-cpp-with-the-microsoft-unit-testing-framework-for-cpp.md)  
  
  **単体テストの実行**  
  
  [テスト エクスプローラーを使用して単体テストを実行する](../test/run-unit-tests-with-test-explorer.md)
