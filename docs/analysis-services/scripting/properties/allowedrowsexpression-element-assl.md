---
title: AllowedRowsExpression 要素 (ASSL) |Microsoft ドキュメント
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b3b1a25e02e987c86dd07ed618e481ddf8fcadf9
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/10/2018
ms.locfileid: "34035493"
---
# <a name="allowedrowsexpression-element-assl"></a>AllowedRowsExpression 要素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  親要素のコンテンツを定義するブール型の Data Analysis Expression (DAX) が含まれます。  
  
## <a name="syntax"></a>構文  
  
```xml  
  
<CellPermission> <!-- or StandardAction -->  
   ...  
   <Expression>...</Expression>  
   ...  
</CellPermission>  
```  
  
## <a name="element-characteristics"></a>要素の特性  
  
|特性|説明|  
|--------------------|-----------------|  
|データ型と長さ|文字列|  
|既定値|なし|  
|Cardinality|1-1 : 必須要素で、1 回だけ出現します|  
  
## <a name="element-relationships"></a>要素の関係  
  
|リレーションシップ|要素|  
|------------------|-------------|  
|親要素|[CellPermission](../../../analysis-services/scripting/objects/cellpermission-element-assl.md)、 [StandardAction](../../../analysis-services/scripting/data-type/standardaction-data-type-assl.md)|  
|子要素|なし|  
  
## <a name="remarks"></a>解説  
 **CellPermission**要素、**式**要素にはによって示される権限に適用されるセルを識別する論理 MDX 式が含まれています、[アクセス](../../../analysis-services/scripting/properties/access-element-assl.md)要素、 **CellPermission**要素。 場合の値、**式**要素を**CellPermission**要素は空では、 **CellPermission**要素は無視されます。  
  
 **StandardAction**要素、**式**要素には、アクションの内容を表す MDX 式が含まれています。 場合の値、**式**要素を**StandardAction**要素は空では、 **StandardAction**要素は無視されます。  
  
 分析管理オブジェクト (AMO) オブジェクト モデルで親に対応する要素は、<xref:Microsoft.AnalysisServices.CellPermission> と <xref:Microsoft.AnalysisServices.StandardAction> です。  
  
## <a name="see-also"></a>参照  
 [プロパティ & #40 です。ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
