---
title: SELECT FROM&lt;構造&gt;です。ケース |Microsoft ドキュメント
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f473cb42230aec0b5e40fb59fe10b2f34013ba2f
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2018
ms.locfileid: "34842105"
---
# <a name="select-from-ltstructuregtcases"></a>SELECT FROM&lt;構造&gt;です。場合
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  マイニング構造の作成に使用されたケースを返します。  
  
 ドリルスルーが構造で使用可能でない場合、ステートメントは失敗します。 また、マイニング構造に対するドリルスルー権限がユーザーに与えられていない場合も、ステートメントは失敗します。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、新しいマイニング構造でドリルスルーが既定で有効にします。 特定の構造に対してドリルスルーが有効にするかどうかを確認するには、確認するかどうかの値、 **CacheMode**プロパティに設定されている**KeepTrainingCases**です。  
  
 場合の値**CacheMode**に変更が**ClearAfterProcessing**構造ケースがキャッシュから消去、および、ドリルスルーを使用することはできません。  
  
> [!NOTE]  
>  データ マイニング拡張機能 (DMX) を使用してマイニング構造のドリルスルーを有効または無効にすることはできません。  
  
## <a name="syntax"></a>構文  
  
```  
  
SELECT [TOP n] <expression list> FROM <structure>.CASES  
[WHERE <condition expression>][ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>引数  
 *n*  
 任意。 返す行数を指定する整数値です。  
  
 *式の一覧*  
 式のコンマ区切りのリストです。  
  
 式には、列識別子、ユーザー定義関数、および VBA 関数を含めることができます。  
  
 *構造体*  
 構造の名前です。  
  
 *条件式*  
 列のリストから返される値を制限する条件です。  
  
 *式 (expression)*  
 任意。 スカラー値を返す式。  
  
## <a name="remarks"></a>コメント  
 モデルと構造の両方についてドリルスルーを有効にした場合、そのマイニング構造とマイニング モデルに対するドリルスルー権限を持つロールのすべてのメンバーは、次の構文を使用して、モデルに含まれていない構造列を返すことができます。  
  
```  
SELECT StructureColumn('<column name>') FROM <model>.CASES  
```  
  
 したがって、機密データまたは個人情報を保護する必要がありますを構築、個人情報をマスクし、付与、するデータ ソース ビュー **AllowDrillthrough**マイニング構造またはマイニング モデルに必要な場合にのみに対する権限。  
  
## <a name="examples"></a>使用例  
 次の例は、マイニング構造に基づく Targeted Mailing に基づく、[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]データベース、および関連するマイニング モデルです。 詳細については、次を参照してください。 [Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)です。  
  
### <a name="example-1-drill-through-to-structure-cases"></a>例 1 : 構造ケースにドリルスルーする  
 次の例では、マイニング構造 Targeted Mailing で最も古い 500 人の顧客のリストが返されます。 このクエリではマイニング モデル内のすべての列が返されますが、行は自転車を購入した顧客に制限され、年齢順に並べ替えられます。 必要な列のみを返すように式のリストを編集することもできます。  
  
```  
SELECT TOP 500 *  
FROM [Targeted Mailing].Cases  
WHERE [Bike Buyer] = 1  
ORDER BY Age DESC;  
```  
  
### <a name="example-2-drillthrough-to-test-or-training-cases-only"></a>例 2 : テスト ケースまたはトレーニング ケースのみにドリルスルーする  
 次の例では、テスト用に予約されている Targeted Mailing の構造ケースのリストが返されます。 マイニング構造に、提示されたテスト セットが含まれていない場合、既定ではすべてのケースがトレーニング ケースとして扱われ、このクエリはケースを返しません。  
  
```  
SELECT [Customer Key], Gender, Age  
FROM [Targeted Mailing].Cases  
WHERE IsTestCase();  
```  
  
 トレーニング ケースを返すには、するには、関数を置き換える`IsTrainingCase()`です。  
  
## <a name="see-also"></a>参照  
 [選択&AMP;#40;DMX&AMP;#41;](../dmx/select-dmx.md)   
 [データ マイニング拡張機能&#40;DMX&#41;データ定義ステートメント](../dmx/dmx-statements-data-definition.md)   
 [データ マイニング拡張機能&#40;DMX&#41;データ操作ステートメント](../dmx/dmx-statements-data-manipulation.md)   
 [データ マイニング拡張機能 &#40;DMX&#41; ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
