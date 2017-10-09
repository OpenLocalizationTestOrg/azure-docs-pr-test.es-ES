---
<span data-ttu-id="67eac-101">título: aaa "lección tutorial de Analysis Services de Azure 11: crear roles | Descripción de Microsoft Docs": describe cómo toocreate roles en Hola proyecto tutorial de Analysis Services de Azure.</span><span class="sxs-lookup"><span data-stu-id="67eac-101">title: aaa"Azure Analysis Services tutorial lesson 11: Create roles | Microsoft Docs" description: Describes how toocreate roles in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="67eac-102">servicios: documentationcenter de analysis services: '' autor: minewiskan manager: erikre editor: '' etiquetas: ''</span><span class="sxs-lookup"><span data-stu-id="67eac-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="67eac-103">MS.AssetId: ms.service: ms.devlang de analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 26/05/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="67eac-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-11-create-roles"></a><span data-ttu-id="67eac-104">Lección 11: Creación de roles</span><span class="sxs-lookup"><span data-stu-id="67eac-104">Lesson 11: Create roles</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="67eac-105">En esta lección, creará roles.</span><span class="sxs-lookup"><span data-stu-id="67eac-105">In this lesson, you create roles.</span></span> <span data-ttu-id="67eac-106">Los roles proporcionan seguridad de objetos y datos de la base de datos de modelo limitando tooonly de acceso a los usuarios que sean miembros del rol.</span><span class="sxs-lookup"><span data-stu-id="67eac-106">Roles provide model database object and data security by limiting access tooonly those users that are role members.</span></span> <span data-ttu-id="67eac-107">Cada rol se define con un permiso único: Ninguno, Lectura, Lectura y procesamiento, Procesamiento o Administrador.</span><span class="sxs-lookup"><span data-stu-id="67eac-107">Each role is defined with a single permission: None, Read, Read and Process, Process, or Administrator.</span></span> <span data-ttu-id="67eac-108">Los roles se pueden definir durante la creación del modelo mediante el Administrador de roles.</span><span class="sxs-lookup"><span data-stu-id="67eac-108">Roles can be defined during model authoring by using Role Manager.</span></span> <span data-ttu-id="67eac-109">Una vez implementado un modelo, puede administrar roles mediante SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="67eac-109">After a model has been deployed, you can manage roles by using SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="67eac-110">más información, consulte toolearn [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="67eac-110">toolearn more, see [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).</span></span>
  
> [!NOTE]  
> <span data-ttu-id="67eac-111">Creación de funciones es toocomplete no es necesario en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="67eac-111">Creating roles is not necessary toocomplete this tutorial.</span></span> <span data-ttu-id="67eac-112">De forma predeterminada, cuenta de hello que ha iniciado sesión con tiene privilegios de administrador en el modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="67eac-112">By default, hello account you are currently logged in with has Administrator privileges on hello model.</span></span> <span data-ttu-id="67eac-113">Sin embargo, para otros usuarios en su toobrowse de organización mediante el uso de un cliente de informes, debe crear al menos un rol con lectura permisos y agregar los usuarios como miembros.</span><span class="sxs-lookup"><span data-stu-id="67eac-113">However, for other users in your organization toobrowse by using a reporting client, you must create at least one role with Read permissions and add those users as members.</span></span>  
  
<span data-ttu-id="67eac-114">Se crean tres roles:</span><span class="sxs-lookup"><span data-stu-id="67eac-114">You create three roles:</span></span>  
  
-   <span data-ttu-id="67eac-115">**Director de ventas** : este rol puede incluir a los usuarios de su organización para la que desea que objetos de modelo de tooall de permiso de lectura de toohave y los datos.</span><span class="sxs-lookup"><span data-stu-id="67eac-115">**Sales Manager** – This role can include users in your organization for which you want toohave Read permission tooall model objects and data.</span></span>  
  
-   <span data-ttu-id="67eac-116">**Analista de ventas EE. UU.** : este rol puede incluir a los usuarios de su organización para la que desea que sólo toobe toobrowse capaz de datos relacionados con toosales Hola Estados Unidos.</span><span class="sxs-lookup"><span data-stu-id="67eac-116">**Sales Analyst US** – This role can include users in your organization for which you want only toobe able toobrowse data related toosales in hello United States.</span></span> <span data-ttu-id="67eac-117">Para este rol, use un toodefine de fórmulas de DAX un *filtro de fila*, lo que restringe los miembros toobrowse únicamente los datos de hello Estados Unidos.</span><span class="sxs-lookup"><span data-stu-id="67eac-117">For this role, you use a DAX formula toodefine a *Row Filter*, which restricts members toobrowse data only for hello United States.</span></span>  
  
-   <span data-ttu-id="67eac-118">**Administrador** : este rol puede incluir a los usuarios para el que desea que los permisos de administrador de toohave, lo que permite acceso ilimitado y permisos de las tareas administrativas de tooperform en la base de datos de modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="67eac-118">**Administrator** – This role can include users for which you want toohave Administrator permission, which allows unlimited access and permissions tooperform administrative tasks on hello model database.</span></span>  
  
<span data-ttu-id="67eac-119">Dado que las cuentas de usuario y de grupo de Windows de su organización son únicas, puede agregar cuentas de su propia organización toomembers.</span><span class="sxs-lookup"><span data-stu-id="67eac-119">Because Windows user and group accounts in your organization are unique, you can add accounts from your particular organization toomembers.</span></span> <span data-ttu-id="67eac-120">Sin embargo, para este tutorial, también puede dejar a los miembros de hello en blanco.</span><span class="sxs-lookup"><span data-stu-id="67eac-120">However, for this tutorial, you can also leave hello members blank.</span></span> <span data-ttu-id="67eac-121">Probar el efecto Hola de cada rol más adelante en la lección 12: analizar en Excel.</span><span class="sxs-lookup"><span data-stu-id="67eac-121">You test hello effect of each role later in Lesson 12: Analyze in Excel.</span></span>  
  
<span data-ttu-id="67eac-122">Estimado toocomplete de tiempo en esta lección: **15 minutos**</span><span class="sxs-lookup"><span data-stu-id="67eac-122">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="67eac-123">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="67eac-123">Prerequisites</span></span>  
<span data-ttu-id="67eac-124">Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden.</span><span class="sxs-lookup"><span data-stu-id="67eac-124">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="67eac-125">Antes de realizar tareas de hello en esta lección, debe haber completado la lección anterior hello: [lección 10: crear particiones](../tutorials/aas-lesson-10-create-partitions.md).</span><span class="sxs-lookup"><span data-stu-id="67eac-125">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span>  
  
## <a name="create-roles"></a><span data-ttu-id="67eac-126">Creación de roles</span><span class="sxs-lookup"><span data-stu-id="67eac-126">Create roles</span></span>  
  
#### <a name="toocreate-a-sales-manager-user-role"></a><span data-ttu-id="67eac-127">toocreate un rol de usuario de administrador de ventas</span><span class="sxs-lookup"><span data-stu-id="67eac-127">toocreate a Sales Manager user role</span></span>  
  
1.  <span data-ttu-id="67eac-128">En el Explorador de modelos tabulares, haga clic con el botón derecho en **Roles** > **Roles**.</span><span class="sxs-lookup"><span data-stu-id="67eac-128">In Tabular Model Explorer, right-click **Roles** > **Roles**.</span></span>  
  
2.  <span data-ttu-id="67eac-129">En el Administrador de roles, haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="67eac-129">In Role Manager, click **New**.</span></span>  
  
3.  <span data-ttu-id="67eac-130">Haga clic en nuevo rol de hello y, a continuación, en hello **nombre** columna, cambie el nombre de rol de hello demasiado**Sales Manager**.</span><span class="sxs-lookup"><span data-stu-id="67eac-130">Click hello new role, and then in hello **Name** column, rename hello role too**Sales Manager**.</span></span>  
  
4.  <span data-ttu-id="67eac-131">Hola **permisos** columna, haga clic en la lista desplegable de hello y, a continuación, seleccione hello **lectura** permiso.</span><span class="sxs-lookup"><span data-stu-id="67eac-131">In hello **Permissions** column, click hello dropdown list, and then select hello **Read** permission.</span></span> 

    ![aas-lesson11-new-role](../tutorials/media/aas-lesson11-new-role.png) 
  
5.  <span data-ttu-id="67eac-133">Opcional: Haga clic en hello **miembros** ficha y, a continuación, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="67eac-133">Optional: Click hello **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="67eac-134">Hola **Seleccionar usuarios o grupos** diálogo cuadro, escriba Hola Windows usuarios o grupos de su organización desea tooinclude en función de Hola.</span><span class="sxs-lookup"><span data-stu-id="67eac-134">In hello **Select Users or Groups** dialog box, enter hello Windows users or groups from your organization you want tooinclude in hello role.</span></span>  
  
#### <a name="toocreate-a-sales-analyst-us-user-role"></a><span data-ttu-id="67eac-135">toocreate un rol de usuario analista de ventas EE. UU.</span><span class="sxs-lookup"><span data-stu-id="67eac-135">toocreate a Sales Analyst US user role</span></span>  
  
1.  <span data-ttu-id="67eac-136">En el Administrador de roles, haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="67eac-136">In Role Manager, click **New**.</span></span>    
  
2.  <span data-ttu-id="67eac-137">Cambiar el nombre de rol de hello demasiado**analista de ventas EE. UU.**.</span><span class="sxs-lookup"><span data-stu-id="67eac-137">Rename hello role too**Sales Analyst US**.</span></span>  
  
3.  <span data-ttu-id="67eac-138">Asigne a este rol el permiso **Lectura**.</span><span class="sxs-lookup"><span data-stu-id="67eac-138">Give this role **Read** permission.</span></span>  
  
4.  <span data-ttu-id="67eac-139">Haga clic en la pestaña Filtros de fila de hello y, a continuación, para hello **DimGeography** tabla solo, en una columna de filtro de DAX hello, Hola de tipo siguiente fórmula:</span><span class="sxs-lookup"><span data-stu-id="67eac-139">Click hello Row Filters tab, and then for hello **DimGeography** table only, in hello DAX Filter column, type hello following formula:</span></span>  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    <span data-ttu-id="67eac-140">Fórmula de un filtro de fila debe resolver el valor de un valor booleano (verdadero/falso) tooa.</span><span class="sxs-lookup"><span data-stu-id="67eac-140">A Row Filter formula must resolve tooa Boolean (TRUE/FALSE) value.</span></span> <span data-ttu-id="67eac-141">Con esta fórmula, se especifica que sólo las filas con valor de código de región del país hello de "US" están usuario de toohello visible.</span><span class="sxs-lookup"><span data-stu-id="67eac-141">With this formula, you are specifying that only rows with hello Country Region Code value of “US” are visible toohello user.</span></span>  
    ![aas-lesson11-role-filter](../tutorials/media/aas-lesson11-role-filter.png) 
  
6.  <span data-ttu-id="67eac-143">Opcional: Haga clic en hello **miembros** ficha y, a continuación, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="67eac-143">Optional: Click hello **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="67eac-144">Hola **Seleccionar usuarios o grupos** diálogo cuadro, escriba Hola Windows usuarios o grupos de su organización desea tooinclude en función de Hola.</span><span class="sxs-lookup"><span data-stu-id="67eac-144">In hello **Select Users or Groups** dialog box, enter hello Windows users or groups from your organization you want tooinclude in hello role.</span></span>  
  
#### <a name="toocreate-an-administrator-user-role"></a><span data-ttu-id="67eac-145">toocreate un rol de usuario de administrador</span><span class="sxs-lookup"><span data-stu-id="67eac-145">toocreate an Administrator user role</span></span>  
  
1.  <span data-ttu-id="67eac-146">Haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="67eac-146">Click **New**.</span></span>  
  
2.  <span data-ttu-id="67eac-147">Cambiar el nombre de rol de hello demasiado**administrador**.</span><span class="sxs-lookup"><span data-stu-id="67eac-147">Rename hello role too**Administrator**.</span></span>  
  
3.  <span data-ttu-id="67eac-148">Asigne a este rol el permiso **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="67eac-148">Give this role **Administrator** permission.</span></span>  
  
4.  <span data-ttu-id="67eac-149">Opcional: Haga clic en hello **miembros** ficha y, a continuación, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="67eac-149">Optional: Click hello **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="67eac-150">Hola **Seleccionar usuarios o grupos** diálogo cuadro, escriba Hola Windows usuarios o grupos de su organización desea tooinclude en función de Hola.</span><span class="sxs-lookup"><span data-stu-id="67eac-150">In hello **Select Users or Groups** dialog box, enter hello Windows users or groups from your organization you want tooinclude in hello role.</span></span> 
  
  
## <a name="whats-next"></a><span data-ttu-id="67eac-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="67eac-151">What's next?</span></span>
<span data-ttu-id="67eac-152">[Lección 12: Analizar en Excel](../tutorials/aas-lesson-12-analyze-in-excel.md)</span><span class="sxs-lookup"><span data-stu-id="67eac-152">[Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>

  
  
