---
title: Visual Studio Emulator for Android | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: tgt-pltfrm-cross-plat
ms.topic: conceptual
ms.assetid: 80f0104f-a4db-44dd-bd55-37bb67776c62
caps.latest.revision: 7
ms.author: crdun
manager: crdun
ms.openlocfilehash: ec7e6d3ee6d27c444d0904e750293a3d82c3ab4a
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54789856"
---
# <a name="visual-studio-emulator-for-android"></a>Visual Studio Emulator for Android
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Visual Studio Emulator for Android は、Android デバイスをエミュレートするデスクトップ アプリケーションです。 物理デバイスを使用しないで Android アプリをデバッグおよびテストできる仮想化環境を提供します。 また、アプリケーションのプロトタイプ用の分離された環境も提供します。  
  
 Visual Studio Emulator for Android は、実際のデバイスに匹敵するパフォーマンスを提供するように設計されています。 ただし、アプリを公開する前に、物理デバイスでアプリをテストすることをお勧めします。  
  
 Android プラットフォームごとに異なるデバイス プロファイル、画面の解像度、および Visual Studio Emulator for Android でサポートされるその他のハードウェア プロパティで、アプリをテストできます。  
  
 このトピックは、次のセクションで構成されています。  
  
-   [インストールとアンインストール](#Installing)  
  
-   [システム要件と下位互換性](#Requirements)  
  
-   [Visual Studio Emulator for Android でのネットワーク](#Networking)  
  
-   [Visual Studio Emulator for Android の構成](#Configuring)  
  
-   [エミュレーターでテストできる機能](#FeaturesTest)  
  
-   [エミュレーターでテストできない機能](#FeaturesNonTest)  
  
-   [サポート リソース](#Support)  
  
##  <a name="Installing"></a> インストールとアンインストール  
 インストール  
  
 Visual Studio Emulator for Android は、Visual Studio で使用できるクロスプラットフォーム ツールのコンポーネントであり、Visual Studio のカスタム セットアップで、[クロスプラットフォーム モバイル開発]、[共通ツールとソフトウェアの開発キット]、[Visual Studio Emulator for Android] を選択するとインストールされます。  
  
 アンインストール  
  
 コントロール パネルの [プログラムの追加と削除] を使用して、Android 用の Visual Studio エミュレーターをアンインストールできます。  
  
> [!NOTE]
>  Visual Studio をアンインストールしても、エミュレーターはアンインストールされません。 エミュレーターを別個にアンインストールする必要があります。  
  
 Visual Studio Emulator for Android をアンインストールしても、エミュレーター用に作成された Hyper-V 仮想イーサネット アダプターは自動的に削除されません。 HYPER-V マネージャーを開き、エミュレーターの VHD イメージの 1 つを選択後、[ネットワーク] タブを選び、このタブに表示される各スイッチで **[削除]** を選択して、これらの仮想アダプター (使用中でない場合) を手動で削除することができます。  
  
##  <a name="Requirements"></a> システム要件と下位互換性  
 Visual Studio Emulator for Android のハードウェア、ソフトウェア、構成の要件に関する重要な情報については、次のトピックをご覧ください。  
  
- [System Requirements for the Visual Studio Emulator for Android](../cross-platform/system-requirements-for-the-visual-studio-emulator-for-android.md)  
  
  Visual Studio Emulator for Android には Visual Studio 2015 が必要です。それより前のバージョンの Visual Studio との下位互換性はありません。  
  
  エミュレーターの新しいバージョンは古いバージョンの上にインストールされます (また、場合によっては、古いイメージが置き換えられて、イメージにインストールされている設定、アプリ、ファイルが破棄されることがあります)。  
  
##  <a name="Networking"></a> Visual Studio Emulator for Android でのネットワーク  
 Visual Studio Emulator for Android のネットワーク接続は、次のような特性のデスクトップ コンピューターの接続と同じように動作します。  
  
- エミュレーターは、独自の IP アドレスを持つ独立したデバイスとしてネットワーク上に表示されます。  
  
- エミュレーターにまだインストールされていない追加のネットワーク ソフトウェアは必要ありません。  
  
- Windows ドメインには参加しません。  
  
  エミュレーターのネットワーク接続の機能を理解するには、Android 電話機から同じネットワークへの Wi-Fi 接続と同じように考えてください。 携帯電話で実行されているアプリが Wi-Fi 接続を介してネットワーク リソースにアクセスできる場合、エミュレーターで実行されているアプリも同じネットワーク リソースにアクセスできます。  
  
  ネットワーク要件について詳しくは、「[Visual Studio Emulator for Android のシステム要件](../cross-platform/system-requirements-for-the-visual-studio-emulator-for-android.md)」をご覧ください。  
  
  ネットワークの問題のトラブルシューティングについて詳しくは、「[Visual Studio Emulator for Android のトラブルシューティング](../cross-platform/troubleshooting-the-visual-studio-emulator-for-android.md)」をご覧ください。  
  
##  <a name="Configuring"></a> Visual Studio Emulator for Android の構成  
 Android アプリでさまざまな Android ハードウェアとの互換性をテストするのは、難しい場合があります。 市場に出回っている Android 携帯電話およびタブレットには、さまざまなバージョン、画面サイズ、ハードウェア構成 (RAM、CPU、アーキテクチャなど) があります Visual Studio Emulator for Android は、デバイス プロファイルを使用することによってこれを簡素化します。 付属のデバイス プロファイルでは、Samsung、Motorola、Sony、LG その他のデバイスを含む、市場で最も人気のあるハードウェアが含まれています。  
  
 Visual Studio 2015 では、Emulator Manager を使用してデバイス プロファイルをインストール、アンインストール、開始できます。 Emulator Manager にアクセスするには、**[ツール]**、**[Visual Studio Emulator for Android]** の順に選択します。  
  
 ![Visual Studio Emulator for Android Manager](../cross-platform/media/android-emu-manager.png "Android_Emu_Manager")  
  
 既定では、4 つのインストール済みデバイス プロファイルがあり (KitKat and Lollipop phone/5" および tablet/7" 構成)、白いテキストとアイコンで示されます。 一覧の他のプロファイルは、**[プロファイルのインストール]** ボタンをクリックしてインストールが完了するまで、グレー表示になっています。 API レベルで一覧をフィルター処理でき、プロファイルの右下にある詳細矢印をクリックすると構成の詳細が表示されます。  
  
 対象にするプロファイルのセットをインストールした後は、緑色の **[プレイ]** ボタンをクリックすることで Manager から新しいプロファイルを直接開始できます。 Visual Studio クロス プラットフォーム モバイル プロジェクト タイプのデバッグ対象ドロップダウン メニューにも表示されます。  
  
##  <a name="FeaturesTest"></a> エミュレーターでテストできる機能  
 エミュレーターでテストできる機能に関する詳細については、この[ドキュメント](http://blogs.msdn.com/b/visualstudioalm/archive/2014/11/12/introducing-visual-studio-s-emulator-for-android.aspx)を参照してください。  
  
##  <a name="FeaturesNonTest"></a> エミュレーターでテストできない機能  
 次の一覧は、エミュレーターでテスト**できない** Android プラットフォームの機能です。 これらの機能は物理デバイスでテストする必要があります。  
  
-   コンパス  
  
-   ジャイロスコープ  
  
-   振動コントローラー  
  
-   明るさ。 エミュレーターの輝度レベルを変更しても、画面上のデバイスの表示方法は視覚的に変わりません。  
  
##  <a name="Support"></a> サポート リソース  
 ホスト コンピューターがシステム要件を満たしていて、このトラブルシューティング ガイドに記載されていない問題が発生した場合は次のようにします。  
  
-   [android エミュレーター](http://stackoverflow.com/questions/tagged/android-emulator)と visual-studio タグの試用について StackOverflow で質問を投稿します。  
  
-   Visual Studio またはエミュレーター マネージャーで、[気に入った機能の報告] を使用して、問題を報告します。  
  
## <a name="see-also"></a>関連項目  
 [Visual Studio Emulator for Android のシステム要件](../cross-platform/system-requirements-for-the-visual-studio-emulator-for-android.md)   
 [Troubleshooting the Visual Studio Emulator for Android](../cross-platform/troubleshooting-the-visual-studio-emulator-for-android.md)
