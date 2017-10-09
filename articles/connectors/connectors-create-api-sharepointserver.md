---
title: "Hola aaaUse conector de servidor de SharePoint en las aplicaciones lógicas | Documentos de Microsoft"
description: "Introducción al uso Hola Hola conector de servidor de SharePoint en las aplicaciones lógicas"
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
ms.openlocfilehash: 3b814f42611e4971ff5c94ae3b021829217911dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sharepoint-connector"></a><span data-ttu-id="f9fb1-103">Empezar a trabajar con el conector de SharePoint de Hola</span><span class="sxs-lookup"><span data-stu-id="f9fb1-103">Get started with hello SharePoint connector</span></span>
<span data-ttu-id="f9fb1-104">Hola conector de SharePoint proporciona un toowork manera con listas en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f9fb1-104">hello SharePoint Connector provides an way toowork with Lists on SharePoint.</span></span>

<span data-ttu-id="f9fb1-105">Para empezar, cree una aplicación lógica; consulte [Creación de su primer flujo de trabajo de aplicación lógica para automatizar los procesos entre aplicaciones de nube y servicios en la nube](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f9fb1-105">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-toosharepoint"></a><span data-ttu-id="f9fb1-106">Crear una conexión tooSharePoint</span><span class="sxs-lookup"><span data-stu-id="f9fb1-106">Create a connection tooSharePoint</span></span>
<span data-ttu-id="f9fb1-107">toouse Hola conector de SharePoint, cree primero un **conexión** especifique los detalles de Hola de estas propiedades:</span><span class="sxs-lookup"><span data-stu-id="f9fb1-107">toouse hello SharePoint Connector , you first create a **connection** then provide hello details for these properties:</span></span> 

| <span data-ttu-id="f9fb1-108">Propiedad</span><span class="sxs-lookup"><span data-stu-id="f9fb1-108">Property</span></span> | <span data-ttu-id="f9fb1-109">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="f9fb1-109">Required</span></span> | <span data-ttu-id="f9fb1-110">Descripción</span><span class="sxs-lookup"><span data-stu-id="f9fb1-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f9fb1-111">Se necesita el cifrado de tokens</span><span class="sxs-lookup"><span data-stu-id="f9fb1-111">Token</span></span> |<span data-ttu-id="f9fb1-112">Sí</span><span class="sxs-lookup"><span data-stu-id="f9fb1-112">Yes</span></span> |<span data-ttu-id="f9fb1-113">Proporcionar credenciales de SharePoint</span><span class="sxs-lookup"><span data-stu-id="f9fb1-113">Provide SharePoint Credentials</span></span> |

<span data-ttu-id="f9fb1-114">tooconnect demasiado**SharePoint**, escriba su tooSharePoint de identidad (nombre de usuario y contraseña, las credenciales de tarjeta inteligente, etc.).</span><span class="sxs-lookup"><span data-stu-id="f9fb1-114">tooconnect too**SharePoint**, enter your identity (username and password, smart card credentials, etc.) tooSharePoint.</span></span> <span data-ttu-id="f9fb1-115">Una vez que haya autenticado, puede continuar conector de SharePoint de hello toouse en la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="f9fb1-115">Once you've been authenticated, you can proceed toouse hello SharePoint connector  in your logic app.</span></span> 

<span data-ttu-id="f9fb1-116">Mientras que en el Diseñador de hello de la aplicación lógica, siga estos pasos toosign en conexión de SharePoint toocreate hello **conexión** para su uso en la aplicación lógica:</span><span class="sxs-lookup"><span data-stu-id="f9fb1-116">While on hello designer of your logic app, follow these steps toosign into SharePoint toocreate hello connection **connection** for use in your logic app:</span></span>

1. <span data-ttu-id="f9fb1-117">Escriba SharePoint en el cuadro de búsqueda de Hola y espere Hola búsqueda tooreturn todas las entradas con SharePoint en nombre de hello:</span><span class="sxs-lookup"><span data-stu-id="f9fb1-117">Enter SharePoint in hello search box and wait for hello search tooreturn all entries with SharePoint in hello name:</span></span>   
   ![Configurar SharePoint][1]  
2. <span data-ttu-id="f9fb1-119">Seleccione **SharePoint - Cuando se crea un archivo**</span><span class="sxs-lookup"><span data-stu-id="f9fb1-119">Select **SharePoint - When a file is created**</span></span>   
3. <span data-ttu-id="f9fb1-120">Seleccione **iniciar sesión en tooSharePoint**:</span><span class="sxs-lookup"><span data-stu-id="f9fb1-120">Select **Sign in tooSharePoint**:</span></span>   
   <span data-ttu-id="f9fb1-121">![Configurar SharePoint][2]</span><span class="sxs-lookup"><span data-stu-id="f9fb1-121">![Configure SharePoint][2]</span></span>    
4. <span data-ttu-id="f9fb1-122">Proporcione su toosign de credenciales de SharePoint en tooauthenticate con SharePoint</span><span class="sxs-lookup"><span data-stu-id="f9fb1-122">Provide your SharePoint credentials toosign in tooauthenticate with SharePoint</span></span>   
   ![Configurar SharePoint][3]     
5. <span data-ttu-id="f9fb1-124">Una vez completa la autenticación de hello estará tooyour redirigida lógica aplicación toocomplete, mediante la configuración de SharePoint **cuando se crea un archivo** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f9fb1-124">After hello authentication completes you'll be redirected tooyour logic app toocomplete it by configuring SharePoint's **When a file is created** dialog.</span></span>          
   <span data-ttu-id="f9fb1-125">![Configurar SharePoint][4]</span><span class="sxs-lookup"><span data-stu-id="f9fb1-125">![Configure SharePoint][4]</span></span>  
6. <span data-ttu-id="f9fb1-126">A continuación, puede agregar otros desencadenadores y las acciones que necesita toocomplete la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="f9fb1-126">You can then add other triggers and actions that you need toocomplete your logic app.</span></span>   
7. <span data-ttu-id="f9fb1-127">Guarde su trabajo mediante la selección **guardar** en la barra de menús de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="f9fb1-127">Save your work by selecting **Save** on hello menu bar above.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="f9fb1-128">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="f9fb1-128">Connector-specific details</span></span>

<span data-ttu-id="f9fb1-129">Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/sharepoint/).</span><span class="sxs-lookup"><span data-stu-id="f9fb1-129">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sharepoint/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="f9fb1-130">Más conectores</span><span class="sxs-lookup"><span data-stu-id="f9fb1-130">More connectors</span></span>
<span data-ttu-id="f9fb1-131">Volver atrás toohello [lista de las API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="f9fb1-131">Go back toohello [APIs list](apis-list.md).</span></span>

[1]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig1.png  
[2]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig2.png 
[3]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig3.png
[4]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig4.png
[5]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig5.png
