---
title: "Problemas al agregar una aplicación de la galería de Azure AD | Microsoft Docs"
description: "Conozca los problemas habituales a los que se enfrentan los usuarios al agregar aplicaciones de la galería de Azure AD y los pasos que se deben dar para resolverlos"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: b3ae472d52208d3c76424d29192c1eb982639572
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="problem-adding-an-azure-ad-gallery-application"></a><span data-ttu-id="3ca8b-103">Problemas al agregar una aplicación de la galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ca8b-103">Problem adding an Azure AD Gallery application</span></span>

<span data-ttu-id="3ca8b-104">Este artículo le ayuda a conocer los problemas habituales a los que se enfrentan los usuarios al agregar aplicaciones de la galería de Azure AD y los pasos que se deben dar para resolverlos.</span><span class="sxs-lookup"><span data-stu-id="3ca8b-104">This article help you to understand the common problems people face when adding Azure AD Gallery applications and what you can do to resolve them.</span></span>

## <a name="i-clicked-the-add-button-and-my-application-took-a-long-time-to-appear"></a><span data-ttu-id="3ca8b-105">Hice clic en el botón "Agregar" y mi aplicación tardó mucho tiempo en aparecer</span><span class="sxs-lookup"><span data-stu-id="3ca8b-105">I clicked the “add” button and my application took a long time to appear</span></span>

<span data-ttu-id="3ca8b-106">En algunas circunstancias, una aplicación puede tardar entre 1 y 2 minutos (a veces, más) en aparecer después de agregarla a su directorio.</span><span class="sxs-lookup"><span data-stu-id="3ca8b-106">Under some circumstances, it can take 1-2 minutes (and sometimes longer) for an application to appear after adding it to your directory.</span></span> <span data-ttu-id="3ca8b-107">Aunque este no es el rendimiento normal esperable, puede ver si la incorporación de la aplicación está en curso haciendo clic en el icono de **notificaciones** (la campana) de la esquina superior derecha de [Azure Portal](https://portal.azure.com/) y buscando una notificación **En curso** o **Completado** con la etiqueta **Crear aplicación**.</span><span class="sxs-lookup"><span data-stu-id="3ca8b-107">While this is not the normal expected performance, you can see the application addition is in progress by clicking on the **Notifications** icon (the bell) in the upper right of the [Azure Portal](https://portal.azure.com/) and looking for an **In Progress** or **Completed** notification labeled **Create application.**</span></span>

<span data-ttu-id="3ca8b-108">Si la aplicación nunca se agrega o se produce un error al hacer clic en el botón **Agregar**, verá una **notificación** con un estado de **Error**.</span><span class="sxs-lookup"><span data-stu-id="3ca8b-108">If your application is never added, or you encounter an error when clicking the **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="3ca8b-109">Si desea obtener más detalles sobre el error para conocer más información o compartirlo con un ingeniero de soporte técnico, puede ver más información sobre el error siguiendo los pasos descritos en [Visualización de los detalles de una notificación del portal](#how-to-see-the-details-of-a-portal-notification).</span><span class="sxs-lookup"><span data-stu-id="3ca8b-109">If you want more details about the error to learn more to or share with a support engingeer, you can see more information about the error by following the steps in the [How to see the details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

## <a name="i-clicked-the-add-button-and-my-application-didnt-appear"></a><span data-ttu-id="3ca8b-110">Hice clic en el botón "Agregar" y mi aplicación no apareció</span><span class="sxs-lookup"><span data-stu-id="3ca8b-110">I clicked the “add” button and my application didn’t appear</span></span>

<span data-ttu-id="3ca8b-111">En ocasiones, debido a problemas transitorios, problemas de red o un error, se produce un error al agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3ca8b-111">Sometimes, due to transient issues, networking problems, or a bug, adding an application fail.</span></span> <span data-ttu-id="3ca8b-112">Puede indicar si esto ocurre si hace clic en el icono de **notificaciones** (la campana) de la esquina superior derecha de Azure Portal y aparece un icono (!) de color rojo junto a la notificación **Crear aplicación**.</span><span class="sxs-lookup"><span data-stu-id="3ca8b-112">You can tell this happens when you click the **Notifications** icon (the bell) in the upper right of the Azure Portal and you see a red (!) icon next to your **Create application** notification.</span></span> <span data-ttu-id="3ca8b-113">Esto indica que se produjo un error al crear la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3ca8b-113">This indicates there was an error when creating the application.</span></span>

<span data-ttu-id="3ca8b-114">Si se produce un error al hacer clic en el botón **Agregar**, verá una **notificación** con un estado de **Error**.</span><span class="sxs-lookup"><span data-stu-id="3ca8b-114">If you encounter an error when clicking the **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="3ca8b-115">Si desea obtener más detalles sobre el error para conocer más información o compartirlo con un ingeniero de soporte técnico, puede ver más información sobre el error siguiendo los pasos descritos en [Visualización de los detalles de una notificación del portal](#how-to-see-the-details-of-a-portal-notification).</span><span class="sxs-lookup"><span data-stu-id="3ca8b-115">If you want more details about the error to learn more to or share with a support engingeer, you can see more information about the error by following the steps in the [How to see the details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

 ## <a name="i-dont-know-how-to-set-up-my-application-once-ive-added-it"></a><span data-ttu-id="3ca8b-116">No sé cómo configurar mi aplicación una vez que la he agregado</span><span class="sxs-lookup"><span data-stu-id="3ca8b-116">I don’t know how to set up my application once I’ve added it</span></span>

<span data-ttu-id="3ca8b-117">Si necesita ayuda para obtener información sobre las aplicaciones, el artículo [Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list) es un buen punto de partida.</span><span class="sxs-lookup"><span data-stu-id="3ca8b-117">If you need help learning about applications, the [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list) article is a good place to start.</span></span>

<span data-ttu-id="3ca8b-118">Además, la [biblioteca de documentos de las aplicaciones de Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) le ayudará a obtener más información sobre el inicio de sesión único con Azure AD y cómo funciona.</span><span class="sxs-lookup"><span data-stu-id="3ca8b-118">In addition to this, the [Azure AD Applications Document Library](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) help you to learn more about single sign-on with Azure AD and how it works.</span></span>

## <a name="how-to-see-the-details-of-a-portal-notification"></a><span data-ttu-id="3ca8b-119">Visualización de los detalles de una notificación del portal</span><span class="sxs-lookup"><span data-stu-id="3ca8b-119">How to see the details of a portal notification</span></span>

<span data-ttu-id="3ca8b-120">Puede ver los detalles de cualquier notificación del portal si sigue los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3ca8b-120">You can see the details of any portal notification by following the steps below:</span></span>

1.  <span data-ttu-id="3ca8b-121">Haga clic en el icono de **notificaciones** (la campana) de la esquina superior derecha de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3ca8b-121">click the **Notifications** icon (the bell) in the upper right of the Azure Portal</span></span>

2.  <span data-ttu-id="3ca8b-122">Seleccione cualquier notificación con un estado de **Error** (aquellas con un icono (!) de color rojo situado junto a ellas).</span><span class="sxs-lookup"><span data-stu-id="3ca8b-122">Select any notification in an **Error** state (those with a red (!) next to them).</span></span>

    >[!NOTE]
    ><span data-ttu-id="3ca8b-123">No puede hacer clic en notificaciones con un estado **Correcto** o **En curso**.</span><span class="sxs-lookup"><span data-stu-id="3ca8b-123">You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
    >
    >

3.  <span data-ttu-id="3ca8b-124">Esto hace que se abra la hoja **Detalles de la notificación**.</span><span class="sxs-lookup"><span data-stu-id="3ca8b-124">This open the **Notification Details** blade.</span></span>

4.  <span data-ttu-id="3ca8b-125">Utilice esta información para conocer más detalles acerca del problema.</span><span class="sxs-lookup"><span data-stu-id="3ca8b-125">Use this information yourself to understand more details about the problem.</span></span>

5.  <span data-ttu-id="3ca8b-126">Si aún necesita ayuda, también puede compartir esta información con un ingeniero de soporte técnico o el grupo de producto para obtener ayuda.</span><span class="sxs-lookup"><span data-stu-id="3ca8b-126">If you still need help, you can also share this information with a support engineer or the product group to get help with your problem.</span></span>

6.  <span data-ttu-id="3ca8b-127">Haga clic en el **icono** de **copia** situado a la derecha del cuadro de texto **Copiar error** para copiar todos los detalles de la notificación para compartirlos con un ingeniero de soporte técnico o un grupo de producto</span><span class="sxs-lookup"><span data-stu-id="3ca8b-127">Click the **copy** **icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer</span></span>

## <a name="how-to-get-help-by-sending-notification-details-to-a-support-engineer"></a><span data-ttu-id="3ca8b-128">Obtención de ayuda mediante el envío de detalles de la notificación a un ingeniero de soporte técnico</span><span class="sxs-lookup"><span data-stu-id="3ca8b-128">How to get help by sending notification details to a support engineer</span></span>

<span data-ttu-id="3ca8b-129">Es muy importante que comparta **todos los detalles que se muestran a continuación** con un ingeniero de soporte técnico si necesita ayuda, para que pueda ayudarle rápidamente.</span><span class="sxs-lookup"><span data-stu-id="3ca8b-129">It is very important that you share **all the details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="3ca8b-130">Puede hacer esto fácilmente **realizando una captura de pantalla** o haciendo clic en el **icono Copiar error**, que se encuentra a la derecha del cuadro de texto **Copiar error**.</span><span class="sxs-lookup"><span data-stu-id="3ca8b-130">You can do this easily by **taking a screenshot,** or by clicking the **Copy error icon**, found to the right of the **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="3ca8b-131">Explicación de los detalles de la notificación</span><span class="sxs-lookup"><span data-stu-id="3ca8b-131">Notification Details Explained</span></span>

<span data-ttu-id="3ca8b-132">A continuación se explica más en profundidad lo que significa cada uno de los elementos de notificación y se dan ejemplos de cada uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="3ca8b-132">The below explains more what each of the notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="3ca8b-133">Elementos esenciales de notificación</span><span class="sxs-lookup"><span data-stu-id="3ca8b-133">Essential Notification Items</span></span>

-   <span data-ttu-id="3ca8b-134">**Título**: el título descriptivo de la notificación</span><span class="sxs-lookup"><span data-stu-id="3ca8b-134">**Title** – the descriptive title of the notification</span></span>

  * <span data-ttu-id="3ca8b-135">Por ejemplo: **Configuración del proxy de aplicación**</span><span class="sxs-lookup"><span data-stu-id="3ca8b-135">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="3ca8b-136">**Descripción**: la descripción de lo que se produjo como resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="3ca8b-136">**Description** – the description of what occurred as a result of the operation</span></span>

    -   <span data-ttu-id="3ca8b-137">Por ejemplo: **la dirección url interna especificada ya se está usando en otra aplicación**</span><span class="sxs-lookup"><span data-stu-id="3ca8b-137">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="3ca8b-138">**Identificador de notificación**: el identificador único de la notificación</span><span class="sxs-lookup"><span data-stu-id="3ca8b-138">**Notification Id** – the unique id of the notification</span></span>

    -   <span data-ttu-id="3ca8b-139">Por ejemplo: **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="3ca8b-139">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="3ca8b-140">**Identificador de solicitud de cliente**: el identificador de solicitud específico generado por el explorador</span><span class="sxs-lookup"><span data-stu-id="3ca8b-140">**Client Request Id** – the specific request id made by your browser</span></span>

    -   <span data-ttu-id="3ca8b-141">Por ejemplo: **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="3ca8b-141">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="3ca8b-142">**Marca de tiempo UTC**: la marca de tiempo durante la que tuvo lugar la notificación, en formato UTC</span><span class="sxs-lookup"><span data-stu-id="3ca8b-142">**Time Stamp UTC** – the timestamp during which the notification occurred, in UTC</span></span>

    -   <span data-ttu-id="3ca8b-143">Por ejemplo: **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="3ca8b-143">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="3ca8b-144">**Identificador de transacción interno**: el identificador interno que podemos utilizar para buscar el error en nuestros sistemas</span><span class="sxs-lookup"><span data-stu-id="3ca8b-144">**Internal Transaction Id** – the internal ID we can use to look the error up in our systems</span></span>

    -   <span data-ttu-id="3ca8b-145">Por ejemplo: **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="3ca8b-145">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="3ca8b-146">**UPN**: el usuario que realizó la operación</span><span class="sxs-lookup"><span data-stu-id="3ca8b-146">**UPN** – the user who performed the operation</span></span>

    -   <span data-ttu-id="3ca8b-147">Por ejemplo: **tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="3ca8b-147">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="3ca8b-148">**Identificador de inquilino**: el identificador único del inquilino del que formaba parte el usuario que realizó la operación</span><span class="sxs-lookup"><span data-stu-id="3ca8b-148">**Tenant Id** – the unique ID of the tenant that the user who performed the operation was a member of</span></span>

    -   <span data-ttu-id="3ca8b-149">Por ejemplo: **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="3ca8b-149">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="3ca8b-150">**Identificador de objeto de usuario**: el identificador único del usuario que realizó la operación</span><span class="sxs-lookup"><span data-stu-id="3ca8b-150">**User object Id** – the unique ID of the user who performed the operation</span></span>

    -   <span data-ttu-id="3ca8b-151">Por ejemplo: **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="3ca8b-151">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="3ca8b-152">Elementos detallados de notificación</span><span class="sxs-lookup"><span data-stu-id="3ca8b-152">Detailed Notification Items</span></span>

-   <span data-ttu-id="3ca8b-153">**Nombre para mostrar**: **(puede estar vacío)** un nombre para mostrar más detallado del error</span><span class="sxs-lookup"><span data-stu-id="3ca8b-153">**Display Name** – **(can be empty)** a more detailed display name for the error</span></span>

    -   <span data-ttu-id="3ca8b-154">Por ejemplo: **Configuración del proxy de aplicación**</span><span class="sxs-lookup"><span data-stu-id="3ca8b-154">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="3ca8b-155">**Estado**: el estado específico de la notificación</span><span class="sxs-lookup"><span data-stu-id="3ca8b-155">**Status** – the specific status of the notification</span></span>

    -   <span data-ttu-id="3ca8b-156">Por ejemplo: **Error**</span><span class="sxs-lookup"><span data-stu-id="3ca8b-156">Example – **Failed**</span></span>

-   <span data-ttu-id="3ca8b-157">**Identificador de objeto**: **(puede estar vacío)** el identificador del objeto en el que se realizó la operación</span><span class="sxs-lookup"><span data-stu-id="3ca8b-157">**Object Id** – **(can be empty)** the object ID against which the operation was performed</span></span>

    -   <span data-ttu-id="3ca8b-158">Por ejemplo: **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="3ca8b-158">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="3ca8b-159">**Detalles**: la descripción detallada de lo que se produjo como resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="3ca8b-159">**Details** – the detailed description of what occurred as a result of the operation</span></span>

    -   <span data-ttu-id="3ca8b-160">Por ejemplo: **la dirección url interna 'http://bing.com/' no es válida puesto que ya está en uso**</span><span class="sxs-lookup"><span data-stu-id="3ca8b-160">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="3ca8b-161">**Copiar error**: haga clic en el **icono de copia** situado a la derecha del cuadro de texto **Copiar error** para copiar todos los detalles de la notificación para compartirlos con un ingeniero de soporte técnico o un grupo de producto</span><span class="sxs-lookup"><span data-stu-id="3ca8b-161">**Copy error** – Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer</span></span>

    -   <span data-ttu-id="3ca8b-162">Por ejemplo, ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="3ca8b-162">Example ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ca8b-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3ca8b-163">Next steps</span></span>
[<span data-ttu-id="3ca8b-164">Administración de aplicaciones con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3ca8b-164">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
