---
title: "AssociationSet 要素 (CSDLBI) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 93e5ac4d-d7e8-490e-b775-28263a48cfcc
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f8635a526095a7182c8415f571e26e6818f209a8
ms.contentlocale: ja-jp
ms.lasthandoff: 09/01/2017

---
# <a name="associationset-element-csdlbi"></a>AssociationSet 要素 (CSDLBI)
  **AssociationSet** 要素は関連付けを定義する複合型です。 CSDLBI データ モデルでは、関連付けは 2 つのテーブル間のリレーションシップを表します。  
  
 **AssociationSet** は、モデル内の一意なリレーションシップに対して個々に指定する必要があります。 **AssociationSet** では **Association** 要素を使用してエンドポイントを定義します。 **AssociationSet** 要素は、データ モデル内のリレーションシップとその使用状況に関するメタデータを定義します。  
  
## <a name="applicable-attributes"></a>該当する属性  
 次の表に、**AssociationSet** 要素を定義する要素と属性を示します。  
  
|名前|必須かどうか|Description|  
|----------|-----------------|-----------------|  
|状態|可|関連付けがアクティブかどうかを示す文字列。 値は State 要素によって定義されます。|  
|[非表示]|いいえ|リレーションシップが表示されるかどうかを示すブール値。 既定では Hidden の値は **false** で、モデル内のすべてのリレーションシップが表示されます。|  
  
## <a name="state-element"></a>State 要素  
 **State** 要素は、関連付けがアクティブで、計算で使用される状態と、関連付けが非アクティブで、計算で明示的に参照される必要がある状態のどちらであるかを示す単純型です。  
  
 2 つのエンティティを接続する複数のアソシエーション セットがある場合は、2 つ以上のアソシエーション セットを Active にマーク付けできません。 つまり、同一の 2 つのテーブル間に 2 つのリレーションシップがある場合にアクティブにできるのは、1 つのリレーションシップのみです。  
  
 次の表に **State** 要素の値を示します。  
  
|値|Description|  
|-----------|-----------------|  
|Active|関連付けがアクティブです。|  
|無効|関連付けがアクティブです。|  
  
## <a name="example"></a>例  
 **テーブル**  
  
 次の例では、AdventureWorks のテーブル モデルのリレーションシップ (CSDLBI Version 1.1) を示します。 既存のリレーションシップ (OrderKey と Date の間) が存在するため、関連付けは Inactive にマークされています。  
  
```  
<AssociationSet   
    Name="InternetSales_Date_Date_Date"  
    Association="Sandbox.InternetSales_Date_Date_Date">  
    <End EntitySet="InternetSales" />  
    <End EntitySet="DimDate" />  
<bi:AssociationSet State="Inactive" />  
</AssociationSet>  
  
```  
  
## <a name="example"></a>例  
 **多次元**  
  
 次の例は、Contoso Operations キューブにおいて Sales テーブルと Currency テーブル間で定義されているリレーションシップを示します。  
  
```  
<AssociationSet   
    Name ="Sales_Currency_Currency_Currency_Name2"  
    Association ="Sandbox.Sales_Currency_Currency_Currency_Name2">  
    <End EntitySet ="Sales" />  
    <End EntitySet ="Currency" />  
<bi:AssociationSet />  
</AssociationSet>  
```  
  
## <a name="see-also"></a>参照  
 [CSDL への BI 注釈のテクニカル リファレンス](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  