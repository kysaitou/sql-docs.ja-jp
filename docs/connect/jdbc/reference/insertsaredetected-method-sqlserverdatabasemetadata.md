---
title: insertsAreDetected メソッド (SQLServerDatabaseMetaData) |Microsoft ドキュメント
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.insertsAreDetected
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f296cc42-9d26-48c3-a360-bcf51c31f7fb
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a4883b1e6baece15e5ef01ddbefc6d4eb5143cb8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "32840577"
---
# <a name="insertsaredetected-method-sqlserverdatabasemetadata"></a>insertsAreDetected メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  メソッドを呼び出すことで可視の行を挿入するを検出できるかどうかを取得[rowInserted](../../../connect/jdbc/reference/rowinserted-method-sqlserverresultset.md)のメソッド、 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)クラスです。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean insertsAreDetected(int type)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *type*  
  
 結果セットの種類を示す整数です。java.sql.ResultSet または SQLServerResultSet での定義に従って、次のいずれかの値を指定します。  
  
## <a name="javasqlresultset-types"></a>java.sql.ResultSet の種類  
 TYPE_FORWARD_ONLY  
  
 TYPE_SCROLL_SENSITIVE  
  
 TYPE_SCROLL_INSENSITIVE  
  
## <a name="sqlserverresultset-types"></a>SQLServerResultSet の種類  
 TYPE_SS_SCROLL_STATIC  
  
 TYPE_SS_SCROLL_KEYSET  
  
 TYPE_SS_DIRECT_FORWARD_ONLY  
  
 TYPE_SS_SERVER_CURSOR_FORWARD_ONLY  
  
 TYPE_SS_SCROLL_DYNAMIC  
  
## <a name="return-value"></a>戻り値  
 **true**行の挿入を検出できる場合は。 それ以外の場合は、 **false**です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この insertsAreDetected メソッドは、java.sql.DatabaseMetaData インターフェイスの insertsAreDetected メソッドによって指定されます。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] どの種類のカーソルの挿入された行は検出されません。  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメソッド](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
