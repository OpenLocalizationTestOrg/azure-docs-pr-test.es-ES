---
title: "Lección 11 del tutorial de Azure Analysis Services: Creación de roles | Microsoft Docs"
description: "Describe cómo crear roles en el proyecto del tutorial de Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: 085a36edd2a0e80123ac8754b438bceadfa6c0e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-11-create-roles"></a><span data-ttu-id="8ef9f-103">Lección 11: Creación de roles</span><span class="sxs-lookup"><span data-stu-id="8ef9f-103">Lesson 11: Create roles</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="8ef9f-104">En esta lección, creará roles.</span><span class="sxs-lookup"><span data-stu-id="8ef9f-104">In this lesson, you create roles.</span></span> <span data-ttu-id="8ef9f-105">Los roles proporcionan seguridad para los objetos y los datos de la base de datos modelo, ya que solo permiten el acceso a los usuarios que son miembros del rol.</span><span class="sxs-lookup"><span data-stu-id="8ef9f-105">Roles provide model database object and data security by limiting access to only those users that are role members.</span></span> <span data-ttu-id="8ef9f-106">Cada rol se define con un permiso único: Ninguno, Lectura, Lectura y procesamiento, Procesamiento o Administrador.</span><span class="sxs-lookup"><span data-stu-id="8ef9f-106">Each role is defined with a single permission: None, Read, Read and Process, Process, or Administrator.</span></span> <span data-ttu-id="8ef9f-107">Los roles se pueden definir durante la creación del modelo mediante el Administrador de roles.</span><span class="sxs-lookup"><span data-stu-id="8ef9f-107">Roles can be defined during model authoring by using Role Manager.</span></span> <span data-ttu-id="8ef9f-108">Una vez implementado un modelo, puede administrar roles mediante SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="8ef9f-108">After a model has been deployed, you can manage roles by using SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="8ef9f-109">Para obtener más información, vea [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="8ef9f-109">To learn more, see [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).</span></span>
  
> [!NOTE]  
> <span data-ttu-id="8ef9f-110">No es necesario crear roles para completar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="8ef9f-110">Creating roles is not necessary to complete this tutorial.</span></span> <span data-ttu-id="8ef9f-111">De forma predeterminada, la cuenta en la que ha iniciado sesión actualmente tiene privilegios de administrador en el modelo.</span><span class="sxs-lookup"><span data-stu-id="8ef9f-111">By default, the account you are currently logged in with has Administrator privileges on the model.</span></span> <span data-ttu-id="8ef9f-112">Pero para que otros usuarios de la organización naveguen mediante el uso de un cliente de creación de informes, debe crear al menos un rol con permisos de lectura y agregar a los usuarios como miembros.</span><span class="sxs-lookup"><span data-stu-id="8ef9f-112">However, for other users in your organization to browse by using a reporting client, you must create at least one role with Read permissions and add those users as members.</span></span>  
  
<span data-ttu-id="8ef9f-113">Se crean tres roles:</span><span class="sxs-lookup"><span data-stu-id="8ef9f-113">You create three roles:</span></span>  
  
-   <span data-ttu-id="8ef9f-114">**Director de ventas**: este rol puede incluir a los usuarios de la organización que quiere que tengan permiso de lectura en todos los objetos y datos del modelo.</span><span class="sxs-lookup"><span data-stu-id="8ef9f-114">**Sales Manager** – This role can include users in your organization for which you want to have Read permission to all model objects and data.</span></span>  
  
-   <span data-ttu-id="8ef9f-115">**Analista de ventas de EE. UU.**: este rol puede incluir a los usuarios de la organización que quiere que solo puedan examinar los datos relacionados con las ventas en Estados Unidos.</span><span class="sxs-lookup"><span data-stu-id="8ef9f-115">**Sales Analyst US** – This role can include users in your organization for which you want only to be able to browse data related to sales in the United States.</span></span> <span data-ttu-id="8ef9f-116">Para este rol se usa una fórmula DAX para definir un *filtro de fila* que hace que los miembros solo puedan examinar los datos de Estados Unidos.</span><span class="sxs-lookup"><span data-stu-id="8ef9f-116">For this role, you use a DAX formula to define a *Row Filter*, which restricts members to browse data only for the United States.</span></span>  
  
-   <span data-ttu-id="8ef9f-117">**Administrador**: este rol puede incluir a los usuarios que quiere que tengan permisos de administrador, lo que permite un acceso ilimitado y permisos para realizar tareas administrativas en la base de datos modelo.</span><span class="sxs-lookup"><span data-stu-id="8ef9f-117">**Administrator** – This role can include users for which you want to have Administrator permission, which allows unlimited access and permissions to perform administrative tasks on the model database.</span></span>  
  
<span data-ttu-id="8ef9f-118">Dado que las cuentas de usuario y de grupo de Windows de la organización son únicas, puede agregar cuentas de su propia organización a los miembros,</span><span class="sxs-lookup"><span data-stu-id="8ef9f-118">Because Windows user and group accounts in your organization are unique, you can add accounts from your particular organization to members.</span></span> <span data-ttu-id="8ef9f-119">Pero para este tutorial también puede dejar los miembros en blanco.</span><span class="sxs-lookup"><span data-stu-id="8ef9f-119">However, for this tutorial, you can also leave the members blank.</span></span> <span data-ttu-id="8ef9f-120">Más adelante en la Lección 12: Analizar en Excel se prueba el efecto de cada rol.</span><span class="sxs-lookup"><span data-stu-id="8ef9f-120">You test the effect of each role later in Lesson 12: Analyze in Excel.</span></span>  
  
<span data-ttu-id="8ef9f-121">Tiempo estimado para completar esta lección: **15 minutos**</span><span class="sxs-lookup"><span data-stu-id="8ef9f-121">Estimated time to complete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="8ef9f-122">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8ef9f-122">Prerequisites</span></span>  
<span data-ttu-id="8ef9f-123">Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden.</span><span class="sxs-lookup"><span data-stu-id="8ef9f-123">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="8ef9f-124">Antes de realizar las tareas de esta lección, debe haber completado la lección anterior: [Lección 10: Creación de particiones](../tutorials/aas-lesson-10-create-partitions.md).</span><span class="sxs-lookup"><span data-stu-id="8ef9f-124">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span>  
  
## <a name="create-roles"></a><span data-ttu-id="8ef9f-125">Creación de roles</span><span class="sxs-lookup"><span data-stu-id="8ef9f-125">Create roles</span></span>  
  
#### <a name="to-create-a-sales-manager-user-role"></a><span data-ttu-id="8ef9f-126">Para crear el rol de usuario Director de ventas</span><span class="sxs-lookup"><span data-stu-id="8ef9f-126">To create a Sales Manager user role</span></span>  
  
1.  <span data-ttu-id="8ef9f-127">En el Explorador de modelos tabulares, haga clic con el botón derecho en **Roles** > **Roles**.</span><span class="sxs-lookup"><span data-stu-id="8ef9f-127">In Tabular Model Explorer, right-click **Roles** > **Roles**.</span></span>  
  
2.  <span data-ttu-id="8ef9f-128">En el Administrador de roles, haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="8ef9f-128">In Role Manager, click **New**.</span></span>  
  
3.  <span data-ttu-id="8ef9f-129">Haga clic en el nuevo rol y en la columna **Nombre**, cambie el nombre del rol a **Jefe de ventas**.</span><span class="sxs-lookup"><span data-stu-id="8ef9f-129">Click the new role, and then in the **Name** column, rename the role to **Sales Manager**.</span></span>  
  
4.  <span data-ttu-id="8ef9f-130">En la columna **Permisos**, haga clic en la lista desplegable y, luego, seleccione el permiso **Lectura**.</span><span class="sxs-lookup"><span data-stu-id="8ef9f-130">In the **Permissions** column, click the dropdown list, and then select the **Read** permission.</span></span> 

    ![aas-lesson11-new-role](../tutorials/media/aas-lesson11-new-role.png) 
  
5.  <span data-ttu-id="8ef9f-132">Opcional: Haga clic en la pestaña **Miembros** y, luego, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="8ef9f-132">Optional: Click the **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="8ef9f-133">En el cuadro de diálogo **Seleccionar usuarios o grupos**, escriba los usuarios o grupos de Windows de la organización que quiere incluir en el rol.</span><span class="sxs-lookup"><span data-stu-id="8ef9f-133">In the **Select Users or Groups** dialog box, enter the Windows users or groups from your organization you want to include in the role.</span></span>  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a><span data-ttu-id="8ef9f-134">Para crear el rol de usuario Analista de ventas de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="8ef9f-134">To create a Sales Analyst US user role</span></span>  
  
1.  <span data-ttu-id="8ef9f-135">En el Administrador de roles, haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="8ef9f-135">In Role Manager, click **New**.</span></span>    
  
2.  <span data-ttu-id="8ef9f-136">Cambie el nombre del rol a **Analista de ventas de EE. UU.**</span><span class="sxs-lookup"><span data-stu-id="8ef9f-136">Rename the role to **Sales Analyst US**.</span></span>  
  
3.  <span data-ttu-id="8ef9f-137">Asigne a este rol el permiso **Lectura**.</span><span class="sxs-lookup"><span data-stu-id="8ef9f-137">Give this role **Read** permission.</span></span>  
  
4.  <span data-ttu-id="8ef9f-138">Haga clic en la pestaña Filtros de fila y, únicamente para la tabla **DimGeography**, escriba la fórmula siguiente en la columna Filtro DAX:</span><span class="sxs-lookup"><span data-stu-id="8ef9f-138">Click the Row Filters tab, and then for the **DimGeography** table only, in the DAX Filter column, type the following formula:</span></span>  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    <span data-ttu-id="8ef9f-139">Una fórmula de filtro de fila debe resolverse en un valor booleano (TRUE/FALSE).</span><span class="sxs-lookup"><span data-stu-id="8ef9f-139">A Row Filter formula must resolve to a Boolean (TRUE/FALSE) value.</span></span> <span data-ttu-id="8ef9f-140">Con esta fórmula se especifica que el usuario solo puede ver las filas con el valor "US" (EE. UU.) para el código de país o región.</span><span class="sxs-lookup"><span data-stu-id="8ef9f-140">With this formula, you are specifying that only rows with the Country Region Code value of “US” are visible to the user.</span></span>  
    ![aas-lesson11-role-filter](../tutorials/media/aas-lesson11-role-filter.png) 
  
6.  <span data-ttu-id="8ef9f-142">Opcional: Haga clic en la pestaña **Miembros** y, luego, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="8ef9f-142">Optional: Click the **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="8ef9f-143">En el cuadro de diálogo **Seleccionar usuarios o grupos**, escriba los usuarios o grupos de Windows de la organización que quiere incluir en el rol.</span><span class="sxs-lookup"><span data-stu-id="8ef9f-143">In the **Select Users or Groups** dialog box, enter the Windows users or groups from your organization you want to include in the role.</span></span>  
  
#### <a name="to-create-an-administrator-user-role"></a><span data-ttu-id="8ef9f-144">Para crear el rol de usuario Administrador</span><span class="sxs-lookup"><span data-stu-id="8ef9f-144">To create an Administrator user role</span></span>  
  
1.  <span data-ttu-id="8ef9f-145">Haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="8ef9f-145">Click **New**.</span></span>  
  
2.  <span data-ttu-id="8ef9f-146">Cambie el nombre del rol a **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="8ef9f-146">Rename the role to **Administrator**.</span></span>  
  
3.  <span data-ttu-id="8ef9f-147">Asigne a este rol el permiso **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="8ef9f-147">Give this role **Administrator** permission.</span></span>  
  
4.  <span data-ttu-id="8ef9f-148">Opcional: Haga clic en la pestaña **Miembros** y, luego, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="8ef9f-148">Optional: Click the **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="8ef9f-149">En el cuadro de diálogo **Seleccionar usuarios o grupos**, escriba los usuarios o grupos de Windows de la organización que quiere incluir en el rol.</span><span class="sxs-lookup"><span data-stu-id="8ef9f-149">In the **Select Users or Groups** dialog box, enter the Windows users or groups from your organization you want to include in the role.</span></span> 
  
  
## <a name="whats-next"></a><span data-ttu-id="8ef9f-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8ef9f-150">What's next?</span></span>
<span data-ttu-id="8ef9f-151">[Lección 12: Analizar en Excel](../tutorials/aas-lesson-12-analyze-in-excel.md)</span><span class="sxs-lookup"><span data-stu-id="8ef9f-151">[Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>

  
  
