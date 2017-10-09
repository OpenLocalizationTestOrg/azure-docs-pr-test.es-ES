---
title: "aaaConfigure el servicio de administración de API con Git - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toosave y configurar la configuración del servicio de administración de API con Git."
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
ms.openlocfilehash: ef7d4c18f2ea3f5c9b86403349a83aef240f979b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosave-and-configure-your-api-management-service-configuration-using-git"></a><span data-ttu-id="11aa4-103">¿Cómo toosave y configurar la configuración del servicio de administración de API con Git</span><span class="sxs-lookup"><span data-stu-id="11aa4-103">How toosave and configure your API Management service configuration using Git</span></span>
> 
> 

<span data-ttu-id="11aa4-104">Cada instancia de servicio de administración de API mantiene una base de datos de configuración que contiene información sobre la configuración de Hola y metadatos de instancia de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="11aa4-104">Each API Management service instance maintains a configuration database that contains information about hello configuration and metadata for hello service instance.</span></span> <span data-ttu-id="11aa4-105">Pueden realizarse cambios instancia del servicio toohello cambiar una configuración en el portal para desarrolladores de hello, mediante un cmdlet de PowerShell, o realizar una llamada de API de REST.</span><span class="sxs-lookup"><span data-stu-id="11aa4-105">Changes can be made toohello service instance by changing a setting in hello publisher portal, using a PowerShell cmdlet, or making a REST API call.</span></span> <span data-ttu-id="11aa4-106">Además métodos toothese, también puede administrar la configuración de la instancia de servicio con Git, permite escenarios de administración de servicios como:</span><span class="sxs-lookup"><span data-stu-id="11aa4-106">In addition toothese methods, you can also manage your service instance configuration using Git, enabling service management scenarios such as:</span></span>

* <span data-ttu-id="11aa4-107">Control de versiones de configuración: descargue y almacene versiones diferentes de la configuración del servicio</span><span class="sxs-lookup"><span data-stu-id="11aa4-107">Configuration versioning - download and store different versions of your service configuration</span></span>
* <span data-ttu-id="11aa4-108">Cambios de configuración de forma masiva: realizar cambios toomultiple partes de la configuración del servicio en el repositorio local e integrar el servidor de toohello atrás de cambios de hello con una sola operación</span><span class="sxs-lookup"><span data-stu-id="11aa4-108">Bulk configuration changes - make changes toomultiple parts of your service configuration in your local repository and integrate hello changes back toohello server with a single operation</span></span>
* <span data-ttu-id="11aa4-109">Familiar Git la cadena de herramientas y flujo de trabajo - usar herramientas de Git de Hola y flujos de trabajo que ya están familiarizados con</span><span class="sxs-lookup"><span data-stu-id="11aa4-109">Familiar Git toolchain and workflow - use hello Git tooling and workflows that you are already familiar with</span></span>

<span data-ttu-id="11aa4-110">Hola siguiente diagrama muestra un resumen de tooconfigure de maneras diferentes de hello su instancia de servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="11aa4-110">hello following diagram shows an overview of hello different ways tooconfigure your API Management service instance.</span></span>

![Configuración de GIT][api-management-git-configure]

<span data-ttu-id="11aa4-112">Al realizar cambios de servicio de tooyour mediante el portal para desarrolladores de hello, cmdlets de PowerShell o API de REST de hello, administra la base de datos de configuración de servicio con hello `https://{name}.management.azure-api.net` extremo, tal y como se muestra en hello derecha del diagrama de Hola.</span><span class="sxs-lookup"><span data-stu-id="11aa4-112">When you make changes tooyour service using hello publisher portal, PowerShell cmdlets, or hello REST API, you are managing your service configuration database using hello `https://{name}.management.azure-api.net` endpoint, as shown on hello right side of hello diagram.</span></span> <span data-ttu-id="11aa4-113">Hola lado izquierdo del diagrama de hello, muestra cómo puede administrar la configuración del servicio mediante Git y repositorio de Git para el servicio que encontrará en `https://{name}.scm.azure-api.net`.</span><span class="sxs-lookup"><span data-stu-id="11aa4-113">hello left side of hello diagram illustrates how you can manage your service configuration using Git and Git repository for your service located at `https://{name}.scm.azure-api.net`.</span></span>

<span data-ttu-id="11aa4-114">Hola pasos proporciona información general de la administración de la instancia de servicio de administración de API con Git.</span><span class="sxs-lookup"><span data-stu-id="11aa4-114">hello following steps provide an overview of managing your API Management service instance using Git.</span></span>

1. <span data-ttu-id="11aa4-115">Acceso a la configuración de Git en el servicio</span><span class="sxs-lookup"><span data-stu-id="11aa4-115">Access Git configuration in your service</span></span>
2. <span data-ttu-id="11aa4-116">Guardar el repositorio de Git servicio tooyour de base de datos de configuración</span><span class="sxs-lookup"><span data-stu-id="11aa4-116">Save your service configuration database tooyour Git repository</span></span>
3. <span data-ttu-id="11aa4-117">Clonar máquina local de hello Git repositorio tooyour</span><span class="sxs-lookup"><span data-stu-id="11aa4-117">Clone hello Git repo tooyour local machine</span></span>
4. <span data-ttu-id="11aa4-118">Extracción repositorio más reciente de hello tooyour en los equipos local y confirme e inserte repositorio de back-tooyour de cambios</span><span class="sxs-lookup"><span data-stu-id="11aa4-118">Pull hello latest repo down tooyour local machine, and commit and push changes back tooyour repo</span></span>
5. <span data-ttu-id="11aa4-119">Implementar cambios de Hola desde el repositorio en la base de datos de configuración de servicio</span><span class="sxs-lookup"><span data-stu-id="11aa4-119">Deploy hello changes from your repo into your service configuration database</span></span>

<span data-ttu-id="11aa4-120">Este artículo se describe cómo tooenable y usar Git toomanage la configuración del servicio y proporciona una referencia de hello archivos y carpetas en el repositorio de Git Hola.</span><span class="sxs-lookup"><span data-stu-id="11aa4-120">This article describes how tooenable and use Git toomanage your service configuration and provides a reference for hello files and folders in hello Git repository.</span></span>

## <a name="access-git-configuration-in-your-service"></a><span data-ttu-id="11aa4-121">Acceso a la configuración de Git en el servicio</span><span class="sxs-lookup"><span data-stu-id="11aa4-121">Access Git configuration in your service</span></span>
<span data-ttu-id="11aa4-122">Puede ver rápidamente estado de saludo de la configuración de Git viendo el icono de Git de hello en la esquina superior derecha de Hola de portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="11aa4-122">You can quickly view hello status of your Git configuration by viewing hello Git icon in hello upper-right corner of hello publisher portal.</span></span> <span data-ttu-id="11aa4-123">En este ejemplo, el mensaje de bienvenida de estado indica que hay repositorio de toohello de los cambios no guardados.</span><span class="sxs-lookup"><span data-stu-id="11aa4-123">In this example, hello status message indicates that there are unsaved changes toohello repository.</span></span> <span data-ttu-id="11aa4-124">Esto es porque la base de datos de configuración de servicio de administración de API de hello aún no se ha guardado toohello repositorio.</span><span class="sxs-lookup"><span data-stu-id="11aa4-124">This is because hello API Management service configuration database has not yet been saved toohello repository.</span></span>

![Estado de Git][api-management-git-icon-enable]

<span data-ttu-id="11aa4-126">tooview y configurar las opciones de configuración de Git, puede haga clic en el icono de Git de hello, o haga clic en hello **seguridad** menú y vaya toohello **repositorio de configuración** ficha.</span><span class="sxs-lookup"><span data-stu-id="11aa4-126">tooview and configure your Git configuration settings, you can either click hello Git icon, or click hello **Security** menu and navigate toohello **Configuration repository** tab.</span></span>

![Habilitar GIT][api-management-enable-git]

> [!IMPORTANT]
> <span data-ttu-id="11aa4-128">Los secretos que no estén definidos como propiedades se almacenan en el repositorio de Hola y permanecerán en su historial de hasta que deshabilite y vuelva a habilitar el acceso de Git.</span><span class="sxs-lookup"><span data-stu-id="11aa4-128">Any secrets that are not defined as properties will be stored in hello repository and will remain in its history until you disable and re-enable Git access.</span></span> <span data-ttu-id="11aa4-129">Propiedades proporcionan un lugar seguro toomanage valores de cadena constante, incluidos los secretos, a través de todas las directivas y configuración de API de modo que no tenga toostore directamente en las instrucciones de directiva.</span><span class="sxs-lookup"><span data-stu-id="11aa4-129">Properties provide a secure place toomanage constant string values, including secrets, across all API configuration and policies, so you don't have toostore them directly in your policy statements.</span></span> <span data-ttu-id="11aa4-130">Para obtener más información, consulte [cómo toouse propiedades en las directivas de administración de API de Azure](api-management-howto-properties.md).</span><span class="sxs-lookup"><span data-stu-id="11aa4-130">For more information, see [How toouse properties in Azure API Management policies](api-management-howto-properties.md).</span></span>
> 
> 

<span data-ttu-id="11aa4-131">Para obtener información sobre la habilitación o deshabilitación del acceso de Git con hello API de REST, consulte [habilitar o deshabilitar el acceso de Git con la API de REST de hello](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span><span class="sxs-lookup"><span data-stu-id="11aa4-131">For information on enabling or disabling Git access using hello REST API, see [Enable or disable Git access using hello REST API](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span></span>

## <a name="toosave-hello-service-configuration-toohello-git-repository"></a><span data-ttu-id="11aa4-132">repositorio de Git toosave Hola servicio configuración toohello</span><span class="sxs-lookup"><span data-stu-id="11aa4-132">toosave hello service configuration toohello Git repository</span></span>
<span data-ttu-id="11aa4-133">Hola primer paso antes de la clonación repositorio hello es estado actual de hello toosave del repositorio de toohello de configuración de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="11aa4-133">hello first step before cloning hello repository is toosave hello current state of hello service configuration toohello repository.</span></span> <span data-ttu-id="11aa4-134">Haga clic en **Guardar configuración toorepository**.</span><span class="sxs-lookup"><span data-stu-id="11aa4-134">Click **Save configuration toorepository**.</span></span>

![Guardar configuración][api-management-save-configuration]

<span data-ttu-id="11aa4-136">Realice los cambios deseados en la pantalla de confirmación de bienvenida y haga clic en **Aceptar** toosave.</span><span class="sxs-lookup"><span data-stu-id="11aa4-136">Make any desired changes on hello confirmation screen and click **Ok** toosave.</span></span>

![Guardar configuración][api-management-save-configuration-confirm]

<span data-ttu-id="11aa4-138">Transcurridos unos instantes se guarda la configuración de Hola y se muestra el estado de la configuración del repositorio de Hola Hola, incluidos Hola fecha y hora del último cambio de configuración de Hola y última sincronización de hello entre la configuración del servicio de Hola y Hola repositorio.</span><span class="sxs-lookup"><span data-stu-id="11aa4-138">After a few moments hello configuration is saved, and hello configuration status of hello repository is displayed, including hello date and time of hello last configuration change and hello last synchronization between hello service configuration and hello repository.</span></span>

![Estado de configuración][api-management-configuration-status]

<span data-ttu-id="11aa4-140">Una vez Hola configuración se ha guardado toohello repositorio, se puede clonar.</span><span class="sxs-lookup"><span data-stu-id="11aa4-140">Once hello configuration is saved toohello repository, it can be cloned.</span></span>

<span data-ttu-id="11aa4-141">Para obtener información acerca de cómo realizar esta operación mediante la API de REST de hello, consulte [configuración de confirmación de instantáneas mediante la API de REST de hello](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span><span class="sxs-lookup"><span data-stu-id="11aa4-141">For information on performing this operation using hello REST API, see [Commit configuration snapshot using hello REST API](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span></span>

## <a name="tooclone-hello-repository-tooyour-local-machine"></a><span data-ttu-id="11aa4-142">equipo local de tooclone Hola repositorio tooyour</span><span class="sxs-lookup"><span data-stu-id="11aa4-142">tooclone hello repository tooyour local machine</span></span>
<span data-ttu-id="11aa4-143">tooclone un repositorio, deberá tooyour repositorio de hello dirección URL, un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="11aa4-143">tooclone a repository, you need hello URL tooyour repository, a user name, and a password.</span></span> <span data-ttu-id="11aa4-144">Hello nombre de usuario y la dirección URL se muestran en parte superior de Hola de hello **repositorio de configuración** ficha.</span><span class="sxs-lookup"><span data-stu-id="11aa4-144">hello user name and URL are displayed near hello top of hello **Configuration repository** tab.</span></span>

![Clonación de git][api-management-configuration-git-clone]

<span data-ttu-id="11aa4-146">contraseña de Hola se genera en parte inferior de Hola de Hola **repositorio de configuración** ficha.</span><span class="sxs-lookup"><span data-stu-id="11aa4-146">hello password is generated at hello bottom of hello **Configuration repository** tab.</span></span>

![Generar contraseña][api-management-generate-password]

<span data-ttu-id="11aa4-148">toogenerate una contraseña, asegúrese en primer lugar ese hello **caducidad** toohello deseado fecha de expiración y la hora del juego y, a continuación, haga clic en **generar Token**.</span><span class="sxs-lookup"><span data-stu-id="11aa4-148">toogenerate a password, first ensure that hello **Expiry** is set toohello desired expiration date and time, and then click **Generate Token**.</span></span>

![Password][api-management-password]

> [!IMPORTANT]
> <span data-ttu-id="11aa4-150">Anote esta contraseña.</span><span class="sxs-lookup"><span data-stu-id="11aa4-150">Make a note of this password.</span></span> <span data-ttu-id="11aa4-151">Una vez que abandona esta contraseña de Hola de página no se mostrará nuevo.</span><span class="sxs-lookup"><span data-stu-id="11aa4-151">Once you leave this page hello password will not be displayed again.</span></span>
> 
> 

<span data-ttu-id="11aa4-152">Hola uso Hola Git Bash en los ejemplos siguientes de la herramienta de [Git para Windows](http://www.git-scm.com/downloads) , pero puede utilizar cualquier herramienta de Git que estás familiarizado con.</span><span class="sxs-lookup"><span data-stu-id="11aa4-152">hello following examples use hello Git Bash tool from [Git for Windows](http://www.git-scm.com/downloads) but you can use any Git tool that you are familiar with.</span></span>

<span data-ttu-id="11aa4-153">Abra la herramienta de Git en la carpeta que desee hello y ejecute Hola siguiendo el equipo local del tooyour de repositorio de comando tooclone Hola git, mediante comandos Hola proporcionada por el portal para desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="11aa4-153">Open your Git tool in hello desired folder and run hello following command tooclone hello git repository tooyour local machine, using hello command provided by hello publisher portal.</span></span>

```
git clone https://bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="11aa4-154">Proporcione el nombre de usuario de hello y una contraseña cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="11aa4-154">Provide hello user name and password when prompted.</span></span>

<span data-ttu-id="11aa4-155">Si aparece algún error, intente modificar la `git clone` comando tooinclude Hola nombre y contraseña, como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="11aa4-155">If you receive any errors, try modifying your `git clone` command tooinclude hello user name and password, as shown in hello following example.</span></span>

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="11aa4-156">Si se trata de un error, pruebe a parte de la contraseña del comando de Hola Hola de codificación de direcciones URL.</span><span class="sxs-lookup"><span data-stu-id="11aa4-156">If this provides an error, try URL encoding hello password portion of hello command.</span></span> <span data-ttu-id="11aa4-157">Toodo de una forma rápida es tooopen Visual Studio y comando siguiente de Hola de problema en hello **ventana Inmediato**.</span><span class="sxs-lookup"><span data-stu-id="11aa4-157">One quick way toodo this is tooopen Visual Studio, and issue hello following command in hello **Immediate Window**.</span></span> <span data-ttu-id="11aa4-158">Hola tooopen **ventana Inmediato**, abra ninguna solución ni proyecto en Visual Studio (o cree una nueva aplicación de consola vacía) y elija **Windows**, **inmediato** desde Hola **depurar** menú.</span><span class="sxs-lookup"><span data-stu-id="11aa4-158">tooopen hello **Immediate Window**, open any solution or project in Visual Studio (or create a new empty console application), and choose **Windows**, **Immediate** from hello **Debug** menu.</span></span>

```
?System.NetWebUtility.UrlEncode("password from publisher portal")
```

<span data-ttu-id="11aa4-159">Usar la contraseña de hello codificado junto con su nombre y del repositorio ubicación tooconstruct Hola git comando user.</span><span class="sxs-lookup"><span data-stu-id="11aa4-159">Use hello encoded password along with your user name and repository location tooconstruct hello git command.</span></span>

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="11aa4-160">Una vez que se clona repositorio Hola puede ver y trabajar con ellos en el sistema de archivos local.</span><span class="sxs-lookup"><span data-stu-id="11aa4-160">Once hello repository is cloned you can view and work with it in your local file system.</span></span> <span data-ttu-id="11aa4-161">Para más información, consulte [Referencia de estructura de archivo y carpeta del repositorio local de Git](#file-and-folder-structure-reference-of-local-git-repository).</span><span class="sxs-lookup"><span data-stu-id="11aa4-161">For more information, see [File and folder structure reference of local Git repository](#file-and-folder-structure-reference-of-local-git-repository).</span></span>

## <a name="tooupdate-your-local-repository-with-hello-most-current-service-instance-configuration"></a><span data-ttu-id="11aa4-162">tooupdate el repositorio local con la configuración de instancia de servicio más reciente de Hola</span><span class="sxs-lookup"><span data-stu-id="11aa4-162">tooupdate your local repository with hello most current service instance configuration</span></span>
<span data-ttu-id="11aa4-163">Si realiza la instancia de servicio de administración de API de cambios tooyour en portal para desarrolladores de Hola o mediante la API de REST de hello, debe guardar estos repositorio de toohello de cambios para que pueda actualizar el repositorio local con los cambios más recientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="11aa4-163">If you make changes tooyour API Management service instance in hello publisher portal or using hello REST API, you must save these changes toohello repository before you can update your local repository with hello latest changes.</span></span> <span data-ttu-id="11aa4-164">toodo, haga clic en **Guardar configuración toorepository** en hello **repositorio de configuración** pestaña en el portal para desarrolladores de hello y, a continuación, emita Hola siguiente comando en el repositorio local.</span><span class="sxs-lookup"><span data-stu-id="11aa4-164">toodo this, click **Save configuration toorepository** on hello **Configuration repository** tab in hello publisher portal, and then issue hello following command in your local repository.</span></span>

```
git pull
```

<span data-ttu-id="11aa4-165">Antes de ejecutar `git pull` Asegúrese de que se encuentra en la carpeta de hello para el repositorio local.</span><span class="sxs-lookup"><span data-stu-id="11aa4-165">Before running `git pull` ensure that you are in hello folder for your local repository.</span></span> <span data-ttu-id="11aa4-166">Si acaba de completar el Hola `git clone` comando, tendrá que cambiar tooyour repositorio de hello directorio mediante la ejecución de un comando similar al siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="11aa4-166">If you have just completed hello `git clone` command, then you must change hello directory tooyour repo by running a command like hello following.</span></span>

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="toopush-changes-from-your-local-repo-toohello-server-repo"></a><span data-ttu-id="11aa4-167">cambios de toopush desde el repositorio de servidor toohello repositorio local</span><span class="sxs-lookup"><span data-stu-id="11aa4-167">toopush changes from your local repo toohello server repo</span></span>
<span data-ttu-id="11aa4-168">toopush cambia desde el repositorio del servidor toohello repositorio local, debe confirmar los cambios y, a continuación, insertarlas toohello repositorio del servidor.</span><span class="sxs-lookup"><span data-stu-id="11aa4-168">toopush changes from your local repository toohello server repository, you must commit your changes and then push them toohello server repository.</span></span> <span data-ttu-id="11aa4-169">toocommit los cambios, abra la herramienta de comandos Git, conmutador toohello directorio del repositorio local y Hola problema después de comandos.</span><span class="sxs-lookup"><span data-stu-id="11aa4-169">toocommit your changes, open your Git command tool, switch toohello directory of your local repository, and issue hello following commands.</span></span>

```
git add --all
git commit -m "Description of your changes"
```

<span data-ttu-id="11aa4-170">toopush todos Hola confirma toohello server, ejecute Hola después del comando.</span><span class="sxs-lookup"><span data-stu-id="11aa4-170">toopush all of hello commits toohello server, run hello following command.</span></span>

```
git push
```

## <a name="toodeploy-any-service-configuration-changes-toohello-api-management-service-instance"></a><span data-ttu-id="11aa4-171">toodeploy las instancias del servicio de administración de API de servicio configuración cambios toohello</span><span class="sxs-lookup"><span data-stu-id="11aa4-171">toodeploy any service configuration changes toohello API Management service instance</span></span>
<span data-ttu-id="11aa4-172">Una vez que los cambios locales están insertadas y sin confirmar toohello repositorio del servidor, puede implementarlos tooyour instancia del servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="11aa4-172">Once your local changes are committed and pushed toohello server repository, you can deploy them tooyour API Management service instance.</span></span>

![Implementación][api-management-configuration-deploy]

<span data-ttu-id="11aa4-174">Para obtener información acerca de cómo realizar esta operación mediante la API de REST de hello, consulte [implementar Git cambia mediante Hola API de REST de base de datos de tooconfiguration](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span><span class="sxs-lookup"><span data-stu-id="11aa4-174">For information on performing this operation using hello REST API, see [Deploy Git changes tooconfiguration database using hello REST API](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span></span>

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a><span data-ttu-id="11aa4-175">Referencia de estructura de archivo y carpeta del repositorio local de Git</span><span class="sxs-lookup"><span data-stu-id="11aa4-175">File and folder structure reference of local Git repository</span></span>
<span data-ttu-id="11aa4-176">Hello archivos y carpetas en el repositorio de git local Hola contienen Hola información de configuración acerca de la instancia de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="11aa4-176">hello files and folders in hello local git repository contain hello configuration information about hello service instance.</span></span>

| <span data-ttu-id="11aa4-177">Elemento</span><span class="sxs-lookup"><span data-stu-id="11aa4-177">Item</span></span> | <span data-ttu-id="11aa4-178">Description</span><span class="sxs-lookup"><span data-stu-id="11aa4-178">Description</span></span> |
| --- | --- |
| <span data-ttu-id="11aa4-179">carpeta raíz de la administración de API</span><span class="sxs-lookup"><span data-stu-id="11aa4-179">root api-management folder</span></span> |<span data-ttu-id="11aa4-180">Contiene la configuración de nivel superior para la instancia de servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="11aa4-180">Contains top-level configuration for hello service instance</span></span> |
| <span data-ttu-id="11aa4-181">carpeta de API</span><span class="sxs-lookup"><span data-stu-id="11aa4-181">apis folder</span></span> |<span data-ttu-id="11aa4-182">Contiene la configuración de Hola de hello API de instancia de servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="11aa4-182">Contains hello configuration for hello apis in hello service instance</span></span> |
| <span data-ttu-id="11aa4-183">carpeta de grupos</span><span class="sxs-lookup"><span data-stu-id="11aa4-183">groups folder</span></span> |<span data-ttu-id="11aa4-184">Contiene configuración de Hola para grupos de hello en la instancia de servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="11aa4-184">Contains hello configuration for hello groups in hello service instance</span></span> |
| <span data-ttu-id="11aa4-185">carpeta de directivas</span><span class="sxs-lookup"><span data-stu-id="11aa4-185">policies folder</span></span> |<span data-ttu-id="11aa4-186">Contiene directivas de hello en la instancia de servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="11aa4-186">Contains hello policies in hello service instance</span></span> |
| <span data-ttu-id="11aa4-187">carpeta portalStyles</span><span class="sxs-lookup"><span data-stu-id="11aa4-187">portalStyles folder</span></span> |<span data-ttu-id="11aa4-188">Contiene la configuración de Hola de personalizaciones del portal para desarrolladores hello en la instancia de servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="11aa4-188">Contains hello configuration for hello developer portal customizations in hello service instance</span></span> |
| <span data-ttu-id="11aa4-189">carpeta de productos</span><span class="sxs-lookup"><span data-stu-id="11aa4-189">products folder</span></span> |<span data-ttu-id="11aa4-190">Contiene configuración de Hola para productos de hello en la instancia de servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="11aa4-190">Contains hello configuration for hello products in hello service instance</span></span> |
| <span data-ttu-id="11aa4-191">carpeta de plantillas</span><span class="sxs-lookup"><span data-stu-id="11aa4-191">templates folder</span></span> |<span data-ttu-id="11aa4-192">Contiene la configuración de Hola de plantillas de correo electrónico de hello en la instancia de servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="11aa4-192">Contains hello configuration for hello email templates in hello service instance</span></span> |

<span data-ttu-id="11aa4-193">Cada carpeta puede contener uno o varios archivos y, en algunos casos, una o varias carpetas; por ejemplo, una carpeta para cada API, producto o grupo.</span><span class="sxs-lookup"><span data-stu-id="11aa4-193">Each folder can contain one or more files, and in some cases one or more folders, for example a folder for each API, product, or group.</span></span> <span data-ttu-id="11aa4-194">Hola archivos dentro de cada carpeta son específicos para el tipo de entidad Hola descrito por el nombre de la carpeta de Hola.</span><span class="sxs-lookup"><span data-stu-id="11aa4-194">hello files within each folder are specific for hello entity type described by hello folder name.</span></span>

| <span data-ttu-id="11aa4-195">Tipo de archivo</span><span class="sxs-lookup"><span data-stu-id="11aa4-195">File type</span></span> | <span data-ttu-id="11aa4-196">Propósito</span><span class="sxs-lookup"><span data-stu-id="11aa4-196">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="11aa4-197">json</span><span class="sxs-lookup"><span data-stu-id="11aa4-197">json</span></span> |<span data-ttu-id="11aa4-198">Información de configuración acerca de la entidad respectiva Hola</span><span class="sxs-lookup"><span data-stu-id="11aa4-198">Configuration information about hello respective entity</span></span> |
| <span data-ttu-id="11aa4-199">html</span><span class="sxs-lookup"><span data-stu-id="11aa4-199">html</span></span> |<span data-ttu-id="11aa4-200">Descripciones de entidad de hello, a menudo se muestran en el portal para desarrolladores de Hola</span><span class="sxs-lookup"><span data-stu-id="11aa4-200">Descriptions about hello entity, often displayed in hello developer portal</span></span> |
| <span data-ttu-id="11aa4-201">xml</span><span class="sxs-lookup"><span data-stu-id="11aa4-201">xml</span></span> |<span data-ttu-id="11aa4-202">Policy statements</span><span class="sxs-lookup"><span data-stu-id="11aa4-202">Policy statements</span></span> |
| <span data-ttu-id="11aa4-203">css</span><span class="sxs-lookup"><span data-stu-id="11aa4-203">css</span></span> |<span data-ttu-id="11aa4-204">Hojas de estilo para la personalización del portal para desarrolladores</span><span class="sxs-lookup"><span data-stu-id="11aa4-204">Style sheets for developer portal customization</span></span> |

<span data-ttu-id="11aa4-205">Estos archivos pueden crear, eliminar, editar y administran en el sistema de archivos local e implementen los cambios de hello toohello espera su instancia de servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="11aa4-205">These files can be created, deleted, edited, and managed on your local file system, and hello changes deployed back toohello your API Management service instance.</span></span>

> [!NOTE]
> <span data-ttu-id="11aa4-206">Hola entidades siguientes no están contenidas en el repositorio de Git de hello y no se puede configurar mediante Git.</span><span class="sxs-lookup"><span data-stu-id="11aa4-206">hello following entities are not contained in hello Git repository and cannot be configured using Git.</span></span>
> 
> * <span data-ttu-id="11aa4-207">Usuarios</span><span class="sxs-lookup"><span data-stu-id="11aa4-207">Users</span></span>
> * <span data-ttu-id="11aa4-208">Suscripciones</span><span class="sxs-lookup"><span data-stu-id="11aa4-208">Subscriptions</span></span>
> * <span data-ttu-id="11aa4-209">Propiedades</span><span class="sxs-lookup"><span data-stu-id="11aa4-209">Properties</span></span>
> * <span data-ttu-id="11aa4-210">Entidades del portal de desarrolladores distintas de los estilos</span><span class="sxs-lookup"><span data-stu-id="11aa4-210">Developer portal entities other than styles</span></span>
> 
> 

### <a name="root-api-management-folder"></a><span data-ttu-id="11aa4-211">Carpeta raíz de la administración de API</span><span class="sxs-lookup"><span data-stu-id="11aa4-211">Root api-management folder</span></span>
<span data-ttu-id="11aa4-212">raíz de Hello `api-management` carpeta contiene un `configuration.json` archivo que contiene información acerca de la instancia de servicio de Hola Hola siguiendo el formato de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="11aa4-212">hello root `api-management` folder contains a `configuration.json` file that contains top-level information about hello service instance in hello following format.</span></span>

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

<span data-ttu-id="11aa4-213">Hola primero cuatro opciones (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, y `UserRegistrationTermsConsentRequired`) asignar toohello siguiente configuración de hello **identidades** ficha hello **seguridad** sección.</span><span class="sxs-lookup"><span data-stu-id="11aa4-213">hello first four settings (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, and `UserRegistrationTermsConsentRequired`) map toohello following settings on hello **Identities** tab in hello **Security** section.</span></span>

| <span data-ttu-id="11aa4-214">Configuración de identidad</span><span class="sxs-lookup"><span data-stu-id="11aa4-214">Identity setting</span></span> | <span data-ttu-id="11aa4-215">Se asigna demasiado</span><span class="sxs-lookup"><span data-stu-id="11aa4-215">Maps too</span></span>|
| --- | --- |
| <span data-ttu-id="11aa4-216">RegistrationEnabled</span><span class="sxs-lookup"><span data-stu-id="11aa4-216">RegistrationEnabled</span></span> |<span data-ttu-id="11aa4-217">**Redirigir a los usuarios anónimos en toosign página** casilla de verificación</span><span class="sxs-lookup"><span data-stu-id="11aa4-217">**Redirect anonymous users toosign-in page** checkbox</span></span> |
| <span data-ttu-id="11aa4-218">UserRegistrationTerms</span><span class="sxs-lookup"><span data-stu-id="11aa4-218">UserRegistrationTerms</span></span> |<span data-ttu-id="11aa4-219">**Condiciones de uso del registro de usuario**</span><span class="sxs-lookup"><span data-stu-id="11aa4-219">**Terms of use on user signup** textbox</span></span> |
| <span data-ttu-id="11aa4-220">UserRegistrationTermsEnabled</span><span class="sxs-lookup"><span data-stu-id="11aa4-220">UserRegistrationTermsEnabled</span></span> |<span data-ttu-id="11aa4-221">**Mostrar condiciones de uso en la página de registro**</span><span class="sxs-lookup"><span data-stu-id="11aa4-221">**Show terms of use on signup page** checkbox</span></span> |
| <span data-ttu-id="11aa4-222">UserRegistrationTermsConsentRequired</span><span class="sxs-lookup"><span data-stu-id="11aa4-222">UserRegistrationTermsConsentRequired</span></span> |<span data-ttu-id="11aa4-223">**Requerir consentimiento**</span><span class="sxs-lookup"><span data-stu-id="11aa4-223">**Require consent** checkbox</span></span> |

![Configuración de identidad][api-management-identity-settings]

<span data-ttu-id="11aa4-225">Hola siguientes cuatro valores (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, y `DelegationValidationKey`) asignar toohello siguiente configuración de hello **delegación** ficha hello **seguridad** sección.</span><span class="sxs-lookup"><span data-stu-id="11aa4-225">hello next four settings (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, and `DelegationValidationKey`) map toohello following settings on hello **Delegation** tab in hello **Security** section.</span></span>

| <span data-ttu-id="11aa4-226">Configuración de delegación</span><span class="sxs-lookup"><span data-stu-id="11aa4-226">Delegation setting</span></span> | <span data-ttu-id="11aa4-227">Se asigna demasiado</span><span class="sxs-lookup"><span data-stu-id="11aa4-227">Maps too</span></span>|
| --- | --- |
| <span data-ttu-id="11aa4-228">DelegationEnabled</span><span class="sxs-lookup"><span data-stu-id="11aa4-228">DelegationEnabled</span></span> |<span data-ttu-id="11aa4-229">Casilla **Delegar inicio de sesión y registro**</span><span class="sxs-lookup"><span data-stu-id="11aa4-229">**Delegate sign-in & sign-up** checkbox</span></span> |
| <span data-ttu-id="11aa4-230">DelegationUrl</span><span class="sxs-lookup"><span data-stu-id="11aa4-230">DelegationUrl</span></span> |<span data-ttu-id="11aa4-231">**Dirección URL del punto de conexión de delegación**</span><span class="sxs-lookup"><span data-stu-id="11aa4-231">**Delegation endpoint URL** textbox</span></span> |
| <span data-ttu-id="11aa4-232">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="11aa4-232">DelegatedSubscriptionEnabled</span></span> |<span data-ttu-id="11aa4-233">**Delegar suscripción de producto**</span><span class="sxs-lookup"><span data-stu-id="11aa4-233">**Delegate product subscription** checkbox</span></span> |
| <span data-ttu-id="11aa4-234">DelegationValidationKey</span><span class="sxs-lookup"><span data-stu-id="11aa4-234">DelegationValidationKey</span></span> |<span data-ttu-id="11aa4-235">**Delegar clave de validación**</span><span class="sxs-lookup"><span data-stu-id="11aa4-235">**Delegate Validation Key** textbox</span></span> |

![Configuración de delegación][api-management-delegation-settings]

<span data-ttu-id="11aa4-237">Hola valor final, `$ref-policy`, asigna el archivo de instrucciones de directiva global toohello para la instancia de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="11aa4-237">hello final setting, `$ref-policy`, maps toohello global policy statements file for hello service instance.</span></span>

### <a name="apis-folder"></a><span data-ttu-id="11aa4-238">carpeta de API</span><span class="sxs-lookup"><span data-stu-id="11aa4-238">apis folder</span></span>
<span data-ttu-id="11aa4-239">Hola `apis` carpeta contiene una carpeta para cada API de instancia de servicio de Hola que contiene los siguientes elementos de Hola.</span><span class="sxs-lookup"><span data-stu-id="11aa4-239">hello `apis` folder contains a folder for each API in hello service instance which contains hello following items.</span></span>

* <span data-ttu-id="11aa4-240">`apis\<api name>\configuration.json`-Esto es configuración de Hola para hello API y contiene información acerca de la dirección URL del servicio de back-end de Hola y las operaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="11aa4-240">`apis\<api name>\configuration.json` - this is hello configuration for hello API and contains information about hello backend service URL and hello operations.</span></span> <span data-ttu-id="11aa4-241">Se trata de hello misma información que se devolverían si estuviera toocall [obtener una API específica](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) con `export=true` en `application/json` formato.</span><span class="sxs-lookup"><span data-stu-id="11aa4-241">This is hello same information that would be returned if you were toocall [Get a specific API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) with `export=true` in `application/json` format.</span></span>
* <span data-ttu-id="11aa4-242">`apis\<api name>\api.description.html`-Esto es una descripción de Hola de hello API y corresponde toohello `description` propiedad de hello [entidad de API](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="11aa4-242">`apis\<api name>\api.description.html` - this is hello description of hello API and corresponds toohello `description` property of hello [API entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span></span>
* <span data-ttu-id="11aa4-243">`apis\<api name>\operations\`-Esta carpeta contiene `<operation name>.description.html` archivos que se asignan las operaciones de toohello Hola API.</span><span class="sxs-lookup"><span data-stu-id="11aa4-243">`apis\<api name>\operations\` - this folder contains `<operation name>.description.html` files that map toohello operations in hello API.</span></span> <span data-ttu-id="11aa4-244">Cada archivo contiene la descripción de Hola de una sola operación Hola API que se asigna toohello `description` propiedad de hello [entidad de operación](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) Hola API de REST.</span><span class="sxs-lookup"><span data-stu-id="11aa4-244">Each file contains hello description of a single operation in hello API which maps toohello `description` property of hello [operation entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) in hello REST API.</span></span>

### <a name="groups-folder"></a><span data-ttu-id="11aa4-245">carpeta de grupos</span><span class="sxs-lookup"><span data-stu-id="11aa4-245">groups folder</span></span>
<span data-ttu-id="11aa4-246">Hola `groups` carpeta contiene una carpeta para cada grupo definido en la instancia de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="11aa4-246">hello `groups` folder contains a folder for each group defined in hello service instance.</span></span>

* <span data-ttu-id="11aa4-247">`groups\<group name>\configuration.json`-es configuración de hello para el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="11aa4-247">`groups\<group name>\configuration.json` - this is hello configuration for hello group.</span></span> <span data-ttu-id="11aa4-248">Se trata de hello misma información que se devolverían si estuviera hello toocall [obtener un grupo específico](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) operación.</span><span class="sxs-lookup"><span data-stu-id="11aa4-248">This is hello same information that would be returned if you were toocall hello [Get a specific group](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) operation.</span></span>
* <span data-ttu-id="11aa4-249">`groups\<group name>\description.html`-Esto es Hola descripción del grupo de Hola y corresponde toohello `description` propiedad de hello [grupo entidad](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="11aa4-249">`groups\<group name>\description.html` - this is hello description of hello group and corresponds toohello `description` property of hello [group entity](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span></span>

### <a name="policies-folder"></a><span data-ttu-id="11aa4-250">carpeta de directivas</span><span class="sxs-lookup"><span data-stu-id="11aa4-250">policies folder</span></span>
<span data-ttu-id="11aa4-251">Hola `policies` carpeta contiene las instrucciones de directiva de hello para la instancia de servicio.</span><span class="sxs-lookup"><span data-stu-id="11aa4-251">hello `policies` folder contains hello policy statements for your service instance.</span></span>

* <span data-ttu-id="11aa4-252">`policies\global.xml` : contiene las directivas definidas en el ámbito global para la instancia de servicio.</span><span class="sxs-lookup"><span data-stu-id="11aa4-252">`policies\global.xml` - contains policies defined at global scope for your service instance.</span></span>
* <span data-ttu-id="11aa4-253">`policies\apis\<api name>\`: si tiene directivas definidas en el ámbito de la API, se encuentran en esta carpeta.</span><span class="sxs-lookup"><span data-stu-id="11aa4-253">`policies\apis\<api name>\` - if you have any policies defined at API scope, they are contained in this folder.</span></span>
* <span data-ttu-id="11aa4-254">`policies\apis\<api name>\<operation name>\`carpeta - si tiene las directivas definidas en el ámbito de la operación, se incluyen en esta carpeta en `<operation name>.xml` archivos que se asignan las instrucciones de directiva de toohello para cada operación.</span><span class="sxs-lookup"><span data-stu-id="11aa4-254">`policies\apis\<api name>\<operation name>\` folder - if you have any policies defined at operation scope, they are contained in this folder in `<operation name>.xml` files that map toohello policy statements for each operation.</span></span>
* <span data-ttu-id="11aa4-255">`policies\products\`-Si tiene las directivas definidas en el ámbito del producto, se incluyen en esta carpeta, que contiene `<product name>.xml` archivos que se asignan las instrucciones de directiva de toohello para cada producto.</span><span class="sxs-lookup"><span data-stu-id="11aa4-255">`policies\products\` - if you have any policies defined at product scope, they are contained in this folder, which contains `<product name>.xml` files that map toohello policy statements for each product.</span></span>

### <a name="portalstyles-folder"></a><span data-ttu-id="11aa4-256">carpeta portalStyles</span><span class="sxs-lookup"><span data-stu-id="11aa4-256">portalStyles folder</span></span>
<span data-ttu-id="11aa4-257">Hola `portalStyles` carpeta contiene la configuración y hojas de estilo para las personalizaciones de portal de desarrollador para la instancia de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="11aa4-257">hello `portalStyles` folder contains configuration and style sheets for developer portal customizations for hello service instance.</span></span>

* <span data-ttu-id="11aa4-258">`portalStyles\configuration.json`-contiene nombres de Hola Hola de hojas de estilos utilizados por el portal para desarrolladores de Hola</span><span class="sxs-lookup"><span data-stu-id="11aa4-258">`portalStyles\configuration.json` - contains hello names of hello style sheets used by hello developer portal</span></span>
* <span data-ttu-id="11aa4-259">`portalStyles\<style name>.css`-cada `<style name>.css` archivo contiene estilos para el portal para desarrolladores de hello (`Preview.css` y `Production.css` de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="11aa4-259">`portalStyles\<style name>.css` - each `<style name>.css` file contains styles for hello developer portal (`Preview.css` and `Production.css` by default).</span></span>

### <a name="products-folder"></a><span data-ttu-id="11aa4-260">carpeta de productos</span><span class="sxs-lookup"><span data-stu-id="11aa4-260">products folder</span></span>
<span data-ttu-id="11aa4-261">Hola `products` carpeta contiene una carpeta para cada producto definido en la instancia de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="11aa4-261">hello `products` folder contains a folder for each product defined in hello service instance.</span></span>

* <span data-ttu-id="11aa4-262">`products\<product name>\configuration.json`-se trata de configuración de hello para el producto de Hola.</span><span class="sxs-lookup"><span data-stu-id="11aa4-262">`products\<product name>\configuration.json` - this is hello configuration for hello product.</span></span> <span data-ttu-id="11aa4-263">Se trata de hello misma información que se devolverían si estuviera hello toocall [obtener un producto específico](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) operación.</span><span class="sxs-lookup"><span data-stu-id="11aa4-263">This is hello same information that would be returned if you were toocall hello [Get a specific product](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) operation.</span></span>
* <span data-ttu-id="11aa4-264">`products\<product name>\product.description.html`-Esto es una descripción de Hola de producto de Hola y corresponde toohello `description` propiedad de hello [entidad product](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) Hola API de REST.</span><span class="sxs-lookup"><span data-stu-id="11aa4-264">`products\<product name>\product.description.html` - this is hello description of hello product and corresponds toohello `description` property of hello [product entity](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) in hello REST API.</span></span>

### <a name="templates"></a><span data-ttu-id="11aa4-265">plantillas</span><span class="sxs-lookup"><span data-stu-id="11aa4-265">templates</span></span>
<span data-ttu-id="11aa4-266">Hola `templates` carpeta contiene la configuración de hello [plantillas de correo electrónico](api-management-howto-configure-notifications.md) de instancia de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="11aa4-266">hello `templates` folder contains configuration for hello [email templates](api-management-howto-configure-notifications.md) of hello service instance.</span></span>

* <span data-ttu-id="11aa4-267">`<template name>\configuration.json`-se trata de configuración de hello para la plantilla de correo electrónico de Hola.</span><span class="sxs-lookup"><span data-stu-id="11aa4-267">`<template name>\configuration.json` - this is hello configuration for hello email template.</span></span>
* <span data-ttu-id="11aa4-268">`<template name>\body.html`-Éste es Hola cuerpo de plantilla de correo electrónico de Hola.</span><span class="sxs-lookup"><span data-stu-id="11aa4-268">`<template name>\body.html` - this is hello body of hello email template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11aa4-269">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="11aa4-269">Next steps</span></span>
<span data-ttu-id="11aa4-270">Para obtener información sobre otra maneras de toomanage su instancia de servicio, vea:</span><span class="sxs-lookup"><span data-stu-id="11aa4-270">For information on other ways toomanage your service instance, see:</span></span>

* <span data-ttu-id="11aa4-271">Administrar la instancia de servicio con hello siguientes cmdlets de PowerShell</span><span class="sxs-lookup"><span data-stu-id="11aa4-271">Manage your service instance using hello following PowerShell cmdlets</span></span>
  * [<span data-ttu-id="11aa4-272">Azure API Management Deployment Management Cmdlets (Cmdlets de administración de la implementación de Administración de API de Azure)</span><span class="sxs-lookup"><span data-stu-id="11aa4-272">Service deployment PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [<span data-ttu-id="11aa4-273">Azure API Management Service Management Cmdlets (Cmdlets de administración del servicio Administración de API de Azure)</span><span class="sxs-lookup"><span data-stu-id="11aa4-273">Service management PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* <span data-ttu-id="11aa4-274">Administrar la instancia de servicio en el portal para desarrolladores de Hola</span><span class="sxs-lookup"><span data-stu-id="11aa4-274">Manage your service instance in hello publisher portal</span></span>
  * [<span data-ttu-id="11aa4-275">Administración de su primera API en Administración de API de Azure</span><span class="sxs-lookup"><span data-stu-id="11aa4-275">Manage your first API</span></span>](api-management-get-started.md)
* <span data-ttu-id="11aa4-276">Administrar la instancia de servicio mediante la API de REST de Hola</span><span class="sxs-lookup"><span data-stu-id="11aa4-276">Manage your service instance using hello REST API</span></span>
  * [<span data-ttu-id="11aa4-277">API Management REST API (API de REST de Administración de API)</span><span class="sxs-lookup"><span data-stu-id="11aa4-277">API Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn776326.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="11aa4-278">Vea un vídeo de introducción.</span><span class="sxs-lookup"><span data-stu-id="11aa4-278">Watch a video overview</span></span>
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




