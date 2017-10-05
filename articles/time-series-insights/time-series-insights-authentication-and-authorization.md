---
title: "Configurar la autenticación y la autorización para una aplicación personalizada que llama a la API de Azure Time Series Insights | Microsoft Docs"
description: "En este tutorial se explica cómo configurar la autenticación y la autorización para una aplicación personalizada que llama a la API de Azure Time Series Insights"
keywords: 
services: time-series-insights
documentationcenter: 
author: dmdenmsft
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/24/2017
ms.author: dmden
ms.openlocfilehash: 4dd4865dc556e09a31d2cb7a32768aeb19ba9900
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="authentication-and-authorization-for-azure-time-series-insights-api"></a><span data-ttu-id="40e84-103">Autenticación y autorización para la API de Azure Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="40e84-103">Authentication and authorization for Azure Time Series Insights API</span></span>

<span data-ttu-id="40e84-104">En este artículo se explica cómo configurar una aplicación personalizada que llama a la API de Azure Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="40e84-104">This article explains how to configure a custom application that calls the Azure Time Series Insights API.</span></span>

## <a name="service-principal"></a><span data-ttu-id="40e84-105">Entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="40e84-105">Service principal</span></span>

<span data-ttu-id="40e84-106">En esta sección se explica cómo configurar una aplicación para acceder a la API de Time Series Insights en nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="40e84-106">This section explains how to configure an application to access the Time Series Insights API on behalf of the application.</span></span> <span data-ttu-id="40e84-107">Después la aplicación puede consultar datos o publicar datos de referencia en el entorno de Time Series Insights con las credenciales de la aplicación en lugar de las del usuario.</span><span class="sxs-lookup"><span data-stu-id="40e84-107">The application can then query data or publish reference data in the Time Series Insights environment with application credentials and not the user credentials.</span></span>

<span data-ttu-id="40e84-108">Si tiene una aplicación que necesita acceder a Time Series Insights, debe configurar una aplicación de Azure Active Directory y asignar las directivas de acceso a datos en el entorno de Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="40e84-108">When you have an application that needs to access Time Series Insights, you must set up an Azure Active Directory application and assign the data access policies in the Time Series Insights environment.</span></span> <span data-ttu-id="40e84-109">Este enfoque es preferible a ejecutar la aplicación con sus propias credenciales por los siguientes motivos:</span><span class="sxs-lookup"><span data-stu-id="40e84-109">This approach is preferable to running the app under your own credentials because:</span></span>

* <span data-ttu-id="40e84-110">Puede asignar a la identidad de la aplicación unos permisos distintos a los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="40e84-110">You can assign permissions to the app identity that are different from your own permissions.</span></span> <span data-ttu-id="40e84-111">Normalmente, estos permisos están restringidos a exactamente aquello que la aplicación debe hacer.</span><span class="sxs-lookup"><span data-stu-id="40e84-111">Typically, these permissions are restricted to exactly what the app needs to do.</span></span> <span data-ttu-id="40e84-112">Por ejemplo, puede permitir que la aplicación solo lea datos en un entorno de Time Series Insights determinado.</span><span class="sxs-lookup"><span data-stu-id="40e84-112">For example, you can allow the app to only read data in a particular Time Series Insights environment.</span></span>
* <span data-ttu-id="40e84-113">No es necesario cambiar las credenciales de la aplicación si las responsabilidades cambian.</span><span class="sxs-lookup"><span data-stu-id="40e84-113">You don't have to change the app's credentials if your responsibilities change.</span></span>
* <span data-ttu-id="40e84-114">Puede usar un certificado o una clave de aplicación para automatizar la autenticación cuando vaya a ejecutar un script desatendido.</span><span class="sxs-lookup"><span data-stu-id="40e84-114">You can use a certificate or an application key to automate authentication when you're running an unattended script.</span></span>

<span data-ttu-id="40e84-115">En este artículo se muestra cómo realizar esos pasos a través de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="40e84-115">This article shows you how to perform those steps through the Azure portal.</span></span> <span data-ttu-id="40e84-116">Se centra en una aplicación de un único inquilino diseñada para ejecutarse en una sola organización.</span><span class="sxs-lookup"><span data-stu-id="40e84-116">It focuses on a single-tenant application where the application is intended to run in only one organization.</span></span> <span data-ttu-id="40e84-117">El usuario normalmente usa aplicaciones de un único inquilino para aplicaciones de línea de negocio que se ejecutan en la organización.</span><span class="sxs-lookup"><span data-stu-id="40e84-117">You typically use single-tenant applications for line-of-business applications that run in your organization.</span></span>

<span data-ttu-id="40e84-118">El flujo de configuración consta de tres pasos de alto nivel:</span><span class="sxs-lookup"><span data-stu-id="40e84-118">The setup flow consists of three high-level steps:</span></span>

1. <span data-ttu-id="40e84-119">Creación de una aplicación en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="40e84-119">Create an application in Azure Active Directory.</span></span>
2. <span data-ttu-id="40e84-120">Autorización a esta aplicación a acceder al entorno de Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="40e84-120">Authorize this application to access the Time Series Insights environment.</span></span>
3. <span data-ttu-id="40e84-121">Uso del identificador y la clave de la aplicación para conseguir un token para la audiencia o el recurso de `"https://api.timeseries.azure.com/"`.</span><span class="sxs-lookup"><span data-stu-id="40e84-121">Use the application ID and key to acquire a token to the `"https://api.timeseries.azure.com/"` audience or resource.</span></span> <span data-ttu-id="40e84-122">Luego el token puede usarse para llamar a la API de Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="40e84-122">The token can then be used to call the Time Series Insights API.</span></span>

<span data-ttu-id="40e84-123">Estos son los pasos detallados:</span><span class="sxs-lookup"><span data-stu-id="40e84-123">Here are the detailed steps:</span></span>

1. <span data-ttu-id="40e84-124">En Azure Portal, seleccione **Azure Active Directory** > **Registros de aplicaciones** > **Nuevo registro de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="40e84-124">In the Azure portal, select **Azure Active Directory** > **App registrations** > **New application registration**.</span></span>

   ![Nuevo registro de aplicaciones en Azure Active Directory](media/authentication-and-authorization/active-directory-new-application-registration.png)  

2. <span data-ttu-id="40e84-126">Asigne un nombre a la aplicación, seleccione **Aplicación web o API** como tipo, seleccione cualquier URI válido para **URL de inicio de sesión** y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="40e84-126">Give the application a name, select the type to be **Web app / API**, select any valid URI for **Sign-on URL**, and click **Create**.</span></span>

   ![Creación de la aplicación en Azure Active Directory](media/authentication-and-authorization/active-directory-create-web-api-application.png)

3. <span data-ttu-id="40e84-128">Seleccione la aplicación recién creada y copie su identificador en el editor de texto que prefiera.</span><span class="sxs-lookup"><span data-stu-id="40e84-128">Select your newly created application and copy its application ID to your favorite text editor.</span></span>

   ![Copia del identificador de la aplicación](media/authentication-and-authorization/active-directory-copy-application-id.png)

4. <span data-ttu-id="40e84-130">Seleccione **Claves**, escriba el nombre de la clave, seleccione la expiración y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="40e84-130">Select **Keys**, enter the key name, select the expiration, and click **Save**.</span></span>

   ![Selección de las claves de aplicación](media/authentication-and-authorization/active-directory-application-keys.png)

   ![Especificación y almacenamiento del nombre y la fecha de expiración de la clave](media/authentication-and-authorization/active-directory-application-keys-save.png)

5. <span data-ttu-id="40e84-133">Copie la clave en el editor de texto que prefiera.</span><span class="sxs-lookup"><span data-stu-id="40e84-133">Copy the key to your favorite text editor.</span></span>

   ![Copia de la clave de la aplicación](media/authentication-and-authorization/active-directory-copy-application-key.png)

6. <span data-ttu-id="40e84-135">Para el entorno de Time Series Insights, seleccione **Directivas de acceso a datos** y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="40e84-135">For the Time Series Insights environment, select **Data Access Policies** and click **Add**.</span></span>

   ![Adición de nueva directiva de acceso a datos al entorno de Time Series Insights](media/authentication-and-authorization/time-series-insights-data-access-policies-add.png)

7. <span data-ttu-id="40e84-137">En el cuadro de diálogo **Seleccionar usuario**, pegue el nombre de la aplicación (del paso 2) o el identificador (del paso 3).</span><span class="sxs-lookup"><span data-stu-id="40e84-137">In the **Select User** dialog box, paste the application name (from step 2) or application ID (from step 3).</span></span>

   ![Búsqueda de una aplicación en el cuadro de diálogo Seleccionar usuario](media/authentication-and-authorization/time-series-insights-data-access-policies-select-user.png)

8. <span data-ttu-id="40e84-139">Seleccione el rol (**Lector** para consultar datos, **Colaborador** para consultar datos y cambiar datos de referencia) y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="40e84-139">Select the role (**Reader** for querying data, **Contributor** for querying data and changing reference data) and click **Ok**.</span></span>

   ![Selección de Lector o Colaborador en el cuadro de diálogo Seleccionar rol](media/authentication-and-authorization/time-series-insights-data-access-policies-select-role.png)

9. <span data-ttu-id="40e84-141">Haga clic en **Aceptar** para guardar la directiva.</span><span class="sxs-lookup"><span data-stu-id="40e84-141">Save the policy by clicking **Ok**.</span></span>

10. <span data-ttu-id="40e84-142">Use el identificador de la aplicación (del paso 3) y la clave (del paso 5) para conseguir el token en nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="40e84-142">Use the application ID (from step 3) and application key (from step 5) to acquire the token on behalf of the application.</span></span> <span data-ttu-id="40e84-143">Luego el token se puede pasar en el encabezado `Authorization` cuando la aplicación llame a la API de Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="40e84-143">The token can then be passed in the `Authorization` header when the application calls the Time Series Insights API.</span></span>

    <span data-ttu-id="40e84-144">Si está usando C#, puede emplear el siguiente código para conseguir el token en nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="40e84-144">If you're using C#, you can use the following code to acquire the token on behalf of the application.</span></span> <span data-ttu-id="40e84-145">Para obtener un ejemplo completo, vea [Consulta de datos mediante C#](time-series-insights-query-data-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="40e84-145">For a complete sample, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

    ```csharp
    var authenticationContext = new AuthenticationContext(
        "https://login.microsoftonline.com/common",
        TokenCache.DefaultShared);

    AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
        // Set the resource URI to the Azure Time Series Insights API
        resource: "https://api.timeseries.azure.com/", 
        clientCredential: new ClientCredential(
            // Application ID of application registered in Azure Active Directory
            clientId: "1bc3af48-7e2f-4845-880a-c7649a6470b8", 
            // Application key of the application that's registered in Azure Active Directory
            clientSecret: "aBcdEffs4XYxoAXzLB1n3R2meNCYdGpIGBc2YC5D6L2="));

    string accessToken = token.AccessToken;
    ```

## <a name="next-steps"></a><span data-ttu-id="40e84-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="40e84-146">Next steps</span></span>

<span data-ttu-id="40e84-147">Use el identificador y la clave de la aplicación en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="40e84-147">Use the application ID and key in your application.</span></span> <span data-ttu-id="40e84-148">Para consultar código de ejemplo que llama a la API de Time Series Insights, vea [Consulta de datos mediante C#](time-series-insights-query-data-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="40e84-148">For sample code that calls the Time Series Insights API, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="40e84-149">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="40e84-149">See also</span></span>

* <span data-ttu-id="40e84-150">Para obtener toda la referencia de la API de consulta, vea [API de consulta](/rest/api/time-series-insights/time-series-insights-reference-queryapi)</span><span class="sxs-lookup"><span data-stu-id="40e84-150">[Query API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) for the full Query API reference</span></span>
* <span data-ttu-id="40e84-151">[Create a service principal in the Azure portal](../azure-resource-manager/resource-group-create-service-principal-portal.md) (Creación de una entidad de servicio en Azure Portal)</span><span class="sxs-lookup"><span data-stu-id="40e84-151">[Create a service principal in the Azure portal](../azure-resource-manager/resource-group-create-service-principal-portal.md)</span></span>
