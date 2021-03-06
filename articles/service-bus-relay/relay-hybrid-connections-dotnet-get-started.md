---
title: .NET での Azure Relay ハイブリッド接続 Websocket の概要 | Microsoft Docs
description: Azure Relay ハイブリッド接続 Websocket 用 C# コンソール アプリケーションを作成します。
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: ''
ms.assetid: d1386900-b942-4abf-acfc-38d2ef826253
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 12/15/2017
ms.author: sethm
ms.openlocfilehash: 5b900f70721f8642e27daf242295fbda77d7df6f
ms.sourcegitcommit: 0a84b090d4c2fb57af3876c26a1f97aac12015c5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/11/2018
ms.locfileid: "38680846"
---
# <a name="get-started-with-relay-hybrid-connections-websockets-in-net"></a>.NET での Relay ハイブリッド接続 Websocket の概要
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

このチュートリアルでは、[Azure Relay ハイブリッド接続](relay-what-is-it.md#hybrid-connections)の概要を紹介します。 対応するリスナー アプリケーションにメッセージを送信するクライアント アプリケーションを作成するために、Microsoft .NET を使用する方法を説明します。 

## <a name="what-will-be-accomplished"></a>作業内容
ハイブリッド接続では、クライアント コンポーネントとサーバー コンポーネントの両方が必要です。 このチュートリアルでは、次の手順に従って 2 つのコンソール アプリケーションを作成します。

1. Azure Portal を使用した Relay 名前空間の作成
2. Azure Portal を使用した、その名前空間内のハイブリッド接続の作成
3. メッセージを受信するサーバー (リスナー) コンソール アプリケーションの作成
4. メッセージを送信するクライアント (送信側) コンソール アプリケーションの作成

## <a name="prerequisites"></a>前提条件

このチュートリアルを完了するには、次の前提条件を用意しておく必要があります。

* [Visual Studio 2015 またはそれ以降](http://www.visualstudio.com)。 このチュートリアルの例では、Visual Studio 2017 を使用します。
* Azure サブスクリプション。

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-by-using-the-azure-portal"></a>1.Azure Portal を使用した名前空間の作成
Relay 名前空間を既に作成してある場合は、「[Azure Portal を使用したハイブリッド接続の作成](#2-create-a-hybrid-connection-using-the-azure-portal)」に進んでください。

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-by-using-the-azure-portal"></a>2.Azure Portal を使用したハイブリッド接続の作成
ハイブリッド接続を既に作成してある場合は、「[サーバー アプリケーションの作成](#3-create-a-server-application-listener)」に進んでください。

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a>手順 3.サーバー アプリケーション (リスナー) の作成
Visual Studio で C# コンソール アプリケーションを作成して、Relay からのメッセージをリッスンおよび受信します。

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-dotnet-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a>4.クライアント アプリケーション (センダー) の作成
Visual Studio で C# コンソール アプリケーションを作成して、Relay にメッセージを送信します。

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-dotnet-get-started-client.md)]

## <a name="5-run-the-applications"></a>5.アプリケーションの実行
1. サーバー アプリケーションを実行します。
2. クライアント アプリケーションを実行し、何かテキストを入力します。
3. サーバー アプリケーション コンソールに、クライアント アプリケーションで入力したテキストが表示されることを確認します。

![アプリケーションの実行](./media/relay-hybrid-connections-dotnet-get-started/running-applications.png)

これで、エンド ツー エンドのハイブリッド接続アプリケーションを作成できました。

## <a name="next-steps"></a>次の手順

* [Relay に関する FAQ](relay-faq.md)
* [名前空間を作成する](relay-create-namespace-portal.md)
* [Node を使って作業を開始する](relay-hybrid-connections-node-get-started.md)

