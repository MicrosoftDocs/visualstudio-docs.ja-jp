---
title: ファイル名拡張子のファイル ハンドラーの指定 | Microsoft Docs
description: OpenWithList と OpenWithProgids を使用して、Visual Studio SDK でファイル拡張子を処理するアプリケーションを特定する方法を説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- file extensions, specifying file handlers
ms.assetid: e3de4730-a95c-465a-b3b2-92ca85364ad7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 65705467b1531e139c0ec857d6a7b57015d5f2f9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089967"
---
# <a name="specifying-file-handlers-for-file-name-extensions"></a>ファイル名拡張子のファイル ハンドラーを指定する
特定のファイル拡張子を持つファイルを処理するアプリケーションを特定する方法は、数多くあります。 OpenWithList 動詞と OpenWithProgids 動詞は、ファイル拡張子のレジストリ エントリの下でファイルハンドラーを指定する 2 つの方法です。

## <a name="openwithlist-verb"></a>OpenWithList 動詞
 Windows エクスプローラーでファイルを右クリックすると、 **[開く]** コマンドが表示されます。 複数の製品が拡張子に関連付けられている場合は、 **[プログラムから開く]** サブメニューが表示されます。

 HKEY_CLASSES_ROOT でファイル拡張子の OpenWithList キーを設定することによって、特定の拡張子のファイルを開くさまざまなアプリケーションを登録できます。 このキーの下に、ファイル拡張子に対して一覧表示されるアプリケーションが、 **[プログラムから開く]** ダイアログ ボックスの **[推奨されたプログラム]** 見出しの下に表示されます。 次の例は、.vcproj ファイル拡張子を開くように登録されているアプリケーションを示しています。

```
HKEY_CLASSES_ROOT\
   .vcproj\
      (default)="VisualStudio.vcproj.14.0"
      OpenWithList\
         devenv.exe
```

> [!NOTE]
> アプリケーションを指定するキーは、HKEY_CLASSES_ROOT\Applications の下の一覧にあります。

 OpenWithList キーを追加することにより、別のアプリケーションに拡張子の所有権がある場合でも、アプリケーションがファイル拡張子をサポートすることが宣言されます。 これは、このアプリケーションまたは別のアプリケーションの将来のバージョンとなる可能性があります。

## <a name="openwithprogids"></a>OpenWithProgIDs
 プログラム識別子 (ProgID) は、アプリケーションまたは COM オブジェクトのバージョンを識別する、ClassID のフレンドリ バージョンです。 共同作成可能なすべてのオブジェクトは、それ自体の ProgID を持つ必要があります。 たとえば、VisualStudio.DTE.7.1 は、VisualStudio.DTE.10.0 が [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] を起動している間に Visual Studio .NET 2003 を起動します。 プロジェクト タイプまたはプロジェクト項目タイプの所有者は、ファイル拡張子のバージョン固有の ProgID を作成する必要があります。 これらの ProgID は、複数の ProgID が同じアプリケーションを起動する場合があるため、冗長である可能性があります。 詳細については、「[ファイル名拡張子の動詞を登録する](../extensibility/registering-verbs-for-file-name-extensions.md)」を参照してください。

 他のベンダーからの登録と重複しないように、バージョン管理されたファイルの ProgID には、次の名前付け規則を使用します。

|[ファイル拡張子]|バージョン管理された ProgID|
|--------------------|----------------------|
|.extension|ProductName. extension.versionMajor.versionMinor|

 バージョン管理された ProgID を HKEY_CLASSES_ROOT\\ *\<extension>* \OpenWithProgids キーに値として追加して、特定の拡張子のファイルを開くことができるさまざまなアプリケーションを登録することができます。 このレジストリ キーには、ファイル拡張子に関連付けられている代替 ProgID の一覧が含まれています。 一覧にある ProgID に関連付けられているアプリケーションは、 **[_製品名_ から開く]** サブメニューに表示されます。 `OpenWithList` キーと `OpenWithProgids` キーの両方に同じアプリケーションが指定されている場合は、オペレーティング システムにより重複部分がマージされます。

> [!NOTE]
> `OpenWithProgids` キーは、Windows XP でのみサポートされています。 このキーは他のオペレーティング システムでは無視されるため、ファイル ハンドラーの唯一の登録としては使用しないでください。 このキーは、Windows XP でのユーザー エクスペリエンスを向上させるために使用します。

 必要な ProgID を、REG_NONE 型の値として追加します。 次のコードは、ファイル拡張子 (.*ext*) の ProgID を登録する例を示しています。

```
HKEY_CLASSES_ROOT\
   .ext\
      (default)="MyProduct.ext.14.0"
      OpenWithProgids
         progid        REG_NONE (zero-length binary value)
         otherprogid   REG_NONE (zero-length binary value)
```

 ファイル拡張子の既定値として指定された ProgID が、既定のファイル ハンドラーです。 以前のバージョンの [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] で提供されていたか、他のアプリケーションで開くように設定できるファイル拡張子の ProgID を変更する場合は、ファイル拡張子の `OpenWithProgids` キーを登録し、一覧にある新しい ProgID を、サポートする古い ProgID と共に指定する必要があります。 次に例を示します。

```
HKEY_CLASSES_ROOT\
   .vcproj\
      (default)="VisualStudio.vcproj.14.0"
      OpenWithProgids
         vcprojfile              //old progid
         VisualStudio.vcproj.12.0 //old progid
         VisualStudio.vcproj.14.0 //new progid
```

 古い ProgID に動詞が関連付けられている場合は、これらの動詞が、ショートカット メニューの **[*製品名* から開く]** にも表示されます。

## <a name="see-also"></a>関連項目
- [ファイル名拡張子について](../extensibility/about-file-name-extensions.md)
- [ファイル名拡張子の動詞を登録する](../extensibility/registering-verbs-for-file-name-extensions.md)
