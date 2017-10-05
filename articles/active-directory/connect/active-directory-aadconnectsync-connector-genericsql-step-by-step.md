---
title: "Conector de SQL genérico paso a paso | Microsoft Docs"
description: "Este artículo le guía paso a paso por un sencillo sistema de Recursos Humanos con el Conector de SQL genérico."
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
ms.openlocfilehash: 3fdc1b405b95180d031aa4ad45b406f7fc149d8f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="generic-sql-connector-step-by-step"></a><span data-ttu-id="dbd65-103">Conector de SQL genérico paso a paso</span><span class="sxs-lookup"><span data-stu-id="dbd65-103">Generic SQL Connector step-by-step</span></span>
<span data-ttu-id="dbd65-104">Este tema es una guía paso a paso.</span><span class="sxs-lookup"><span data-stu-id="dbd65-104">This topic is a step-by-step guide.</span></span> <span data-ttu-id="dbd65-105">Crea una sencilla base de datos de ejemplo de Recursos Humanos y la usa para importar algunos usuarios y su pertenencia a grupos.</span><span class="sxs-lookup"><span data-stu-id="dbd65-105">It creates a simple sample HR database and use it for importing some users and their group membership.</span></span>

## <a name="prepare-the-sample-database"></a><span data-ttu-id="dbd65-106">Preparación de la base de datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="dbd65-106">Prepare the sample database</span></span>
<span data-ttu-id="dbd65-107">En un servidor que esté ejecutando SQL Server, ejecute el script de SQL que encontrará en el [Apéndice A](#appendix-a). Este script crea una base de datos de ejemplo con el nombre GSQLDEMO.</span><span class="sxs-lookup"><span data-stu-id="dbd65-107">On a server running SQL Server, run the SQL script found in [Appendix A](#appendix-a). This script creates a sample database with the name GSQLDEMO.</span></span> <span data-ttu-id="dbd65-108">El modelo de objetos de la base de datos creada es similar al de esta imagen: </span><span class="sxs-lookup"><span data-stu-id="dbd65-108">The object model for the created database looks like this picture:</span></span>  
<span data-ttu-id="dbd65-109">![Modelo de objetos](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span><span class="sxs-lookup"><span data-stu-id="dbd65-109">![Object Model](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span></span>

<span data-ttu-id="dbd65-110">Cree también el usuario que quiera usar para conectarse a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="dbd65-110">Also create a user you want to use to connect to the database.</span></span> <span data-ttu-id="dbd65-111">En este tutorial, el usuario se llama FABRIKAM\SQLUser y está ubicado en el dominio.</span><span class="sxs-lookup"><span data-stu-id="dbd65-111">In this walkthrough, the user is called FABRIKAM\SQLUser and located in the domain.</span></span>

## <a name="create-the-odbc-connection-file"></a><span data-ttu-id="dbd65-112">Creación del archivo de conexión de ODBC</span><span class="sxs-lookup"><span data-stu-id="dbd65-112">Create the ODBC connection file</span></span>
<span data-ttu-id="dbd65-113">El conector de SQL genérico usa ODBC para conectarse al servidor remoto.</span><span class="sxs-lookup"><span data-stu-id="dbd65-113">The Generic SQL Connector is using ODBC to connect to the remote server.</span></span> <span data-ttu-id="dbd65-114">Primero debemos crear un archivo con la información de conexión de ODBC.</span><span class="sxs-lookup"><span data-stu-id="dbd65-114">First we need to create a file with the ODBC connection information.</span></span>

1. <span data-ttu-id="dbd65-115">Inicie la utilidad de administración de ODBC en el servidor: </span><span class="sxs-lookup"><span data-stu-id="dbd65-115">Start the ODBC management utility on your server:</span></span>  
   ![ODBC](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc.png)
2. <span data-ttu-id="dbd65-117">Seleccione la pestaña **DSN de archivo**.</span><span class="sxs-lookup"><span data-stu-id="dbd65-117">Select the tab **File DSN**.</span></span> <span data-ttu-id="dbd65-118">Haga clic en **Agregar...**.</span><span class="sxs-lookup"><span data-stu-id="dbd65-118">Click **Add...**.</span></span>  
   <span data-ttu-id="dbd65-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span><span class="sxs-lookup"><span data-stu-id="dbd65-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span></span>
3. <span data-ttu-id="dbd65-120">El controlador integrado funciona correctamente, así que selecciónelo y haga clic en **Siguiente>**.</span><span class="sxs-lookup"><span data-stu-id="dbd65-120">The out-of-box driver works fine, so select it and click **Next>**.</span></span>  
   <span data-ttu-id="dbd65-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span><span class="sxs-lookup"><span data-stu-id="dbd65-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span></span>
4. <span data-ttu-id="dbd65-122">Asigne un nombre al archivo, como **GenericSQL**.</span><span class="sxs-lookup"><span data-stu-id="dbd65-122">Give the file a name, such as **GenericSQL**.</span></span>  
   <span data-ttu-id="dbd65-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span><span class="sxs-lookup"><span data-stu-id="dbd65-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span></span>
5. <span data-ttu-id="dbd65-124">Haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="dbd65-124">Click **Finish**.</span></span>  
   <span data-ttu-id="dbd65-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span><span class="sxs-lookup"><span data-stu-id="dbd65-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span></span>
6. <span data-ttu-id="dbd65-126">Ahora configuraremos la conexión.</span><span class="sxs-lookup"><span data-stu-id="dbd65-126">Time to configure the connection.</span></span> <span data-ttu-id="dbd65-127">Escriba una buena descripción para el origen de datos, así como el nombre del servidor que ejecuta SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dbd65-127">Give the data source a good description and provide the name of the server running SQL Server.</span></span>  
   ![ODBC5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc5.png)
7. <span data-ttu-id="dbd65-129">Seleccione la autenticación de SQL.</span><span class="sxs-lookup"><span data-stu-id="dbd65-129">Select how to authenticate with SQL.</span></span> <span data-ttu-id="dbd65-130">En este caso, usaremos Autenticación de Windows.</span><span class="sxs-lookup"><span data-stu-id="dbd65-130">In this case, we use Windows Authentication.</span></span>  
   ![ODBC6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc6.png)
8. <span data-ttu-id="dbd65-132">Proporcione el nombre de la base de datos de ejemplo, **GSQLDEMO**.</span><span class="sxs-lookup"><span data-stu-id="dbd65-132">Provide the name of the sample database, **GSQLDEMO**.</span></span>  
   <span data-ttu-id="dbd65-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span><span class="sxs-lookup"><span data-stu-id="dbd65-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span></span>
9. <span data-ttu-id="dbd65-134">Mantenga las opciones predeterminadas de esta pantalla.</span><span class="sxs-lookup"><span data-stu-id="dbd65-134">Keep everything default on this screen.</span></span> <span data-ttu-id="dbd65-135">Haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="dbd65-135">Click **Finish**.</span></span>  
   <span data-ttu-id="dbd65-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span><span class="sxs-lookup"><span data-stu-id="dbd65-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span></span>
10. <span data-ttu-id="dbd65-137">Para comprobar que todo funciona según lo esperado, haga clic en **Probar origen de datos**.</span><span class="sxs-lookup"><span data-stu-id="dbd65-137">To verify everything is working as expected, click **Test Data Source**.</span></span>  
    <span data-ttu-id="dbd65-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span><span class="sxs-lookup"><span data-stu-id="dbd65-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span></span>
11. <span data-ttu-id="dbd65-139">Asegúrese de que la prueba se ha realizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="dbd65-139">Make sure the test is successful.</span></span>  
    ![ODBC10](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc10.png)
12. <span data-ttu-id="dbd65-141">Ahora, el archivo de configuración de ODBC debe de aparecer en DSN de archivo.</span><span class="sxs-lookup"><span data-stu-id="dbd65-141">The ODBC configuration file should now be visible in File DSN.</span></span>  
    ![ODBC11](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc11.png)

<span data-ttu-id="dbd65-143">Ya tenemos el archivo que necesitamos y podemos comenzar a crear el conector.</span><span class="sxs-lookup"><span data-stu-id="dbd65-143">We now have the file we need and can start creating the Connector.</span></span>

## <a name="create-the-generic-sql-connector"></a><span data-ttu-id="dbd65-144">Creación del conector de SQL genérico</span><span class="sxs-lookup"><span data-stu-id="dbd65-144">Create the Generic SQL Connector</span></span>
1. <span data-ttu-id="dbd65-145">En la interfaz de usuario de Synchronization Service Manager, seleccione **Conectores** y **Crear**.</span><span class="sxs-lookup"><span data-stu-id="dbd65-145">In the Synchronization Service Manager UI, select **Connectors** and **Create**.</span></span> <span data-ttu-id="dbd65-146">Seleccione **SQL genérico (Microsoft)** y asígnele un nombre descriptivo.</span><span class="sxs-lookup"><span data-stu-id="dbd65-146">Select **Generic SQL (Microsoft)** and give it a descriptive name.</span></span>  
   <span data-ttu-id="dbd65-147">![Conector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span><span class="sxs-lookup"><span data-stu-id="dbd65-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span></span>
2. <span data-ttu-id="dbd65-148">Busque el archivo DSN que ha creado en la sección anterior y cárguelo en el servidor.</span><span class="sxs-lookup"><span data-stu-id="dbd65-148">Find the DSN file you created in the previous section and upload it to the server.</span></span> <span data-ttu-id="dbd65-149">Proporcione las credenciales para conectarse a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="dbd65-149">Provide the credentials to connect to the database.</span></span>  
   ![Conector2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector2.png)
3. <span data-ttu-id="dbd65-151">En este tutorial, hemos optado por una opción sencilla y hemos tenido en cuenta que hay dos tipos de objetos, **User** y **Group**.</span><span class="sxs-lookup"><span data-stu-id="dbd65-151">In this walkthrough, we are making it easy for us and say that there are two object types, **User** and **Group**.</span></span>
   <span data-ttu-id="dbd65-152">![Conector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span><span class="sxs-lookup"><span data-stu-id="dbd65-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span></span>
4. <span data-ttu-id="dbd65-153">Para encontrar los atributos, queremos que el conector los detecte examinando la propia tabla.</span><span class="sxs-lookup"><span data-stu-id="dbd65-153">To find the attributes, we want the Connector to detect those attributes by looking at the table itself.</span></span> <span data-ttu-id="dbd65-154">Puesto que **Users** es una palabra reservada en SQL, debemos escribirla entre corchetes [].</span><span class="sxs-lookup"><span data-stu-id="dbd65-154">Since **Users** is a reserved word in SQL, we need to provide it in square brackets [ ].</span></span>  
   <span data-ttu-id="dbd65-155">![Conector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span><span class="sxs-lookup"><span data-stu-id="dbd65-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span></span>
5. <span data-ttu-id="dbd65-156">Ahora definiremos el atributo de delimitador y el atributo DN.</span><span class="sxs-lookup"><span data-stu-id="dbd65-156">Time to define the anchor attribute and the DN attribute.</span></span> <span data-ttu-id="dbd65-157">Para **Users**, usamos la combinación de los atributos username y EmployeeID.</span><span class="sxs-lookup"><span data-stu-id="dbd65-157">For **Users**, we use the combination of the two attributes username and EmployeeID.</span></span> <span data-ttu-id="dbd65-158">Para **Group**, usamos GroupName (aunque no sea muy realista para la vida real, para este tutorial funciona).</span><span class="sxs-lookup"><span data-stu-id="dbd65-158">For **group**, we use GroupName (not realistic in real-life, but for this walkthrough it works).</span></span>
   <span data-ttu-id="dbd65-159">![Conector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span><span class="sxs-lookup"><span data-stu-id="dbd65-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span></span>
6. <span data-ttu-id="dbd65-160">No todos los tipos de atributo se pueden detectar en una base de datos SQL,</span><span class="sxs-lookup"><span data-stu-id="dbd65-160">Not all attribute types can be detected in a SQL database.</span></span> <span data-ttu-id="dbd65-161">como sucede con el tipo de atributo de referencia.</span><span class="sxs-lookup"><span data-stu-id="dbd65-161">The reference attribute type in particular cannot.</span></span> <span data-ttu-id="dbd65-162">Para el tipo de objeto de grupo, necesitamos cambiar OwnerID y MemberID de referencia.</span><span class="sxs-lookup"><span data-stu-id="dbd65-162">For the group object type, we need to change the OwnerID and MemberID to reference.</span></span>  
   ![Conector6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector6.png)
7. <span data-ttu-id="dbd65-164">Los atributos que hemos seleccionado como atributos de referencia en el paso anterior requieren el tipo de objeto al que hacen referencia estos valores.</span><span class="sxs-lookup"><span data-stu-id="dbd65-164">The attributes we selected as reference attributes in the previous step require the object type these values are a reference to.</span></span> <span data-ttu-id="dbd65-165">En nuestro caso, el tipo de objeto de usuario.</span><span class="sxs-lookup"><span data-stu-id="dbd65-165">In our case, the User object type.</span></span>  
   ![Conector7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector7.png)
8. <span data-ttu-id="dbd65-167">En la página Parámetros globales, seleccione **Marca de agua** como estrategia diferencial.</span><span class="sxs-lookup"><span data-stu-id="dbd65-167">On the Global Parameters page, select **Watermark** as the delta strategy.</span></span> <span data-ttu-id="dbd65-168">Escriba también en el formato de fecha y hora **aaaa-MM-dd HH:mm:ss**.</span><span class="sxs-lookup"><span data-stu-id="dbd65-168">Also type in the date/time format **yyyy-MM-dd HH:mm:ss**.</span></span>
   <span data-ttu-id="dbd65-169">![Conector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span><span class="sxs-lookup"><span data-stu-id="dbd65-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span></span>
9. <span data-ttu-id="dbd65-170">En la página **Configurar particiones y jerarquías** , seleccione ambos tipos de objeto.</span><span class="sxs-lookup"><span data-stu-id="dbd65-170">On the **Configure Partitions and Hierarchies** page, select both object types.</span></span>
   <span data-ttu-id="dbd65-171">![Conector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span><span class="sxs-lookup"><span data-stu-id="dbd65-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span></span>
10. <span data-ttu-id="dbd65-172">En **Seleccionar tipos de objeto** y **Seleccionar atributos**, seleccione los dos tipos de objeto y todos los atributos.</span><span class="sxs-lookup"><span data-stu-id="dbd65-172">On the **Select Object Types** and **Select Attributes**, select both object types and all attributes.</span></span> <span data-ttu-id="dbd65-173">En la página **Configurar delimitadores**, haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="dbd65-173">On the **Configure Anchors** page, click **Finish**.</span></span>

## <a name="create-run-profiles"></a><span data-ttu-id="dbd65-174">Creación de perfiles de ejecución</span><span class="sxs-lookup"><span data-stu-id="dbd65-174">Create Run Profiles</span></span>
1. <span data-ttu-id="dbd65-175">En la interfaz de usuario de Synchronization Service Manager, seleccione **Connectors** (Conectores) y **Configure Run Profiles** (Configurar perfiles de ejecución).</span><span class="sxs-lookup"><span data-stu-id="dbd65-175">In the Synchronization Service Manager UI, select **Connectors**, and **Configure Run Profiles**.</span></span> <span data-ttu-id="dbd65-176">Haga clic en **New Profile**(Nuevo perfil).</span><span class="sxs-lookup"><span data-stu-id="dbd65-176">Click **New Profile**.</span></span> <span data-ttu-id="dbd65-177">Comenzaremos por **Full Import**(Importación completa).</span><span class="sxs-lookup"><span data-stu-id="dbd65-177">We start with **Full Import**.</span></span>  
   <span data-ttu-id="dbd65-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span><span class="sxs-lookup"><span data-stu-id="dbd65-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span></span>
2. <span data-ttu-id="dbd65-179">Seleccione el tipo **Full Import (Stage Only)**(Importación completa [solo fase]).</span><span class="sxs-lookup"><span data-stu-id="dbd65-179">Select the type **Full Import (Stage Only)**.</span></span>  
   <span data-ttu-id="dbd65-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span><span class="sxs-lookup"><span data-stu-id="dbd65-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span></span>
3. <span data-ttu-id="dbd65-181">Seleccione la partición **OBJECT=User**.</span><span class="sxs-lookup"><span data-stu-id="dbd65-181">Select the partition **OBJECT=User**.</span></span>  
   <span data-ttu-id="dbd65-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span><span class="sxs-lookup"><span data-stu-id="dbd65-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span></span>
4. <span data-ttu-id="dbd65-183">Seleccione **Table** (Tabla) y escriba **[USERS]**.</span><span class="sxs-lookup"><span data-stu-id="dbd65-183">Select **Table** and type **[USERS]**.</span></span> <span data-ttu-id="dbd65-184">Desplácese hacia abajo hasta la sección de tipo de objeto con varios valores y escriba los datos como en la imagen siguiente.</span><span class="sxs-lookup"><span data-stu-id="dbd65-184">Scroll down to the multi-valued object type section and enter the data as in the following picture.</span></span> <span data-ttu-id="dbd65-185">Seleccione **Finish** (Finalizar) para guardar la fase.</span><span class="sxs-lookup"><span data-stu-id="dbd65-185">Select **Finish** to save the step.</span></span>  
   <span data-ttu-id="dbd65-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span><span class="sxs-lookup"><span data-stu-id="dbd65-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span></span>  
   <span data-ttu-id="dbd65-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span><span class="sxs-lookup"><span data-stu-id="dbd65-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span></span>  
5. <span data-ttu-id="dbd65-188">Seleccione **New step**(Nuevo paso).</span><span class="sxs-lookup"><span data-stu-id="dbd65-188">Select **New Step**.</span></span> <span data-ttu-id="dbd65-189">Esta vez, seleccione **OBJECT=Group**.</span><span class="sxs-lookup"><span data-stu-id="dbd65-189">This time, select **OBJECT=Group**.</span></span> <span data-ttu-id="dbd65-190">En la última página, use la configuración como se muestra en la imagen siguiente.</span><span class="sxs-lookup"><span data-stu-id="dbd65-190">On the last page, use the configuration as in the following picture.</span></span> <span data-ttu-id="dbd65-191">Haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="dbd65-191">Click **Finish**.</span></span>  
   <span data-ttu-id="dbd65-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span><span class="sxs-lookup"><span data-stu-id="dbd65-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span></span>  
   <span data-ttu-id="dbd65-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span><span class="sxs-lookup"><span data-stu-id="dbd65-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span></span>  
6. <span data-ttu-id="dbd65-194">Opcional: si lo desea, puede configurar perfiles de ejecución adicionales.</span><span class="sxs-lookup"><span data-stu-id="dbd65-194">Optional: If you want to, you can configure additional run profiles.</span></span> <span data-ttu-id="dbd65-195">En este tutorial se usa solo la importación completa.</span><span class="sxs-lookup"><span data-stu-id="dbd65-195">For this walkthrough, only the Full Import is used.</span></span>
7. <span data-ttu-id="dbd65-196">Haga clic en **OK** (Aceptar) para terminar de cambiar los perfiles de ejecución.</span><span class="sxs-lookup"><span data-stu-id="dbd65-196">Click **OK** to finish changing run profiles.</span></span>

## <a name="add-some-test-data-and-test-the-import"></a><span data-ttu-id="dbd65-197">Adición de algunos datos de prueba y prueba de la importación</span><span class="sxs-lookup"><span data-stu-id="dbd65-197">Add some test data and test the import</span></span>
<span data-ttu-id="dbd65-198">Rellene algunos datos de prueba en la base de datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="dbd65-198">Fill out some test data in your sample database.</span></span> <span data-ttu-id="dbd65-199">Cuando haya terminado, seleccione **Run** (Ejecutar) y **Full import** (Importación completa).</span><span class="sxs-lookup"><span data-stu-id="dbd65-199">When you are ready, select **Run** and **Full import**.</span></span>

<span data-ttu-id="dbd65-200">Este usuario tiene dos números de teléfono y un grupo con algunos miembros.</span><span class="sxs-lookup"><span data-stu-id="dbd65-200">Here is a user with two phone numbers and a group with some members.</span></span>  
![cs1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs1.png)  
![cs2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs2.png)  

## <a name="appendix-a"></a><span data-ttu-id="dbd65-203">Apéndice A</span><span class="sxs-lookup"><span data-stu-id="dbd65-203">Appendix A</span></span>
<span data-ttu-id="dbd65-204">**Script de SQL para crear la base de datos de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="dbd65-204">**SQL script to create the sample database**</span></span>

```SQL
---Creating the Database---------
Create Database GSQLDEMO
Go
-------Using the Database-----------
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
