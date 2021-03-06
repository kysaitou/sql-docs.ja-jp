---
title: SELECT FROM&lt;モデル&gt;(DMX) |Microsoft ドキュメント
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: aac800e225eb5323b1bffeafda77d059f0a837e2
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2018
ms.locfileid: "34842175"
---
# <a name="select-from-ltmodelgt-dmx"></a>SELECT FROM&lt;モデル&gt;(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  空の予測結合を実行し、指定された列の最も可能性の高い値を返します。 マイニング モデルのコンテンツのみが予測の作成に使用できます。  
  
## <a name="syntax"></a>構文  
  
```  
  
SELECT <expression list> [TOP <n>] FROM <model>   
[WHERE <condition list>]   
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>引数  
 *式の一覧*  
 式、予測、または列のみの予測のコンマ区切りのリストです。  
  
 *n*  
 任意。 返す行数を指定する整数値です。  
  
 *model*  
 モデル識別子です。  
  
 *条件の一覧*  
 任意。 列の一覧から返される値を制限する条件です。  
  
 *式 (expression)*  
 任意。 スカラー値を返す式。  
  
## <a name="remarks"></a>コメント  
 内の列、*式リスト*予測または予測のみとして定義されているか、予測可能列に関連する必要があります。  
  
## <a name="naive-bayes-example"></a>Naive Bayes の例  
 次の例は、Bike Buyer 列で空の予測結合を実行し、TM Naive Bayes マイニング モデルの最も可能性の高い状態を返します。  
  
```  
SELECT ([Bike Buyer]) FROM [TM_Naive_Bayes]  
```  
  
## <a name="time-series-example"></a>時系列の例  
 次の例は、Forecasting モデルの Amount 列で予測を実行し、次の 4 回のステップを返します。 Model Region 列は、自転車のモデルと地域を単一の識別子に結合します。 クエリを使用して、 [PredictTimeSeries &#40;DMX&#41; ](../dmx/predicttimeseries-dmx.md) 、予測を実行する関数。  
  
```  
SELECT [Model Region], PredictTimeSeries(Amount, 4)   
FROM Forecasting  
```  
  
## <a name="see-also"></a>参照  
 [選択&AMP;#40;DMX&AMP;#41;](../dmx/select-dmx.md)   
 [データ マイニング拡張機能&#40;DMX&#41;データ定義ステートメント](../dmx/dmx-statements-data-definition.md)   
 [データ マイニング拡張機能&#40;DMX&#41;データ操作ステートメント](../dmx/dmx-statements-data-manipulation.md)   
 [データ マイニング拡張機能 &#40;DMX&#41; ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
