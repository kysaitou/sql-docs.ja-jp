---
title: Filter (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- Filter
- Filter_TSQL
- Filter (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- Filter method
ms.assetid: 82a8f54a-3a47-4e20-b13a-b148029c5448
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d641d4db466ee0d01d88aa129fd554eec3c1d23a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "33059788"
---
# <a name="filter-geography-data-type"></a>Filter (geography データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  インデックスが使用可能である場合に、**geography** インスタンスが別の **geography** インスタンスと交差するかどうかを判断する、高速のインデックス専用積集合メソッドを提供するメソッドです。  
  
 **geography** インスタンスがもう一方の **geography** インスタンスと交差している可能性がある場合、1 を返します。 このメソッドは偽陽性の戻り値を生成する場合があり、正確な結果はプランによって異なります。 **geography** インスタンスの交差が見つからない場合は、正確な 0 値 (真陰性の戻り値) を返します。  
  
 インデックスが使用できない場合、または使用されていない場合、このメソッドは、同じパラメーターを使用して呼び出した場合の **STIntersects()** と同じ値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
.Filter ( other_geography )  
```  
  
## <a name="arguments"></a>引数  
 *other_geography*  
 Filter() を呼び出したインスタンスと比較される、別の **geography** インスタンスです。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **bit**  
  
 CLR の戻り値の型: **SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 このメソッドは決定的でなく、正確ではありません。  
  
## <a name="examples"></a>使用例  
 `Filter()` を使用して 2 つの `geography` インスタンスが相互に交差しているかどうかを調べる例を次に示します。  
  
```  
CREATE TABLE sample (id int primary key, g geography);  
INSERT INTO sample VALUES  
   (0, geography::Point(45, -120, 4326)),  
   (1, geography::Point(45, -120.1, 4326)),  
   (2, geography::Point(45, -120.2, 4326)),  
   (3, geography::Point(45, -120.3, 4326)),  
   (4, geography::Point(45, -120.4, 4326));  
  
CREATE SPATIAL INDEX sample_idx on sample(g);  
SELECT id  
FROM sample   
WHERE g.Filter(geography::Parse(  
   'POLYGON((-120.1 44.9, -119.9 44.9, -119.9 45.1, -120.1 45.1, -120.1 44.9))')) = 1;  
```  
  
## <a name="see-also"></a>参照  
 [Geography インスタンスの拡張メソッド](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [STIntersects &#40;geography データ型&#41;](../../t-sql/spatial-geography/stintersects-geography-data-type.md)  
  
  
