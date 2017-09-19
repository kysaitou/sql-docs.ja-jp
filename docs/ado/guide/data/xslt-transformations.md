---
title: "XSLT 変換 |Microsoft ドキュメント"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XSLT transformations in ADO
ms.assetid: 1a46196e-839f-4734-a59e-2c64609ffb9e
caps.latest.revision: 3
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 36b39d14a4856d882add1e9bafdc9457fa3b8bc1
ms.contentlocale: ja-jp
ms.lasthandoff: 09/09/2017

---
# <a name="xslt-transformations"></a>XSLT 変換
XSLT は、別の形式に変換する、生成された XML に適用できます。 ADO では、XML 形式を理解することは、わかりやすい形式に変換できる XSLT テンプレートの開発に役立ちます。  
  
 たとえば、レコード セットの各行を rs: データ要素の内部 z: 行要素として保存することがわかります。 同様に、レコード セットの各フィールドは、この要素の属性値のペアとして保存されます。  
  
## <a name="remarks"></a>解説  
 次の XSLT スクリプトは、ブラウザーに表示される HTML テーブルに変換する前のセクションで示した XML を適用できます。  
  
```  
<?xml version="1.0" encoding="ISO-8859-1"?>  
<html xmlns:xsl="http://www.w3.org/TR/WD-xsl">  
<body STYLE="font-family:Arial, helvetica, sans-serif; font-size:12pt; background-color:white">  
<table border="1" style="table-layout:fixed" width="600">  
  <col width="200"></col>  
  <tr bgcolor="teal">  
    <th><font color="white">CustomerId</font></th>  
    <th><font color="white">CompanyName</font></th>  
    <th><font color="white">ContactName</font></th>  
  </tr>  
<xsl:for-each select="xml/rs:data/z:row">  
  <tr bgcolor="navy">  
    <td><font color="white"><xsl:value-of select="@CustomerID"/></font></td>  
    <td><font color="white"><xsl:value-of select="@CompanyName"/></font></td>  
    <td><font color="white"><xsl:value-of select="@ContactName"/></font></td>   
  </tr>  
</xsl:for-each>  
</table>  
</body>  
</html>  
```  
  
 XSLT では、テーブルの見出しとレコード セットの各フィールドを表示する HTML テーブルに、ADO Save メソッドによって生成された XML ストリームに変換します。 テーブルの見出しおよび行も、割り当てられている異なるフォントと色。  
  
## <a name="see-also"></a>参照  
 [XML 形式で保持するレコード](../../../ado/guide/data/persisting-records-in-xml-format.md)