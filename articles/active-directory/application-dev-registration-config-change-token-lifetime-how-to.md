---
title: 独自に開発したアプリケーションのトークン有効期間の既定値を変更する方法 | Microsoft Docs
description: Azure AD で開発しているアプリケーションのトークンの有効期間ポリシーを更新する方法
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: barbkess
ms.openlocfilehash: bd963253ee796fb56405e8da855475df2d2f5d08
ms.sourcegitcommit: 95d9a6acf29405a533db943b1688612980374272
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2018
ms.locfileid: "36335341"
---
# <a name="how-to-change-the-token-lifetime-defaults-for-a-custom-developed-application"></a>独自に開発したアプリケーションのトークン有効期間の既定値を変更する方法

Azure AD Premium では、非機密クライアントに対して発行されたトークンの有効期間をアプリ開発者とテナント管理者が構成できます。 トークンの有効期間ポリシーは、テナント全体またはアクセスされるリソースに対して設定されます。

 * トークンの有効期間ポリシーを設定するには、[Azure AD PowerShell モジュール](https://www.powershellgallery.com/packages/AzureADPreview)をダウンロードする必要があります。

 * **Connect-AzureAD -Confirm** コマンドを実行します。

 * 次のサンプル ポリシーは、MaxAgeSingleFactor 更新トークンを設定します。 次のポリシーを作成します。 ```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```

 * その他のカスタム ポリシーを作成する方法については、[トークンの有効期間の構成](https://docs.microsoft.com/azure/active-directory/active-directory-configurable-token-lifetimes)に関するドキュメントを参照してください。

## <a name="next-steps"></a>次の手順
[トークンの有効期間の構成](https://docs.microsoft.com/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[Azure AD のトークン リファレンス](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims)

