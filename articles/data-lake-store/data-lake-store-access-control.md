---
title: "aaaOverview de control de acceso en el almacén de Data Lake | Documentos de Microsoft"
description: "Descripción de cómo funciona el control de acceso en Azure Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d16f8c09-c954-40d3-afab-c86ffa8c353d
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 1cc5d578f22ef0a123a1547abebfb4795ea09139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="access-control-in-azure-data-lake-store"></a><span data-ttu-id="69f45-103">Control de acceso en Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="69f45-103">Access control in Azure Data Lake Store</span></span>

<span data-ttu-id="69f45-104">Almacén de Azure Data Lake implementa un modelo de control de acceso que se deriva de HDFS, que a su vez deriva de modelo de control de acceso de hello POSIX.</span><span class="sxs-lookup"><span data-stu-id="69f45-104">Azure Data Lake Store implements an access control model that derives from HDFS, which in turn derives from hello POSIX access control model.</span></span> <span data-ttu-id="69f45-105">En este artículo se resume los conceptos básicos de hello del modelo de control de acceso de hello para el almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="69f45-105">This article summarizes hello basics of hello access control model for Data Lake Store.</span></span> <span data-ttu-id="69f45-106">vea toolearn más información sobre el modelo de control de acceso HDFS de hello [HDFS permisos guía](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).</span><span class="sxs-lookup"><span data-stu-id="69f45-106">toolearn more about hello HDFS access control model, see [HDFS Permissions Guide](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).</span></span>

## <a name="access-control-lists-on-files-and-folders"></a><span data-ttu-id="69f45-107">Listas de control de acceso en archivos y carpetas</span><span class="sxs-lookup"><span data-stu-id="69f45-107">Access control lists on files and folders</span></span>

<span data-ttu-id="69f45-108">Hay dos tipos de listas de control de acceso (ACL): **ACL de acceso** y **ACL predeterminadas**.</span><span class="sxs-lookup"><span data-stu-id="69f45-108">There are two kinds of access control lists (ACLs), **Access ACLs** and **Default ACLs**.</span></span>

* <span data-ttu-id="69f45-109">**Obtener acceso a ACL**: estos objetos de tooan de acceso de control.</span><span class="sxs-lookup"><span data-stu-id="69f45-109">**Access ACLs**: These control access tooan object.</span></span> <span data-ttu-id="69f45-110">Tanto los archivos como las carpetas tienen ACL de acceso.</span><span class="sxs-lookup"><span data-stu-id="69f45-110">Files and folders both have Access ACLs.</span></span>

* <span data-ttu-id="69f45-111">**ACL predeterminadas**: "Plantilla" de ACL asociada a una carpeta que determinan Hola acceso ACL para los elementos secundarios que se crean en esa carpeta.</span><span class="sxs-lookup"><span data-stu-id="69f45-111">**Default ACLs**: A "template" of ACLs associated with a folder that determine hello Access ACLs for any child items that are created under that folder.</span></span> <span data-ttu-id="69f45-112">Los archivos no tienen ACL predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="69f45-112">Files do not have Default ACLs.</span></span>

![ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-1.png)

<span data-ttu-id="69f45-114">ACL de acceso y ACL predeterminada tienen Hola misma estructura.</span><span class="sxs-lookup"><span data-stu-id="69f45-114">Both Access ACLs and Default ACLs have hello same structure.</span></span>

![ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-2.png)



> [!NOTE]
> <span data-ttu-id="69f45-116">Hola cambiante ACL predeterminada de un elemento primario no afecta a Hola acceso ACL o ACL predeterminada de los elementos secundarios que ya existen.</span><span class="sxs-lookup"><span data-stu-id="69f45-116">Changing hello Default ACL on a parent does not affect hello Access ACL or Default ACL of child items that already exist.</span></span>
>
>

## <a name="users-and-identities"></a><span data-ttu-id="69f45-117">Usuarios e identidades</span><span class="sxs-lookup"><span data-stu-id="69f45-117">Users and identities</span></span>

<span data-ttu-id="69f45-118">Todos los archivos y carpetas tienen permisos distintos para estas identidades:</span><span class="sxs-lookup"><span data-stu-id="69f45-118">Every file and folder has distinct permissions for these identities:</span></span>

* <span data-ttu-id="69f45-119">Hola propietaria de usuario del archivo hello</span><span class="sxs-lookup"><span data-stu-id="69f45-119">hello owning user of hello file</span></span>
* <span data-ttu-id="69f45-120">grupo de propietario de Hola</span><span class="sxs-lookup"><span data-stu-id="69f45-120">hello owning group</span></span>
* <span data-ttu-id="69f45-121">Usuarios designados</span><span class="sxs-lookup"><span data-stu-id="69f45-121">Named users</span></span>
* <span data-ttu-id="69f45-122">Grupos designados</span><span class="sxs-lookup"><span data-stu-id="69f45-122">Named groups</span></span>
* <span data-ttu-id="69f45-123">Los restantes usuarios</span><span class="sxs-lookup"><span data-stu-id="69f45-123">All other users</span></span>

<span data-ttu-id="69f45-124">identidades de Hola de usuarios y grupos son las identidades de Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="69f45-124">hello identities of users and groups are Azure Active Directory (Azure AD) identities.</span></span> <span data-ttu-id="69f45-125">Por lo que, a menos que se indique lo contrario, un "usuario", en el contexto de hello Lake del almacén de datos, puede ya sea significar que un usuario de Azure AD o un grupo de seguridad de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="69f45-125">So unless otherwise noted, a "user," in hello context of Data Lake Store, can either mean an Azure AD user or an Azure AD security group.</span></span>

## <a name="permissions"></a><span data-ttu-id="69f45-126">Permisos</span><span class="sxs-lookup"><span data-stu-id="69f45-126">Permissions</span></span>

<span data-ttu-id="69f45-127">Hola permisos en un objeto de sistema de archivos son **lectura**, **escribir**, y **Execute**, y puede utilizarse en archivos y carpetas como se muestra en hello en la tabla siguiente:</span><span class="sxs-lookup"><span data-stu-id="69f45-127">hello permissions on a filesystem object are **Read**, **Write**, and **Execute**, and they can be used on files and folders as shown in hello following table:</span></span>

|            |    <span data-ttu-id="69f45-128">Archivo</span><span class="sxs-lookup"><span data-stu-id="69f45-128">File</span></span>     |   <span data-ttu-id="69f45-129">Carpeta</span><span class="sxs-lookup"><span data-stu-id="69f45-129">Folder</span></span> |
|------------|-------------|----------|
| <span data-ttu-id="69f45-130">**Lectura (R)**</span><span class="sxs-lookup"><span data-stu-id="69f45-130">**Read (R)**</span></span> | <span data-ttu-id="69f45-131">Puede leer el contenido de Hola de un archivo</span><span class="sxs-lookup"><span data-stu-id="69f45-131">Can read hello contents of a file</span></span> | <span data-ttu-id="69f45-132">Requiere **lectura** y **Execute** contenido de hello toolist de carpeta Hola</span><span class="sxs-lookup"><span data-stu-id="69f45-132">Requires **Read** and **Execute** toolist hello contents of hello folder</span></span>|
| <span data-ttu-id="69f45-133">**Escritura (W)**</span><span class="sxs-lookup"><span data-stu-id="69f45-133">**Write (W)**</span></span> | <span data-ttu-id="69f45-134">Puede escribir o anexar archivo tooa</span><span class="sxs-lookup"><span data-stu-id="69f45-134">Can write or append tooa file</span></span> | <span data-ttu-id="69f45-135">Requiere **escribir** y **Execute** toocreate los elementos secundarios en una carpeta</span><span class="sxs-lookup"><span data-stu-id="69f45-135">Requires **Write** and **Execute** toocreate child items in a folder</span></span> |
| <span data-ttu-id="69f45-136">**Ejecución (X)**</span><span class="sxs-lookup"><span data-stu-id="69f45-136">**Execute (X)**</span></span> | <span data-ttu-id="69f45-137">No significa nada en el contexto de Hola de almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="69f45-137">Does not mean anything in hello context of Data Lake Store</span></span> | <span data-ttu-id="69f45-138">Elementos secundarios de tootraverse necesario Hola de una carpeta</span><span class="sxs-lookup"><span data-stu-id="69f45-138">Required tootraverse hello child items of a folder</span></span> |

### <a name="short-forms-for-permissions"></a><span data-ttu-id="69f45-139">Formas abreviadas de los permisos</span><span class="sxs-lookup"><span data-stu-id="69f45-139">Short forms for permissions</span></span>

<span data-ttu-id="69f45-140">**RWX** es usado tooindicate **lectura + escribir y ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="69f45-140">**RWX** is used tooindicate **Read + Write + Execute**.</span></span> <span data-ttu-id="69f45-141">Existe un formato numérico más reducido en el que **lectura = 4**, **escribir = 2**, y **Execute = 1**, suma Hola de los cuales representa los permisos de Hola.</span><span class="sxs-lookup"><span data-stu-id="69f45-141">A more condensed numeric form exists in which **Read=4**, **Write=2**, and **Execute=1**, hello sum of which represents hello permissions.</span></span> <span data-ttu-id="69f45-142">A continuación se muestran algunos ejemplos.</span><span class="sxs-lookup"><span data-stu-id="69f45-142">Following are some examples.</span></span>

| <span data-ttu-id="69f45-143">Formato numérico</span><span class="sxs-lookup"><span data-stu-id="69f45-143">Numeric form</span></span> | <span data-ttu-id="69f45-144">Formato abreviado</span><span class="sxs-lookup"><span data-stu-id="69f45-144">Short form</span></span> |      <span data-ttu-id="69f45-145">Qué significa</span><span class="sxs-lookup"><span data-stu-id="69f45-145">What it means</span></span>     |
|--------------|------------|------------------------|
| <span data-ttu-id="69f45-146">7</span><span class="sxs-lookup"><span data-stu-id="69f45-146">7</span></span>            | <span data-ttu-id="69f45-147">RWX</span><span class="sxs-lookup"><span data-stu-id="69f45-147">RWX</span></span>        | <span data-ttu-id="69f45-148">Lectura + Escritura + Ejecución</span><span class="sxs-lookup"><span data-stu-id="69f45-148">Read + Write + Execute</span></span> |
| <span data-ttu-id="69f45-149">5</span><span class="sxs-lookup"><span data-stu-id="69f45-149">5</span></span>            | <span data-ttu-id="69f45-150">R-X</span><span class="sxs-lookup"><span data-stu-id="69f45-150">R-X</span></span>        | <span data-ttu-id="69f45-151">Lectura + ejecución</span><span class="sxs-lookup"><span data-stu-id="69f45-151">Read + Execute</span></span>         |
| <span data-ttu-id="69f45-152">4</span><span class="sxs-lookup"><span data-stu-id="69f45-152">4</span></span>            | <span data-ttu-id="69f45-153">R--</span><span class="sxs-lookup"><span data-stu-id="69f45-153">R--</span></span>        | <span data-ttu-id="69f45-154">Lectura</span><span class="sxs-lookup"><span data-stu-id="69f45-154">Read</span></span>                   |
| <span data-ttu-id="69f45-155">0</span><span class="sxs-lookup"><span data-stu-id="69f45-155">0</span></span>            | ---        | <span data-ttu-id="69f45-156">Sin permisos</span><span class="sxs-lookup"><span data-stu-id="69f45-156">No permissions</span></span>         |


### <a name="permissions-do-not-inherit"></a><span data-ttu-id="69f45-157">Los permisos no se heredan</span><span class="sxs-lookup"><span data-stu-id="69f45-157">Permissions do not inherit</span></span>

<span data-ttu-id="69f45-158">Modelo de estilo de POSIX Hola utilizado por el almacén de Data Lake, permisos para un elemento se almacenan en el propio elemento Hola.</span><span class="sxs-lookup"><span data-stu-id="69f45-158">In hello POSIX-style model that's used by Data Lake Store, permissions for an item are stored on hello item itself.</span></span> <span data-ttu-id="69f45-159">En otras palabras, no pueden heredarse los permisos para un elemento de elementos primarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="69f45-159">In other words, permissions for an item cannot be inherited from hello parent items.</span></span>

## <a name="common-scenarios-related-toopermissions"></a><span data-ttu-id="69f45-160">Toopermissions relacionados de escenarios comunes</span><span class="sxs-lookup"><span data-stu-id="69f45-160">Common scenarios related toopermissions</span></span>

<span data-ttu-id="69f45-161">Estos son algunos toohelp escenarios comunes que comprenda qué permisos son necesarios tooperform determinadas operaciones en una cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="69f45-161">Following are some common scenarios toohelp you understand which permissions are needed tooperform certain operations on a Data Lake Store account.</span></span>

### <a name="permissions-needed-tooread-a-file"></a><span data-ttu-id="69f45-162">Permisos necesarios tooread un archivo</span><span class="sxs-lookup"><span data-stu-id="69f45-162">Permissions needed tooread a file</span></span>

![ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-3.png)

* <span data-ttu-id="69f45-164">Para leer el toobe de archivo hello, Hola llamador necesidades **lectura** permisos.</span><span class="sxs-lookup"><span data-stu-id="69f45-164">For hello file toobe read, hello caller needs **Read** permissions.</span></span>
* <span data-ttu-id="69f45-165">Para todos hello carpetas en la estructura de carpetas de Hola que contienen el archivo hello, Hola llamador necesidades **Execute** permisos.</span><span class="sxs-lookup"><span data-stu-id="69f45-165">For all hello folders in hello folder structure that contain hello file, hello caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-tooappend-tooa-file"></a><span data-ttu-id="69f45-166">Permisos necesarios tooappend tooa archivo</span><span class="sxs-lookup"><span data-stu-id="69f45-166">Permissions needed tooappend tooa file</span></span>

![ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-4.png)

* <span data-ttu-id="69f45-168">Para hello toobe de archivo se anexa a, Hola llamador necesidades **escribir** permisos.</span><span class="sxs-lookup"><span data-stu-id="69f45-168">For hello file toobe appended to, hello caller needs **Write** permissions.</span></span>
* <span data-ttu-id="69f45-169">Para todos hello las carpetas que contienen el archivo hello, Hola llamador necesidades **Execute** permisos.</span><span class="sxs-lookup"><span data-stu-id="69f45-169">For all hello folders that contain hello file, hello caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-toodelete-a-file"></a><span data-ttu-id="69f45-170">Permisos necesarios toodelete un archivo</span><span class="sxs-lookup"><span data-stu-id="69f45-170">Permissions needed toodelete a file</span></span>

![ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-5.png)

* <span data-ttu-id="69f45-172">Para la carpeta principal de hello, Hola llamador necesidades **escribir + ejecutar** permisos.</span><span class="sxs-lookup"><span data-stu-id="69f45-172">For hello parent folder, hello caller needs **Write + Execute** permissions.</span></span>
* <span data-ttu-id="69f45-173">Para todos los hello otras carpetas en la ruta de acceso del archivo de hello, Hola llamador necesidades **Execute** permisos.</span><span class="sxs-lookup"><span data-stu-id="69f45-173">For all hello other folders in hello file’s path, hello caller needs **Execute** permissions.</span></span>



> [!NOTE]
> <span data-ttu-id="69f45-174">Escribir permisos en el archivo hello no son necesario toodelete, siempre y cuando Hola dos condiciones anteriores son ciertas.</span><span class="sxs-lookup"><span data-stu-id="69f45-174">Write permissions on hello file are not required toodelete it as long as hello previous two conditions are true.</span></span>
>
>

### <a name="permissions-needed-tooenumerate-a-folder"></a><span data-ttu-id="69f45-175">Permisos necesarios tooenumerate una carpeta</span><span class="sxs-lookup"><span data-stu-id="69f45-175">Permissions needed tooenumerate a folder</span></span>

![ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-6.png)

* <span data-ttu-id="69f45-177">Para tooenumerate de la carpeta de hello, Hola llamador necesidades **lectura + Execute** permisos.</span><span class="sxs-lookup"><span data-stu-id="69f45-177">For hello folder tooenumerate, hello caller needs **Read + Execute** permissions.</span></span>
* <span data-ttu-id="69f45-178">Para todos los hello carpetas antecesor, Hola llamador necesidades **Execute** permisos.</span><span class="sxs-lookup"><span data-stu-id="69f45-178">For all hello ancestor folders, hello caller needs **Execute** permissions.</span></span>

## <a name="viewing-permissions-in-hello-azure-portal"></a><span data-ttu-id="69f45-179">Ver permisos en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="69f45-179">Viewing permissions in hello Azure portal</span></span>

<span data-ttu-id="69f45-180">De hello **Explorador de datos** hoja de hello cuenta de almacén de Data Lake, haga clic en **acceso** toosee hello las ACL para un archivo o una carpeta.</span><span class="sxs-lookup"><span data-stu-id="69f45-180">From hello **Data Explorer** blade of hello Data Lake Store account, click **Access** toosee hello ACLs for a file or a folder.</span></span> <span data-ttu-id="69f45-181">Haga clic en **acceso** toosee hello las ACL para hello **catálogo** carpeta bajo hello **mydatastore** cuenta.</span><span class="sxs-lookup"><span data-stu-id="69f45-181">Click **Access** toosee hello ACLs for hello **catalog** folder under hello **mydatastore** account.</span></span>

![ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-1.png)

<span data-ttu-id="69f45-183">En esta hoja, la sección superior hello muestra un resumen de los permisos de Hola que tiene.</span><span class="sxs-lookup"><span data-stu-id="69f45-183">On this blade, hello top section shows an overview of hello permissions that you have.</span></span> <span data-ttu-id="69f45-184">(En la captura de pantalla de hello, usuario de hello es Bob). A continuación, se muestran los permisos de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="69f45-184">(In hello screenshot, hello user is Bob.) Following that, hello access permissions are shown.</span></span> <span data-ttu-id="69f45-185">Después de eso, de hello **acceso** hoja, haga clic en **vista Simple** toosee Hola vista más sencilla.</span><span class="sxs-lookup"><span data-stu-id="69f45-185">After that, from hello **Access** blade, click **Simple View** toosee hello simpler view.</span></span>

![ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-simple-view.png)

<span data-ttu-id="69f45-187">Haga clic en **vista avanzada** toosee hello más vista avanzada, donde se muestran los conceptos de Hola de ACL predeterminada, la máscara y superusuario.</span><span class="sxs-lookup"><span data-stu-id="69f45-187">Click **Advanced View** toosee hello more advanced view, where hello concepts of Default ACLs, mask, and super-user are shown.</span></span>

![ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-advance-view.png)

## <a name="hello-super-user"></a><span data-ttu-id="69f45-189">superusuario de Hola</span><span class="sxs-lookup"><span data-stu-id="69f45-189">hello super-user</span></span>

<span data-ttu-id="69f45-190">Un superusuario tiene Hola la mayoría de los derechos de todos los usuarios de Hola Hola almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="69f45-190">A super-user has hello most rights of all hello users in hello Data Lake Store.</span></span> <span data-ttu-id="69f45-191">Un superusuario:</span><span class="sxs-lookup"><span data-stu-id="69f45-191">A super-user:</span></span>

* <span data-ttu-id="69f45-192">Tiene permisos de RWX demasiado**todos los** archivos y carpetas.</span><span class="sxs-lookup"><span data-stu-id="69f45-192">Has RWX Permissions too**all** files and folders.</span></span>
* <span data-ttu-id="69f45-193">Puede cambiar los permisos de Hola en cualquier archivo o carpeta.</span><span class="sxs-lookup"><span data-stu-id="69f45-193">Can change hello permissions on any file or folder.</span></span>
* <span data-ttu-id="69f45-194">Puede cambiar Hola posee el usuario o grupo de cualquier archivo o carpeta propietario.</span><span class="sxs-lookup"><span data-stu-id="69f45-194">Can change hello owning user or owning group of any file or folder.</span></span>

<span data-ttu-id="69f45-195">En Azure, una cuenta de Data Lake Store tiene varios roles de Azure, incluidos:</span><span class="sxs-lookup"><span data-stu-id="69f45-195">In Azure, a Data Lake Store account has several Azure roles, including:</span></span>

* <span data-ttu-id="69f45-196">Propietarios</span><span class="sxs-lookup"><span data-stu-id="69f45-196">Owners</span></span>
* <span data-ttu-id="69f45-197">Colaboradores</span><span class="sxs-lookup"><span data-stu-id="69f45-197">Contributors</span></span>
* <span data-ttu-id="69f45-198">Lectores</span><span class="sxs-lookup"><span data-stu-id="69f45-198">Readers</span></span>

<span data-ttu-id="69f45-199">Todas las personas de hello **propietarios** rol para una cuenta de almacén de Data Lake automáticamente es un superusuario para esa cuenta.</span><span class="sxs-lookup"><span data-stu-id="69f45-199">Everyone in hello **Owners** role for a Data Lake Store account is automatically a super-user for that account.</span></span> <span data-ttu-id="69f45-200">más información, consulte toolearn [el control de acceso basado en roles](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="69f45-200">toolearn more, see [Role-based access control](../active-directory/role-based-access-control-configure.md).</span></span>
<span data-ttu-id="69f45-201">Si desea toocreate una función de control de acceso basados en roles (RBAC) personalizado que tenga permisos de superusuario, necesita hello toohave los siguientes permisos:</span><span class="sxs-lookup"><span data-stu-id="69f45-201">If you want toocreate a custom role-based-access control (RBAC) role that has super-user permissions, it needs toohave hello following permissions:</span></span>
- <span data-ttu-id="69f45-202">Microsoft.DataLakeStore/accounts/Superuser/action</span><span class="sxs-lookup"><span data-stu-id="69f45-202">Microsoft.DataLakeStore/accounts/Superuser/action</span></span>
- <span data-ttu-id="69f45-203">Microsoft.Authorization/roleAssignments/write</span><span class="sxs-lookup"><span data-stu-id="69f45-203">Microsoft.Authorization/roleAssignments/write</span></span>


## <a name="hello-owning-user"></a><span data-ttu-id="69f45-204">usuario propietario de Hola</span><span class="sxs-lookup"><span data-stu-id="69f45-204">hello owning user</span></span>

<span data-ttu-id="69f45-205">usuario de Hola que ha creado el elemento de hello automáticamente es hello propietaria de usuario del elemento de Hola.</span><span class="sxs-lookup"><span data-stu-id="69f45-205">hello user who created hello item is automatically hello owning user of hello item.</span></span> <span data-ttu-id="69f45-206">Un usuario propietario puede:</span><span class="sxs-lookup"><span data-stu-id="69f45-206">An owning user can:</span></span>

* <span data-ttu-id="69f45-207">Cambiar los permisos de Hola de un archivo que pertenece.</span><span class="sxs-lookup"><span data-stu-id="69f45-207">Change hello permissions of a file that is owned.</span></span>
* <span data-ttu-id="69f45-208">Cambiar Hola propietaria de grupo de un archivo de propiedad, como usuario propietario de hello también es miembro del grupo de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="69f45-208">Change hello owning group of a file that is owned, as long as hello owning user is also a member of hello target group.</span></span>

> [!NOTE]
> <span data-ttu-id="69f45-209">Hola propietaria usuario *no se puede* cambiar Hola propietaria de usuario de otro archivo de propiedad.</span><span class="sxs-lookup"><span data-stu-id="69f45-209">hello owning user *cannot* change hello owning user of another owned file.</span></span> <span data-ttu-id="69f45-210">Solo los usuarios superobligatorios pueden cambiar Hola propietaria de usuario de un archivo o carpeta.</span><span class="sxs-lookup"><span data-stu-id="69f45-210">Only super-users can change hello owning user of a file or folder.</span></span>
>
>

## <a name="hello-owning-group"></a><span data-ttu-id="69f45-211">grupo de propietario de Hola</span><span class="sxs-lookup"><span data-stu-id="69f45-211">hello owning group</span></span>

<span data-ttu-id="69f45-212">Hola POSIX ACL, cada usuario está asociado con un "grupo principal".</span><span class="sxs-lookup"><span data-stu-id="69f45-212">In hello POSIX ACLs, every user is associated with a "primary group."</span></span> <span data-ttu-id="69f45-213">Por ejemplo, el usuario "alice" podría pertenecer toohello grupo de "Finanzas".</span><span class="sxs-lookup"><span data-stu-id="69f45-213">For example, user "alice" might belong toohello "finance" group.</span></span> <span data-ttu-id="69f45-214">Alice también es posible que pertenezca a grupos de toomultiple, pero un grupo siempre se designa como su grupo principal.</span><span class="sxs-lookup"><span data-stu-id="69f45-214">Alice might also belong toomultiple groups, but one group is always designated as her primary group.</span></span> <span data-ttu-id="69f45-215">En POSIX, cuando Alice crea un archivo, Hola propietaria de grupo de ese archivo se establece tooher grupo primario, que en este caso es "Finanzas".</span><span class="sxs-lookup"><span data-stu-id="69f45-215">In POSIX, when Alice creates a file, hello owning group of that file is set tooher primary group, which in this case is "finance."</span></span>

<span data-ttu-id="69f45-216">Cuando se crea un nuevo elemento de sistema de archivos, almacén de Data Lake asigna un toohello valor grupo propietario.</span><span class="sxs-lookup"><span data-stu-id="69f45-216">When a new filesystem item is created, Data Lake Store assigns a value toohello owning group.</span></span>

* <span data-ttu-id="69f45-217">**Caso 1**: carpeta de raíz de Hola "/".</span><span class="sxs-lookup"><span data-stu-id="69f45-217">**Case 1**: hello root folder "/".</span></span> <span data-ttu-id="69f45-218">Esta carpeta se crea cuando se crea una cuenta de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="69f45-218">This folder is created when a Data Lake Store account is created.</span></span> <span data-ttu-id="69f45-219">En este caso, grupo de propietario de Hola se establece toohello usuario que creó la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="69f45-219">In this case, hello owning group is set toohello user who created hello account.</span></span>
* <span data-ttu-id="69f45-220">**Caso 2** (los demás casos): cuando se crea un nuevo elemento, grupo de propietario de Hola se copia desde la carpeta principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="69f45-220">**Case 2** (Every other case): When a new item is created, hello owning group is copied from hello parent folder.</span></span>

<span data-ttu-id="69f45-221">grupo de propietario de Hello puede cambiarse mediante:</span><span class="sxs-lookup"><span data-stu-id="69f45-221">hello owning group can be changed by:</span></span>
* <span data-ttu-id="69f45-222">Cualquier superusuario.</span><span class="sxs-lookup"><span data-stu-id="69f45-222">Any super-users.</span></span>
* <span data-ttu-id="69f45-223">Hola posee el usuario, si el usuario propietario de hello también es miembro del grupo de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="69f45-223">hello owning user, if hello owning user is also a member of hello target group.</span></span>

## <a name="access-check-algorithm"></a><span data-ttu-id="69f45-224">Algoritmo de comprobación de acceso</span><span class="sxs-lookup"><span data-stu-id="69f45-224">Access check algorithm</span></span>

<span data-ttu-id="69f45-225">Hola siguiente ilustración representa el algoritmo de comprobación de acceso de Hola para las cuentas de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="69f45-225">hello following illustration represents hello access check algorithm for Data Lake Store accounts.</span></span>

![Algoritmo de ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-algorithm.png)


## <a name="hello-mask-and-effective-permissions"></a><span data-ttu-id="69f45-227">máscara de Hola y "permisos efectivos"</span><span class="sxs-lookup"><span data-stu-id="69f45-227">hello mask and "effective permissions"</span></span>

<span data-ttu-id="69f45-228">Hola **máscara** es un RWX valor que es acceso toolimit usado para **denominado usuarios**, hello **grupo propietario**, y **con grupos con nombre** cuando esté listo realizar el algoritmo de comprobación de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="69f45-228">hello **mask** is an RWX value that is used toolimit access for **named users**, hello **owning group**, and **named groups** when you're performing hello access check algorithm.</span></span> <span data-ttu-id="69f45-229">Estos son conceptos clave de Hola de máscara de Hola.</span><span class="sxs-lookup"><span data-stu-id="69f45-229">Here are hello key concepts for hello mask.</span></span>

* <span data-ttu-id="69f45-230">máscara de Hello crea "permisos efectivos".</span><span class="sxs-lookup"><span data-stu-id="69f45-230">hello mask creates "effective permissions."</span></span> <span data-ttu-id="69f45-231">Es decir, modifica los permisos de hello en tiempo de Hola de comprobación de acceso.</span><span class="sxs-lookup"><span data-stu-id="69f45-231">That is, it modifies hello permissions at hello time of access check.</span></span>
* <span data-ttu-id="69f45-232">máscara de Hello puede modificarse directamente por el propietario del archivo hello y a los usuarios superobligatorios.</span><span class="sxs-lookup"><span data-stu-id="69f45-232">hello mask can be directly edited by hello file owner and any super-users.</span></span>
* <span data-ttu-id="69f45-233">máscara de Hello puede quitar el permiso efectivo de permisos toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="69f45-233">hello mask can remove permissions toocreate hello effective permission.</span></span> <span data-ttu-id="69f45-234">máscara de Hello *no* agregar permiso efectivo de permisos toohello.</span><span class="sxs-lookup"><span data-stu-id="69f45-234">hello mask *cannot* add permissions toohello effective permission.</span></span>

<span data-ttu-id="69f45-235">Veamos algunos ejemplos.</span><span class="sxs-lookup"><span data-stu-id="69f45-235">Let's look at some examples.</span></span> <span data-ttu-id="69f45-236">En el siguiente ejemplo de Hola, máscara de Hola se establece demasiado**RWX**, lo que significa que esa máscara hello no quite los permisos.</span><span class="sxs-lookup"><span data-stu-id="69f45-236">In hello following example, hello mask is set too**RWX**, which means that hello mask does not remove any permissions.</span></span> <span data-ttu-id="69f45-237">permisos efectivos de Hola para hello con el nombre de usuario, grupo de propietario y con el nombre de grupo no se modifican durante la comprobación de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="69f45-237">hello effective permissions for hello named user, owning group, and named group are not altered during hello access check.</span></span>

![ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-mask-1.png)

<span data-ttu-id="69f45-239">En el siguiente ejemplo de Hola, máscara de Hola se establece demasiado**R-X**.</span><span class="sxs-lookup"><span data-stu-id="69f45-239">In hello following example, hello mask is set too**R-X**.</span></span> <span data-ttu-id="69f45-240">Esto significa que **desactiva los permisos de escritura de hello** para **con el nombre de usuario**, **grupo propietario**, y **denominado grupo** en tiempo de Hola de acceso comprobación.</span><span class="sxs-lookup"><span data-stu-id="69f45-240">This means that it **turns off hello Write permissions** for **named user**, **owning group**, and **named group** at hello time of access check.</span></span>

![ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-mask-2.png)

<span data-ttu-id="69f45-242">Como referencia, es aquí donde la máscara de Hola para un archivo o una carpeta aparece en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="69f45-242">For reference, here is where hello mask for a file or folder appears in hello Azure portal.</span></span>

![ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-mask-view.png)

> [!NOTE]
> <span data-ttu-id="69f45-244">Para una nueva cuenta de almacén de Data Lake, Hola para hello ACL de acceso y de máscara ACL predeterminada de raíz de hello predeterminado tooRWX de la carpeta ("/").</span><span class="sxs-lookup"><span data-stu-id="69f45-244">For a new Data Lake Store account, hello mask for hello Access ACL and Default ACL of hello root folder ("/") defaults tooRWX.</span></span>
>
>

## <a name="permissions-on-new-files-and-folders"></a><span data-ttu-id="69f45-245">Permisos en los archivos y carpetas nuevos</span><span class="sxs-lookup"><span data-stu-id="69f45-245">Permissions on new files and folders</span></span>

<span data-ttu-id="69f45-246">Cuando se crea un nuevo archivo o carpeta en una carpeta existente, determina Hola ACL predeterminada en la carpeta principal de hello:</span><span class="sxs-lookup"><span data-stu-id="69f45-246">When a new file or folder is created under an existing folder, hello Default ACL on hello parent folder determines:</span></span>

- <span data-ttu-id="69f45-247">La ACL predeterminada y la ACL de acceso de una carpeta secundaria.</span><span class="sxs-lookup"><span data-stu-id="69f45-247">A child folder’s Default ACL and Access ACL.</span></span>
- <span data-ttu-id="69f45-248">La ACL de acceso de un archivo secundario (los archivos no tienen ninguna ACL predeterminada).</span><span class="sxs-lookup"><span data-stu-id="69f45-248">A child file's Access ACL (files do not have a Default ACL).</span></span>

### <a name="hello-access-acl-of-a-child-file-or-folder"></a><span data-ttu-id="69f45-249">Hola acceso ACL de un archivo secundario o una carpeta</span><span class="sxs-lookup"><span data-stu-id="69f45-249">hello Access ACL of a child file or folder</span></span>

<span data-ttu-id="69f45-250">Cuando se crea un archivo secundario o una carpeta, predeterminado ACL del elemento primario de hello se copiará como Hola acceso ACL de archivos secundarios de Hola o una carpeta.</span><span class="sxs-lookup"><span data-stu-id="69f45-250">When a child file or folder is created, hello parent's Default ACL is copied as hello Access ACL of hello child file or folder.</span></span> <span data-ttu-id="69f45-251">Además, si **otros** usuario tiene permisos de RWX predeterminado del elemento primario de hello ACL, se quita de la ACL de acceso del elemento de hello secundarios.</span><span class="sxs-lookup"><span data-stu-id="69f45-251">Also, if **other** user has RWX permissions in hello parent's default ACL, it is removed from hello child item's Access ACL.</span></span>

![ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-child-items-1.png)

<span data-ttu-id="69f45-253">En la mayoría de los escenarios, información anterior de hello es todo lo que necesita tooknow acerca de cómo se determinan los ACL de acceso de un elemento secundario.</span><span class="sxs-lookup"><span data-stu-id="69f45-253">In most scenarios, hello previous information is all you need tooknow about how a child item’s Access ACL is determined.</span></span> <span data-ttu-id="69f45-254">Sin embargo, si está familiarizado con los sistemas POSIX y detallados desee toounderstand cómo se consigue esta transformación, vea la sección de hello [rol del Umask en la creación de hello acceso ACL para los nuevos archivos y carpetas](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="69f45-254">However, if you are familiar with POSIX systems and want toounderstand in-depth how this transformation is achieved, see hello section [Umask’s role in creating hello Access ACL for new files and folders](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) later in this article.</span></span>


### <a name="a-child-folders-default-acl"></a><span data-ttu-id="69f45-255">ACL predeterminada de una carpeta secundaria.</span><span class="sxs-lookup"><span data-stu-id="69f45-255">A child folder's Default ACL</span></span>

<span data-ttu-id="69f45-256">Cuando se crea una carpeta secundaria en una carpeta primaria, ACL predeterminada de la carpeta principal Hola se copió sea ACL predeterminada de la carpeta de toohello secundarios.</span><span class="sxs-lookup"><span data-stu-id="69f45-256">When a child folder is created under a parent folder, hello parent folder's Default ACL is copied over as is toohello child folder's Default ACL.</span></span>

![ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-child-items-2.png)

## <a name="advanced-topics-for-understanding-acls-in-data-lake-store"></a><span data-ttu-id="69f45-258">Temas avanzados para entender las ACL en Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="69f45-258">Advanced topics for understanding ACLs in Data Lake Store</span></span>

<span data-ttu-id="69f45-259">Los siguientes son algunos toohelp temas avanzados que comprenda cómo se determinan las ACL para el almacén de Data Lake archivos o carpetas.</span><span class="sxs-lookup"><span data-stu-id="69f45-259">Following are some advanced topics toohelp you understand how ACLs are determined for Data Lake Store files or folders.</span></span>

### <a name="umasks-role-in-creating-hello-access-acl-for-new-files-and-folders"></a><span data-ttu-id="69f45-260">Rol del umask en la creación de hello acceso ACL para los nuevos archivos y carpetas</span><span class="sxs-lookup"><span data-stu-id="69f45-260">Umask’s role in creating hello Access ACL for new files and folders</span></span>

<span data-ttu-id="69f45-261">En un sistema compatible con POSIX, concepto general de hello es ese umask es un valor de 9 bits en carpeta principal de Hola que ha usado el permiso de hello tootransform para **propietario usuario**, **grupo propietario**, y  **otros** en hello acceso ACL de un archivo secundario nuevo o una carpeta.</span><span class="sxs-lookup"><span data-stu-id="69f45-261">In a POSIX-compliant system, hello general concept is that umask is a 9-bit value on hello parent folder that's used tootransform hello permission for **owning user**, **owning group**, and **other** on hello Access ACL of a new child file or folder.</span></span> <span data-ttu-id="69f45-262">bits de Hola de un umask identifican qué tooturn bits off en ACL de acceso del elemento de hello secundarios.</span><span class="sxs-lookup"><span data-stu-id="69f45-262">hello bits of a umask identify which bits tooturn off in hello child item’s Access ACL.</span></span> <span data-ttu-id="69f45-263">Por lo tanto se utiliza tooselectively evitar la propagación de Hola de permisos para **propietaria de usuario**, **grupo propietario**, y **otros**.</span><span class="sxs-lookup"><span data-stu-id="69f45-263">Thus it is used tooselectively prevent hello propagation of permissions for **owning user**, **owning group**, and **other**.</span></span>

<span data-ttu-id="69f45-264">En un sistema HDFS, Hola umask suele ser una opción de configuración en todo el sitio que está controlada por los administradores.</span><span class="sxs-lookup"><span data-stu-id="69f45-264">In an HDFS system, hello umask is typically a sitewide configuration option that is controlled by administrators.</span></span> <span data-ttu-id="69f45-265">Data Lake Store usa una **umask para toda la cuenta** que no se puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="69f45-265">Data Lake Store uses an **account-wide umask** that cannot be changed.</span></span> <span data-ttu-id="69f45-266">Hola siguiente tabla muestra hello desenmascara almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="69f45-266">hello following table shows hello unmask for Data Lake Store.</span></span>

| <span data-ttu-id="69f45-267">Grupo de usuarios</span><span class="sxs-lookup"><span data-stu-id="69f45-267">User group</span></span>  | <span data-ttu-id="69f45-268">Configuración</span><span class="sxs-lookup"><span data-stu-id="69f45-268">Setting</span></span> | <span data-ttu-id="69f45-269">Efecto en la ACL de acceso de un nuevo elemento secundario</span><span class="sxs-lookup"><span data-stu-id="69f45-269">Effect on new child item's Access ACL</span></span> |
|------------ |---------|---------------------------------------|
| <span data-ttu-id="69f45-270">usuario propietario</span><span class="sxs-lookup"><span data-stu-id="69f45-270">Owning user</span></span> | ---     | <span data-ttu-id="69f45-271">Sin efecto</span><span class="sxs-lookup"><span data-stu-id="69f45-271">No effect</span></span>                             |
| <span data-ttu-id="69f45-272">grupo propietario</span><span class="sxs-lookup"><span data-stu-id="69f45-272">Owning group</span></span>| ---     | <span data-ttu-id="69f45-273">Sin efecto</span><span class="sxs-lookup"><span data-stu-id="69f45-273">No effect</span></span>                             |
| <span data-ttu-id="69f45-274">otro</span><span class="sxs-lookup"><span data-stu-id="69f45-274">Other</span></span>       | <span data-ttu-id="69f45-275">RWX</span><span class="sxs-lookup"><span data-stu-id="69f45-275">RWX</span></span>     | <span data-ttu-id="69f45-276">Se elimina lectura + escritura + ejecución</span><span class="sxs-lookup"><span data-stu-id="69f45-276">Remove Read + Write + Execute</span></span>         |

<span data-ttu-id="69f45-277">Hola sigue en la ilustración muestra este umask en acción.</span><span class="sxs-lookup"><span data-stu-id="69f45-277">hello following illustration shows this umask in action.</span></span> <span data-ttu-id="69f45-278">efecto neto de Hello es tooremove **lectura + escribir y ejecutar** para **otros** usuario.</span><span class="sxs-lookup"><span data-stu-id="69f45-278">hello net effect is tooremove **Read + Write + Execute** for **other** user.</span></span> <span data-ttu-id="69f45-279">Porque Hola umask no especificó los bits de **propietario usuario** y **grupo propietario**, esos permisos no se transforman.</span><span class="sxs-lookup"><span data-stu-id="69f45-279">Because hello umask did not specify bits for **owning user** and **owning group**, those permissions are not transformed.</span></span>

![ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-umask.png)

### <a name="hello-sticky-bit"></a><span data-ttu-id="69f45-281">bit rápidas Hola</span><span class="sxs-lookup"><span data-stu-id="69f45-281">hello sticky bit</span></span>

<span data-ttu-id="69f45-282">bit rápidas de Hello es una característica avanzada más de un sistema de archivos POSIX.</span><span class="sxs-lookup"><span data-stu-id="69f45-282">hello sticky bit is a more advanced feature of a POSIX filesystem.</span></span> <span data-ttu-id="69f45-283">En contexto de hello Lake del almacén de datos, es poco probable que se necesitarán ese bit rápidas Hola.</span><span class="sxs-lookup"><span data-stu-id="69f45-283">In hello context of Data Lake Store, it is unlikely that hello sticky bit will be needed.</span></span>

<span data-ttu-id="69f45-284">Hello tabla siguiente muestra cómo funciona el bit rápidas de hello en el almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="69f45-284">hello following table shows how hello sticky bit works in Data Lake Store.</span></span>

| <span data-ttu-id="69f45-285">Grupo de usuarios</span><span class="sxs-lookup"><span data-stu-id="69f45-285">User group</span></span>         | <span data-ttu-id="69f45-286">Archivo</span><span class="sxs-lookup"><span data-stu-id="69f45-286">File</span></span>    | <span data-ttu-id="69f45-287">Carpeta</span><span class="sxs-lookup"><span data-stu-id="69f45-287">Folder</span></span> |
|--------------------|---------|-------------------------|
| <span data-ttu-id="69f45-288">Sticky Bits **DESACTIVADO**</span><span class="sxs-lookup"><span data-stu-id="69f45-288">Sticky bit **OFF**</span></span> | <span data-ttu-id="69f45-289">Sin efecto</span><span class="sxs-lookup"><span data-stu-id="69f45-289">No effect</span></span>   | <span data-ttu-id="69f45-290">Sin efecto.</span><span class="sxs-lookup"><span data-stu-id="69f45-290">No effect.</span></span>           |
| <span data-ttu-id="69f45-291">Sticky Bits **ACTIVADO**</span><span class="sxs-lookup"><span data-stu-id="69f45-291">Sticky bit **ON**</span></span>  | <span data-ttu-id="69f45-292">Sin efecto</span><span class="sxs-lookup"><span data-stu-id="69f45-292">No effect</span></span>   | <span data-ttu-id="69f45-293">Impide que nadie excepto **usuarios superobligatorios** hello y **propietaria de usuario** de un elemento secundario de eliminar o cambiar el nombre de ese elemento secundario.</span><span class="sxs-lookup"><span data-stu-id="69f45-293">Prevents anyone except **super-users** and hello **owning user** of a child item from deleting or renaming that child item.</span></span>               |

<span data-ttu-id="69f45-294">bit rápidas Hello no se muestra en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="69f45-294">hello sticky bit is not shown in hello Azure portal.</span></span>

## <a name="common-questions-about-acls-in-data-lake-store"></a><span data-ttu-id="69f45-295">Preguntas frecuentes sobre las ACL en Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="69f45-295">Common questions about ACLs in Data Lake Store</span></span>

<span data-ttu-id="69f45-296">Estas son algunas preguntas que surgen a menudo con respecto a las ACL en Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="69f45-296">Here are some questions that come up often about ACLs in Data Lake Store.</span></span>

### <a name="do-i-have-tooenable-support-for-acls"></a><span data-ttu-id="69f45-297">¿Tengo que tooenable compatibilidad con las ACL?</span><span class="sxs-lookup"><span data-stu-id="69f45-297">Do I have tooenable support for ACLs?</span></span>

<span data-ttu-id="69f45-298">No.</span><span class="sxs-lookup"><span data-stu-id="69f45-298">No.</span></span> <span data-ttu-id="69f45-299">El control de acceso mediante las ACL siempre está activado en las cuentas de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="69f45-299">Access control via ACLs is always on for a Data Lake Store account.</span></span>

### <a name="which-permissions-are-required-toorecursively-delete-a-folder-and-its-contents"></a><span data-ttu-id="69f45-300">¿Qué permisos están toorecursively necesario eliminar una carpeta y su contenido?</span><span class="sxs-lookup"><span data-stu-id="69f45-300">Which permissions are required toorecursively delete a folder and its contents?</span></span>

* <span data-ttu-id="69f45-301">debe tener la carpeta principal de Hello **escribir + ejecutar** permisos.</span><span class="sxs-lookup"><span data-stu-id="69f45-301">hello parent folder must have **Write + Execute** permissions.</span></span>
* <span data-ttu-id="69f45-302">Hola toobe carpeta eliminado, y requiere que todas las carpetas dentro de él, **lectura + escribir y ejecutar** permisos.</span><span class="sxs-lookup"><span data-stu-id="69f45-302">hello folder toobe deleted, and every folder within it, requires **Read + Write + Execute** permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="69f45-303">No es necesario escribir permisos toodelete archivos en carpetas.</span><span class="sxs-lookup"><span data-stu-id="69f45-303">You do not need Write permissions toodelete files in folders.</span></span> <span data-ttu-id="69f45-304">Además, Hola carpeta raíz "/" puede **nunca** puede eliminar.</span><span class="sxs-lookup"><span data-stu-id="69f45-304">Also, hello root folder "/" can **never** be deleted.</span></span>
>
>

### <a name="who-is-hello-owner-of-a-file-or-folder"></a><span data-ttu-id="69f45-305">¿Quién es el propietario de Hola de un archivo o carpeta?</span><span class="sxs-lookup"><span data-stu-id="69f45-305">Who is hello owner of a file or folder?</span></span>

<span data-ttu-id="69f45-306">creador de Hola de un archivo o carpeta se convierte en propietario de Hola.</span><span class="sxs-lookup"><span data-stu-id="69f45-306">hello creator of a file or folder becomes hello owner.</span></span>

### <a name="which-group-is-set-as-hello-owning-group-of-a-file-or-folder-at-creation"></a><span data-ttu-id="69f45-307">¿El grupo al que se establece como Hola grupo de un archivo o carpeta en la creación del propietario?</span><span class="sxs-lookup"><span data-stu-id="69f45-307">Which group is set as hello owning group of a file or folder at creation?</span></span>

<span data-ttu-id="69f45-308">grupo de propietario de Hola se copia desde Hola posee el grupo de la carpeta principal de hello en qué Hola se crea un nuevo archivo o carpeta.</span><span class="sxs-lookup"><span data-stu-id="69f45-308">hello owning group is copied from hello owning group of hello parent folder under which hello new file or folder is created.</span></span>

### <a name="i-am-hello-owning-user-of-a-file-but-i-dont-have-hello-rwx-permissions-i-need-what-do-i-do"></a><span data-ttu-id="69f45-309">Soy Hola propietaria de usuario de un archivo pero no tengo permisos de RWX Hola que necesito.</span><span class="sxs-lookup"><span data-stu-id="69f45-309">I am hello owning user of a file but I don’t have hello RWX permissions I need.</span></span> <span data-ttu-id="69f45-310">¿Qué puedo hacer?</span><span class="sxs-lookup"><span data-stu-id="69f45-310">What do I do?</span></span>

<span data-ttu-id="69f45-311">usuario propietario de Hello puede cambiar Hola permisos de hello archivo toogive ellos mismos los permisos RWX que necesitan.</span><span class="sxs-lookup"><span data-stu-id="69f45-311">hello owning user can change hello permissions of hello file toogive themselves any RWX permissions they need.</span></span>

### <a name="when-i-look-at-acls-in-hello-azure-portal-i-see-user-names-but-through-apis-i-see-guids-why-is-that"></a><span data-ttu-id="69f45-312">Si se observan las ACL en hello portal de Azure ver nombres de usuario pero a través de API, veo GUID, ¿por qué?</span><span class="sxs-lookup"><span data-stu-id="69f45-312">When I look at ACLs in hello Azure portal I see user names but through APIs, I see GUIDs, why is that?</span></span>

<span data-ttu-id="69f45-313">Las entradas de las ACL de Hola se almacenan como GUID correspondientes toousers en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="69f45-313">Entries in hello ACLs are stored as GUIDs that correspond toousers in Azure AD.</span></span> <span data-ttu-id="69f45-314">Hola API devuelven Hola GUID tal cual.</span><span class="sxs-lookup"><span data-stu-id="69f45-314">hello APIs return hello GUIDs as is.</span></span> <span data-ttu-id="69f45-315">Hola portal de Azure intenta toomake ACL más fácil toouse por traducción Hola GUID en nombres descriptivos siempre que sea posible.</span><span class="sxs-lookup"><span data-stu-id="69f45-315">hello Azure portal tries toomake ACLs easier toouse by translating hello GUIDs into friendly names when possible.</span></span>

### <a name="why-do-i-sometimes-see-guids-in-hello-acls-when-im-using-hello-azure-portal"></a><span data-ttu-id="69f45-316">¿Por qué a veces aparece GUID en las ACL de hello cuando utilizo Hola portal de Azure?</span><span class="sxs-lookup"><span data-stu-id="69f45-316">Why do I sometimes see GUIDs in hello ACLs when I'm using hello Azure portal?</span></span>

<span data-ttu-id="69f45-317">Un GUID se muestra al usuario de hello no existe en Azure AD ya.</span><span class="sxs-lookup"><span data-stu-id="69f45-317">A GUID is shown when hello user doesn't exist in Azure AD anymore.</span></span> <span data-ttu-id="69f45-318">Normalmente esto sucede cuando el usuario de hello ha dejado la empresa de Hola o si se ha eliminado su cuenta en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="69f45-318">Usually this happens when hello user has left hello company or if their account has been deleted in Azure AD.</span></span>

### <a name="does-data-lake-store-support-inheritance-of-acls"></a><span data-ttu-id="69f45-319">¿Admite Data Lake Store la herencia de ACL?</span><span class="sxs-lookup"><span data-stu-id="69f45-319">Does Data Lake Store support inheritance of ACLs?</span></span>

<span data-ttu-id="69f45-320">No.</span><span class="sxs-lookup"><span data-stu-id="69f45-320">No.</span></span>

### <a name="what-is-hello-difference-between-mask-and-umask"></a><span data-ttu-id="69f45-321">¿Cuál es la diferencia de hello entre máscara y umask?</span><span class="sxs-lookup"><span data-stu-id="69f45-321">What is hello difference between mask and umask?</span></span>

| <span data-ttu-id="69f45-322">mask</span><span class="sxs-lookup"><span data-stu-id="69f45-322">mask</span></span> | <span data-ttu-id="69f45-323">umask</span><span class="sxs-lookup"><span data-stu-id="69f45-323">umask</span></span>|
|------|------|
| <span data-ttu-id="69f45-324">Hola **máscara** propiedad está disponible en todos los archivos y carpetas.</span><span class="sxs-lookup"><span data-stu-id="69f45-324">hello **mask** property is available on every file and folder.</span></span> | <span data-ttu-id="69f45-325">Hola **umask** es una propiedad de hello cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="69f45-325">hello **umask** is a property of hello Data Lake Store account.</span></span> <span data-ttu-id="69f45-326">Por lo que hay solo un único umask Hola almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="69f45-326">So there is only a single umask in hello Data Lake Store.</span></span>    |
| <span data-ttu-id="69f45-327">propiedad de máscara de Hello en un archivo o carpeta puede ser modificado por hello posee el usuario o grupo de un archivo o un superusuario propietario.</span><span class="sxs-lookup"><span data-stu-id="69f45-327">hello mask property on a file or folder can be altered by hello owning user or owning group of a file or a super-user.</span></span> | <span data-ttu-id="69f45-328">no se puede modificar la propiedad de umask Hola por cualquier usuario, incluso un superusuario.</span><span class="sxs-lookup"><span data-stu-id="69f45-328">hello umask property cannot be modified by any user, even a super-user.</span></span> <span data-ttu-id="69f45-329">Es un valor constante y que no puede cambiarse.</span><span class="sxs-lookup"><span data-stu-id="69f45-329">It is an unchangeable, constant value.</span></span>|
| <span data-ttu-id="69f45-330">propiedad de máscara de Hola se utiliza durante el algoritmo de comprobación de acceso de hello en tiempo de ejecución toodetermine si un usuario tiene tooperform derecho hello en la operación en un archivo o carpeta.</span><span class="sxs-lookup"><span data-stu-id="69f45-330">hello mask property is used during hello access check algorithm at runtime toodetermine whether a user has hello right tooperform on operation on a file or folder.</span></span> <span data-ttu-id="69f45-331">rol de Hola de máscara de hello es toocreate "permisos efectivos" en tiempo de Hola de comprobación de acceso.</span><span class="sxs-lookup"><span data-stu-id="69f45-331">hello role of hello mask is toocreate "effective permissions" at hello time of access check.</span></span> | <span data-ttu-id="69f45-332">Hola umask no se utiliza durante la comprobación de acceso en absoluto.</span><span class="sxs-lookup"><span data-stu-id="69f45-332">hello umask is not used during access check at all.</span></span> <span data-ttu-id="69f45-333">Hola umask es toodetermine usado Hola acceso ACL de nuevos elementos secundarios de una carpeta.</span><span class="sxs-lookup"><span data-stu-id="69f45-333">hello umask is used toodetermine hello Access ACL of new child items of a folder.</span></span> |
| <span data-ttu-id="69f45-334">máscara de Hello es un valor RWX de 3 bits que se aplica toonamed usuario, nombre de grupo y usuario propietario en tiempo de Hola de comprobación de acceso.</span><span class="sxs-lookup"><span data-stu-id="69f45-334">hello mask is a 3-bit RWX value that applies toonamed user, named group, and owning user at hello time of access check.</span></span>| <span data-ttu-id="69f45-335">umask Hello es un valor de 9 bits que se aplica toohello posee el usuario, grupo, propietario y **otros** de un nuevo elemento secundario.</span><span class="sxs-lookup"><span data-stu-id="69f45-335">hello umask is a 9-bit value that applies toohello owning user, owning group, and **other** of a new child.</span></span>|

### <a name="where-can-i-learn-more-about-posix-access-control-model"></a><span data-ttu-id="69f45-336">¿Dónde puedo obtener más información sobre el modelo de control de acceso POSIX?</span><span class="sxs-lookup"><span data-stu-id="69f45-336">Where can I learn more about POSIX access control model?</span></span>

* <span data-ttu-id="69f45-337">[POSIX Access Control Lists on Linux](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html) (Listas de control de acceso de POSIX en Linux)</span><span class="sxs-lookup"><span data-stu-id="69f45-337">[POSIX Access Control Lists on Linux](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html)</span></span>

* <span data-ttu-id="69f45-338">[HDFS Permission Guide](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html) (Guía de permisos de HDFS)</span><span class="sxs-lookup"><span data-stu-id="69f45-338">[HDFS permission guide](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)</span></span>

* [<span data-ttu-id="69f45-339">POSIX FAQ (PREGUNTAS MÁS FRECUENTES SOBRE POSIX)</span><span class="sxs-lookup"><span data-stu-id="69f45-339">POSIX FAQ</span></span>](http://www.opengroup.org/austin/papers/posix_faq.html)

* [<span data-ttu-id="69f45-340">POSIX 1003.1 2008</span><span class="sxs-lookup"><span data-stu-id="69f45-340">POSIX 1003.1 2008</span></span>](http://standards.ieee.org/findstds/standard/1003.1-2008.html)

* [<span data-ttu-id="69f45-341">POSIX 1003.1 2013</span><span class="sxs-lookup"><span data-stu-id="69f45-341">POSIX 1003.1 2013</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2013edition/)

* [<span data-ttu-id="69f45-342">POSIX 1003.1 2016</span><span class="sxs-lookup"><span data-stu-id="69f45-342">POSIX 1003.1 2016</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2016edition/)

* [<span data-ttu-id="69f45-343">ACL de POSIX en Ubuntu</span><span class="sxs-lookup"><span data-stu-id="69f45-343">POSIX ACL on Ubuntu</span></span>](https://help.ubuntu.com/community/FilePermissionsACLs)

* <span data-ttu-id="69f45-344">[ACL: Using Access Control Lists on Linux](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/) (ACL: uso de listas de control de acceso en Linux)</span><span class="sxs-lookup"><span data-stu-id="69f45-344">[ACL using access control lists on Linux](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/)</span></span>

## <a name="see-also"></a><span data-ttu-id="69f45-345">Consulte también</span><span class="sxs-lookup"><span data-stu-id="69f45-345">See also</span></span>

* [<span data-ttu-id="69f45-346">Información general del Almacén de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="69f45-346">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
