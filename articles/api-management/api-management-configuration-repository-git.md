---
title: "Configuración del servicio API Management con Git - Azure | Microsoft Docs"
description: "Obtenga información sobre cómo guardar y configurar la configuración del servicio de administración de API mediante Git."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: mattfarm
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: f5d6bb7ccbf15424e9940ccda2fac668a2af5a57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-save-and-configure-your-api-management-service-configuration-using-git"></a><span data-ttu-id="d86b3-103">Guardado y configuración del servicio Administración de API mediante Git</span><span class="sxs-lookup"><span data-stu-id="d86b3-103">How to save and configure your API Management service configuration using Git</span></span>
> 
> 

<span data-ttu-id="d86b3-104">Cada instancia del servicio Administración de API mantiene una base de datos de configuración que contiene información sobre la configuración y los metadatos de la instancia del servicio.</span><span class="sxs-lookup"><span data-stu-id="d86b3-104">Each API Management service instance maintains a configuration database that contains information about the configuration and metadata for the service instance.</span></span> <span data-ttu-id="d86b3-105">Es posible hacer cambios en la instancia del servicio; para ello, modifique un valor del portal para editores con un cmdlet de PowerShell o realice una llamada de API de REST.</span><span class="sxs-lookup"><span data-stu-id="d86b3-105">Changes can be made to the service instance by changing a setting in the publisher portal, using a PowerShell cmdlet, or making a REST API call.</span></span> <span data-ttu-id="d86b3-106">Pero esto no es todo, también puede administrar la configuración de la instancia del servicio con Git, con lo que se posibilitan escenarios de administración de servicio como los siguientes:</span><span class="sxs-lookup"><span data-stu-id="d86b3-106">In addition to these methods, you can also manage your service instance configuration using Git, enabling service management scenarios such as:</span></span>

* <span data-ttu-id="d86b3-107">Control de versiones de configuración: descargue y almacene versiones diferentes de la configuración del servicio</span><span class="sxs-lookup"><span data-stu-id="d86b3-107">Configuration versioning - download and store different versions of your service configuration</span></span>
* <span data-ttu-id="d86b3-108">Cambios masivos en la configuración: realice cambios en varios ajustes de la configuración del servicio en el repositorio local e integre los cambios de nuevo en el servidor con una sola operación</span><span class="sxs-lookup"><span data-stu-id="d86b3-108">Bulk configuration changes - make changes to multiple parts of your service configuration in your local repository and integrate the changes back to the server with a single operation</span></span>
* <span data-ttu-id="d86b3-109">Cadena de herramientas y flujo de trabajo familiares de Git: use las herramientas y los flujos de trabajo de Git con los que ya está familiarizado</span><span class="sxs-lookup"><span data-stu-id="d86b3-109">Familiar Git toolchain and workflow - use the Git tooling and workflows that you are already familiar with</span></span>

<span data-ttu-id="d86b3-110">El diagrama siguiente muestra de forma global los distintos modos de configurar la instancia del servicio de Administración de API.</span><span class="sxs-lookup"><span data-stu-id="d86b3-110">The following diagram shows an overview of the different ways to configure your API Management service instance.</span></span>

![Configuración de GIT][api-management-git-configure]

<span data-ttu-id="d86b3-112">Cuando hace cambios en el servicio mediante el portal para editores, los cmdlets de PowerShell o la API de REST, está administrando la base de datos de configuración del servicio mediante el punto de conexión `https://{name}.management.azure-api.net` , tal como se muestra en el lado derecho del diagrama.</span><span class="sxs-lookup"><span data-stu-id="d86b3-112">When you make changes to your service using the publisher portal, PowerShell cmdlets, or the REST API, you are managing your service configuration database using the `https://{name}.management.azure-api.net` endpoint, as shown on the right side of the diagram.</span></span> <span data-ttu-id="d86b3-113">En el lado izquierdo del diagrama se muestra cómo administrar la configuración del servicio mediante Git y el repositorio de Git para el servicio ubicado en `https://{name}.scm.azure-api.net`.</span><span class="sxs-lookup"><span data-stu-id="d86b3-113">The left side of the diagram illustrates how you can manage your service configuration using Git and Git repository for your service located at `https://{name}.scm.azure-api.net`.</span></span>

<span data-ttu-id="d86b3-114">Los pasos siguientes proporcionan una visión general sobre el proceso de administración de la instancia del servicio de Administración de API mediante Git.</span><span class="sxs-lookup"><span data-stu-id="d86b3-114">The following steps provide an overview of managing your API Management service instance using Git.</span></span>

1. <span data-ttu-id="d86b3-115">Acceso a la configuración de Git en el servicio</span><span class="sxs-lookup"><span data-stu-id="d86b3-115">Access Git configuration in your service</span></span>
2. <span data-ttu-id="d86b3-116">Guardar la base de datos de configuración del servicio en el repositorio de Git</span><span class="sxs-lookup"><span data-stu-id="d86b3-116">Save your service configuration database to your Git repository</span></span>
3. <span data-ttu-id="d86b3-117">Clonar el repositorio de Git en el equipo local</span><span class="sxs-lookup"><span data-stu-id="d86b3-117">Clone the Git repo to your local machine</span></span>
4. <span data-ttu-id="d86b3-118">Desplegar el repositorio más reciente en el equipo local, y confirmar e insertar los cambios de nuevo en el repositorio</span><span class="sxs-lookup"><span data-stu-id="d86b3-118">Pull the latest repo down to your local machine, and commit and push changes back to your repo</span></span>
5. <span data-ttu-id="d86b3-119">Implementar los cambios desde el repositorio en la base de datos de configuración del servicio</span><span class="sxs-lookup"><span data-stu-id="d86b3-119">Deploy the changes from your repo into your service configuration database</span></span>

<span data-ttu-id="d86b3-120">Este artículo describe cómo habilitar y usar Git para administrar la configuración del servicio y sirve como referencia para los archivos y las carpetas del repositorio Git.</span><span class="sxs-lookup"><span data-stu-id="d86b3-120">This article describes how to enable and use Git to manage your service configuration and provides a reference for the files and folders in the Git repository.</span></span>

## <a name="access-git-configuration-in-your-service"></a><span data-ttu-id="d86b3-121">Acceso a la configuración de Git en el servicio</span><span class="sxs-lookup"><span data-stu-id="d86b3-121">Access Git configuration in your service</span></span>
<span data-ttu-id="d86b3-122">Puede ver rápidamente el estado de la configuración Git en el icono de Git, en la esquina superior derecha del portal del editor.</span><span class="sxs-lookup"><span data-stu-id="d86b3-122">You can quickly view the status of your Git configuration by viewing the Git icon in the upper-right corner of the publisher portal.</span></span> <span data-ttu-id="d86b3-123">En este ejemplo, el mensaje de estado indica que hay cambios no guardados en el repositorio.</span><span class="sxs-lookup"><span data-stu-id="d86b3-123">In this example, the status message indicates that there are unsaved changes to the repository.</span></span> <span data-ttu-id="d86b3-124">Esto es porque la base de datos de configuración del servicio de Administración de API aún no se ha guardado en el repositorio.</span><span class="sxs-lookup"><span data-stu-id="d86b3-124">This is because the API Management service configuration database has not yet been saved to the repository.</span></span>

![Estado de Git][api-management-git-icon-enable]

<span data-ttu-id="d86b3-126">Para ver y configurar las opciones de configuración Git, puede hacer clic en el icono de Git o en el menú **Seguridad** e ir a la pestaña **Repositorio de configuraciones**.</span><span class="sxs-lookup"><span data-stu-id="d86b3-126">To view and configure your Git configuration settings, you can either click the Git icon, or click the **Security** menu and navigate to the **Configuration repository** tab.</span></span>

![Habilitar GIT][api-management-enable-git]

> [!IMPORTANT]
> <span data-ttu-id="d86b3-128">Los secretos que no se definan como propiedades se almacenarán en el repositorio y permanecerán en su historial hasta que deshabilite y vuelva a habilitar el acceso de Git.</span><span class="sxs-lookup"><span data-stu-id="d86b3-128">Any secrets that are not defined as properties will be stored in the repository and will remain in its history until you disable and re-enable Git access.</span></span> <span data-ttu-id="d86b3-129">Las propiedades proporcionan un lugar seguro para administrar los valores de cadena constante, como los secretos, a través de toda la configuración y las directivas de API, por lo que no tiene que almacenarlos directamente en las instrucciones de directiva.</span><span class="sxs-lookup"><span data-stu-id="d86b3-129">Properties provide a secure place to manage constant string values, including secrets, across all API configuration and policies, so you don't have to store them directly in your policy statements.</span></span> <span data-ttu-id="d86b3-130">Para obtener más información, consulte [How to use properties in Azure API Management policies](api-management-howto-properties.md)(Uso de propiedades en directivas de Administración de API de Azure).</span><span class="sxs-lookup"><span data-stu-id="d86b3-130">For more information, see [How to use properties in Azure API Management policies](api-management-howto-properties.md).</span></span>
> 
> 

<span data-ttu-id="d86b3-131">Para obtener información sobre la habilitación o la deshabilitación del acceso de Git mediante la API de REST, consulte [Enable or disable Git access using the REST API](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit)(Habilitación o deshabilitación del acceso de Git mediante la API de REST).</span><span class="sxs-lookup"><span data-stu-id="d86b3-131">For information on enabling or disabling Git access using the REST API, see [Enable or disable Git access using the REST API](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span></span>

## <a name="to-save-the-service-configuration-to-the-git-repository"></a><span data-ttu-id="d86b3-132">Guardado de la configuración del servicio en el repositorio de Git</span><span class="sxs-lookup"><span data-stu-id="d86b3-132">To save the service configuration to the Git repository</span></span>
<span data-ttu-id="d86b3-133">El primer paso antes de la clonación del repositorio es guardar el estado actual de la configuración del servicio en el repositorio.</span><span class="sxs-lookup"><span data-stu-id="d86b3-133">The first step before cloning the repository is to save the current state of the service configuration to the repository.</span></span> <span data-ttu-id="d86b3-134">Haga clic en **Guardar configuración en repositorio**.</span><span class="sxs-lookup"><span data-stu-id="d86b3-134">Click **Save configuration to repository**.</span></span>

![Guardar configuración][api-management-save-configuration]

<span data-ttu-id="d86b3-136">Realice los cambios necesarios en la pantalla de confirmación y haga clic en **Aceptar** para guardar.</span><span class="sxs-lookup"><span data-stu-id="d86b3-136">Make any desired changes on the confirmation screen and click **Ok** to save.</span></span>

![Guardar configuración][api-management-save-configuration-confirm]

<span data-ttu-id="d86b3-138">Transcurridos unos segundos, la configuración se guarda y se muestra el estado de configuración del repositorio, incluidas la fecha y la hora del último cambio de configuración y la última sincronización entre la configuración del servicio y el repositorio.</span><span class="sxs-lookup"><span data-stu-id="d86b3-138">After a few moments the configuration is saved, and the configuration status of the repository is displayed, including the date and time of the last configuration change and the last synchronization between the service configuration and the repository.</span></span>

![Estado de configuración][api-management-configuration-status]

<span data-ttu-id="d86b3-140">Una vez que la configuración se guarda en el repositorio, se puede clonar.</span><span class="sxs-lookup"><span data-stu-id="d86b3-140">Once the configuration is saved to the repository, it can be cloned.</span></span>

<span data-ttu-id="d86b3-141">Para obtener información acerca de cómo realizar esta operación mediante la API de REST, consulte [Commit configuration snapshot using the REST API](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot)(Confirmación de la instantánea de configuración mediante la API de REST).</span><span class="sxs-lookup"><span data-stu-id="d86b3-141">For information on performing this operation using the REST API, see [Commit configuration snapshot using the REST API](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span></span>

## <a name="to-clone-the-repository-to-your-local-machine"></a><span data-ttu-id="d86b3-142">Para clonar el repositorio en el equipo local</span><span class="sxs-lookup"><span data-stu-id="d86b3-142">To clone the repository to your local machine</span></span>
<span data-ttu-id="d86b3-143">Para clonar un repositorio, necesitará la dirección URL del repositorio, un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="d86b3-143">To clone a repository, you need the URL to your repository, a user name, and a password.</span></span> <span data-ttu-id="d86b3-144">El nombre de usuario y la dirección URL se muestran cerca de la parte superior de la pestaña **Repositorio de configuración** .</span><span class="sxs-lookup"><span data-stu-id="d86b3-144">The user name and URL are displayed near the top of the **Configuration repository** tab.</span></span>

![Clonación de git][api-management-configuration-git-clone]

<span data-ttu-id="d86b3-146">La contraseña se genera en la parte inferior de la pestaña **Repositorio de configuración** .</span><span class="sxs-lookup"><span data-stu-id="d86b3-146">The password is generated at the bottom of the **Configuration repository** tab.</span></span>

![Generar contraseña][api-management-generate-password]

<span data-ttu-id="d86b3-148">Para generar una contraseña, primero asegúrese de que el campo **Expiración** refleja la fecha y la hora de caducidad deseada y luego haga clic en **Generar token**.</span><span class="sxs-lookup"><span data-stu-id="d86b3-148">To generate a password, first ensure that the **Expiry** is set to the desired expiration date and time, and then click **Generate Token**.</span></span>

![Password][api-management-password]

> [!IMPORTANT]
> <span data-ttu-id="d86b3-150">Anote esta contraseña.</span><span class="sxs-lookup"><span data-stu-id="d86b3-150">Make a note of this password.</span></span> <span data-ttu-id="d86b3-151">Una vez que salga de esta página, la contraseña no se volverá a mostrar.</span><span class="sxs-lookup"><span data-stu-id="d86b3-151">Once you leave this page the password will not be displayed again.</span></span>
> 
> 

<span data-ttu-id="d86b3-152">En los ejemplos siguientes se usa la herramienta Git Bash desde [Git para Windows](http://www.git-scm.com/downloads) , pero puede usar cualquier herramienta de Git con la que esté familiarizado.</span><span class="sxs-lookup"><span data-stu-id="d86b3-152">The following examples use the Git Bash tool from [Git for Windows](http://www.git-scm.com/downloads) but you can use any Git tool that you are familiar with.</span></span>

<span data-ttu-id="d86b3-153">Abra su herramienta Git en la carpeta deseada y ejecute el siguiente comando para clonar el repositorio de git en el equipo local, usando para ello el comando incluido en el portal para editores.</span><span class="sxs-lookup"><span data-stu-id="d86b3-153">Open your Git tool in the desired folder and run the following command to clone the git repository to your local machine, using the command provided by the publisher portal.</span></span>

```
git clone https://bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="d86b3-154">Proporcione el nombre de usuario y la contraseña cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="d86b3-154">Provide the user name and password when prompted.</span></span>

<span data-ttu-id="d86b3-155">Si recibe algún error, pruebe a modificar su comando `git clone` para incluir el nombre de usuario y la contraseña, como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="d86b3-155">If you receive any errors, try modifying your `git clone` command to include the user name and password, as shown in the following example.</span></span>

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="d86b3-156">Si de este modo aparece un error, pruebe a codificar como dirección URL la parte de la contraseña del comando.</span><span class="sxs-lookup"><span data-stu-id="d86b3-156">If this provides an error, try URL encoding the password portion of the command.</span></span> <span data-ttu-id="d86b3-157">Una manera rápida de hacer esto es abrir Visual Studio y emitir el siguiente comando en la **Ventana Inmediato**.</span><span class="sxs-lookup"><span data-stu-id="d86b3-157">One quick way to do this is to open Visual Studio, and issue the following command in the **Immediate Window**.</span></span> <span data-ttu-id="d86b3-158">Para abrir la **Ventana Inmediato**, abra cualquier solución o proyecto en Visual Studio (o cree una aplicación de consola vacía) y elija **Ventanas**, **Inmediato** en el menú **Depurar**.</span><span class="sxs-lookup"><span data-stu-id="d86b3-158">To open the **Immediate Window**, open any solution or project in Visual Studio (or create a new empty console application), and choose **Windows**, **Immediate** from the **Debug** menu.</span></span>

```
?System.NetWebUtility.UrlEncode("password from publisher portal")
```

<span data-ttu-id="d86b3-159">Utilice la contraseña codificada junto con su nombre de usuario y ubicación de repositorio para construir el comando git.</span><span class="sxs-lookup"><span data-stu-id="d86b3-159">Use the encoded password along with your user name and repository location to construct the git command.</span></span>

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="d86b3-160">Una vez que se clone el repositorio, podrá ver y trabajar con él en el sistema de archivos local.</span><span class="sxs-lookup"><span data-stu-id="d86b3-160">Once the repository is cloned you can view and work with it in your local file system.</span></span> <span data-ttu-id="d86b3-161">Para más información, consulte [Referencia de estructura de archivo y carpeta del repositorio local de Git](#file-and-folder-structure-reference-of-local-git-repository).</span><span class="sxs-lookup"><span data-stu-id="d86b3-161">For more information, see [File and folder structure reference of local Git repository](#file-and-folder-structure-reference-of-local-git-repository).</span></span>

## <a name="to-update-your-local-repository-with-the-most-current-service-instance-configuration"></a><span data-ttu-id="d86b3-162">Para actualizar su repositorio local con la configuración de instancia de servicio más reciente</span><span class="sxs-lookup"><span data-stu-id="d86b3-162">To update your local repository with the most current service instance configuration</span></span>
<span data-ttu-id="d86b3-163">Si realiza cambios en la instancia del servicio de Administración de API en el portal para editores o mediante la API de REST, debe guardar estos cambios en el repositorio para poder actualizar el repositorio local con los cambios más recientes.</span><span class="sxs-lookup"><span data-stu-id="d86b3-163">If you make changes to your API Management service instance in the publisher portal or using the REST API, you must save these changes to the repository before you can update your local repository with the latest changes.</span></span> <span data-ttu-id="d86b3-164">Para ello, haga clic en **Guardar configuración en repositorio** en la pestaña **Repositorio de configuración** del portal para editores y emita el siguiente comando en el repositorio local.</span><span class="sxs-lookup"><span data-stu-id="d86b3-164">To do this, click **Save configuration to repository** on the **Configuration repository** tab in the publisher portal, and then issue the following command in your local repository.</span></span>

```
git pull
```

<span data-ttu-id="d86b3-165">Antes de ejecutar `git pull` , asegúrese de que se encuentra en la carpeta del repositorio local.</span><span class="sxs-lookup"><span data-stu-id="d86b3-165">Before running `git pull` ensure that you are in the folder for your local repository.</span></span> <span data-ttu-id="d86b3-166">Si acaba de completar el comando `git clone` , debe cambiar el directorio a su repositorio ejecutando un comando similar al siguiente.</span><span class="sxs-lookup"><span data-stu-id="d86b3-166">If you have just completed the `git clone` command, then you must change the directory to your repo by running a command like the following.</span></span>

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="to-push-changes-from-your-local-repo-to-the-server-repo"></a><span data-ttu-id="d86b3-167">Para insertar los cambios desde su repositorio local al repositorio del servidor</span><span class="sxs-lookup"><span data-stu-id="d86b3-167">To push changes from your local repo to the server repo</span></span>
<span data-ttu-id="d86b3-168">Para insertar los cambios desde el repositorio local al repositorio del servidor, debe confirmar los cambios y, a continuación, insertarlos en el repositorio del servidor.</span><span class="sxs-lookup"><span data-stu-id="d86b3-168">To push changes from your local repository to the server repository, you must commit your changes and then push them to the server repository.</span></span> <span data-ttu-id="d86b3-169">Para confirmar los cambios, abra la herramienta de comandos de Git, cambie al directorio del repositorio local y emita los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="d86b3-169">To commit your changes, open your Git command tool, switch to the directory of your local repository, and issue the following commands.</span></span>

```
git add --all
git commit -m "Description of your changes"
```

<span data-ttu-id="d86b3-170">Para insertar todas las confirmaciones en el servidor, ejecute el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="d86b3-170">To push all of the commits to the server, run the following command.</span></span>

```
git push
```

## <a name="to-deploy-any-service-configuration-changes-to-the-api-management-service-instance"></a><span data-ttu-id="d86b3-171">Para implementar los cambios de la configuración del servicio en la instancia del servicio de Administración de API</span><span class="sxs-lookup"><span data-stu-id="d86b3-171">To deploy any service configuration changes to the API Management service instance</span></span>
<span data-ttu-id="d86b3-172">Una vez confirmados los cambios locales e insertados en el repositorio del servidor, puede implementarlos en la instancia del servicio Administración de API.</span><span class="sxs-lookup"><span data-stu-id="d86b3-172">Once your local changes are committed and pushed to the server repository, you can deploy them to your API Management service instance.</span></span>

![Implementación][api-management-configuration-deploy]

<span data-ttu-id="d86b3-174">Para obtener información acerca de cómo realizar esta operación mediante la API de REST, consulte [Deploy Git changes to configuration database using the REST API](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration)(Implementación de cambios de Git en la base de datos de configuración mediante la API de REST).</span><span class="sxs-lookup"><span data-stu-id="d86b3-174">For information on performing this operation using the REST API, see [Deploy Git changes to configuration database using the REST API](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span></span>

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a><span data-ttu-id="d86b3-175">Referencia de estructura de archivo y carpeta del repositorio local de Git</span><span class="sxs-lookup"><span data-stu-id="d86b3-175">File and folder structure reference of local Git repository</span></span>
<span data-ttu-id="d86b3-176">Los archivos y carpetas del repositorio local de Git contienen la información de configuración acerca de la instancia de servicio.</span><span class="sxs-lookup"><span data-stu-id="d86b3-176">The files and folders in the local git repository contain the configuration information about the service instance.</span></span>

| <span data-ttu-id="d86b3-177">Elemento</span><span class="sxs-lookup"><span data-stu-id="d86b3-177">Item</span></span> | <span data-ttu-id="d86b3-178">Description</span><span class="sxs-lookup"><span data-stu-id="d86b3-178">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d86b3-179">carpeta raíz de la administración de API</span><span class="sxs-lookup"><span data-stu-id="d86b3-179">root api-management folder</span></span> |<span data-ttu-id="d86b3-180">Contiene la configuración de nivel superior para la instancia de servicio</span><span class="sxs-lookup"><span data-stu-id="d86b3-180">Contains top-level configuration for the service instance</span></span> |
| <span data-ttu-id="d86b3-181">carpeta de API</span><span class="sxs-lookup"><span data-stu-id="d86b3-181">apis folder</span></span> |<span data-ttu-id="d86b3-182">Contiene la configuración para las API de la instancia de servicio</span><span class="sxs-lookup"><span data-stu-id="d86b3-182">Contains the configuration for the apis in the service instance</span></span> |
| <span data-ttu-id="d86b3-183">carpeta de grupos</span><span class="sxs-lookup"><span data-stu-id="d86b3-183">groups folder</span></span> |<span data-ttu-id="d86b3-184">Contiene la configuración para los grupos de la instancia de servicio</span><span class="sxs-lookup"><span data-stu-id="d86b3-184">Contains the configuration for the groups in the service instance</span></span> |
| <span data-ttu-id="d86b3-185">carpeta de directivas</span><span class="sxs-lookup"><span data-stu-id="d86b3-185">policies folder</span></span> |<span data-ttu-id="d86b3-186">Contiene las directivas de la instancia de servicio</span><span class="sxs-lookup"><span data-stu-id="d86b3-186">Contains the policies in the service instance</span></span> |
| <span data-ttu-id="d86b3-187">carpeta portalStyles</span><span class="sxs-lookup"><span data-stu-id="d86b3-187">portalStyles folder</span></span> |<span data-ttu-id="d86b3-188">Contiene la configuración para las personalizaciones del portal para desarrolladores de la instancia de servicio</span><span class="sxs-lookup"><span data-stu-id="d86b3-188">Contains the configuration for the developer portal customizations in the service instance</span></span> |
| <span data-ttu-id="d86b3-189">carpeta de productos</span><span class="sxs-lookup"><span data-stu-id="d86b3-189">products folder</span></span> |<span data-ttu-id="d86b3-190">Contiene la configuración para los productos de la instancia de servicio</span><span class="sxs-lookup"><span data-stu-id="d86b3-190">Contains the configuration for the products in the service instance</span></span> |
| <span data-ttu-id="d86b3-191">carpeta de plantillas</span><span class="sxs-lookup"><span data-stu-id="d86b3-191">templates folder</span></span> |<span data-ttu-id="d86b3-192">Contiene la configuración para las plantillas de correo electrónico de la instancia de servicio</span><span class="sxs-lookup"><span data-stu-id="d86b3-192">Contains the configuration for the email templates in the service instance</span></span> |

<span data-ttu-id="d86b3-193">Cada carpeta puede contener uno o varios archivos y, en algunos casos, una o varias carpetas; por ejemplo, una carpeta para cada API, producto o grupo.</span><span class="sxs-lookup"><span data-stu-id="d86b3-193">Each folder can contain one or more files, and in some cases one or more folders, for example a folder for each API, product, or group.</span></span> <span data-ttu-id="d86b3-194">Los archivos dentro de cada carpeta son específicos del tipo de entidad descrito por el nombre de la carpeta.</span><span class="sxs-lookup"><span data-stu-id="d86b3-194">The files within each folder are specific for the entity type described by the folder name.</span></span>

| <span data-ttu-id="d86b3-195">Tipo de archivo</span><span class="sxs-lookup"><span data-stu-id="d86b3-195">File type</span></span> | <span data-ttu-id="d86b3-196">Propósito</span><span class="sxs-lookup"><span data-stu-id="d86b3-196">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="d86b3-197">json</span><span class="sxs-lookup"><span data-stu-id="d86b3-197">json</span></span> |<span data-ttu-id="d86b3-198">Información de configuración acerca de la entidad correspondiente</span><span class="sxs-lookup"><span data-stu-id="d86b3-198">Configuration information about the respective entity</span></span> |
| <span data-ttu-id="d86b3-199">html</span><span class="sxs-lookup"><span data-stu-id="d86b3-199">html</span></span> |<span data-ttu-id="d86b3-200">Descripción de la entidad, a menudo mostrada en el portal para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="d86b3-200">Descriptions about the entity, often displayed in the developer portal</span></span> |
| <span data-ttu-id="d86b3-201">xml</span><span class="sxs-lookup"><span data-stu-id="d86b3-201">xml</span></span> |<span data-ttu-id="d86b3-202">Policy statements</span><span class="sxs-lookup"><span data-stu-id="d86b3-202">Policy statements</span></span> |
| <span data-ttu-id="d86b3-203">css</span><span class="sxs-lookup"><span data-stu-id="d86b3-203">css</span></span> |<span data-ttu-id="d86b3-204">Hojas de estilo para la personalización del portal para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="d86b3-204">Style sheets for developer portal customization</span></span> |

<span data-ttu-id="d86b3-205">Estos archivos pueden crear, eliminar, editar y administrar en el sistema de archivos local, y los cambios se pueden implementar de nuevo en la instancia de servicio de Administración de API.</span><span class="sxs-lookup"><span data-stu-id="d86b3-205">These files can be created, deleted, edited, and managed on your local file system, and the changes deployed back to the your API Management service instance.</span></span>

> [!NOTE]
> <span data-ttu-id="d86b3-206">Las siguientes entidades no están en el repositorio de Git y no se pueden configurar mediante Git.</span><span class="sxs-lookup"><span data-stu-id="d86b3-206">The following entities are not contained in the Git repository and cannot be configured using Git.</span></span>
> 
> * <span data-ttu-id="d86b3-207">Usuarios</span><span class="sxs-lookup"><span data-stu-id="d86b3-207">Users</span></span>
> * <span data-ttu-id="d86b3-208">Suscripciones</span><span class="sxs-lookup"><span data-stu-id="d86b3-208">Subscriptions</span></span>
> * <span data-ttu-id="d86b3-209">Propiedades</span><span class="sxs-lookup"><span data-stu-id="d86b3-209">Properties</span></span>
> * <span data-ttu-id="d86b3-210">Entidades del portal de desarrolladores distintas de los estilos</span><span class="sxs-lookup"><span data-stu-id="d86b3-210">Developer portal entities other than styles</span></span>
> 
> 

### <a name="root-api-management-folder"></a><span data-ttu-id="d86b3-211">Carpeta raíz de la administración de API</span><span class="sxs-lookup"><span data-stu-id="d86b3-211">Root api-management folder</span></span>
<span data-ttu-id="d86b3-212">La carpeta raíz `api-management` contiene un archivo `configuration.json` con información de nivel superior sobre la instancia de servicio en el formato siguiente.</span><span class="sxs-lookup"><span data-stu-id="d86b3-212">The root `api-management` folder contains a `configuration.json` file that contains top-level information about the service instance in the following format.</span></span>

```json
{
  "settings": {
    "RegistrationEnabled": "True",
    "UserRegistrationTerms": null,
    "UserRegistrationTermsEnabled": "False",
    "UserRegistrationTermsConsentRequired": "False",
    "DelegationEnabled": "False",
    "DelegationUrl": "",
    "DelegatedSubscriptionEnabled": "False",
    "DelegationValidationKey": ""
  },
  "$ref-policy": "api-management/policies/global.xml"
}
```

<span data-ttu-id="d86b3-213">Los primeros cuatro valores (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled` y `UserRegistrationTermsConsentRequired`) se asignan a la siguiente configuración en la pestaña **Identidades** de la sección **Seguridad**.</span><span class="sxs-lookup"><span data-stu-id="d86b3-213">The first four settings (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, and `UserRegistrationTermsConsentRequired`) map to the following settings on the **Identities** tab in the **Security** section.</span></span>

| <span data-ttu-id="d86b3-214">Configuración de identidad</span><span class="sxs-lookup"><span data-stu-id="d86b3-214">Identity setting</span></span> | <span data-ttu-id="d86b3-215">Se asigna a</span><span class="sxs-lookup"><span data-stu-id="d86b3-215">Maps to</span></span> |
| --- | --- |
| <span data-ttu-id="d86b3-216">RegistrationEnabled</span><span class="sxs-lookup"><span data-stu-id="d86b3-216">RegistrationEnabled</span></span> |<span data-ttu-id="d86b3-217">**Redirigir a los usuarios anónimos a la página de inicio de sesión** </span><span class="sxs-lookup"><span data-stu-id="d86b3-217">**Redirect anonymous users to sign-in page** checkbox</span></span> |
| <span data-ttu-id="d86b3-218">UserRegistrationTerms</span><span class="sxs-lookup"><span data-stu-id="d86b3-218">UserRegistrationTerms</span></span> |<span data-ttu-id="d86b3-219">**Condiciones de uso del registro de usuario** </span><span class="sxs-lookup"><span data-stu-id="d86b3-219">**Terms of use on user signup** textbox</span></span> |
| <span data-ttu-id="d86b3-220">UserRegistrationTermsEnabled</span><span class="sxs-lookup"><span data-stu-id="d86b3-220">UserRegistrationTermsEnabled</span></span> |<span data-ttu-id="d86b3-221">**Mostrar condiciones de uso en la página de registro** </span><span class="sxs-lookup"><span data-stu-id="d86b3-221">**Show terms of use on signup page** checkbox</span></span> |
| <span data-ttu-id="d86b3-222">UserRegistrationTermsConsentRequired</span><span class="sxs-lookup"><span data-stu-id="d86b3-222">UserRegistrationTermsConsentRequired</span></span> |<span data-ttu-id="d86b3-223">**Requerir consentimiento** </span><span class="sxs-lookup"><span data-stu-id="d86b3-223">**Require consent** checkbox</span></span> |

![Configuración de identidad][api-management-identity-settings]

<span data-ttu-id="d86b3-225">La cuatro valores siguientes (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled` y `DelegationValidationKey`) se asignan a la siguiente configuración en la pestaña **Delegación** de la sección **Seguridad**.</span><span class="sxs-lookup"><span data-stu-id="d86b3-225">The next four settings (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, and `DelegationValidationKey`) map to the following settings on the **Delegation** tab in the **Security** section.</span></span>

| <span data-ttu-id="d86b3-226">Configuración de delegación</span><span class="sxs-lookup"><span data-stu-id="d86b3-226">Delegation setting</span></span> | <span data-ttu-id="d86b3-227">Se asigna a</span><span class="sxs-lookup"><span data-stu-id="d86b3-227">Maps to</span></span> |
| --- | --- |
| <span data-ttu-id="d86b3-228">DelegationEnabled</span><span class="sxs-lookup"><span data-stu-id="d86b3-228">DelegationEnabled</span></span> |<span data-ttu-id="d86b3-229">Casilla **Delegar inicio de sesión y registro**</span><span class="sxs-lookup"><span data-stu-id="d86b3-229">**Delegate sign-in & sign-up** checkbox</span></span> |
| <span data-ttu-id="d86b3-230">DelegationUrl</span><span class="sxs-lookup"><span data-stu-id="d86b3-230">DelegationUrl</span></span> |<span data-ttu-id="d86b3-231">**Dirección URL del punto de conexión de delegación** </span><span class="sxs-lookup"><span data-stu-id="d86b3-231">**Delegation endpoint URL** textbox</span></span> |
| <span data-ttu-id="d86b3-232">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="d86b3-232">DelegatedSubscriptionEnabled</span></span> |<span data-ttu-id="d86b3-233">**Delegar suscripción de producto** </span><span class="sxs-lookup"><span data-stu-id="d86b3-233">**Delegate product subscription** checkbox</span></span> |
| <span data-ttu-id="d86b3-234">DelegationValidationKey</span><span class="sxs-lookup"><span data-stu-id="d86b3-234">DelegationValidationKey</span></span> |<span data-ttu-id="d86b3-235">**Delegar clave de validación** </span><span class="sxs-lookup"><span data-stu-id="d86b3-235">**Delegate Validation Key** textbox</span></span> |

![Configuración de delegación][api-management-delegation-settings]

<span data-ttu-id="d86b3-237">El valor final, `$ref-policy`, se asigna al archivo de instrucciones de directiva global para la instancia de servicio.</span><span class="sxs-lookup"><span data-stu-id="d86b3-237">The final setting, `$ref-policy`, maps to the global policy statements file for the service instance.</span></span>

### <a name="apis-folder"></a><span data-ttu-id="d86b3-238">carpeta de API</span><span class="sxs-lookup"><span data-stu-id="d86b3-238">apis folder</span></span>
<span data-ttu-id="d86b3-239">La carpeta `apis` contiene una carpeta para cada API de la instancia de servicio que contiene los elementos siguientes.</span><span class="sxs-lookup"><span data-stu-id="d86b3-239">The `apis` folder contains a folder for each API in the service instance which contains the following items.</span></span>

* <span data-ttu-id="d86b3-240">`apis\<api name>\configuration.json`: es la configuración de la API y contiene información acerca de la dirección URL del servicio back-end y las operaciones.</span><span class="sxs-lookup"><span data-stu-id="d86b3-240">`apis\<api name>\configuration.json` - this is the configuration for the API and contains information about the backend service URL and the operations.</span></span> <span data-ttu-id="d86b3-241">Se trata de la misma información que se devolvería si se llamase a [Obtener una API específica](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) con `export=true` en formato `application/json`.</span><span class="sxs-lookup"><span data-stu-id="d86b3-241">This is the same information that would be returned if you were to call [Get a specific API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) with `export=true` in `application/json` format.</span></span>
* <span data-ttu-id="d86b3-242">`apis\<api name>\api.description.html`: es la descripción de la API y corresponde a la propiedad `description` de la [entidad de API](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="d86b3-242">`apis\<api name>\api.description.html` - this is the description of the API and corresponds to the `description` property of the [API entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span></span>
* <span data-ttu-id="d86b3-243">`apis\<api name>\operations\`: esta carpeta contiene archivos `<operation name>.description.html` que se asignan a las operaciones de la API.</span><span class="sxs-lookup"><span data-stu-id="d86b3-243">`apis\<api name>\operations\` - this folder contains `<operation name>.description.html` files that map to the operations in the API.</span></span> <span data-ttu-id="d86b3-244">Cada archivo contiene la descripción de una única operación en la API que se asigna a la propiedad `description` de la [entidad de operación](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) en la API de REST.</span><span class="sxs-lookup"><span data-stu-id="d86b3-244">Each file contains the description of a single operation in the API which maps to the `description` property of the [operation entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) in the REST API.</span></span>

### <a name="groups-folder"></a><span data-ttu-id="d86b3-245">carpeta de grupos</span><span class="sxs-lookup"><span data-stu-id="d86b3-245">groups folder</span></span>
<span data-ttu-id="d86b3-246">La carpeta `groups` contiene una carpeta para cada grupo definido en la instancia de servicio.</span><span class="sxs-lookup"><span data-stu-id="d86b3-246">The `groups` folder contains a folder for each group defined in the service instance.</span></span>

* <span data-ttu-id="d86b3-247">`groups\<group name>\configuration.json`: es la configuración para el grupo.</span><span class="sxs-lookup"><span data-stu-id="d86b3-247">`groups\<group name>\configuration.json` - this is the configuration for the group.</span></span> <span data-ttu-id="d86b3-248">Se trata de la misma información que se devolvería si se llamase a la operación [Obtener un grupo específico](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) .</span><span class="sxs-lookup"><span data-stu-id="d86b3-248">This is the same information that would be returned if you were to call the [Get a specific group](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) operation.</span></span>
* <span data-ttu-id="d86b3-249">`groups\<group name>\description.html`: es la descripción del grupo y corresponde a la propiedad `description` de la [entidad de servicio](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="d86b3-249">`groups\<group name>\description.html` - this is the description of the group and corresponds to the `description` property of the [group entity](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span></span>

### <a name="policies-folder"></a><span data-ttu-id="d86b3-250">carpeta de directivas</span><span class="sxs-lookup"><span data-stu-id="d86b3-250">policies folder</span></span>
<span data-ttu-id="d86b3-251">La carpeta `policies` contiene las instrucciones de directiva para la instancia de servicio.</span><span class="sxs-lookup"><span data-stu-id="d86b3-251">The `policies` folder contains the policy statements for your service instance.</span></span>

* <span data-ttu-id="d86b3-252">`policies\global.xml` : contiene las directivas definidas en el ámbito global para la instancia de servicio.</span><span class="sxs-lookup"><span data-stu-id="d86b3-252">`policies\global.xml` - contains policies defined at global scope for your service instance.</span></span>
* <span data-ttu-id="d86b3-253">`policies\apis\<api name>\`: si tiene directivas definidas en el ámbito de la API, se encuentran en esta carpeta.</span><span class="sxs-lookup"><span data-stu-id="d86b3-253">`policies\apis\<api name>\` - if you have any policies defined at API scope, they are contained in this folder.</span></span>
* <span data-ttu-id="d86b3-254">Carpeta `policies\apis\<api name>\<operation name>\`: si tiene directivas definidas en el ámbito de la operación, se encuentran en esta carpeta en archivos `<operation name>.xml` que se asignan a las instrucciones de directiva para cada operación.</span><span class="sxs-lookup"><span data-stu-id="d86b3-254">`policies\apis\<api name>\<operation name>\` folder - if you have any policies defined at operation scope, they are contained in this folder in `<operation name>.xml` files that map to the policy statements for each operation.</span></span>
* <span data-ttu-id="d86b3-255">`policies\products\`: si tiene directivas definidas en el ámbito del producto, se encuentran esta carpeta, que contiene archivos `<product name>.xml` que se asignan a las instrucciones de directiva para cada producto.</span><span class="sxs-lookup"><span data-stu-id="d86b3-255">`policies\products\` - if you have any policies defined at product scope, they are contained in this folder, which contains `<product name>.xml` files that map to the policy statements for each product.</span></span>

### <a name="portalstyles-folder"></a><span data-ttu-id="d86b3-256">carpeta portalStyles</span><span class="sxs-lookup"><span data-stu-id="d86b3-256">portalStyles folder</span></span>
<span data-ttu-id="d86b3-257">La carpeta `portalStyles` contiene la configuración y las hojas de estilo para las personalizaciones del portal para desarrolladores de la instancia de servicio.</span><span class="sxs-lookup"><span data-stu-id="d86b3-257">The `portalStyles` folder contains configuration and style sheets for developer portal customizations for the service instance.</span></span>

* <span data-ttu-id="d86b3-258">`portalStyles\configuration.json`: contiene los nombres de las hojas de estilos usadas por el portal de desarrolladores</span><span class="sxs-lookup"><span data-stu-id="d86b3-258">`portalStyles\configuration.json` - contains the names of the style sheets used by the developer portal</span></span>
* <span data-ttu-id="d86b3-259">`portalStyles\<style name>.css`: cada archivo `<style name>.css` contiene estilos para el portal para desarrolladores (`Preview.css` y `Production.css` de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="d86b3-259">`portalStyles\<style name>.css` - each `<style name>.css` file contains styles for the developer portal (`Preview.css` and `Production.css` by default).</span></span>

### <a name="products-folder"></a><span data-ttu-id="d86b3-260">carpeta de productos</span><span class="sxs-lookup"><span data-stu-id="d86b3-260">products folder</span></span>
<span data-ttu-id="d86b3-261">La carpeta `products` contiene una carpeta para cada producto que se define en la instancia de servicio.</span><span class="sxs-lookup"><span data-stu-id="d86b3-261">The `products` folder contains a folder for each product defined in the service instance.</span></span>

* <span data-ttu-id="d86b3-262">`products\<product name>\configuration.json`: es la configuración del producto.</span><span class="sxs-lookup"><span data-stu-id="d86b3-262">`products\<product name>\configuration.json` - this is the configuration for the product.</span></span> <span data-ttu-id="d86b3-263">Se trata de la misma información que se devolvería si se llamase a la operación [Obtener un producto específico](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) .</span><span class="sxs-lookup"><span data-stu-id="d86b3-263">This is the same information that would be returned if you were to call the [Get a specific product](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) operation.</span></span>
* <span data-ttu-id="d86b3-264">`products\<product name>\product.description.html`: es la descripción del producto y corresponde a la propiedad `description` de la [entidad de producto](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) de la API de REST.</span><span class="sxs-lookup"><span data-stu-id="d86b3-264">`products\<product name>\product.description.html` - this is the description of the product and corresponds to the `description` property of the [product entity](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) in the REST API.</span></span>

### <a name="templates"></a><span data-ttu-id="d86b3-265">plantillas</span><span class="sxs-lookup"><span data-stu-id="d86b3-265">templates</span></span>
<span data-ttu-id="d86b3-266">La carpeta `templates` contiene la configuración para las [plantillas de correo electrónico](api-management-howto-configure-notifications.md) de la instancia de servicio.</span><span class="sxs-lookup"><span data-stu-id="d86b3-266">The `templates` folder contains configuration for the [email templates](api-management-howto-configure-notifications.md) of the service instance.</span></span>

* <span data-ttu-id="d86b3-267">`<template name>\configuration.json` : es la configuración de la plantilla de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="d86b3-267">`<template name>\configuration.json` - this is the configuration for the email template.</span></span>
* <span data-ttu-id="d86b3-268">`<template name>\body.html` : es el cuerpo de la plantilla de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="d86b3-268">`<template name>\body.html` - this is the body of the email template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d86b3-269">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d86b3-269">Next steps</span></span>
<span data-ttu-id="d86b3-270">Para obtener información sobre otras formas de administrar la instancia de servicio, consulte:</span><span class="sxs-lookup"><span data-stu-id="d86b3-270">For information on other ways to manage your service instance, see:</span></span>

* <span data-ttu-id="d86b3-271">Administrar la instancia de servicio con los siguientes cmdlets de PowerShell</span><span class="sxs-lookup"><span data-stu-id="d86b3-271">Manage your service instance using the following PowerShell cmdlets</span></span>
  * [<span data-ttu-id="d86b3-272">Azure API Management Deployment Management Cmdlets (Cmdlets de administración de la implementación de Administración de API de Azure)</span><span class="sxs-lookup"><span data-stu-id="d86b3-272">Service deployment PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [<span data-ttu-id="d86b3-273">Azure API Management Service Management Cmdlets (Cmdlets de administración del servicio Administración de API de Azure)</span><span class="sxs-lookup"><span data-stu-id="d86b3-273">Service management PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* <span data-ttu-id="d86b3-274">Administrar la instancia de servicio en el portal para editores</span><span class="sxs-lookup"><span data-stu-id="d86b3-274">Manage your service instance in the publisher portal</span></span>
  * [<span data-ttu-id="d86b3-275">Administración de su primera API en Administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="d86b3-275">Manage your first API</span></span>](api-management-get-started.md)
* <span data-ttu-id="d86b3-276">Administrar la instancia de servicio mediante la API de REST</span><span class="sxs-lookup"><span data-stu-id="d86b3-276">Manage your service instance using the REST API</span></span>
  * [<span data-ttu-id="d86b3-277">API Management REST API (API de REST de Administración de API)</span><span class="sxs-lookup"><span data-stu-id="d86b3-277">API Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn776326.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="d86b3-278">Vea un vídeo de introducción.</span><span class="sxs-lookup"><span data-stu-id="d86b3-278">Watch a video overview</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Configuration-over-Git/player]
> 
> 

[api-management-enable-git]: ./media/api-management-configuration-repository-git/api-management-enable-git.png
[api-management-git-enabled]: ./media/api-management-configuration-repository-git/api-management-git-enabled.png
[api-management-save-configuration]: ./media/api-management-configuration-repository-git/api-management-save-configuration.png
[api-management-save-configuration-confirm]: ./media/api-management-configuration-repository-git/api-management-save-configuration-confirm.png
[api-management-configuration-status]: ./media/api-management-configuration-repository-git/api-management-configuration-status.png
[api-management-configuration-git-clone]: ./media/api-management-configuration-repository-git/api-management-configuration-git-clone.png
[api-management-generate-password]: ./media/api-management-configuration-repository-git/api-management-generate-password.png
[api-management-password]: ./media/api-management-configuration-repository-git/api-management-password.png
[api-management-git-configure]: ./media/api-management-configuration-repository-git/api-management-git-configure.png
[api-management-configuration-deploy]: ./media/api-management-configuration-repository-git/api-management-configuration-deploy.png
[api-management-identity-settings]: ./media/api-management-configuration-repository-git/api-management-identity-settings.png
[api-management-delegation-settings]: ./media/api-management-configuration-repository-git/api-management-delegation-settings.png
[api-management-git-icon-enable]: ./media/api-management-configuration-repository-git/api-management-git-icon-enable.png




