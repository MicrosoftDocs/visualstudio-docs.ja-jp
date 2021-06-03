---
title: メニュー コマンドへのアイコンの追加 | Microsoft Docs
description: Visual Studio 統合開発環境 (IDE) のメニューとツール バーの両方に表示できるコマンドにアイコンを追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- icons [Visual Studio], adding to toolbars
- toolbars [Visual Studio], adding icons to commands
- commands [Visual Studio], adding icons
ms.assetid: 362a0c7e-5729-4297-a83f-1aba1a37fd44
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 01f159b9f07cd0d530039e0d5707cf38d51610ef
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097591"
---
# <a name="add-icons-to-menu-commands"></a>メニュー コマンドにアイコンを追加する
コマンドは、メニューとツール バーの両方に表示できます。 ツール バーでは、コマンドをアイコンだけで表示する (領域を節約するため) ことが一般的であるのに対して、メニューでは、コマンドは通常、アイコンとテキストの両方で表示されます。

 アイコンは幅が 16 ピクセル、高さが 16 ピクセルであり、8 ビットの色深度 (256 色) または 32 ビットの色深度 (トゥルー カラー) のどちらにもできます。 32 ビット カラー アイコンが推奨されます。 アイコンは通常、1 つのビットマップ内で水平方向の 1 行に配置されますが、複数のビットマップも許可されます。 このビットマップは、そのビットマップで使用可能な個々のアイコンと共に *.vsct* ファイルで宣言されます。 詳細については、「[Bitmaps 要素](../extensibility/bitmaps-element.md)」のリファレンスを参照してください。

## <a name="add-an-icon-to-a-command"></a>コマンドにアイコンを追加する
 次の手順では、メニュー コマンドを含む既存の VSPackage プロジェクトがあることを前提にしています。 これを行う方法を見つけるには、「[メニュー コマンドを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。

1. 色深度が 32 ビットのビットマップを作成します。 アイコンは常に 16 x 16 であるため、このビットマップは高さが 16 ピクセル、幅が 16 ピクセルの倍数である必要があります。

     各アイコンは、ビットマップ上で 1 行内に互いに横に並べて配置されます。 各アイコン内の透明度の場所を示すには、アルファ チャネルを使用します。

     8 ビットの色深度を使用する場合は、マゼンタ `RGB(255,0,255)` を透明度として使用します。 ただし、32 ビット カラー アイコンが推奨されます。

2. アイコン ファイルを VSPackage プロジェクト内の *Resources* ディレクトリにコピーします。 **ソリューション エクスプローラー** で、プロジェクトにアイコンを追加します。 (**Resources** を選択し、コンテキスト メニューの **[追加]** 、 **[既存項目]** の順にクリックして、アイコン ファイルを選択します)。

3. エディターで *.vsct* ファイルを開きます。

4. **testIcon** の名前を持つ `GuidSymbol` 要素を追加します。 GUID を作成し ( **[ツール]**  >  **[GUID の作成]** の順に選択し、 **[レジストリ形式]** を選択して **[コピー]** をクリックします)、それを `value` 属性に貼り付けます。 結果は次のようになります。

    ```xml
    <!-- Create your own GUID -->
    <GuidSymbol name="testIcon" value="{00000000-0000-0000-0000-0000}">
    ```

5. アイコンの `<IDSymbol>` を追加します。 `name` 属性はアイコンの ID であり、`value` はストリップ上のその位置を示します (存在する場合)。 アイコンが 1 つしかない場合は、1 を追加します。 結果は次のようになります。

    ```xml
    <!-- Create your own GUID -->
    <GuidSymbol name="testIcon" value="{00000000-0000-0000-0000-0000}">
        <IDSymbol name="testIcon1" value="1" />
    </GuidSymbol>
    ```

6. アイコンを含むビットマップを表すために、 *.vsct* ファイルの `<Bitmaps>` セクション内に `<Bitmap>` を作成します。

    - `guid` 値を、前の手順で作成した `<GuidSymbol>` 要素の名前に設定します。

    - `href` 値をビットマップ ファイルの相対パス (この場合は、**Resources\\<アイコン ファイル名\>** に設定します。

    - `usedList` 値を、前に作成した IDSymbol に設定します。 この属性では、VSPackage で使用されるアイコンのコンマ区切りリストを指定します。 このリストにないアイコンは、コンパイルから除外されます。

         Bitmap ブロックは次のようになります。

        ```xml
        <Bitmap guid="testIcon" href="Resources\<icon file name>" usedList="testIcon1"/>
        ```

7. 既存の `<Button>` 要素で、`Icon` 要素を、前に作成した GUIDSymbol と IDSymbol の値に設定します。 これらの値を持つ Button 要素の例を次に示します。

    ```xml
    <Button guid="guidAddIconCmdSet" id="cmdidMyCommand" priority="0x0100" type="Button">
        <Parent guid="guidAddIconCmdSet" id="MyMenuGroup" />
        <Icon guid="testIcon" id="testIcon1" />
        <Strings>
            <ButtonText>My Command name</ButtonText>
        </Strings>
    </Button>
    ```

8. アイコンをテストします。 プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスで、コマンドを見つけます。 そこには、追加したアイコンが表示されます。

## <a name="see-also"></a>関連項目
- [メニューとコマンドの拡張](../extensibility/extending-menus-and-commands.md)
- [VSCT XML スキーマ リファレンス](../extensibility/vsct-xml-schema-reference.md)
