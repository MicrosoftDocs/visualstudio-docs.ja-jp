---
title: MT タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- VC.Project.VCManifestTool.ResourceOutputFileName
- VC.Project.VCManifestTool.SuppressDependencyElement
- VC.Project.VCManifestTool.ManifestFromManagedAssembly
- VC.Project.VCManifestTool.GenerateCategoryTags
- VC.Project.VCManifestTool.EnableDPIAwareness
- vc.task.mt
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- MSBUILD (Visual C++), MT task
- MT task (MSBuild (Visual C++))
ms.assetid: bb94913c-1042-4968-9f08-b394518e899f
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 957e40a44c4f396fbd31b9062cfacddfd78cc8d5
ms.sourcegitcommit: a83c60bb00bf95e6bea037f0e1b9696c64deda3c
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2019
ms.locfileid: "54805475"
---
# <a name="mt-task"></a>MT タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Microsoft マニフェスト ツール mt.exe をラップします。 詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「Mt.exe」 (Mt.exe) を参照してください。  
  
## <a name="parameters"></a>パラメーター  
 以下の表で、**MT** タスクのパラメーターについて説明します。 タスク パラメーターの大部分とパラメーターのいくつかのセットは、コマンド ライン オプションに対応します。  
  
> [!NOTE]
>  mt.exe のドキュメントではコマンド ライン オプションのプレフィックスとしてハイフン (**-**) を使用していますが、このトピックではスラッシュ (**/**) を使用しています。 どちらのプレフィックスも使用できます。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|**AdditionalManifestFiles**|省略可能な **String[]** 型のパラメーターです。<br /><br /> 1 つ以上のマニフェスト ファイルの名前を指定します。<br /><br /> 詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「Mt.exe」 (Mt.exe) の **/manifest** オプションを参照してください。|  
|**AdditionalOptions**|省略可能な **String** 型のパラメーターです。<br /><br /> コマンド ライン オプションのリスト。 たとえば、"*/option1 /option2 /option#*" のような形式です。 他の **MT** タスク パラメーターでは表されないコマンド ライン オプションを指定する場合は、このパラメーターを使用します。<br /><br /> 詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「Mt.exe」 (Mt.exe) を参照してください。|  
|**AssemblyIdentity**|省略可能な **String** 型のパラメーターです。<br /><br /> マニュフェストの **assemblyIdentity** 要素の属性値を指定します。 コマンド区切りのリストを指定します。最初のコンポーネントは `name` 属性の値で、その後に *\<属性名>=<attribute_value>* という形式の 1 つ以上の名前/値のペアが続きます。<br /><br /> 詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「Mt.exe」 (Mt.exe) の **/identity** オプションを参照してください。|  
|**ComponentFileName**|省略可能な **String** 型のパラメーターです。<br /><br /> .rgs ファイルまたは .tlb ファイルからビルドするダイナミック リンク ライブラリの名前を指定します。 **RegistrarScriptFile** または **TypeLibraryFile** MT タスク パラメーターを指定する場合、このパラメーターは必須です。<br /><br /> 詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「Mt.exe」 (Mt.exe) の **/dll** オプションを参照してください。|  
|**DependencyInformationFile**|省略可能な **String** 型のパラメーターです。<br /><br /> マニフェスト ツールのビルド依存関係情報を追跡するために Visual Studio で使用される依存関係情報ファイルを指定します。|  
|**EmbedManifest**|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合は、アセンブリにマニフェスト ファイルを埋め込みます。 `false` の場合は、スタンドアロン マニフェスト ファイルとして作成します。|  
|**EnableDPIAwareness**|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合は、アプリケーションを DPI 対応としてマークするマニフェスト情報を追加します。 DPI 対応のアプリケーションを作成すると、さまざまな高 DPI のディスプレイ設定で一貫して適切なユーザー インターフェイスの表示を実現できます。<br /><br /> 詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「High DPI」 (高 DPI) を参照してください。|  
|**GenerateCatalogFiles**|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合は、カタログ定義 (.cdf) ファイルを生成します。<br /><br /> 詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「Mt.exe」 (Mt.exe) の **/makecdfs** オプションを参照してください。|  
|**GenerateCategoryTags**|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合は、カテゴリ タグが生成されます。 このパラメーターが `true` の場合は、**ManifestFromManagedAssemblyMT** タスク パラメーターも指定する必要があります。<br /><br /> 詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「Mt.exe」 (Mt.exe) の **/category** オプションを参照してください。|  
|**InputResourceManifests**|省略可能な **String** 型のパラメーターです。<br /><br /> 識別子が指定されている RT_MANIFEST 型のリソースからマニュフェストを入力します。 _\<file>[_**;**_[_**#**_]<resource_id>]_ という形式のリソースを指定します。省略可能な `resource_id` パラメーターは負以外の 16 ビットの数値です。<br /><br /> `resource_id` が指定されていない場合、CREATEPROCESS_MANIFEST_RESOURCE の既定値 (1) が使用されます。<br /><br /> 詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「Mt.exe」 (Mt.exe) の **/inputresource** オプションを参照してください。|  
|**ManifestFromManagedAssembly**|省略可能な **String** 型のパラメーターです。<br /><br /> 指定されたマネージド アセンブリからマニフェストを生成します。<br /><br /> 詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「Mt.exe」 (Mt.exe) の **/managedassemblyname** オプションを参照してください。|  
|**ManifestToIgnore**|省略可能な **String** 型のパラメーターです。<br /><br /> (使用されていません)。|  
|**OutputManifestFile**|省略可能な **String** 型のパラメーターです。<br /><br /> 出力マニュフェストの名前を指定します。 このパラメーターを省略し、操作対象のマニフェストが 1 つだけの場合、そのマニフェストがそのまま変更されます。<br /><br /> 詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「Mt.exe」 (Mt.exe) の **/out** オプションを参照してください。|  
|**OutputResourceManifests**|省略可能な **String** 型のパラメーターです。<br /><br /> 識別子が指定されている RT_MANIFEST 型のリソースにマニュフェストを出力します。 リソースは _\<file>[_**;**_[_**#**_]<resource_id>]_ という形式になります。省略可能な `resource_id` パラメーターは負以外の 16 ビットの数値です。<br /><br /> `resource_id` が指定されていない場合、CREATEPROCESS_MANIFEST_RESOURCE の既定値 (1) が使用されます。<br /><br /> 詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「Mt.exe」 (Mt.exe) の **/outputresource** オプションを参照してください。|  
|**RegistrarScriptFile**|省略可能な **String** 型のパラメーターです。<br /><br /> registration-free COM マニフェスト サポートに対して使用されるレジスタ スクリプト (.rgs) ファイルの名前を指定します。<br /><br /> 詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「Mt.exe」 (Mt.exe) の **/rgs** オプションを参照してください。|  
|**ReplacementsFile**|省略可能な **String** 型のパラメーターです。<br /><br /> レジスタ スクリプト (.rgs) ファイルで置換できる文字列の値を格納するファイルを指定します。<br /><br /> 詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「Mt.exe」 (Mt.exe) の **/replacements** オプションを参照してください。|  
|**ResourceOutputFileName**|省略可能な **String** 型のパラメーターです。<br /><br /> マニフェストをプロジェクト出力に埋め込むために使用する出力リソース ファイルを指定します。|  
|**Sources**|省略可能な `ITaskItem[]` 型のパラメーターです。<br /><br /> スペースで区切られたマニフェスト ソース ファイルのリストを指定します。<br /><br /> 詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「Mt.exe」 (Mt.exe) の **/manifest** オプションを参照してください。|  
|**SuppressDependencyElement**|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合は、依存関係要素を使用せずにマニフェストを生成します。 このパラメーターが `true` の場合は、**ManifestFromManagedAssemblyMT** タスク パラメーターも指定します。<br /><br /> 詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「Mt.exe」 (Mt.exe) の **/nodependency** オプションを参照してください。|  
|**SuppressStartupBanner**|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、タスクの開始時に著作権およびバージョン番号のメッセージが表示されないようにします。<br /><br /> 詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「Mt.exe」 (Mt.exe) の **/nologo** オプションを参照してください。|  
|**TrackerLogDirectory**|省略可能な `String` 型のパラメーターです。<br /><br /> このタスクの追跡ログの格納先となる中間ディレクトリを指定します。|  
|**TypeLibraryFile**|省略可能な **String** 型のパラメーターです。<br /><br /> タイプ ライブラリ (.tlb) ファイルの名前を指定します。 このパラメーターを指定する場合は、**ComponentFileNameMT** タスク パラメーターも指定します。<br /><br /> 詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「Mt.exe」 (Mt.exe) の **/tlb** オプションを参照してください。|  
|**UpdateFileHashes**|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合は、**UpdateFileHashesSearchPathMT** タスク パラメーターで指定されたパスでファイルのハッシュ値を計算し、その計算値を使用して、マニュフェストの **file** 要素の **hash** 属性値を更新します。<br /><br /> 詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「Mt.exe」 (Mt.exe) の **/hashupdate** オプションを参照してください。 この表の **UpdateFileHashesSearchPath** パラメーターも参照してください。|  
|**UpdateFileHashesSearchPath**|省略可能な `String` 型のパラメーターです。<br /><br /> ファイル ハッシュの更新時に使用する検索パスを指定します。 このパラメーターは **UpdateFileHashesMT** タスク パラメーターと共に使用します。<br /><br /> 詳細については、この表の **UpdateFileHashes** パラメーターを参照してください。|  
|**VerboseOutput**|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合は、詳細なデバッグ情報を表示します。<br /><br /> 詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「Mt.exe」 (Mt.exe) の **/verbose** オプションを参照してください。|  
  
## <a name="remarks"></a>解説  
  
## <a name="see-also"></a>関連項目
 [Task Reference (タスク リファレンス)](../msbuild/msbuild-task-reference.md)
