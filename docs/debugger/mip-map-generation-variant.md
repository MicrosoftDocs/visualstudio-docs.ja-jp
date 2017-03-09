---
title: "ミップマップ生成バリアント | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "vs-ide-debug"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3b4b3583-0b01-4f5d-aacb-3f96d19111d9
caps.latest.revision: 6
caps.handback.revision: 6
author: "mikejo5000"
ms.author: "mikejo"
manager: "ghogen"
---
# ミップマップ生成バリアント
[!INCLUDE[vs2017banner](../code-quality/includes/vs2017banner.md)]

レンダー ターゲットではないテクスチャで MIP マップを有効にします。  
  
## 解釈  
 MIP マップは主に、テクスチャの小さいバージョンを事前に計算することにより、縮小時にテクスチャでエイリアシング効果を除去する目的で使用されます。  これらの追加のテクスチャは \(オリジナルのテクスチャよりも 33% 増の\) GPU メモリを消費しますが、効率も良くなります。これは、より多くの表面が GPU テクスチャ キャッシュに適合し、そのコンテンツで高い使用率を実現するためです。  
  
 3\-D シーンでは、追加のテクスチャを格納するメモリが使用できる場合は、レンダリング パフォーマンスとイメージの品質の両方が向上するため、MIP マップを推奨します。  
  
 このバリアントでパフォーマンスが大幅に向上する場合は、MIP マップを有効にしないでテクスチャを使用いるため、テクスチャのキャッシュを最大限に利用できていないことを示しています。  
  
## 解説  
 MIP マップの生成は、ソース テクスチャを作成する `ID3D11Device::CreateTexture2D` への呼び出しがあるたびに強制的に行われます。  具体的には、MIP マップの生成は、`pDesc` に渡された D3D11\_TEXTUR2D\_DESC オブジェクトが、不変のシェーダー リソースを記述する場合に強制的に行われます。つまり、  
  
-   BindFlags メンバーは D3D11\_BIND\_SHADER\_RESOURCE フラグを設定するだけです。  
  
-   Usage メンバーは、D3D11\_USAGE\_DEFUALT または D3D11\_USAGE\_IMMUTABLE に設定されます。  
  
-   CPUAccessFlags メンバーは 0 に設定されます\(CPU アクセスなし\)。  
  
-   SampleDesc メンバーは自身の Count メンバーを 1 に設定します \(Multi\-Sample Anti\-Aliasing \(MSAA\) なし\)。  
  
-   MipLevels メンバーは 1 に設定されます \(既存の MIP マップなし\)。  
  
 アプリケーションによって初期データが提供されたときに、テクスチャ形式は、D3D11\_FORMAT\_SUPPORT\_MIP\_AUTOGEN で定義されているように自動の MIP マップ生成をサポートしている必要があります \(ただし、形式が BC1、BC2、または BC3 の場合は除きます\)。サポートしていない場合はテクスチャは修正できず、初期データが提供されたときに MIP マップは生成されません。  
  
 テクスチャに対して MIP マップが自動的に生成された場合は、再生中に `ID3D11Device::CreateShaderResourceView` に対する呼び出しが修正され、テクスチャのサンプリング中に MIP チェーンを使用できるようになります。  
  
## 使用例  
 **Mip\-map Generation** バリアントは、次のようなコードを使用して再現することができます。  
  
```  
D3D11_TEXTURE2D_DESC texture_description;  
  
// ...  
  
texture_description.MipLevels = 0; // generate a full mipchain  
  
std::vector<D3D11_SUBRESOURCE_DATA> initial_data(num_mips);  
  
for (auto&& mip_level : initial_data)  
{  
    // fill mip_level with the application-supplied initial data  
}  
  
d3d_device->CreateTexture2D(&texture_description, initial_data.data(), &texture)  
```  
  
 完全な MIP チェーンを持つテクスチャを作成するには、`D3D11_TEXTURE2D_DESC::MipLevels` を 0 に設定します。  完全な MIP チェーンの MIP レベルの数は floor\(log2\(n\) \+ 1\) となります。n はテクスチャの最大のディメンションです。  
  
 `CreateTexture2D` に初期データを提供する場合は、各 MIP レベルに D3D11\_SUBRESOURCE\_DATA オブジェクトを提供しなければならないことに注意してください。  
  
> [!NOTE]
>  MIP レベルを自動的に生成する代わりに独自の MIP レベル コンテンツを提供する場合は、MIP マップ テクスチャをサポートしているイメージ エディターを使用してテクスチャを作成し、ファイルをロードして、MIP レベルを `CreateTexture2D` へ渡す必要があります。  
  
## 参照  
 [ハーフ\/クォーター テクスチャ ディメンション バリアント](../debugger/half-quarter-texture-dimensions-variant.md)