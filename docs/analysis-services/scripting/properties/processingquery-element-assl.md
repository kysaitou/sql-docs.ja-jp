---
title: "ProcessingQuery 要素 (ASSL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- ProcessingQuery Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- ProcessingQuery element
ms.assetid: d18e6f4b-c24c-4f73-8b85-4b6e8a82a695
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f9c2d9f0607e51f754657a5cbd2750eff5fc173a
ms.contentlocale: ja-jp
ms.lasthandoff: 09/01/2017

---
# <a name="processingquery-element-assl"></a>ProcessingQuery 要素 (ASSL)
  増分処理ステータスの通知のために実行するクエリのパラメーター化されたテキストを格納します。  
  
## <a name="syntax"></a>構文  
  
```xml  
  
<IncrementalProcessingNotification>  
   ...  
   <ProcessingQuery>...</ProcessingQuery>  
   ...  
</IncrementalProcessingNotification>  
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
|親要素|[IncrementalProcessingNotification](../../../analysis-services/scripting/objects/incrementalprocessingnotification-element-assl.md)|  
|子要素|なし|  
  
## <a name="remarks"></a>解説  
 内のテーブル、 [DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)によって参照される、 **ProcessingQuery** 、兄弟要素によって識別される[TableID](../../../analysis-services/scripting/properties/tableid-element-assl.md)です。  
  
 親に対応する要素**ProcessingQuery**分析管理オブジェクト (AMO) オブジェクト モデルは<xref:Microsoft.AnalysisServices.IncrementalProcessingNotification>します。  
  
## <a name="see-also"></a>参照  
 [プロパティ & #40 です。ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  