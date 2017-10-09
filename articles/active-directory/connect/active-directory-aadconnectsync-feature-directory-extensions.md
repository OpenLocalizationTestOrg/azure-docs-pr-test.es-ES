---
title: "Sincronización de Azure AD Connect: Extensiones de directorio | Microsoft Docs"
description: "Este tema describe la característica de extensiones de directorio de hello en Azure AD Connect."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 995ee876-4415-4bb0-a258-cca3cbb02193
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 31525ae914aa4d9e047ea1515b460a8311d5c815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-directory-extensions"></a><span data-ttu-id="ea91e-103">Sincronización de Azure AD Connect: Extensiones de directorio</span><span class="sxs-lookup"><span data-stu-id="ea91e-103">Azure AD Connect sync: Directory extensions</span></span>
<span data-ttu-id="ea91e-104">Extensiones de directorio permite esquemas de hello tooextend en Azure AD con sus propios atributos de la instancia local de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ea91e-104">Directory extensions allows you tooextend hello schema in Azure AD with your own attributes from on-premises Active Directory.</span></span> <span data-ttu-id="ea91e-105">Esta característica le permite consumir atributos continuar toomanage local toobuild las aplicaciones LOB.</span><span class="sxs-lookup"><span data-stu-id="ea91e-105">This feature allows you toobuild LOB apps consuming attributes you continue toomanage on-premises.</span></span> <span data-ttu-id="ea91e-106">Estos atributos se pueden consumir mediante [extensiones de directorio de Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) o [Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="ea91e-106">These attributes can be consumed through [Azure AD Graph directory extensions](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) or [Microsoft Graph](https://graph.microsoft.io/).</span></span> <span data-ttu-id="ea91e-107">Puede ver Hola atributos disponible mediante [explorer de Azure AD Graph](https://graphexplorer.cloudapp.net) y [el Explorador de Microsoft Graph](https://graphexplorer2.azurewebsites.net/) respectivamente.</span><span class="sxs-lookup"><span data-stu-id="ea91e-107">You can see hello attributes available using [Azure AD Graph explorer](https://graphexplorer.cloudapp.net) and [Microsoft Graph explorer](https://graphexplorer2.azurewebsites.net/) respectively.</span></span>

<span data-ttu-id="ea91e-108">En la actualidad, ninguna carga de trabajo de Office 365 consume estos atributos.</span><span class="sxs-lookup"><span data-stu-id="ea91e-108">At present no Office 365 workload consumes these attributes.</span></span>

<span data-ttu-id="ea91e-109">Configurar los atributos adicionales que desee toosynchronize en la ruta de acceso de configuración personalizada de hello en el Asistente para la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea91e-109">You configure which additional attributes you want toosynchronize in hello custom settings path in hello installation wizard.</span></span>
<span data-ttu-id="ea91e-110">![Asistente para la extensión de esquema](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span><span class="sxs-lookup"><span data-stu-id="ea91e-110">![Schema Extension Wizard](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span></span>  
<span data-ttu-id="ea91e-111">instalación de Hello muestra hello siguientes atributos, que son candidatas válidas:</span><span class="sxs-lookup"><span data-stu-id="ea91e-111">hello installation shows hello following attributes, which are valid candidates:</span></span>

* <span data-ttu-id="ea91e-112">Tipos de objetos de usuario y de grupo</span><span class="sxs-lookup"><span data-stu-id="ea91e-112">User and Group object types</span></span>
* <span data-ttu-id="ea91e-113">Atributos de valor único: cadena, booleano, entero y binario</span><span class="sxs-lookup"><span data-stu-id="ea91e-113">Single-valued attributes: String, Boolean, Integer, Binary</span></span>
* <span data-ttu-id="ea91e-114">Atributos multivalor: cadena y binario</span><span class="sxs-lookup"><span data-stu-id="ea91e-114">Multi-valued attributes: String, Binary</span></span>

<span data-ttu-id="ea91e-115">lista de Hola de atributos es de lectura de caché de esquema de hello creado durante la instalación de Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="ea91e-115">hello list of attributes is read from hello schema cache created during installation of Azure AD Connect.</span></span> <span data-ttu-id="ea91e-116">Si se ha ampliado el esquema de Active Directory de hello con atributos adicionales, Hola [se debe actualizar el esquema](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) antes de que estos nuevos atributos están visibles.</span><span class="sxs-lookup"><span data-stu-id="ea91e-116">If you have extended hello Active Directory schema with additional attributes, then hello [schema must be refreshed](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) before these new attributes are visible.</span></span>

<span data-ttu-id="ea91e-117">Un objeto en Azure AD puede tener los atributos de las extensiones de directorio too100.</span><span class="sxs-lookup"><span data-stu-id="ea91e-117">An object in Azure AD can have up too100 directory extensions attributes.</span></span> <span data-ttu-id="ea91e-118">longitud máxima de Hello es 250 caracteres.</span><span class="sxs-lookup"><span data-stu-id="ea91e-118">hello max length is 250 characters.</span></span> <span data-ttu-id="ea91e-119">Si un valor de atributo es más largo, se trunca el motor de sincronización Hola.</span><span class="sxs-lookup"><span data-stu-id="ea91e-119">If an attribute value is longer, then it is truncated by hello sync engine.</span></span>

<span data-ttu-id="ea91e-120">Durante la instalación de Azure AD Connect, se registra una aplicación donde estos atributos estén disponibles.</span><span class="sxs-lookup"><span data-stu-id="ea91e-120">During installation of Azure AD Connect, an application is registered where these attributes are available.</span></span> <span data-ttu-id="ea91e-121">Puede ver esta aplicación Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ea91e-121">You can see this application in hello Azure portal.</span></span>  
![Aplicación de extensión de esquema](./media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

<span data-ttu-id="ea91e-123">Estos atributos están ahora disponibles en Graph: </span><span class="sxs-lookup"><span data-stu-id="ea91e-123">These attributes are now available through Graph:</span></span>  
![Grafo](./media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

<span data-ttu-id="ea91e-125">atributos de Hello tienen el prefijo con la extensión\_{AppClientId}\_.</span><span class="sxs-lookup"><span data-stu-id="ea91e-125">hello attributes are prefixed with extension\_{AppClientId}\_.</span></span> <span data-ttu-id="ea91e-126">Hola AppClientId tiene Hola mismo valor para todos los atributos en el inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea91e-126">hello AppClientId has hello same value for all attributes in your Azure AD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea91e-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ea91e-127">Next steps</span></span>
<span data-ttu-id="ea91e-128">Obtener más información sobre hello [sincronización de Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuración.</span><span class="sxs-lookup"><span data-stu-id="ea91e-128">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="ea91e-129">Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="ea91e-129">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
