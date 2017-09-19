---
title: "executeUpdate (java.lang.String, int) メソッド |Microsoft ドキュメント"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerStatement.executeUpdate (java.lang.String, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c52a20e-527e-4d14-9a5a-4cd195aac8ed
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bb27e4538eccf87257d16555505442f76461adb0
ms.contentlocale: ja-jp
ms.lasthandoff: 09/09/2017

---
# <a name="executeupdate-method-javalangstring-int"></a>executeUpdate (java.lang.String, int) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定された SQL ステートメントと信号の実行、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]キー、自動生成されるかどうかについて、指定したフラグとこれによって生成される[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)オブジェクトを取得を可能にする必要があります。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final int executeUpdate(java.lang.String sql,  
                               int flag)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *sql*  
  
 A**文字列**SQL ステートメントを含むです。  
  
 *フラグ*  
  
 **Int**を自動生成キーを可能にするかどうかを示す値。 次のいずれかの定数を指定します。  
  
 RETURN_GENERATED_KEYS  
  
 NO_GENERATED_KEYS  
  
## <a name="return-value"></a>戻り値  
 **Int** DDL ステートメントを使用する場合、影響を受ける行または 0 の数を示すです。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この executeUpdate メソッドは、java.sql.Statement インターフェイスの executeUpdate メソッドによって指定されます。  
  
 更新数、1 より大きいかを使用して、1 つ以上の結果セットを生成する結果がストアド プロシージャを実行する場合、[実行](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md)ストアド プロシージャを実行するメソッド。  
  
## <a name="see-also"></a>参照  
 [executeUpdate メソッド & #40 です。SQLServerStatement &#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)   
 [SQLServerStatement のメンバー](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement クラス](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  