---
title: "aaaHow toosecure acceso tooAzure el catálogo de datos | Documentos de Microsoft"
description: "En este artículo se explica cómo toosecure el catálogo de datos y sus activos de datos."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: d7c35fd57d8add1cdc152b75f111879288e1548f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-access-toodata-catalog-and-data-assets"></a><span data-ttu-id="12d34-103">Cómo toosecure tener acceso a los activos de datos y catálogo toodata</span><span class="sxs-lookup"><span data-stu-id="12d34-103">How toosecure access toodata catalog and data assets</span></span>
> [!IMPORTANT]
> <span data-ttu-id="12d34-104">Esta característica solo está disponible en edición standard de Hola de catálogo de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="12d34-104">This feature is available only in hello standard edition of Azure Data Catalog.</span></span>

<span data-ttu-id="12d34-105">Catálogo de datos de Azure permite toospecify quién puede acceder al catálogo de datos de Hola y qué operaciones (registrar, anotar, tomar posesión) pueden realizar en los metadatos de catálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="12d34-105">Azure Data Catalog allows you toospecify who can access hello data catalog and what operations (register, annotate, take ownership) they can perform on metadata in hello catalog.</span></span> 

## <a name="catalog-users-and-permissions"></a><span data-ttu-id="12d34-106">Usuarios del catálogo y permisos</span><span class="sxs-lookup"><span data-stu-id="12d34-106">Catalog users and permissions</span></span>
<span data-ttu-id="12d34-107">toogive un usuario o un hello grupo acceder tooa el catálogo de datos y establecer permisos:</span><span class="sxs-lookup"><span data-stu-id="12d34-107">toogive a user or a group hello access tooa data catalog and set permissions:</span></span>

1. <span data-ttu-id="12d34-108">En hello [página principal de su catálogo de datos](http://www.azuredatacatalog.com), haga clic en **configuración** en la barra de herramientas de Hola.</span><span class="sxs-lookup"><span data-stu-id="12d34-108">On hello [home page of your data catalog](http://www.azuredatacatalog.com),  click **Settings** on hello toolbar.</span></span>

    ![catálogo de datos: configuración](media/data-catalog-how-to-secure-catalog/data-catalog-settings.png)
2. <span data-ttu-id="12d34-110">En la página de configuración de hello, expanda hello **usuarios catálogo** sección.</span><span class="sxs-lookup"><span data-stu-id="12d34-110">In hello settings page, expand hello **Catalog Users** section.</span></span>
    <span data-ttu-id="12d34-111">![Usuarios del catálogo: agregar](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span><span class="sxs-lookup"><span data-stu-id="12d34-111">![Catalog Users - Add](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span></span>
3. <span data-ttu-id="12d34-112">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="12d34-112">Click **Add**.</span></span>
4. <span data-ttu-id="12d34-113">Escriba Hola completo **nombre de usuario** o nombre de hello **grupo de seguridad** en hello Azure Active Directory (AAD) asociados con el catálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="12d34-113">Enter hello fully qualified **user name** or name of hello **security group** in hello Azure Active Directory (AAD) associated with hello catalog.</span></span> <span data-ttu-id="12d34-114">Use la coma (\`,’) como separador si está agregando más de un usuario o grupo.</span><span class="sxs-lookup"><span data-stu-id="12d34-114">Use comma (\`,’) as a separator if you are adding more than one user or group.</span></span>
    <span data-ttu-id="12d34-115">![Usuarios del catálogo: usuarios o grupos](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span><span class="sxs-lookup"><span data-stu-id="12d34-115">![Catalog Users - users or groups](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span></span>
5. <span data-ttu-id="12d34-116">Presione **ENTRAR** o **ficha** fuera del cuadro de texto de Hola.</span><span class="sxs-lookup"><span data-stu-id="12d34-116">Press **ENTER** or **TAB** out of hello text box.</span></span> 
6.  <span data-ttu-id="12d34-117">Confirme que todos los permisos (**anotar**, **registrar**, y **Take Ownership**) se asignan toothese usuarios o grupos de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="12d34-117">Confirm that all permissions (**Annotate**, **Register**, and **Take Ownership**) are assigned toothese users or groups by default.</span></span> <span data-ttu-id="12d34-118">Es decir, Hola usuario o grupo puede [registrar activos de datos]( data-catalog-how-to-register.md), [anotar los activos de datos]( data-catalog-how-to-annotate.md), y [tomar posesión de activos de datos]( data-catalog-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="12d34-118">That is, hello user or group can [register data assets]( data-catalog-how-to-register.md), [annotate data assets]( data-catalog-how-to-annotate.md), and [take ownership of data assets]( data-catalog-how-to-manage.md).</span></span> 
    <span data-ttu-id="12d34-119">![Usuarios del catálogo: permisos predeterminados](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="12d34-119">![Catalog Users - default permissions](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span></span>
7.  <span data-ttu-id="12d34-120">toogive un usuario o grupo sólo Hola lee catálogo toohello de acceso, desactive hello **anotar** opción para ese usuario o grupo.</span><span class="sxs-lookup"><span data-stu-id="12d34-120">toogive a user or group only hello read access toohello catalog, clear hello **annotate** option for that user or group.</span></span> <span data-ttu-id="12d34-121">Al hacerlo, Hola usuario o grupo no puede anotar los activos de datos en el catálogo de hello pero puede verlos.</span><span class="sxs-lookup"><span data-stu-id="12d34-121">When you do so, hello user or group cannot annotate data assets in hello catalog but they can view them.</span></span> 
8.  <span data-ttu-id="12d34-122">toodeny un usuario o grupo de registro de recursos de datos, desactive hello **registrar** opción para ese usuario o grupo.</span><span class="sxs-lookup"><span data-stu-id="12d34-122">toodeny a user or group from registering data assets, clear hello **register** option for that user or group.</span></span>
9.  <span data-ttu-id="12d34-123">un usuario tomar posesión de un recurso de datos, desactive hello toodeny **tomar posesión** opción para ese usuario o grupo.</span><span class="sxs-lookup"><span data-stu-id="12d34-123">toodeny a user from taking ownership of a data asset, clear hello **take ownership** option for that user or group.</span></span> 
10. <span data-ttu-id="12d34-124">Haga clic en un usuario o grupo de usuarios del catálogo, toodelete **x** Hola/grupo de usuarios en parte inferior de Hola de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="12d34-124">toodelete a user/group from catalog users, click **x** for hello user/group at hello bottom of hello list.</span></span> 
    <span data-ttu-id="12d34-125">![Usuarios del catálogo: eliminar usuario](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="12d34-125">![Catalog Users - delete user](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="12d34-126">Se recomienda que agregue directamente los usuarios toocatalog de grupos de seguridad en lugar de agregar usuarios y asignar permisos.</span><span class="sxs-lookup"><span data-stu-id="12d34-126">We recommend that you add security groups toocatalog users rather than adding users directly and assign permissions.</span></span> <span data-ttu-id="12d34-127">A continuación, agregar grupos de seguridad de toohello de los usuarios que coinciden con sus roles y sus catálogos de toohello de acceso necesario.</span><span class="sxs-lookup"><span data-stu-id="12d34-127">Then, add users toohello security groups that match their roles and their required access toohello catalog.</span></span>

## <a name="special-considerations"></a><span data-ttu-id="12d34-128">Consideraciones especiales</span><span class="sxs-lookup"><span data-stu-id="12d34-128">Special considerations</span></span>

- <span data-ttu-id="12d34-129">permisos de Hello asignan toosecurity grupos son aditivas.</span><span class="sxs-lookup"><span data-stu-id="12d34-129">hello permissions assigned toosecurity groups are additive.</span></span> <span data-ttu-id="12d34-130">Por ejemplo, un usuario pertenece a dos grupos.</span><span class="sxs-lookup"><span data-stu-id="12d34-130">Say, a user is in two groups.</span></span> <span data-ttu-id="12d34-131">En un grupo tiene permisos de anotación y en otro no.</span><span class="sxs-lookup"><span data-stu-id="12d34-131">One group has annotate permissions and other group does not have annotate permissions.</span></span> <span data-ttu-id="12d34-132">Por lo tanto, el usuario tiene permisos de anotación.</span><span class="sxs-lookup"><span data-stu-id="12d34-132">Then, user has annotate permissions.</span></span> 
- <span data-ttu-id="12d34-133">asignar permisos de Hello explícitamente Hola de reemplazo de usuario de tooa permisos asignados toogroups toowhich Hola usuario pertenece.</span><span class="sxs-lookup"><span data-stu-id="12d34-133">hello permissions assigned explicitly tooa user override hello permissions assigned toogroups toowhich hello user belongs.</span></span> <span data-ttu-id="12d34-134">En el ejemplo anterior de hello, por ejemplo, ha agregado explícitamente usuarios de toocatalog de usuario de hello y no asigna permisos de anotar.</span><span class="sxs-lookup"><span data-stu-id="12d34-134">In hello previous example, say, you explicitly added hello user toocatalog users and do not assign annotate permissions.</span></span> <span data-ttu-id="12d34-135">usuario Hello no puede anotar los activos de datos aunque el usuario de hello es agregar anotaciones a un miembro de un grupo que tenga permisos.</span><span class="sxs-lookup"><span data-stu-id="12d34-135">hello user cannot annotate data assets even though hello user is a member of a group that does have annotate permissions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12d34-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="12d34-136">Next steps</span></span>
- [<span data-ttu-id="12d34-137">Introducción al Catálogo de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="12d34-137">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)

