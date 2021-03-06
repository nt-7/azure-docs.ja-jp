---
title: アプリケーションにユーザーとグループを割り当てる方法 | Microsoft Docs
description: アプリケーションにユーザーを割り当ててアクセス権を付与する
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
ms.openlocfilehash: 46586bd423500f5d7bb34f58a5833d4bb3613bb3
ms.sourcegitcommit: 95d9a6acf29405a533db943b1688612980374272
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2018
ms.locfileid: "36330827"
---
# <a name="how-to-assign-users-and-groups-to-an-application"></a>アプリケーションにユーザーとグループを割り当てる方法

特定のアプリケーションに対してユーザーが次の操作を行えるようにするには、まず、**ユーザーをアプリケーションに割り当て**、アクセス権を付与する必要があります。

-   **アプリケーションの URL に直接移動**して、アプリケーションにアクセスする (SP によって開始されたサインオンとも呼ばれる)。

-   アプリケーションの **[プロパティ]** ページにある**ユーザー アクセス URL** を使用して、アプリケーションにアクセスする (IDP によって開始されたサインオンとも呼ばれる)。

-   アプリケーションが[アプリケーション アクセス パネル](https://myapps.microsoft.com/)またはモバイル アプリケーションに表示されていることを確認する。

-   [Office 365 アプリケーション起動プログラム](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a)にアプリケーションが表示されていることを確認する。

## <a name="methods-to-assign-applications-with-azure-active-directory"></a>Azure Active Directory を使用してアプリケーションを割り当てる方法 

Azure Active Directory でアプリケーションを割り当てる方法は 3 つあります。

-   [管理者としてアプリケーションにユーザーを直接割り当てる](#assign-a-user-directly-as-an-administrator)

-   [管理者としてアプリケーションにグループを直接割り当てる](#assign-a-group-directly-to-an-application-as-an-administrator)

-   [セルフ サービス アプリケーションへのアクセスを有効にすることでユーザーによる独自のアプリケーションの検索を許可する](#enable-self-service-application-access-to-allow-users-to-find-their-own-applications)

## <a name="assign-a-user-directly-as-an-administrator"></a>管理者としてユーザーを直接割り当てる

1 人以上のユーザーをアプリケーションに直接割り当てるには、次の手順に従います。

1.  [**Azure Portal**](https://portal.azure.com/) を開き、**グローバル管理者**としてサインインします。

2.  左側のメイン ナビゲーション メニューの上部にある **[すべてのサービス]** をクリックして **[Azure Active Directory 拡張機能]** を開きます。

3.  フィルター検索ボックスに「**Azure Active Directory**」と入力し、**[Azure Active Directory]** 項目を選択します。

4.  Azure Active Directory の左側にあるナビゲーション メニューで **[エンタープライズ アプリケーション]** をクリックします。

5.  **[すべてのアプリケーション]** をクリックして、すべてのアプリケーションの一覧を表示します。

  * ここに表示したいアプリケーションが表示されない場合は、**[All Applications List (すべてのアプリケーション リスト)]** の上部にある **[フィルター]** コントロールを使用して、**[表示]** オプションを **[すべてのアプリケーション]** に設定します。

6.  ユーザーを割り当てるアプリケーションを一覧から選びます。

7.  アプリケーションが読み込まれたら、アプリケーションの左側のナビゲーション メニューで **[ユーザーとグループ]** をクリックします。

8.  **[ユーザーとグループ]** 一覧の上部にある **[追加]** ボタンをクリックして、**[割り当ての追加]** ウィンドウを開きます。

9.  **[割り当ての追加]** ウィンドウから **[ユーザーとグループ]** セレクターをクリックします。

10. 割り当てる対象のユーザーの**フル ネーム**または**電子メール アドレス**を **[名前または電子メール アドレスで検索]** 検索ボックスに入力します。

11. リスト内で**ユーザー**にポインターを合わせ、**チェック ボックス**を表示します。 ユーザーのプロファイル写真またはロゴの横にあるチェック ボックスをオンにして、ユーザーを **[選択済み]** リストに追加します。

12. **省略可能:** **複数のユーザーを追加**する場合は、別の**フル ネーム**または**電子メール アドレス**を **[名前または電子メール アドレスで検索]** 検索ボックスに入力し、チェック ボックスをオンにして **[選択済み]** リストにこのユーザーを追加します。

13. ユーザーの選択が完了したら、**[選択]** ボタンをクリックして、アプリケーションに割り当てるユーザーとグループの一覧に追加します。

14. **省略可能:** **[割り当ての追加]** ウィンドウで **[ロールの選択]** セレクターをクリックして、選択したユーザーに割り当てるロールを選択します。

15. **[割り当て]** ボタンをクリックして、選択したユーザーにアプリケーションを割り当てます。

少し待つと、選択したユーザーが、ソリューションの説明セクションで説明されているメソッドを使用してそれらのアプリケーションを起動できるようになります。

## <a name="assign-a-group-directly-to-an-application-as-an-administrator"></a>管理者としてアプリケーションにグループを直接割り当てる

1 つ以上のグループをアプリケーションに直接割り当てるには、次の手順に従います。

1.  [**Azure Portal**](https://portal.azure.com/) を開き、**グローバル管理者**としてサインインします。

2.  左側のメイン ナビゲーション メニューの上部にある **[すべてのサービス]** をクリックして **[Azure Active Directory 拡張機能]** を開きます。

3.  フィルター検索ボックスに「**Azure Active Directory**」と入力し、**[Azure Active Directory]** 項目を選択します。

4.  Azure Active Directory の左側にあるナビゲーション メニューで **[エンタープライズ アプリケーション]** をクリックします。

5.  **[すべてのアプリケーション]** をクリックして、すべてのアプリケーションの一覧を表示します。

  * ここに表示したいアプリケーションが表示されない場合は、**[All Applications List (すべてのアプリケーション リスト)]** の上部にある **[フィルター]** コントロールを使用して、**[表示]** オプションを **[すべてのアプリケーション]** に設定します。

6.  ユーザーを割り当てるアプリケーションを一覧から選びます。

7.  アプリケーションが読み込まれたら、アプリケーションの左側のナビゲーション メニューで **[ユーザーとグループ]** をクリックします。

8.  **[ユーザーとグループ]** 一覧の上部にある **[追加]** ボタンをクリックして、**[割り当ての追加]** ウィンドウを開きます。

9.  **[割り当ての追加]** ウィンドウから **[ユーザーとグループ]** セレクターをクリックします。

10. **[名前または電子メール アドレスで検索]** 検索ボックスに、割り当てるグループの**完全なグループ名**を入力します。

11. リスト内で**グループ**にポインターを合わせ、**チェック ボックス**を表示します。 グループのプロファイル写真またはロゴの横にあるチェック ボックスをオンにして、ユーザーを **[選択済み]** リストに追加します。

12. **省略可能:** **複数のグループを追加**する場合、別の**完全なグループ名**を **[名前または電子メール アドレスで検索]** 検索ボックスに入力し、チェック ボックスをオンにして、**[選択済み]** リストにこのグループを追加します。

13. グループの選択が完了したら、**[選択]** ボタンをクリックして、アプリケーションに割り当てるユーザーとグループの一覧に追加します。

14. **省略可能:** **[割り当ての追加]** ウィンドウで **[ロールの選択]** セレクターをクリックして、選択したグループに割り当てるロールを選択します。

15. **[割り当て]** ボタンをクリックして、選択したグループにアプリケーションを割り当てます。

少し待つと、選択したグループ内のユーザーが、ソリューションの説明セクションで説明されているメソッドを使用してそれらのアプリケーションを起動できるようになります。 これらが動的グループである場合、割り当てられているグループ内のユーザーに割り当てが表示されるまでに、さらに処理時間がかかる可能性があります。

## <a name="enable-self-service-application-access-to-allow-users-to-find-their-own-applications"></a>セルフ サービス アプリケーションへのアクセスを有効にすることでユーザーによる独自のアプリケーションの検索を許可する

セルフ サービス アプリケーションへのアクセスは、ユーザーにアプリケーションの自己検出を許可したり、必要に応じてビジネス グループによるこれらのアプリケーションへのアクセス承認を許可したりする場合に優れた方法です。 ビジネス グループがアクセス パネルから直接、ユーザーに割り当てられた (パスワード シングル サインオン アプリケーションに関する)資格情報を管理できるようにすることができます。

アプリケーションに対するセルフ サービス アクセスを有効にするには、次の手順を実行します。

1.  [**Azure Portal**](https://portal.azure.com/) を開き、**グローバル管理者**としてサインインします。

2.  左側のメイン ナビゲーション メニューの上部にある **[すべてのサービス]** をクリックして **[Azure Active Directory 拡張機能]** を開きます。

3.  フィルター検索ボックスに「**Azure Active Directory**」と入力し、**[Azure Active Directory]** 項目を選択します。

4.  Azure Active Directory の左側にあるナビゲーション メニューで **[エンタープライズ アプリケーション]** をクリックします。

5.  **[すべてのアプリケーション]** をクリックして、すべてのアプリケーションの一覧を表示します。

   * ここに表示したいアプリケーションが表示されない場合は、**[All Applications List (すべてのアプリケーション リスト)]** の上部にある **[フィルター]** コントロールを使用して、**[表示]** オプションを **[すべてのアプリケーション]** に設定します。

6.  セルフサービス アクセスを有効にするアプリケーションを一覧から選択します。

7.  アプリケーションを読み込んだら、アプリケーションの左側にあるナビゲーション メニューで **[セルフサービス]** をクリックします。

8.  このアプリケーションへのセルフ サービス アプリケーションのアクセスを有効にするには、**[このアプリケーションへのアクセスの要求をユーザーに許可しますか?]** トグルを **[はい]** にします。

9.  次に、このアプリケーションへのアクセスを要求するユーザーを追加するグループを選択するには、**[割り当てられたユーザーが追加されるグループ]** ラベルの横にあるセレクターをクリックしてグループを選択します。

10. **省略可能:** ユーザーのアクセスが許可される前にビジネス承認が必要な場合は、**[このアプリケーションへのアクセスを許可する前に承認が必要ですか?]** トグルを **[はい]** に設定します。

11. **省略可能: パスワード シングル サインオンのみを使用するアプリケーションで、** これらのビジネス承認者による承認されたユーザーへのアプリケーションに送信されるパスワードの指定を許可する場合、**[このアプリケーションに対するユーザーのパスワードを設定することを承認者に許可しますか?]** トグルを **[はい]** に設定します。

12. **省略可能:** このアプリケーションへのアクセスの承認を許可するビジネス承認者を指定するには、**[このアプリケーションへのアクセスの承認が許可されているユーザー]** ラベルの横にあるセレクターをクリックして、最大 10 人のビジネス承認者を選択します。

  >[!NOTE]
  >グループはサポートされていません。
  >
  >

13. **省略可能:** **ロールを公開するアプリケーションで**セルフ サービス アクセスが承認されたユーザーをロールに割り当てるには、**[このアプリケーションでは、どのロールにユーザーを割り当てる必要がありますか?]** の横にあるセレクターをクリックして、これらのユーザーに割り当てられる必要のあるロールを選択します。

14. ウィンドウの上部にある **[保存]** をクリックして完了します。

セルフ サービス アプリケーションの構成を完了したら、ユーザーは [[アプリケーション アクセス パネル]](https://myapps.microsoft.com/) に移動して **[+ 追加]** ボタンをクリックすることで、セルフ サービス アクセスが有効なアプリを検索できます。 ビジネス承認者には、[[アプリケーション アクセス パネル]](https://myapps.microsoft.com/) に通知も表示されます。 ユーザーが、承認が必要なアプリケーションへのアクセスを要求した場合、それを通知する電子メールを有効にできます。 

これらの承認は、単一の承認ワークフローでのみサポートされます。つまり、複数の承認者を指定しても、いずれか 1 人の承認者がアプリケーションへのアクセスを承認する可能性があります。

## <a name="next-steps"></a>次の手順
[アプリケーション プロキシを使用してアプリにシングル サインオンを提供](manage-apps/application-proxy-configure-single-sign-on-with-kcd.md)
