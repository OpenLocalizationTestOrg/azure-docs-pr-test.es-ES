---
title: aaaGeneric conector de SQL paso a paso | Documentos de Microsoft
description: "En este artículo es recorrer a través de un sistema de recursos humanos simple utilizando paso a paso Hola conector de SQL genérico."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 28c1cc60-24fd-4d0d-a36d-b4aba6de86e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b1b5f89ab588de6f92f173a7bc00f97180067669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="generic-sql-connector-step-by-step"></a><span data-ttu-id="2198e-103">Conector de SQL genérico paso a paso</span><span class="sxs-lookup"><span data-stu-id="2198e-103">Generic SQL Connector step-by-step</span></span>
<span data-ttu-id="2198e-104">Este tema es una guía paso a paso.</span><span class="sxs-lookup"><span data-stu-id="2198e-104">This topic is a step-by-step guide.</span></span> <span data-ttu-id="2198e-105">Crea una sencilla base de datos de ejemplo de Recursos Humanos y la usa para importar algunos usuarios y su pertenencia a grupos.</span><span class="sxs-lookup"><span data-stu-id="2198e-105">It creates a simple sample HR database and use it for importing some users and their group membership.</span></span>

## <a name="prepare-hello-sample-database"></a><span data-ttu-id="2198e-106">Preparar la base de datos de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="2198e-106">Prepare hello sample database</span></span>
<span data-ttu-id="2198e-107">En un servidor que ejecuta SQL Server, ejecute el script SQL de Hola se encuentra en [Apéndice A](#appendix-a). Este script crea una base de datos de ejemplo con el nombre de hello GSQLDEMO.</span><span class="sxs-lookup"><span data-stu-id="2198e-107">On a server running SQL Server, run hello SQL script found in [Appendix A](#appendix-a). This script creates a sample database with hello name GSQLDEMO.</span></span> <span data-ttu-id="2198e-108">modelo de objetos de Hola para hello crea base de datos parece esta imagen:</span><span class="sxs-lookup"><span data-stu-id="2198e-108">hello object model for hello created database looks like this picture:</span></span>  
<span data-ttu-id="2198e-109">![Modelo de objetos](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span><span class="sxs-lookup"><span data-stu-id="2198e-109">![Object Model](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span></span>

<span data-ttu-id="2198e-110">Crear un usuario de base de datos de toouse tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="2198e-110">Also create a user you want toouse tooconnect toohello database.</span></span> <span data-ttu-id="2198e-111">En este tutorial, se denomina FABRIKAM\SQLUser usuario Hola y se encuentra en dominio Hola.</span><span class="sxs-lookup"><span data-stu-id="2198e-111">In this walkthrough, hello user is called FABRIKAM\SQLUser and located in hello domain.</span></span>

## <a name="create-hello-odbc-connection-file"></a><span data-ttu-id="2198e-112">Crear archivo de conexión de ODBC Hola</span><span class="sxs-lookup"><span data-stu-id="2198e-112">Create hello ODBC connection file</span></span>
<span data-ttu-id="2198e-113">Hola genérico conector de SQL está usando el servidor remoto de ODBC tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="2198e-113">hello Generic SQL Connector is using ODBC tooconnect toohello remote server.</span></span> <span data-ttu-id="2198e-114">Primero necesitamos toocreate un archivo con hello información de conexión de ODBC.</span><span class="sxs-lookup"><span data-stu-id="2198e-114">First we need toocreate a file with hello ODBC connection information.</span></span>

1. <span data-ttu-id="2198e-115">Iniciar la utilidad de administración de ODBC hello en el servidor:</span><span class="sxs-lookup"><span data-stu-id="2198e-115">Start hello ODBC management utility on your server:</span></span>  
   ![ODBC](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc.png)
2. <span data-ttu-id="2198e-117">Pestaña Hola seleccione **DSN de archivo**.</span><span class="sxs-lookup"><span data-stu-id="2198e-117">Select hello tab **File DSN**.</span></span> <span data-ttu-id="2198e-118">Haga clic en **Agregar...**.</span><span class="sxs-lookup"><span data-stu-id="2198e-118">Click **Add...**.</span></span>  
   <span data-ttu-id="2198e-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span><span class="sxs-lookup"><span data-stu-id="2198e-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span></span>
3. <span data-ttu-id="2198e-120">Hello out-of-box controlador funciona bien, por lo que selecciónelo y haga clic en **siguiente >**.</span><span class="sxs-lookup"><span data-stu-id="2198e-120">hello out-of-box driver works fine, so select it and click **Next>**.</span></span>  
   <span data-ttu-id="2198e-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span><span class="sxs-lookup"><span data-stu-id="2198e-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span></span>
4. <span data-ttu-id="2198e-122">Asigne un nombre, como de archivo hello **GenericSQL**.</span><span class="sxs-lookup"><span data-stu-id="2198e-122">Give hello file a name, such as **GenericSQL**.</span></span>  
   <span data-ttu-id="2198e-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span><span class="sxs-lookup"><span data-stu-id="2198e-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span></span>
5. <span data-ttu-id="2198e-124">Haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="2198e-124">Click **Finish**.</span></span>  
   <span data-ttu-id="2198e-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span><span class="sxs-lookup"><span data-stu-id="2198e-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span></span>
6. <span data-ttu-id="2198e-126">Conexión en tiempo de tooconfigure Hola.</span><span class="sxs-lookup"><span data-stu-id="2198e-126">Time tooconfigure hello connection.</span></span> <span data-ttu-id="2198e-127">Proporcionar una buena descripción de origen de datos de Hola y proporcione Hola nombre del servidor de Hola que ejecuta SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2198e-127">Give hello data source a good description and provide hello name of hello server running SQL Server.</span></span>  
   ![ODBC5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc5.png)
7. <span data-ttu-id="2198e-129">Seleccione cómo tooauthenticate con SQL.</span><span class="sxs-lookup"><span data-stu-id="2198e-129">Select how tooauthenticate with SQL.</span></span> <span data-ttu-id="2198e-130">En este caso, usaremos Autenticación de Windows.</span><span class="sxs-lookup"><span data-stu-id="2198e-130">In this case, we use Windows Authentication.</span></span>  
   ![ODBC6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc6.png)
8. <span data-ttu-id="2198e-132">Proporcione Hola nombre de base de datos de ejemplo de Hola **GSQLDEMO**.</span><span class="sxs-lookup"><span data-stu-id="2198e-132">Provide hello name of hello sample database, **GSQLDEMO**.</span></span>  
   <span data-ttu-id="2198e-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span><span class="sxs-lookup"><span data-stu-id="2198e-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span></span>
9. <span data-ttu-id="2198e-134">Mantenga las opciones predeterminadas de esta pantalla.</span><span class="sxs-lookup"><span data-stu-id="2198e-134">Keep everything default on this screen.</span></span> <span data-ttu-id="2198e-135">Haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="2198e-135">Click **Finish**.</span></span>  
   <span data-ttu-id="2198e-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span><span class="sxs-lookup"><span data-stu-id="2198e-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span></span>
10. <span data-ttu-id="2198e-137">tooverify que todo funciona según lo esperado, haga clic en **origen de datos de prueba**.</span><span class="sxs-lookup"><span data-stu-id="2198e-137">tooverify everything is working as expected, click **Test Data Source**.</span></span>  
    <span data-ttu-id="2198e-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span><span class="sxs-lookup"><span data-stu-id="2198e-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span></span>
11. <span data-ttu-id="2198e-139">Asegúrese de que la prueba de hello es correcta.</span><span class="sxs-lookup"><span data-stu-id="2198e-139">Make sure hello test is successful.</span></span>  
    ![ODBC10](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc10.png)
12. <span data-ttu-id="2198e-141">archivo de configuración de ODBC de Hello ahora debe estar visible en el DSN de archivo.</span><span class="sxs-lookup"><span data-stu-id="2198e-141">hello ODBC configuration file should now be visible in File DSN.</span></span>  
    ![ODBC11](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc11.png)

<span data-ttu-id="2198e-143">Ahora tenemos archivos de Hola se necesita y puede empezar a crear Hola conector.</span><span class="sxs-lookup"><span data-stu-id="2198e-143">We now have hello file we need and can start creating hello Connector.</span></span>

## <a name="create-hello-generic-sql-connector"></a><span data-ttu-id="2198e-144">Crear hello conector de SQL genérico</span><span class="sxs-lookup"><span data-stu-id="2198e-144">Create hello Generic SQL Connector</span></span>
1. <span data-ttu-id="2198e-145">Hola UI Synchronization Service Manager, seleccione **conectores** y **crear**.</span><span class="sxs-lookup"><span data-stu-id="2198e-145">In hello Synchronization Service Manager UI, select **Connectors** and **Create**.</span></span> <span data-ttu-id="2198e-146">Seleccione **SQL genérico (Microsoft)** y asígnele un nombre descriptivo.</span><span class="sxs-lookup"><span data-stu-id="2198e-146">Select **Generic SQL (Microsoft)** and give it a descriptive name.</span></span>  
   <span data-ttu-id="2198e-147">![Conector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span><span class="sxs-lookup"><span data-stu-id="2198e-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span></span>
2. <span data-ttu-id="2198e-148">Buscar archivo DSN de hello que creó en la sección anterior de Hola y cargarlo toohello server.</span><span class="sxs-lookup"><span data-stu-id="2198e-148">Find hello DSN file you created in hello previous section and upload it toohello server.</span></span> <span data-ttu-id="2198e-149">Proporcionar la base de datos de hello credenciales tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="2198e-149">Provide hello credentials tooconnect toohello database.</span></span>  
   ![Conector2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector2.png)
3. <span data-ttu-id="2198e-151">En este tutorial, hemos optado por una opción sencilla y hemos tenido en cuenta que hay dos tipos de objetos, **User** y **Group**.</span><span class="sxs-lookup"><span data-stu-id="2198e-151">In this walkthrough, we are making it easy for us and say that there are two object types, **User** and **Group**.</span></span>
   <span data-ttu-id="2198e-152">![Conector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span><span class="sxs-lookup"><span data-stu-id="2198e-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span></span>
4. <span data-ttu-id="2198e-153">atributos de hello toofind, queremos Hola conector toodetect esos atributos examinando la propia tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="2198e-153">toofind hello attributes, we want hello Connector toodetect those attributes by looking at hello table itself.</span></span> <span data-ttu-id="2198e-154">Puesto que **usuarios** es una palabra reservada en SQL, necesitamos tooprovide en cuadrado corchetes [].</span><span class="sxs-lookup"><span data-stu-id="2198e-154">Since **Users** is a reserved word in SQL, we need tooprovide it in square brackets [ ].</span></span>  
   <span data-ttu-id="2198e-155">![Conector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span><span class="sxs-lookup"><span data-stu-id="2198e-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span></span>
5. <span data-ttu-id="2198e-156">Atributo de delimitador de tiempo toodefine hello y atributo DN de Hola.</span><span class="sxs-lookup"><span data-stu-id="2198e-156">Time toodefine hello anchor attribute and hello DN attribute.</span></span> <span data-ttu-id="2198e-157">Para **usuarios**, usamos la combinación de Hola de nombre de usuario de hello dos atributos y EmployeeID.</span><span class="sxs-lookup"><span data-stu-id="2198e-157">For **Users**, we use hello combination of hello two attributes username and EmployeeID.</span></span> <span data-ttu-id="2198e-158">Para **Group**, usamos GroupName (aunque no sea muy realista para la vida real, para este tutorial funciona).</span><span class="sxs-lookup"><span data-stu-id="2198e-158">For **group**, we use GroupName (not realistic in real-life, but for this walkthrough it works).</span></span>
   <span data-ttu-id="2198e-159">![Conector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span><span class="sxs-lookup"><span data-stu-id="2198e-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span></span>
6. <span data-ttu-id="2198e-160">No todos los tipos de atributo se pueden detectar en una base de datos SQL,</span><span class="sxs-lookup"><span data-stu-id="2198e-160">Not all attribute types can be detected in a SQL database.</span></span> <span data-ttu-id="2198e-161">tipo de atributo de referencia de Hello en particular no puede.</span><span class="sxs-lookup"><span data-stu-id="2198e-161">hello reference attribute type in particular cannot.</span></span> <span data-ttu-id="2198e-162">Para tipo de objeto de grupo de hello, necesitamos toochange Hola OwnerID y MemberID tooreference.</span><span class="sxs-lookup"><span data-stu-id="2198e-162">For hello group object type, we need toochange hello OwnerID and MemberID tooreference.</span></span>  
   ![Conector6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector6.png)
7. <span data-ttu-id="2198e-164">atributos de Hello seleccionamos como atributos de referencia en el paso anterior de hello requieren estos valores son una referencia al tipo de objeto de Hola.</span><span class="sxs-lookup"><span data-stu-id="2198e-164">hello attributes we selected as reference attributes in hello previous step require hello object type these values are a reference to.</span></span> <span data-ttu-id="2198e-165">En nuestro caso, Hola tipo de objeto de usuario.</span><span class="sxs-lookup"><span data-stu-id="2198e-165">In our case, hello User object type.</span></span>  
   ![Conector7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector7.png)
8. <span data-ttu-id="2198e-167">En la página de parámetros globales de hello, seleccione **marca de agua** como estrategia de hello delta.</span><span class="sxs-lookup"><span data-stu-id="2198e-167">On hello Global Parameters page, select **Watermark** as hello delta strategy.</span></span> <span data-ttu-id="2198e-168">Escribir en formato de fecha y hora de hello **aaaa-MM-dd hh**.</span><span class="sxs-lookup"><span data-stu-id="2198e-168">Also type in hello date/time format **yyyy-MM-dd HH:mm:ss**.</span></span>
   <span data-ttu-id="2198e-169">![Conector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span><span class="sxs-lookup"><span data-stu-id="2198e-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span></span>
9. <span data-ttu-id="2198e-170">En hello **configurar particiones y jerarquías** , seleccione ambos tipos de objeto.</span><span class="sxs-lookup"><span data-stu-id="2198e-170">On hello **Configure Partitions and Hierarchies** page, select both object types.</span></span>
   <span data-ttu-id="2198e-171">![Conector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span><span class="sxs-lookup"><span data-stu-id="2198e-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span></span>
10. <span data-ttu-id="2198e-172">En hello **seleccionar tipos de objeto** y **seleccionar los atributos**, seleccione los tipos de objeto y todos los atributos.</span><span class="sxs-lookup"><span data-stu-id="2198e-172">On hello **Select Object Types** and **Select Attributes**, select both object types and all attributes.</span></span> <span data-ttu-id="2198e-173">En hello **configurar delimitadores** página, haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="2198e-173">On hello **Configure Anchors** page, click **Finish**.</span></span>

## <a name="create-run-profiles"></a><span data-ttu-id="2198e-174">Creación de perfiles de ejecución</span><span class="sxs-lookup"><span data-stu-id="2198e-174">Create Run Profiles</span></span>
1. <span data-ttu-id="2198e-175">Hola UI Synchronization Service Manager, seleccione **conectores**, y **configurar perfiles de ejecución**.</span><span class="sxs-lookup"><span data-stu-id="2198e-175">In hello Synchronization Service Manager UI, select **Connectors**, and **Configure Run Profiles**.</span></span> <span data-ttu-id="2198e-176">Haga clic en **New Profile**(Nuevo perfil).</span><span class="sxs-lookup"><span data-stu-id="2198e-176">Click **New Profile**.</span></span> <span data-ttu-id="2198e-177">Comenzaremos por **Full Import**(Importación completa).</span><span class="sxs-lookup"><span data-stu-id="2198e-177">We start with **Full Import**.</span></span>  
   <span data-ttu-id="2198e-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span><span class="sxs-lookup"><span data-stu-id="2198e-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span></span>
2. <span data-ttu-id="2198e-179">Seleccione el tipo de hello **importación completa (solo etapa)**.</span><span class="sxs-lookup"><span data-stu-id="2198e-179">Select hello type **Full Import (Stage Only)**.</span></span>  
   <span data-ttu-id="2198e-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span><span class="sxs-lookup"><span data-stu-id="2198e-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span></span>
3. <span data-ttu-id="2198e-181">Seleccione la partición de hello **objeto = usuario**.</span><span class="sxs-lookup"><span data-stu-id="2198e-181">Select hello partition **OBJECT=User**.</span></span>  
   <span data-ttu-id="2198e-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span><span class="sxs-lookup"><span data-stu-id="2198e-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span></span>
4. <span data-ttu-id="2198e-183">Seleccione **Table** (Tabla) y escriba **[USERS]**.</span><span class="sxs-lookup"><span data-stu-id="2198e-183">Select **Table** and type **[USERS]**.</span></span> <span data-ttu-id="2198e-184">Desplácese hacia abajo de la sección de tipo de objeto con varios valores de toohello y escriba datos Hola Hola después de la imagen.</span><span class="sxs-lookup"><span data-stu-id="2198e-184">Scroll down toohello multi-valued object type section and enter hello data as in hello following picture.</span></span> <span data-ttu-id="2198e-185">Seleccione **finalizar** paso de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="2198e-185">Select **Finish** toosave hello step.</span></span>  
   <span data-ttu-id="2198e-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span><span class="sxs-lookup"><span data-stu-id="2198e-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span></span>  
   <span data-ttu-id="2198e-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span><span class="sxs-lookup"><span data-stu-id="2198e-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span></span>  
5. <span data-ttu-id="2198e-188">Seleccione **New step**(Nuevo paso).</span><span class="sxs-lookup"><span data-stu-id="2198e-188">Select **New Step**.</span></span> <span data-ttu-id="2198e-189">Esta vez, seleccione **OBJECT=Group**.</span><span class="sxs-lookup"><span data-stu-id="2198e-189">This time, select **OBJECT=Group**.</span></span> <span data-ttu-id="2198e-190">En la última página de hello, utilice la configuración de hello en hello después de la imagen.</span><span class="sxs-lookup"><span data-stu-id="2198e-190">On hello last page, use hello configuration as in hello following picture.</span></span> <span data-ttu-id="2198e-191">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="2198e-191">Click **Finish**.</span></span>  
   <span data-ttu-id="2198e-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span><span class="sxs-lookup"><span data-stu-id="2198e-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span></span>  
   <span data-ttu-id="2198e-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span><span class="sxs-lookup"><span data-stu-id="2198e-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span></span>  
6. <span data-ttu-id="2198e-194">Opcional: si lo desea, puede configurar perfiles de ejecución adicionales.</span><span class="sxs-lookup"><span data-stu-id="2198e-194">Optional: If you want to, you can configure additional run profiles.</span></span> <span data-ttu-id="2198e-195">En este tutorial, se usa solo Hola importación completa.</span><span class="sxs-lookup"><span data-stu-id="2198e-195">For this walkthrough, only hello Full Import is used.</span></span>
7. <span data-ttu-id="2198e-196">Haga clic en **Aceptar** toofinish cambiar perfiles de ejecución.</span><span class="sxs-lookup"><span data-stu-id="2198e-196">Click **OK** toofinish changing run profiles.</span></span>

## <a name="add-some-test-data-and-test-hello-import"></a><span data-ttu-id="2198e-197">Agregue algunos importación de Hola de datos y de prueba de prueba</span><span class="sxs-lookup"><span data-stu-id="2198e-197">Add some test data and test hello import</span></span>
<span data-ttu-id="2198e-198">Rellene algunos datos de prueba en la base de datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="2198e-198">Fill out some test data in your sample database.</span></span> <span data-ttu-id="2198e-199">Cuando haya terminado, seleccione **Run** (Ejecutar) y **Full import** (Importación completa).</span><span class="sxs-lookup"><span data-stu-id="2198e-199">When you are ready, select **Run** and **Full import**.</span></span>

<span data-ttu-id="2198e-200">Este usuario tiene dos números de teléfono y un grupo con algunos miembros.</span><span class="sxs-lookup"><span data-stu-id="2198e-200">Here is a user with two phone numbers and a group with some members.</span></span>  
![cs1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs1.png)  
![cs2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs2.png)  

## <a name="appendix-a"></a><span data-ttu-id="2198e-203">Apéndice A</span><span class="sxs-lookup"><span data-stu-id="2198e-203">Appendix A</span></span>
<span data-ttu-id="2198e-204">**Base de datos de ejemplo de Hola de toocreate SQL script**</span><span class="sxs-lookup"><span data-stu-id="2198e-204">**SQL script toocreate hello sample database**</span></span>

```SQL
---Creating hello Database---------
Create Database GSQLDEMO
Go
-------Using hello Database-----------
Use [GSQLDEMO]
Go
-------------------------------------
USE [GSQLDEMO]
GO
/****** Object:  Table [dbo].[GroupMembers]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GroupMembers](
    [MemberID] [int] NOT NULL,
    [Group_ID] [int] NOT NULL
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[GROUPS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GROUPS](
    [GroupID] [int] NOT NULL,
    [GROUPNAME] [nvarchar](200) NOT NULL,
    [DESCRIPTION] [nvarchar](200) NULL,
    [WATERMARK] [datetime] NULL,
    [OwnerID] [int] NULL,
PRIMARY KEY CLUSTERED
(
    [GroupID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[USERPHONE]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
SET ANSI_PADDING ON
GO
CREATE TABLE [dbo].[USERPHONE](
    [USER_ID] [int] NULL,
    [Phone] [varchar](20) NULL
) ON [PRIMARY]

GO
SET ANSI_PADDING OFF
GO
/****** Object:  Table [dbo].[USERS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[USERS](
    [USERID] [int] NOT NULL,
    [USERNAME] [nvarchar](200) NOT NULL,
    [FirstName] [nvarchar](100) NULL,
    [LastName] [nvarchar](100) NULL,
    [DisplayName] [nvarchar](100) NULL,
    [ACCOUNTDISABLED] [bit] NULL,
    [EMPLOYEEID] [int] NOT NULL,
    [WATERMARK] [datetime] NULL,
PRIMARY KEY CLUSTERED
(
    [USERID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_GROUPS] FOREIGN KEY([Group_ID])
REFERENCES [dbo].[GROUPS] ([GroupID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_GROUPS]
GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_USERS] FOREIGN KEY([MemberID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_USERS]
GO
ALTER TABLE [dbo].[GROUPS]  WITH CHECK ADD  CONSTRAINT [FK_GROUPS_USERS] FOREIGN KEY([OwnerID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GROUPS] CHECK CONSTRAINT [FK_GROUPS_USERS]
GO
ALTER TABLE [dbo].[USERPHONE]  WITH CHECK ADD  CONSTRAINT [FK_USERPHONE_USER] FOREIGN KEY([USER_ID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[USERPHONE] CHECK CONSTRAINT [FK_USERPHONE_USER]
GO
```
