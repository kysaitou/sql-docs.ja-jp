---
title: "Intersect (MDX) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- INTERSECT
dev_langs:
- kbMDX
helpviewer_keywords:
- Intersect function
ms.assetid: 0de8fbb4-e2db-480c-86f1-2abbbcfdb1d8
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 07f59caff53819cb2ccea52d7f3372a4d3b97c65
ms.contentlocale: ja-jp
ms.lasthandoff: 08/02/2017

---
# <a name="intersect-mdx"></a>Intersect (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定された 2 つのセットの積集合を返します。重複部分を保持することも可能です。  
  
## <a name="syntax"></a>構文  
  
```  
  
Intersect(Set_Expression1 , Set_Expression2 [ , ALL ] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression1*  
 セットを返す有効な多次元式 (MDX) です。  
  
 *Set_Expression2*  
 セットを返す有効な多次元式 (MDX) です。  
  
## <a name="remarks"></a>解説  
 **Intersect**関数は、2 つのセットの積集合を返します。 既定では、両方のセットの重複部分を削除してから積集合を取得します。 指定された 2 つのセットの次元は同一である必要があります。  
  
 省略可能な**すべて**フラグは、重複部分を保持します。 場合**すべて**を指定すると、 **Intersect**関数が通常どおり、積の要素と交差して、2 番目のセットで一致する複製されている最初のセット内の重複は各交差しています。 指定された 2 つのセットの次元は同一である必要があります。  
  
## <a name="example"></a>例  
 次のクエリは 2003 年と 2004 年を返します。2 つのメンバーは指定された両方のセットに示されます。  
  
 `SELECT`  
  
 `INTERSECT(`  
  
 `{[Date].[Calendar Year].&[2001], [Date].[Calendar Year].&[2002],[Date].[Calendar Year].&[2003]}`  
  
 `, {[Date].[Calendar Year].&[2002],[Date].[Calendar Year].&[2003], [Date].[Calendar Year].&[2004]})`  
  
 `ON 0`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 次のクエリは、指定された 2 つのセットには異なる階層のメンバーが含まれているので失敗します。  
  
 `SELECT`  
  
 `INTERSECT(`  
  
 `{[Date].[Calendar Year].&[2001]}`  
  
 `, {[Customer].[City].&[Abingdon]&[ENG]})`  
  
 `ON 0`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス & #40 です。MDX と #41 です。](../mdx/mdx-function-reference-mdx.md)  
  
  
