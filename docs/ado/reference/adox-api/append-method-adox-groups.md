---
title: "Append メソッド (ADOX グループ) |Microsoft ドキュメント"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Groups::raw_Append
- Groups::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 56b94fc6-7ef0-4e4a-82a3-033b94c46036
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ed08c3fc0f871c1e7fb8a5885f44390770d4a7a5
ms.contentlocale: ja-jp
ms.lasthandoff: 09/09/2017

---
# <a name="append-method-adox-groups"></a>Append メソッド (ADOX グループ)
新しく追加[グループ](../../../ado/reference/adox-api/group-object-adox.md)オブジェクトを[グループ](../../../ado/reference/adox-api/groups-collection-adox.md)コレクション。  
  
## <a name="syntax"></a>構文  
  
```  
  
Groups.Append Group  
```  
  
#### <a name="parameters"></a>パラメーター  
 *[グループ]*  
 **グループ**追加するオブジェクトまたはグループを作成し、追加の名前。  
  
## <a name="remarks"></a>解説  
 **グループ**のコレクション、[カタログ](../../../ado/reference/adox-api/catalog-object-adox.md)のすべてのカタログのグループ アカウントを表します。 **グループ**のコレクション、[ユーザー](../../../ado/reference/adox-api/user-object-adox.md)ユーザーが所属するグループのみを表します。  
  
 プロバイダーがグループの作成をサポートしていない場合は、エラーが発生します。  
  
> [!NOTE]
>  追加の前に、**グループ**オブジェクトを**グループ**のコレクション、**ユーザー**オブジェクト、**グループ**が同じオブジェクト[名前](../../../ado/reference/adox-api/name-property-adox.md)追加する 1 つに既に存在すると、**グループ**のコレクション、**カタログ**です。  
  
## <a name="applies-to"></a>適用対象  
 [グループのコレクション (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)  
  
## <a name="see-also"></a>参照  
 [グループとユーザーの追加、ChangePassword メソッドの例 (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Append メソッド (ADOX 列)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append メソッド (ADOX インデックス)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append メソッド (ADOX キー)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append メソッド (ADOX プロシージャ)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append メソッド (ADOX テーブル)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append メソッド (ADOX ユーザー)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append メソッド (ADOX ビュー)](../../../ado/reference/adox-api/append-method-adox-views.md)