---
title: Linux VM の MSI を使用した Azure Key Vault へのアクセス
description: Linux VM 管理対象サービス ID (MSI) を使用して Azure Resource Manager にアクセスするプロセスについて説明するチュートリアルです。
services: active-directory
documentationcenter: ''
author: daveba
manager: mtillman
editor: daveba
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/15/2017
ms.author: daveba
ROBOTS: NOINDEX,NOFOLLOW
ms.openlocfilehash: a6ca37105cfff8542f0c4a8af3112fa317416c56
ms.sourcegitcommit: 0a84b090d4c2fb57af3876c26a1f97aac12015c5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/11/2018
ms.locfileid: "38611253"
---
# <a name="use-a-linux-vm-managed-service-identity-msi-to-access-azure-key-vault"></a>Linux VM 管理対象サービス ID (MSI) を使用した Azure Key Vault へのアクセス 

[!INCLUDE[preview-notice](~/includes/active-directory-msi-preview-notice-ua.md)]

このチュートリアルでは、Linux 仮想マシンの管理対象サービス ID (MSI) を有効にし、その ID を使用して Azure Key Vault にアクセスする方法について説明します。 ブートストラップとして機能する Key Vault により、クライアント アプリケーションは、Azure Active Directory (AD) で保護されていないリソースにシークレットを使用してアクセスできます。 管理対象サービス ID は Azure によって自動的に管理され、コードに資格情報を挿入しなくても、Azure AD の認証をサポートするサービスを認証できます。 

学習内容は次のとおりです。

> [!div class="checklist"]
> * Linux 仮想マシンで MSI を有効にする 
> * Key Vault に格納されているシークレットへ VM のアクセスを許可する 
> * VM ID を使用してアクセス トークンを取得して、Key Vault からシークレットを取得する 
 
## <a name="prerequisites"></a>前提条件

[!INCLUDE [msi-core-prereqs](~/includes/active-directory-msi-core-prereqs-ua.md)]

[!INCLUDE [msi-tut-prereqs](~/includes/active-directory-msi-tut-prereqs.md)]

## <a name="sign-in-to-azure"></a>Azure へのサインイン
Azure Portal ([https://portal.azure.com](https://portal.azure.com)) にサインインします。 

## <a name="create-a-linux-virtual-machine-in-a-new-resource-group"></a>新しいリソース グループに Linux 仮想マシンを作成する

このチュートリアルでは、新しい Linux VM を作成します。 既存の VM で MSI を有効にすることもできます。

1. Azure Portal の左上隅にある **[リソースの作成]** をクリックします。
2. **[コンピューティング]**、**[Ubuntu Server 16.04 LTS]** の順に選択します。
3. 仮想マシンの情報を入力します。 **[認証の種類]** で、**[SSH 公開キー]** または **[パスワード]** を選択します。 作成した資格情報を使用して VM にログインできます。

    ![イメージ テキスト](~/articles/active-directory/media/msi-tutorial-linux-vm-access-arm/msi-linux-vm.png)

4. ドロップダウンで仮想マシンの**サブスクリプション**を選択します。
5. 仮想マシンを作成する新しい**リソース グループ**を選択するには、**[新規作成]** を選択します。 完了したら、**[OK]** をクリックします。
6. VM のサイズを選択します。 その他のサイズも表示するには、**[すべて表示]** を選択するか、[サポートされるディスクの種類] フィルターを変更します。 設定ページで、既定値のまま **[OK]** をクリックします。

## <a name="enable-msi-on-your-vm"></a>VM で MSI を有効にする

仮想マシンの MSI を使用すると、コードに資格情報を挿入しなくても、Azure AD からアクセス トークンを取得できます。 内部的には、MSI を有効にすると、VM に MSI VM 拡張機能がインストールされ、VM の MSI が有効化されます。  

1. MSI を有効にする**仮想マシン**を選択します。
2. 左側のナビゲーション バーで、**[構成]** をクリックします。
3. **管理対象のサービス ID** が表示されます。 MSI を登録して有効にする場合は **[はい]** を選択し、無効にする場合は [いいえ] を選択します。
4. **[保存]** をクリックして構成を保存します。

    ![イメージ テキスト](~/articles/active-directory/media/msi-tutorial-linux-vm-access-arm/msi-linux-extension.png)

5. この **Linux VM** で有効になっている拡張機能を確認する場合は、**[拡張機能]** をクリックします。 MSI が有効になっている場合、**ManagedIdentityExtensionforLinux** が一覧に表示されます。

    ![イメージ テキスト](~/articles/active-directory/media/msi-tutorial-linux-vm-access-arm/msi-extension-value.png)


## <a name="grant-your-vm-access-to-a-secret-stored-in-a-key-vault"></a>Key Vault に格納されているシークレットへ VM のアクセスを許可する  

MSI を使用すると、Azure Active Directory 認証をサポートするリソースに対して認証するためのアクセス トークンをコードで取得できます。 ただし、すべての Azure サービスが Azure AD 認証をサポートしているわけではありません。 MSI をこれらのサービスとともに使用するには、Azure Key Vault にサービス資格情報を保存し、MSI を使用して Key Vault にアクセスして、資格情報を取得します。 

まず、Key Vault を作成し、VM の ID に Key Vault へのアクセスを許可する必要があります。   

1. 左側のナビゲーション バーの上部で、**[+ 新規]**、**[セキュリティ + ID]**、**[Key Vault]** の順に選択します。  
2. 新しい Key Vault の**名前**を入力します。 
3. 以前に作成した VM と同じサブスクリプションおよびリソース グループで、Key Vault を見つけます。 
4. **[アクセス ポリシー]** を選択して **[新規追加]** ボタンをクリックします。 
5. テンプレートの [構成] で、**[シークレットの管理]** を選択します。 
6. **[プリンシパルの選択]** を選択し、検索フィールドに以前に作成した VM の名前を入力します。  結果一覧で VM を選択し、**[選択]** をクリックします。 
7. **[OK]** をクリックして新しいアクセス ポリシーの追加を終了し、**[OK]** をクリックしてアクセス ポリシーの選択を完了します。 
8. **[作成]** をクリックして Key Vault の作成を完了します。 

    ![イメージ テキスト](~/articles/active-directory/media/msi-tutorial-windows-vm-access-nonaad/msi-blade.png)

次に、Key Vault にシークレットを追加して、後で VM で実行されているコードを使用して、シークレットを取得できるようにします。 

1. **[すべてのリソース]** を選択し、作成した Key Vault を検索して選択します。 
2. **[シークレット]** を選択し、**[追加]** をクリックします。 
3. **[アップロード オプション]** から **[手動]** を選択します。 
4. シークレットの名前と値を指定します。  値は任意のものを指定できます。 
5. アクティブ化した日付と有効期限の日付をクリアのままにし、**[有効]** を **[はい]** のままにします。 
6. **[作成]** をクリックしてシークレットを作成します。 
 
## <a name="get-an-access-token-using-the-vms-identity-and-use-it-to-retrieve-the-secret-from-the-key-vault"></a>VM の ID を使用してアクセス トークンを取得して、Key Vault からシークレットを取得する  

これらの手順を完了するには、SSH クライアントが必要です。  Windows を使用している場合は、[Windows Subsystem for Linux](https://msdn.microsoft.com/commandline/wsl/about) で SSH クライアントを使用することができます。 SSH クライアント キーの構成について支援が必要な場合は、「[Azure 上の Windows で SSH キーを使用する方法](~/articles/virtual-machines/linux/ssh-from-windows.md)」または「[Azure に Linux VM 用の SSH 公開キーと秘密キーのペアを作成して使用する方法](~/articles/virtual-machines/linux/mac-create-ssh-keys.md)」をご覧ください。
 
1. ポータルで Linux VM に移動し、**[概要]** の **[接続]** をクリックします。 
2. 任意の SSH クライアントを使用して、VM に**接続**します。 
3. ターミナル ウィンドウで、CURL を使用して、ローカルの MSI エンドポイントに対して Azure Key Vault のアクセス トークンを取得するよう要求します。  
 
    アクセス トークンの CURL 要求を次に示します。  
    
    ```bash
    curl http://localhost:50342/oauth2/token --data "resource=https://vault.azure.net" -H Metadata:true  
    ```
    応答には、リソース マネージャーへのアクセスに必要なアクセス トークンが含まれています。 
    
    応答:  
    
    ```bash
    {"access_token":"eyJ0eXAi...",
    "refresh_token":"",
    "expires_in":"3599",
    "expires_on":"1504130527",
    "not_before":"1504126627",
    "resource":"https://vault.azure.net",
    "token_type":"Bearer"} 
    ```
    
    このアクセス トークンを使用して Azure Key Vault に認証することができます。  次の CURL 要求は、CURL と Key Vault REST API を使用して Key Vault からシークレットを読み取る方法を示しています。  Key Vault の **[概要]** ページの **[要点]** セクションにある Key Vault の URL が必要です。  前の呼び出しで取得したアクセス トークンも必要になります。 
        
    ```bash
    curl https://<YOUR-KEY-VAULT-URL>/secrets/<secret-name>?api-version=2016-10-01 -H "Authorization: Bearer <ACCESS TOKEN>" 
    ```
    
    応答は次のようになります。 
    
    ```bash
    {"value":"p@ssw0rd!","id":"https://mytestkeyvault.vault.azure.net/secrets/MyTestSecret/7c2204c6093c4d859bc5b9eff8f29050","attributes":{"enabled":true,"created":1505088747,"updated":1505088747,"recoveryLevel":"Purgeable"}} 
    ```
    
Key Vault からシークレットを取得した後は、名前とパスワードを必要とするサービスへの認証にそのシークレットを使用できます。


## <a name="related-content"></a>関連コンテンツ

- MSI の概要については、[管理対象サービス ID の概要](msi-overview.md)に関する記事をご覧ください。

Microsoft のコンテンツ改善のため、次のコメント セクションよりご意見をお寄せください。




