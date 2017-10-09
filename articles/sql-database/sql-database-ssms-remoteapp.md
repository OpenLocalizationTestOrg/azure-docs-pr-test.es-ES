---
title: aaaConnect tooSQL base de datos mediante SQL Server Management Studio en Azure RemoteApp | Documentos de Microsoft
description: "Use este tutorial toolearn cómo toouse SQL Server Management Studio en Azure RemoteApp para la seguridad y rendimiento al conectarse tooSQL base de datos"
services: sql-database
documentationcenter: 
author: adhurwit
manager: jhubbard
ms.assetid: 1052c83c-e7f5-4736-922f-216194d8874b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: adhurwit
ms.openlocfilehash: 73994f9a1eb3e48efa5d7c4f976b00cfcbc88d75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-tooconnect-toosql-database"></a><span data-ttu-id="bf090-103">Usar SQL Server Management Studio en Azure RemoteApp tooconnect tooSQL base de datos</span><span class="sxs-lookup"><span data-stu-id="bf090-103">Use SQL Server Management Studio in Azure RemoteApp tooconnect tooSQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bf090-104">Azure RemoteApp va a dejar de estar disponible.</span><span class="sxs-lookup"><span data-stu-id="bf090-104">Azure RemoteApp is being discontinued.</span></span> <span data-ttu-id="bf090-105">Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="bf090-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
>

## <a name="introduction"></a><span data-ttu-id="bf090-106">Introducción</span><span class="sxs-lookup"><span data-stu-id="bf090-106">Introduction</span></span>
<span data-ttu-id="bf090-107">Este tutorial muestra cómo toouse SQL Server Management Studio (SSMS) en Azure RemoteApp tooconnect tooSQL base de datos.</span><span class="sxs-lookup"><span data-stu-id="bf090-107">This tutorial shows you how toouse SQL Server Management Studio (SSMS) in Azure RemoteApp tooconnect tooSQL Database.</span></span> <span data-ttu-id="bf090-108">Le guía a través del proceso de Hola de configuración de SQL Server Management Studio en Azure RemoteApp, explica las ventajas de Hola y muestra las características de seguridad que puede usar en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bf090-108">It walks you through hello process of setting up SQL Server Management Studio in Azure RemoteApp, explains hello benefits, and shows security features that you can use in Azure Active Directory.</span></span>

<span data-ttu-id="bf090-109">**Estimado toocomplete de tiempo:** 45 minutos</span><span class="sxs-lookup"><span data-stu-id="bf090-109">**Estimated time toocomplete:** 45 minutes</span></span>

## <a name="ssms-in-azure-remoteapp"></a><span data-ttu-id="bf090-110">SSMS en Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="bf090-110">SSMS in Azure RemoteApp</span></span>
<span data-ttu-id="bf090-111">Azure RemoteApp es un servicio RDS de Azure que ofrece aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="bf090-111">Azure RemoteApp is an RDS service in Azure that delivers applications.</span></span> <span data-ttu-id="bf090-112">Puede obtener más información sobre esta herramienta aquí: [¿Qué es RemoteApp?](../remoteapp/remoteapp-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="bf090-112">You can learn more about it here: [What is RemoteApp?](../remoteapp/remoteapp-whatis.md)</span></span>

<span data-ttu-id="bf090-113">SSMS que se ejecuta en Azure RemoteApp proporciona Hola misma experiencia que ejecute SSMS localmente.</span><span class="sxs-lookup"><span data-stu-id="bf090-113">SSMS running in Azure RemoteApp gives you hello same experience as running SSMS locally.</span></span>

![Captura de pantalla que muestra a SSMS ejecutándose en Azure RemoteApp][1]

## <a name="benefits"></a><span data-ttu-id="bf090-115">Ventajas</span><span class="sxs-lookup"><span data-stu-id="bf090-115">Benefits</span></span>
<span data-ttu-id="bf090-116">Hay muchas ventajas toousing SSMS en Azure RemoteApp, incluido:</span><span class="sxs-lookup"><span data-stu-id="bf090-116">There are many benefits toousing SSMS in Azure RemoteApp, including:</span></span>

* <span data-ttu-id="bf090-117">El puerto 1433 en el servidor de SQL Azure no tiene toobe expone externamente (fuera de Azure).</span><span class="sxs-lookup"><span data-stu-id="bf090-117">Port 1433 on Azure SQL server does not have toobe exposed externally (outside of Azure).</span></span>
* <span data-ttu-id="bf090-118">No hay tookeep necesidad de agregar y quitar direcciones IP en firewall de servidor de SQL Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="bf090-118">No need tookeep adding and removing IP addresses in hello Azure SQL server firewall.</span></span>
* <span data-ttu-id="bf090-119">Todas las conexiones de Azure RemoteApp se realizan a través de HTTPS en el puerto 443 mediante un protocolo cifrado de escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="bf090-119">All Azure RemoteApp connections occur over HTTPS on port 443 using encrypted Remote Desktop protocol</span></span>
* <span data-ttu-id="bf090-120">Es multiusuario y se puede escalar.</span><span class="sxs-lookup"><span data-stu-id="bf090-120">It is multi-user and can scale.</span></span>
* <span data-ttu-id="bf090-121">Hay un aumento del rendimiento de con SSMS en hello misma región que Hola base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="bf090-121">There is a performance gain from having SSMS in hello same region as hello SQL Database.</span></span>
* <span data-ttu-id="bf090-122">Puede auditar el uso de RemoteApp de Azure con la edición Premium Hola de Azure Active Directory que tiene informes de actividad de usuario.</span><span class="sxs-lookup"><span data-stu-id="bf090-122">You can audit use of Azure RemoteApp with hello Premium edition of Azure Active Directory which has user activity reports.</span></span>
* <span data-ttu-id="bf090-123">Puede habilitar la autenticación multifactor (MFA).</span><span class="sxs-lookup"><span data-stu-id="bf090-123">You can enable multi-factor authentication (MFA).</span></span>
* <span data-ttu-id="bf090-124">SSMS en cualquier lugar al usar cualquiera de hello admite el acceso los clientes de Azure RemoteApp que incluye iOS, Android, Mac, Windows Phone y equipos que ejecutan Windows.</span><span class="sxs-lookup"><span data-stu-id="bf090-124">Access SSMS anywhere when using any of hello supported Azure RemoteApp clients which includes iOS, Android, Mac, Windows Phone, and Windows PC’s.</span></span>

## <a name="create-hello-azure-remoteapp-collection"></a><span data-ttu-id="bf090-125">Crear la colección de RemoteApp de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="bf090-125">Create hello Azure RemoteApp collection</span></span>
<span data-ttu-id="bf090-126">Estos es Hola pasos toocreate la colección de RemoteApp de Azure con SSMS:</span><span class="sxs-lookup"><span data-stu-id="bf090-126">Here are hello steps toocreate your Azure RemoteApp collection with SSMS:</span></span>

### <a name="1-create-a-new-windows-vm-from-image"></a><span data-ttu-id="bf090-127">1. Cree una nueva máquina virtual de Windows desde una imagen</span><span class="sxs-lookup"><span data-stu-id="bf090-127">1. Create a new Windows VM from Image</span></span>
<span data-ttu-id="bf090-128">Usar hello "Windows Server remoto escritorio sesión Host Windows Server 2012 R2" imagen de hello Galería toomake la nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bf090-128">Use hello "Windows Server Remote Desktop Session Host Windows Server 2012 R2" Image from hello Gallery toomake your new VM.</span></span>

### <a name="2-install-ssms-from-sql-express"></a><span data-ttu-id="bf090-129">2. Instale SSMS desde SQL Express</span><span class="sxs-lookup"><span data-stu-id="bf090-129">2. Install SSMS from SQL Express</span></span>
<span data-ttu-id="bf090-130">Vaya a Hola nueva máquina virtual y navegar por la página de descarga de toothis: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span><span class="sxs-lookup"><span data-stu-id="bf090-130">Go onto hello new VM and navigate toothis download page: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span></span>

<span data-ttu-id="bf090-131">Hay una descarga de tooonly opción SSMS.</span><span class="sxs-lookup"><span data-stu-id="bf090-131">There is an option tooonly download SSMS.</span></span> <span data-ttu-id="bf090-132">Después de la descarga, vaya al directorio de instalación de Hola y ejecute el programa de instalación tooinstall SSMS.</span><span class="sxs-lookup"><span data-stu-id="bf090-132">After download, go into hello install directory and run Setup tooinstall SSMS.</span></span>

<span data-ttu-id="bf090-133">También debe tooinstall SQL Server 2014 Service Pack 1.</span><span class="sxs-lookup"><span data-stu-id="bf090-133">You also need tooinstall SQL Server 2014 Service Pack 1.</span></span> <span data-ttu-id="bf090-134">Puede descargarlo aquí: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span><span class="sxs-lookup"><span data-stu-id="bf090-134">You can download it here: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span></span>

<span data-ttu-id="bf090-135">El Service Pack 1 de SQL Server 2014 incluye funciones esenciales para trabajar con la Base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="bf090-135">SQL Server 2014 Service Pack 1 includes essential functionality for working with Azure SQL Database.</span></span>

### <a name="3-run-validate-script-and-sysprep"></a><span data-ttu-id="bf090-136">3. Ejecute un script Validate y Sysprep</span><span class="sxs-lookup"><span data-stu-id="bf090-136">3. Run Validate script and Sysprep</span></span>
<span data-ttu-id="bf090-137">En hello escritorio de hello VM es un script de PowerShell denominado validar.</span><span class="sxs-lookup"><span data-stu-id="bf090-137">On hello desktop of hello VM is a PowerShell script called Validate.</span></span> <span data-ttu-id="bf090-138">Ejecútelo haciendo doble clic.</span><span class="sxs-lookup"><span data-stu-id="bf090-138">Run this by double-clicking.</span></span> <span data-ttu-id="bf090-139">Comprobará que hello VM es listo toobe que se usa para hospedar remota de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="bf090-139">It will verify that hello VM is ready toobe used for remote hosting of applications.</span></span> <span data-ttu-id="bf090-140">Una vez completada la comprobación, le preguntará toorun sysprep - elija toorun lo.</span><span class="sxs-lookup"><span data-stu-id="bf090-140">When verification is complete, it will ask toorun sysprep - choose toorun it.</span></span>

<span data-ttu-id="bf090-141">Cuando sysprep finalice, se apagará Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bf090-141">When sysprep completes, it will shut down hello VM.</span></span>

<span data-ttu-id="bf090-142">toolearn más información acerca de cómo crear una imagen de Azure RemoteApp, consulte: [cómo toocreate una plantilla de RemoteApp de la imagen en Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="bf090-142">toolearn more about creating a Azure RemoteApp image, see: [How toocreate a RemoteApp template image in Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span></span>

### <a name="4-capture-image"></a><span data-ttu-id="bf090-143">4. Capture la imagen</span><span class="sxs-lookup"><span data-stu-id="bf090-143">4. Capture image</span></span>
<span data-ttu-id="bf090-144">Cuando Hola VM ha dejado de ejecutarse, disponible en el portal actual de Hola y capturarlo.</span><span class="sxs-lookup"><span data-stu-id="bf090-144">When hello VM has stopped running, find it in hello current portal and capture it.</span></span>

<span data-ttu-id="bf090-145">toolearn más acerca de cómo capturar una imagen, vea [capturar una imagen de una máquina virtual de Windows Azure creada con el modelo de implementación clásica de Hola](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="bf090-145">toolearn more about capturing an image, see [Capture an image of an Azure Windows virtual machine created with hello classic deployment model](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

### <a name="5-add-tooazure-remoteapp-template-images"></a><span data-ttu-id="bf090-146">5. Agregar imágenes de plantilla de RemoteApp tooAzure</span><span class="sxs-lookup"><span data-stu-id="bf090-146">5. Add tooAzure RemoteApp Template images</span></span>
<span data-ttu-id="bf090-147">Hola Azure RemoteApp sección del portal actual de hello, vaya la ficha de imágenes de plantilla toohello y haga clic en Agregar.</span><span class="sxs-lookup"><span data-stu-id="bf090-147">In hello Azure RemoteApp section of hello current portal, go toohello Template Images tab and click Add.</span></span> <span data-ttu-id="bf090-148">En el cuadro emergente de hello, seleccione "Importar una imagen de la biblioteca de máquinas virtuales" y, a continuación, elija Hola imagen que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="bf090-148">In hello pop-up box, select "Import an image from your Virtual Machines library" and then choose hello Image that you just created.</span></span>

### <a name="6-create-cloud-collection"></a><span data-ttu-id="bf090-149">6. Cree una colección en la nube</span><span class="sxs-lookup"><span data-stu-id="bf090-149">6. Create cloud collection</span></span>
<span data-ttu-id="bf090-150">En el portal actual de hello, cree una nueva colección de nube de RemoteApp de Azure.</span><span class="sxs-lookup"><span data-stu-id="bf090-150">In hello current portal, create a new Azure RemoteApp Cloud Collection.</span></span> <span data-ttu-id="bf090-151">Elija Hola imagen de plantilla que acaba de importar con SSMS instalado en él.</span><span class="sxs-lookup"><span data-stu-id="bf090-151">Choose hello Template Image that you just imported with SSMS installed on it.</span></span>

![Creación de una nueva colección en la nube][2]

### <a name="7-publish-ssms"></a><span data-ttu-id="bf090-153">7. Publique SSMS</span><span class="sxs-lookup"><span data-stu-id="bf090-153">7. Publish SSMS</span></span>
<span data-ttu-id="bf090-154">En hello publicar pestaña de la nueva colección de nube, seleccione Publicar una aplicación de Hola menú Inicio y luego elija SSMS de lista Hola.</span><span class="sxs-lookup"><span data-stu-id="bf090-154">On hello Publishing tab of your new cloud collection, select Publish an application from hello Start Menu and then choose SSMS from hello list.</span></span>

![Aplicación de publicación][5]

### <a name="8-add-users"></a><span data-ttu-id="bf090-156">8. Agregar usuarios</span><span class="sxs-lookup"><span data-stu-id="bf090-156">8. Add users</span></span>
<span data-ttu-id="bf090-157">En la ficha acceso de usuario de hello puede seleccionar usuarios Hola que tendrán acceso toothis Azure RemoteApp colección que solo incluye SSMS.</span><span class="sxs-lookup"><span data-stu-id="bf090-157">On hello User Access tab you can select hello users that will have access toothis Azure RemoteApp collection which only includes SSMS.</span></span>

![Agregar usuario][6]

### <a name="9-install-hello-azure-remoteapp-client-application"></a><span data-ttu-id="bf090-159">9. Instalar la aplicación de cliente de hello Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="bf090-159">9. Install hello Azure RemoteApp client application</span></span>
<span data-ttu-id="bf090-160">Puede descargar e instalar un cliente de Azure RemoteApp aquí: [Descargar | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span><span class="sxs-lookup"><span data-stu-id="bf090-160">You can download and install a Azure RemoteApp client here: [Download | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span></span>

## <a name="configure-azure-sql-server"></a><span data-ttu-id="bf090-161">Configuración de un servidor Azure SQL</span><span class="sxs-lookup"><span data-stu-id="bf090-161">Configure Azure SQL server</span></span>
<span data-ttu-id="bf090-162">Hola solo configuración necesaria es tooensure que da servicio a Azure está habilitado firewall de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf090-162">hello only configuration needed is tooensure that Azure Services is enabled for hello firewall.</span></span> <span data-ttu-id="bf090-163">Si utiliza esta solución, no deberá tooadd cualquier firewall de Hola de tooopen de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="bf090-163">If you use this solution, then you do not need tooadd any IP addresses tooopen hello firewall.</span></span> <span data-ttu-id="bf090-164">tráfico de red de Hola que se permite toohello SQL Server es de otros servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="bf090-164">hello network traffic that is allowed toohello SQL Server is from other Azure services.</span></span>

![Permiso de Azure][4]

## <a name="multi-factor-authentication-mfa"></a><span data-ttu-id="bf090-166">Multi-Factor Authentication (MFA)</span><span class="sxs-lookup"><span data-stu-id="bf090-166">Multi-Factor Authentication (MFA)</span></span>
<span data-ttu-id="bf090-167">MFA se puede habilitar específicamente para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="bf090-167">MFA can be enabled for this application specifically.</span></span> <span data-ttu-id="bf090-168">Vaya a toohello de pestaña de las aplicaciones de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bf090-168">Go toohello Applications tab of your Azure Active Directory.</span></span> <span data-ttu-id="bf090-169">Encontrará una entrada para Microsoft Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="bf090-169">You will find an entry for Microsoft Azure RemoteApp.</span></span> <span data-ttu-id="bf090-170">Si hace clic en esa aplicación y, a continuación, configura, verá Hola página donde puede habilitar MFA para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="bf090-170">If you click that application and then configure, you will see hello page below where you can enable MFA for this application.</span></span>

![Habilitar MFA][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a><span data-ttu-id="bf090-172">Auditoría de actividad de usuario con Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="bf090-172">Audit user activity with Azure Active Directory Premium</span></span>
<span data-ttu-id="bf090-173">Si no tiene Azure AD Premium, tendrá que tooturn encenderlo en Hola sección de licencias de su directorio.</span><span class="sxs-lookup"><span data-stu-id="bf090-173">If you do not have Azure AD Premium, then you have tooturn it on in hello Licenses section of your directory.</span></span> <span data-ttu-id="bf090-174">Con Premium habilitado, puede asignar a usuarios a nivel de toohello Premium.</span><span class="sxs-lookup"><span data-stu-id="bf090-174">With Premium enabled, you can assign users toohello Premium level.</span></span>

<span data-ttu-id="bf090-175">Cuando algún usuario tooa en Azure Active Directory, a continuación, puede ir toohello actividad pestaña toosee inicio de sesión información tooAzure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="bf090-175">When you go tooa user in your Azure Active Directory, you can then go toohello Activity tab toosee login information tooAzure RemoteApp.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf090-176">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bf090-176">Next steps</span></span>
<span data-ttu-id="bf090-177">Después de completar todos los Hola por encima de los pasos, se pueda toorun hello Azure RemoteApp cliente y el registro de con un usuario asignado.</span><span class="sxs-lookup"><span data-stu-id="bf090-177">After completing all hello above steps, you will be able toorun hello Azure RemoteApp client and log-in with an assigned user.</span></span> <span data-ttu-id="bf090-178">Se le mostrará con SSMS como uno de sus aplicaciones y ejecutarla como lo haría si se instalaron en el equipo con acceso a tooAzure SQL server.</span><span class="sxs-lookup"><span data-stu-id="bf090-178">You will be presented with SSMS as one of your applications, and you can run it as you would if it were installed on your computer with access tooAzure SQL server.</span></span>

<span data-ttu-id="bf090-179">Para obtener más información sobre cómo toomake Hola conexión tooSQL base de datos, vea [conectarse tooSQL base de datos con SQL Server Management Studio y realizar una consulta de T-SQL de ejemplo](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="bf090-179">For more information on how toomake hello connection tooSQL Database, see [Connect tooSQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>

<span data-ttu-id="bf090-180">Eso es todo por ahora.</span><span class="sxs-lookup"><span data-stu-id="bf090-180">That's everything for now.</span></span> <span data-ttu-id="bf090-181">¡Disfrute!</span><span class="sxs-lookup"><span data-stu-id="bf090-181">Enjoy!</span></span>

<!--Image references-->
[1]: ./media/sql-database-ssms-remoteapp/ssms.png
[2]: ./media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: ./media/sql-database-ssms-remoteapp/mfa.png
[4]: ./media/sql-database-ssms-remoteapp/allowazure.png
[5]: ./media/sql-database-ssms-remoteapp/publish.png
[6]: ./media/sql-database-ssms-remoteapp/user.png