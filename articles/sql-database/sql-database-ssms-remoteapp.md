---
title: "Conéctese a SQL Database con SQL Server Management Studio en Azure RemoteApp | Microsoft Docs"
description: Use este tutorial para aprender a utilizar SQL Server Management Studio en Azure RemoteApp y optimizar la seguridad y el rendimiento al conectarse a la Base de datos SQL
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
ms.openlocfilehash: ae1f2fa38d38fe6c10bc7960fddb07ae330d1eeb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-to-connect-to-sql-database"></a><span data-ttu-id="3d6e7-103">Utilización de SQL Server Management Studio en Azure RemoteApp para conectarse a una base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="3d6e7-103">Use SQL Server Management Studio in Azure RemoteApp to connect to SQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3d6e7-104">Azure RemoteApp va a dejar de estar disponible.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-104">Azure RemoteApp is being discontinued.</span></span> <span data-ttu-id="3d6e7-105">Para más información, lea el [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="3d6e7-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
>

## <a name="introduction"></a><span data-ttu-id="3d6e7-106">Introducción</span><span class="sxs-lookup"><span data-stu-id="3d6e7-106">Introduction</span></span>
<span data-ttu-id="3d6e7-107">Este tutorial le muestra cómo utilizar SQL Server Management Studio (SSMS) en Azure RemoteApp para conectarse a una base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-107">This tutorial shows you how to use SQL Server Management Studio (SSMS) in Azure RemoteApp to connect to SQL Database.</span></span> <span data-ttu-id="3d6e7-108">Le guiará a través del proceso de configuración de SQL Server Management Studio en Azure RemoteApp, le explicará sus ventajas y le mostrará las características de seguridad que puede utilizar en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-108">It walks you through the process of setting up SQL Server Management Studio in Azure RemoteApp, explains the benefits, and shows security features that you can use in Azure Active Directory.</span></span>

<span data-ttu-id="3d6e7-109">**Tiempo estimado para completar el tutorial:** 45 minutos.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-109">**Estimated time to complete:** 45 minutes</span></span>

## <a name="ssms-in-azure-remoteapp"></a><span data-ttu-id="3d6e7-110">SSMS en Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="3d6e7-110">SSMS in Azure RemoteApp</span></span>
<span data-ttu-id="3d6e7-111">Azure RemoteApp es un servicio RDS de Azure que ofrece aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-111">Azure RemoteApp is an RDS service in Azure that delivers applications.</span></span> <span data-ttu-id="3d6e7-112">Puede obtener más información sobre esta herramienta aquí: [¿Qué es RemoteApp?](../remoteapp/remoteapp-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="3d6e7-112">You can learn more about it here: [What is RemoteApp?](../remoteapp/remoteapp-whatis.md)</span></span>

<span data-ttu-id="3d6e7-113">Si ejecuta SSMS en Azure RemoteApp obtendrá la misma experiencia que si lo ejecuta localmente.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-113">SSMS running in Azure RemoteApp gives you the same experience as running SSMS locally.</span></span>

![Captura de pantalla que muestra a SSMS ejecutándose en Azure RemoteApp][1]

## <a name="benefits"></a><span data-ttu-id="3d6e7-115">Ventajas</span><span class="sxs-lookup"><span data-stu-id="3d6e7-115">Benefits</span></span>
<span data-ttu-id="3d6e7-116">Hay muchas ventajas por utilizar SSMS en Azure RemoteApp, entre las que se incluyen:</span><span class="sxs-lookup"><span data-stu-id="3d6e7-116">There are many benefits to using SSMS in Azure RemoteApp, including:</span></span>

* <span data-ttu-id="3d6e7-117">El puerto 1433 en el servidor Azure SQL no tiene que exponerse externamente (fuera de Azure).</span><span class="sxs-lookup"><span data-stu-id="3d6e7-117">Port 1433 on Azure SQL server does not have to be exposed externally (outside of Azure).</span></span>
* <span data-ttu-id="3d6e7-118">No es necesario agregar ni quitar direcciones IP en el firewall del servidor Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-118">No need to keep adding and removing IP addresses in the Azure SQL server firewall.</span></span>
* <span data-ttu-id="3d6e7-119">Todas las conexiones de Azure RemoteApp se realizan a través de HTTPS en el puerto 443 mediante un protocolo cifrado de escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="3d6e7-119">All Azure RemoteApp connections occur over HTTPS on port 443 using encrypted Remote Desktop protocol</span></span>
* <span data-ttu-id="3d6e7-120">Es multiusuario y se puede escalar.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-120">It is multi-user and can scale.</span></span>
* <span data-ttu-id="3d6e7-121">Hay una mejora del rendimiento si dispone de SSMS en la misma región que la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-121">There is a performance gain from having SSMS in the same region as the SQL Database.</span></span>
* <span data-ttu-id="3d6e7-122">Puede auditar la utilización de Azure RemoteApp con la versión Premium Edition de Azure Active Directory que tiene informes de actividad de usuario.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-122">You can audit use of Azure RemoteApp with the Premium edition of Azure Active Directory which has user activity reports.</span></span>
* <span data-ttu-id="3d6e7-123">Puede habilitar la autenticación multifactor (MFA).</span><span class="sxs-lookup"><span data-stu-id="3d6e7-123">You can enable multi-factor authentication (MFA).</span></span>
* <span data-ttu-id="3d6e7-124">Puede obtener acceso a SSMS en cualquier lugar al utilizar cualquiera de los clientes compatibles con Azure RemoteApp, entre los que se incluyen iOS, Android, Mac, Windows Phone y Windows PC.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-124">Access SSMS anywhere when using any of the supported Azure RemoteApp clients which includes iOS, Android, Mac, Windows Phone, and Windows PC’s.</span></span>

## <a name="create-the-azure-remoteapp-collection"></a><span data-ttu-id="3d6e7-125">Creación de una colección de Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-125">Create the Azure RemoteApp collection</span></span>
<span data-ttu-id="3d6e7-126">Estos son los pasos para crear la colección de Azure RemoteApp con SSMS:</span><span class="sxs-lookup"><span data-stu-id="3d6e7-126">Here are the steps to create your Azure RemoteApp collection with SSMS:</span></span>

### <a name="1-create-a-new-windows-vm-from-image"></a><span data-ttu-id="3d6e7-127">1. Cree una nueva máquina virtual de Windows desde una imagen</span><span class="sxs-lookup"><span data-stu-id="3d6e7-127">1. Create a new Windows VM from Image</span></span>
<span data-ttu-id="3d6e7-128">Utilice la imagen "Windows Server Remote Desktop Session Host Windows Server 2012 R2" de la galería para crear la nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-128">Use the "Windows Server Remote Desktop Session Host Windows Server 2012 R2" Image from the Gallery to make your new VM.</span></span>

### <a name="2-install-ssms-from-sql-express"></a><span data-ttu-id="3d6e7-129">2. Instale SSMS desde SQL Express</span><span class="sxs-lookup"><span data-stu-id="3d6e7-129">2. Install SSMS from SQL Express</span></span>
<span data-ttu-id="3d6e7-130">Vaya a la nueva máquina virtual y navegue hasta esta página de descarga: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span><span class="sxs-lookup"><span data-stu-id="3d6e7-130">Go onto the new VM and navigate to this download page: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span></span>

<span data-ttu-id="3d6e7-131">Hay una opción para descargar solo SSMS.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-131">There is an option to only download SSMS.</span></span> <span data-ttu-id="3d6e7-132">Después de la descarga, vaya al directorio de instalación y ejecute el programa de instalación para instalar SSMS.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-132">After download, go into the install directory and run Setup to install SSMS.</span></span>

<span data-ttu-id="3d6e7-133">También debe instalar el Service Pack 1 de SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-133">You also need to install SQL Server 2014 Service Pack 1.</span></span> <span data-ttu-id="3d6e7-134">Puede descargarlo aquí: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span><span class="sxs-lookup"><span data-stu-id="3d6e7-134">You can download it here: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span></span>

<span data-ttu-id="3d6e7-135">El Service Pack 1 de SQL Server 2014 incluye funciones esenciales para trabajar con la Base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-135">SQL Server 2014 Service Pack 1 includes essential functionality for working with Azure SQL Database.</span></span>

### <a name="3-run-validate-script-and-sysprep"></a><span data-ttu-id="3d6e7-136">3. Ejecute un script Validate y Sysprep</span><span class="sxs-lookup"><span data-stu-id="3d6e7-136">3. Run Validate script and Sysprep</span></span>
<span data-ttu-id="3d6e7-137">En el escritorio de la máquina virtual hay un script de PowerShell denominado Validate.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-137">On the desktop of the VM is a PowerShell script called Validate.</span></span> <span data-ttu-id="3d6e7-138">Ejecútelo haciendo doble clic.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-138">Run this by double-clicking.</span></span> <span data-ttu-id="3d6e7-139">Comprobará que la máquina virtual está lista para ser utilizada para el hospedaje remoto de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-139">It will verify that the VM is ready to be used for remote hosting of applications.</span></span> <span data-ttu-id="3d6e7-140">Cuando finalice la comprobación, se le pedirá que ejecute sysprep. Elija la opción para ejecutarlo.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-140">When verification is complete, it will ask to run sysprep - choose to run it.</span></span>

<span data-ttu-id="3d6e7-141">Cuando finalice sysprep, apagará la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-141">When sysprep completes, it will shut down the VM.</span></span>

<span data-ttu-id="3d6e7-142">Para obtener más información acerca de la creación de una imagen de Azure RemoteApp, consulte: [How to create a RemoteApp template image in Azure (Cómo crear una imagen de plantilla de RemoteApp en Azure)](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="3d6e7-142">To learn more about creating a Azure RemoteApp image, see: [How to create a RemoteApp template image in Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span></span>

### <a name="4-capture-image"></a><span data-ttu-id="3d6e7-143">4. Capture la imagen</span><span class="sxs-lookup"><span data-stu-id="3d6e7-143">4. Capture image</span></span>
<span data-ttu-id="3d6e7-144">Cuando la máquina virtual haya dejado de ejecutarse, busque la imagen en el portal actual y captúrela.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-144">When the VM has stopped running, find it in the current portal and capture it.</span></span>

<span data-ttu-id="3d6e7-145">Para más información sobre la captura de una imagen, consulte [Captura de una imagen de una máquina virtual Windows de Azure creada con el modelo de implementación clásico](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="3d6e7-145">To learn more about capturing an image, see [Capture an image of an Azure Windows virtual machine created with the classic deployment model](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

### <a name="5-add-to-azure-remoteapp-template-images"></a><span data-ttu-id="3d6e7-146">5. Agréguela a las imágenes de plantilla de Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="3d6e7-146">5. Add to Azure RemoteApp Template images</span></span>
<span data-ttu-id="3d6e7-147">En la sección de Azure RemoteApp del portal actual, vaya a la pestaña Imágenes de plantilla y haga clic en Agregar.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-147">In the Azure RemoteApp section of the current portal, go to the Template Images tab and click Add.</span></span> <span data-ttu-id="3d6e7-148">En el cuadro emergente, seleccione "Importar una imagen de la biblioteca de máquinas virtuales" y, a continuación, elija la imagen que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-148">In the pop-up box, select "Import an image from your Virtual Machines library" and then choose the Image that you just created.</span></span>

### <a name="6-create-cloud-collection"></a><span data-ttu-id="3d6e7-149">6. Cree una colección en la nube</span><span class="sxs-lookup"><span data-stu-id="3d6e7-149">6. Create cloud collection</span></span>
<span data-ttu-id="3d6e7-150">En el portal actual, cree una nueva colección en la nube de Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-150">In the current portal, create a new Azure RemoteApp Cloud Collection.</span></span> <span data-ttu-id="3d6e7-151">Elija la imagen de plantilla que acaba de importar con SSMS instalado.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-151">Choose the Template Image that you just imported with SSMS installed on it.</span></span>

![Creación de una nueva colección en la nube][2]

### <a name="7-publish-ssms"></a><span data-ttu-id="3d6e7-153">7. Publique SSMS</span><span class="sxs-lookup"><span data-stu-id="3d6e7-153">7. Publish SSMS</span></span>
<span data-ttu-id="3d6e7-154">En la pestaña Publicación de la nueva colección en la nube, seleccione Publicar una aplicación en el menú Inicio y, a continuación, elija SSMS en la lista.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-154">On the Publishing tab of your new cloud collection, select Publish an application from the Start Menu and then choose SSMS from the list.</span></span>

![Aplicación de publicación][5]

### <a name="8-add-users"></a><span data-ttu-id="3d6e7-156">8. Agregar usuarios</span><span class="sxs-lookup"><span data-stu-id="3d6e7-156">8. Add users</span></span>
<span data-ttu-id="3d6e7-157">En la pestaña Acceso de usuario puede seleccionar los usuarios que tendrán acceso a esta colección de Azure RemoteApp que solo incluye SSMS.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-157">On the User Access tab you can select the users that will have access to this Azure RemoteApp collection which only includes SSMS.</span></span>

![Agregar usuario][6]

### <a name="9-install-the-azure-remoteapp-client-application"></a><span data-ttu-id="3d6e7-159">9. Instale la aplicación de cliente de Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="3d6e7-159">9. Install the Azure RemoteApp client application</span></span>
<span data-ttu-id="3d6e7-160">Puede descargar e instalar un cliente de Azure RemoteApp aquí: [Descargar | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span><span class="sxs-lookup"><span data-stu-id="3d6e7-160">You can download and install a Azure RemoteApp client here: [Download | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span></span>

## <a name="configure-azure-sql-server"></a><span data-ttu-id="3d6e7-161">Configuración de un servidor Azure SQL</span><span class="sxs-lookup"><span data-stu-id="3d6e7-161">Configure Azure SQL server</span></span>
<span data-ttu-id="3d6e7-162">La única configuración necesaria es asegurarse de que los servicios de Azure estén habilitados para el firewall.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-162">The only configuration needed is to ensure that Azure Services is enabled for the firewall.</span></span> <span data-ttu-id="3d6e7-163">Si utiliza esta solución, no es necesario agregar ninguna dirección IP para abrir el firewall.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-163">If you use this solution, then you do not need to add any IP addresses to open the firewall.</span></span> <span data-ttu-id="3d6e7-164">El tráfico de red que se permite hacia SQL Server es de otros servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-164">The network traffic that is allowed to the SQL Server is from other Azure services.</span></span>

![Permiso de Azure][4]

## <a name="multi-factor-authentication-mfa"></a><span data-ttu-id="3d6e7-166">Multi-Factor Authentication (MFA)</span><span class="sxs-lookup"><span data-stu-id="3d6e7-166">Multi-Factor Authentication (MFA)</span></span>
<span data-ttu-id="3d6e7-167">MFA se puede habilitar específicamente para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-167">MFA can be enabled for this application specifically.</span></span> <span data-ttu-id="3d6e7-168">Vaya a la pestaña Aplicaciones de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-168">Go to the Applications tab of your Azure Active Directory.</span></span> <span data-ttu-id="3d6e7-169">Encontrará una entrada para Microsoft Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-169">You will find an entry for Microsoft Azure RemoteApp.</span></span> <span data-ttu-id="3d6e7-170">Si hace clic en esa aplicación y, a continuación, configura, verá la página siguiente, donde podrá habilitar MFA para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-170">If you click that application and then configure, you will see the page below where you can enable MFA for this application.</span></span>

![Habilitar MFA][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a><span data-ttu-id="3d6e7-172">Auditoría de actividad de usuario con Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="3d6e7-172">Audit user activity with Azure Active Directory Premium</span></span>
<span data-ttu-id="3d6e7-173">Si no tiene Azure AD Premium, tendrá que activarlo en la sección de licencias de su directorio.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-173">If you do not have Azure AD Premium, then you have to turn it on in the Licenses section of your directory.</span></span> <span data-ttu-id="3d6e7-174">Con Premium habilitado, puede asignar usuarios al nivel Premium.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-174">With Premium enabled, you can assign users to the Premium level.</span></span>

<span data-ttu-id="3d6e7-175">Cuando vaya a un usuario de Azure Active Directory, a continuación, puede ir a la pestaña de actividad para ver la información de inicio de sesión en Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-175">When you go to a user in your Azure Active Directory, you can then go to the Activity tab to see login information to Azure RemoteApp.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d6e7-176">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3d6e7-176">Next steps</span></span>
<span data-ttu-id="3d6e7-177">Después de completar todos los pasos anteriores, podrá ejecutar el cliente de Azure RemoteApp y el inicio de sesión con un usuario asignado.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-177">After completing all the above steps, you will be able to run the Azure RemoteApp client and log-in with an assigned user.</span></span> <span data-ttu-id="3d6e7-178">Se le presentará SSMS como una de sus aplicaciones y podrá ejecutarla como lo haría si la hubiera instalado en el equipo con acceso al servidor Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-178">You will be presented with SSMS as one of your applications, and you can run it as you would if it were installed on your computer with access to Azure SQL server.</span></span>

<span data-ttu-id="3d6e7-179">Para más información sobre cómo realizar la conexión a la base de datos SQL, consulte [Conexión a la Base de datos SQL con SQL Server Management Studio y realización de una consulta de T-SQL de ejemplo](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="3d6e7-179">For more information on how to make the connection to SQL Database, see [Connect to SQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>

<span data-ttu-id="3d6e7-180">Eso es todo por ahora.</span><span class="sxs-lookup"><span data-stu-id="3d6e7-180">That's everything for now.</span></span> <span data-ttu-id="3d6e7-181">¡Disfrute!</span><span class="sxs-lookup"><span data-stu-id="3d6e7-181">Enjoy!</span></span>

<!--Image references-->
[1]: ./media/sql-database-ssms-remoteapp/ssms.png
[2]: ./media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: ./media/sql-database-ssms-remoteapp/mfa.png
[4]: ./media/sql-database-ssms-remoteapp/allowazure.png
[5]: ./media/sql-database-ssms-remoteapp/publish.png
[6]: ./media/sql-database-ssms-remoteapp/user.png