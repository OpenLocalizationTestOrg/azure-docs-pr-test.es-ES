---
title: Uso del conector de SharePoint Server en Logic Apps | Microsoft Docs
description: "Introducción al uso del conector de SharePoint Server en Logic Apps"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 0238a060-d592-4719-b7a2-26064c437a1a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 0f3274816e279a1aa57febaa2f8294914900799a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-sharepoint-connector"></a><span data-ttu-id="38989-103">Introducción al conector de SharePoint</span><span class="sxs-lookup"><span data-stu-id="38989-103">Get started with the SharePoint connector</span></span>
<span data-ttu-id="38989-104">El conector de SharePoint ofrece una manera de trabajar con listas en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="38989-104">The SharePoint Connector provides an way to work with Lists on SharePoint.</span></span>

<span data-ttu-id="38989-105">Para empezar, cree una aplicación lógica; consulte [Creación de su primer flujo de trabajo de aplicación lógica para automatizar los procesos entre aplicaciones de nube y servicios en la nube](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="38989-105">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-sharepoint"></a><span data-ttu-id="38989-106">Creación de una conexión a SharePoint</span><span class="sxs-lookup"><span data-stu-id="38989-106">Create a connection to SharePoint</span></span>
<span data-ttu-id="38989-107">Para usar el conector de SharePoint, cree primero una **conexión** y, después, especifique los detalles de las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="38989-107">To use the SharePoint Connector , you first create a **connection** then provide the details for these properties:</span></span> 

| <span data-ttu-id="38989-108">Propiedad</span><span class="sxs-lookup"><span data-stu-id="38989-108">Property</span></span> | <span data-ttu-id="38989-109">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="38989-109">Required</span></span> | <span data-ttu-id="38989-110">Descripción</span><span class="sxs-lookup"><span data-stu-id="38989-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38989-111">Se necesita el cifrado de tokens</span><span class="sxs-lookup"><span data-stu-id="38989-111">Token</span></span> |<span data-ttu-id="38989-112">Sí</span><span class="sxs-lookup"><span data-stu-id="38989-112">Yes</span></span> |<span data-ttu-id="38989-113">Proporcionar credenciales de SharePoint</span><span class="sxs-lookup"><span data-stu-id="38989-113">Provide SharePoint Credentials</span></span> |

<span data-ttu-id="38989-114">Para poder establecer la conexión con **SharePoint**, especifique su identidad (nombre de usuario y contraseña, credenciales de tarjeta inteligente, etc.) a SharePoint.</span><span class="sxs-lookup"><span data-stu-id="38989-114">To connect to **SharePoint**, enter your identity (username and password, smart card credentials, etc.) to SharePoint.</span></span> <span data-ttu-id="38989-115">Después de autenticarse, podrá usar el conector de SharePoint en la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="38989-115">Once you've been authenticated, you can proceed to use the SharePoint connector  in your logic app.</span></span> 

<span data-ttu-id="38989-116">Mientras se encuentra en el diseñador de la aplicación lógica, siga estos pasos para iniciar sesión en SharePoint y crear la **conexión** para su uso en la aplicación lógica:</span><span class="sxs-lookup"><span data-stu-id="38989-116">While on the designer of your logic app, follow these steps to sign into SharePoint to create the connection **connection** for use in your logic app:</span></span>

1. <span data-ttu-id="38989-117">Escriba SharePoint en el cuadro de búsqueda y espere a que la búsqueda devuelva todas las entradas que incluyan SharePoint en el nombre:</span><span class="sxs-lookup"><span data-stu-id="38989-117">Enter SharePoint in the search box and wait for the search to return all entries with SharePoint in the name:</span></span>   
   ![Configurar SharePoint][1]  
2. <span data-ttu-id="38989-119">Seleccione **SharePoint - Cuando se crea un archivo**</span><span class="sxs-lookup"><span data-stu-id="38989-119">Select **SharePoint - When a file is created**</span></span>   
3. <span data-ttu-id="38989-120">Seleccione **Sign in to SharePoint** (Iniciar sesión en SharePoint):</span><span class="sxs-lookup"><span data-stu-id="38989-120">Select **Sign in to SharePoint**:</span></span>   
   <span data-ttu-id="38989-121">![Configurar SharePoint][2]</span><span class="sxs-lookup"><span data-stu-id="38989-121">![Configure SharePoint][2]</span></span>    
4. <span data-ttu-id="38989-122">Proporcione sus credenciales de SharePoint para iniciar sesión para autenticarse con SharePoint </span><span class="sxs-lookup"><span data-stu-id="38989-122">Provide your SharePoint credentials to sign in to authenticate with SharePoint</span></span>   
   ![Configurar SharePoint][3]     
5. <span data-ttu-id="38989-124">Una vez completada la autenticación se le redirigirá a la aplicación lógica para terminar mediante la configuración del diálogo de SharePoint **Cuando se crea un archivo** .</span><span class="sxs-lookup"><span data-stu-id="38989-124">After the authentication completes you'll be redirected to your logic app to complete it by configuring SharePoint's **When a file is created** dialog.</span></span>          
   <span data-ttu-id="38989-125">![Configurar SharePoint][4]</span><span class="sxs-lookup"><span data-stu-id="38989-125">![Configure SharePoint][4]</span></span>  
6. <span data-ttu-id="38989-126">A continuación, puede agregar otros desencadenadores y acciones que necesita para completar la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="38989-126">You can then add other triggers and actions that you need to complete your logic app.</span></span>   
7. <span data-ttu-id="38989-127">Guarde el trabajo seleccionando **Guardar** en la barra de menús superior.</span><span class="sxs-lookup"><span data-stu-id="38989-127">Save your work by selecting **Save** on the menu bar above.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="38989-128">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="38989-128">Connector-specific details</span></span>

<span data-ttu-id="38989-129">Vea los desencadenadores y las acciones definidos en Swagger y vea también todos los límites en los [detalles del conector](/connectors/sharepoint/).</span><span class="sxs-lookup"><span data-stu-id="38989-129">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sharepoint/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="38989-130">Más conectores</span><span class="sxs-lookup"><span data-stu-id="38989-130">More connectors</span></span>
<span data-ttu-id="38989-131">Volver a la [lista de API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="38989-131">Go back to the [APIs list](apis-list.md).</span></span>

[1]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig1.png  
[2]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig2.png 
[3]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig3.png
[4]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig4.png
[5]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig5.png
