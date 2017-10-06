---
title: "Conector de base de datos de Oracle aaaAdd hello en sus aplicaciones de la lógica de Azure | Documentos de Microsoft"
description: "Usar el conector de base de datos de Oracle de hello en una aplicación de lógica"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: mandia; ladocs
ms.openlocfilehash: 8a802a6c4782e210ff71848614152cb46ba5d651
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-oracle-database-connector"></a><span data-ttu-id="ccc61-103">Empezar a trabajar con el conector de base de datos de Oracle Hola</span><span class="sxs-lookup"><span data-stu-id="ccc61-103">Get started with hello Oracle Database connector</span></span>

<span data-ttu-id="ccc61-104">Mediante el conector de base de datos de Oracle de hello, crear organizativas flujos de trabajo que utilizan datos de la base de datos existente.</span><span class="sxs-lookup"><span data-stu-id="ccc61-104">Using hello Oracle Database connector, you create organizational workflows that use data in your existing database.</span></span> <span data-ttu-id="ccc61-105">Este conector puede conectarse tooan base de datos de Oracle local o una máquina virtual de Azure con la base de datos de Oracle instalada.</span><span class="sxs-lookup"><span data-stu-id="ccc61-105">This connector can connect tooan on-premises Oracle Database, or an Azure virtual machine with Oracle Database installed.</span></span> <span data-ttu-id="ccc61-106">Con este conector, puede hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ccc61-106">With this connector, you can:</span></span>

* <span data-ttu-id="ccc61-107">Compilar el flujo de trabajo mediante la adición de una base de datos de los clientes de tooa cliente nuevo o actualizar un pedido en una base de datos de pedidos.</span><span class="sxs-lookup"><span data-stu-id="ccc61-107">Build your workflow by adding a new customer tooa customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="ccc61-108">Usar acciones tooget una fila de datos, insertar una fila nueva e incluso eliminar.</span><span class="sxs-lookup"><span data-stu-id="ccc61-108">Use actions tooget a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="ccc61-109">Por ejemplo, al crear un registro en Dynamics CRM Online (un desencadenador), inserte una fila en una base de datos de Oracle (una acción).</span><span class="sxs-lookup"><span data-stu-id="ccc61-109">For example, when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Oracle Database (an action).</span></span> 

<span data-ttu-id="ccc61-110">Este tema muestra cómo toouse Hola conector de base de datos de Oracle en una aplicación de lógica.</span><span class="sxs-lookup"><span data-stu-id="ccc61-110">This topic shows you how toouse hello Oracle Database connector in a logic app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ccc61-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ccc61-111">Prerequisites</span></span>

* <span data-ttu-id="ccc61-112">Versiones de Oracle compatibles:</span><span class="sxs-lookup"><span data-stu-id="ccc61-112">Supported Oracle versions:</span></span> 
    * <span data-ttu-id="ccc61-113">Oracle 9 y versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="ccc61-113">Oracle 9 and later</span></span>
    * <span data-ttu-id="ccc61-114">Software cliente de Oracle 8.1.7 y posteriores</span><span class="sxs-lookup"><span data-stu-id="ccc61-114">Oracle client software 8.1.7 and later</span></span>

* <span data-ttu-id="ccc61-115">Hola de instalación local de puerta de enlace de datos.</span><span class="sxs-lookup"><span data-stu-id="ccc61-115">Install hello on-premises data gateway.</span></span> <span data-ttu-id="ccc61-116">[Conectar datos tooon locales desde las aplicaciones lógicas](../logic-apps/logic-apps-gateway-connection.md) listas Hola pasos.</span><span class="sxs-lookup"><span data-stu-id="ccc61-116">[Connect tooon-premises data from logic apps](../logic-apps/logic-apps-gateway-connection.md) lists hello steps.</span></span> <span data-ttu-id="ccc61-117">puerta de enlace de Hello es necesario tooconnect tooan base de datos de Oracle local o una máquina virtual de Azure con la base de datos de Oracle instalada.</span><span class="sxs-lookup"><span data-stu-id="ccc61-117">hello gateway is required tooconnect tooan on-premises Oracle Database, or an Azure VM with Oracle DB installed.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="ccc61-118">puerta de enlace de datos de Hello local actúa como un puente y proporciona a una transferencia de datos seguros entre los datos locales (datos que no están en la nube de hello) y las aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="ccc61-118">hello on-premises data gateway acts as a bridge, and provides a secure data transfer between on-premises data (data that is not in hello cloud) and your logic apps.</span></span> <span data-ttu-id="ccc61-119">Hola misma puerta de enlace se puede utilizar con varios servicios y varios orígenes de datos.</span><span class="sxs-lookup"><span data-stu-id="ccc61-119">hello same gateway can be used with multiple services, and multiple data sources.</span></span> <span data-ttu-id="ccc61-120">Por lo tanto, puede que solo tenga puerta de enlace de hello tooinstall una vez.</span><span class="sxs-lookup"><span data-stu-id="ccc61-120">So, you may only need tooinstall hello gateway once.</span></span>

* <span data-ttu-id="ccc61-121">Instalar Hola cliente de Oracle en la máquina de Hola donde instaló la puerta de enlace de datos de hello en local.</span><span class="sxs-lookup"><span data-stu-id="ccc61-121">Install hello Oracle Client on hello machine where you installed hello on-premises data gateway.</span></span> <span data-ttu-id="ccc61-122">Asegúrese de tooinstall Hola proveedor de datos de Oracle de 64 bits para .NET de Oracle:</span><span class="sxs-lookup"><span data-stu-id="ccc61-122">Be sure tooinstall hello 64-bit Oracle Data Provider for .NET from Oracle:</span></span>  

  [<span data-ttu-id="ccc61-123">64-bits ODAC 12c versión 4 (12.1.0.2.4) para Windows x64</span><span class="sxs-lookup"><span data-stu-id="ccc61-123">64-bit ODAC 12c Release 4 (12.1.0.2.4) for Windows x64</span></span>](http://www.oracle.com/technetwork/database/windows/downloads/index-090165.html)

    > [!TIP]
    > <span data-ttu-id="ccc61-124">Si no está instalado el cliente de Oracle de hello, se produce un error cuando intente toocreate o usar conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="ccc61-124">If hello Oracle client is not installed, an error occurs when you try toocreate or use hello connection.</span></span> <span data-ttu-id="ccc61-125">Consulte los errores comunes de hello en este tema.</span><span class="sxs-lookup"><span data-stu-id="ccc61-125">See hello common errors in this topic.</span></span>


## <a name="add-hello-connector"></a><span data-ttu-id="ccc61-126">Agregar conector Hola</span><span class="sxs-lookup"><span data-stu-id="ccc61-126">Add hello connector</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ccc61-127">Este conector no tiene ningún desencadenador.</span><span class="sxs-lookup"><span data-stu-id="ccc61-127">This connector does not have any triggers.</span></span> <span data-ttu-id="ccc61-128">Solo tiene acciones.</span><span class="sxs-lookup"><span data-stu-id="ccc61-128">It has only actions.</span></span> <span data-ttu-id="ccc61-129">Por lo que cuando se crea la aplicación lógica, agregue otro toostart de desencadenador la aplicación lógica, como **programación - periodicidad**, o **de solicitud / respuesta - respuesta**.</span><span class="sxs-lookup"><span data-stu-id="ccc61-129">So when you create your logic app, add another trigger toostart your logic app, such as **Schedule - Recurrence**, or **Request / Response - Response**.</span></span> 

1. <span data-ttu-id="ccc61-130">Hola [portal de Azure](https://portal.azure.com), cree una aplicación lógica en blanco.</span><span class="sxs-lookup"><span data-stu-id="ccc61-130">In hello [Azure portal](https://portal.azure.com), create a blank logic app.</span></span>

2. <span data-ttu-id="ccc61-131">En el inicio de saludo de la aplicación lógica, seleccione hello **de solicitud / respuesta - solicitud** desencadenador:</span><span class="sxs-lookup"><span data-stu-id="ccc61-131">At hello start of your logic app, select hello **Request / Response - Request** trigger:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/request-trigger.png)

3. <span data-ttu-id="ccc61-132">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ccc61-132">Select **Save**.</span></span> <span data-ttu-id="ccc61-133">Cuando lo guarde, se generará automáticamente la URL de solicitud.</span><span class="sxs-lookup"><span data-stu-id="ccc61-133">When you save, a request URL is automatically generated.</span></span> 

4. <span data-ttu-id="ccc61-134">Seleccione **Nuevo paso** y seleccione **Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="ccc61-134">Select **New step**, and select **Add an action**.</span></span> <span data-ttu-id="ccc61-135">Escriba `oracle` toosee Hola acciones disponibles:</span><span class="sxs-lookup"><span data-stu-id="ccc61-135">Type in `oracle` toosee hello available actions:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/oracledb-actions.png)

    > [!TIP]
    > <span data-ttu-id="ccc61-136">Esto también es toosee de manera más rápida de Hola Hola desencadenadores y las acciones disponibles para cualquier conector.</span><span class="sxs-lookup"><span data-stu-id="ccc61-136">This is also hello quickest way toosee hello triggers and actions available for any connector.</span></span> <span data-ttu-id="ccc61-137">Tipo de parte del nombre de conector de hello, como `oracle`.</span><span class="sxs-lookup"><span data-stu-id="ccc61-137">Type in part of hello connector name, such as `oracle`.</span></span> <span data-ttu-id="ccc61-138">Diseñador de Hello enumera todos los desencadenadores y las medidas.</span><span class="sxs-lookup"><span data-stu-id="ccc61-138">hello designer lists any triggers and any actions.</span></span> 

5. <span data-ttu-id="ccc61-139">Seleccione una de las acciones de hello, como **base de datos de Oracle - Get fila**.</span><span class="sxs-lookup"><span data-stu-id="ccc61-139">Select one of hello actions, such as **Oracle Database - Get row**.</span></span> <span data-ttu-id="ccc61-140">Seleccione **Connect via on-premises data gateway** (Conectarse a través de la puerta de enlace de datos local).</span><span class="sxs-lookup"><span data-stu-id="ccc61-140">Select **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="ccc61-141">Escriba el nombre de servidor de Oracle de hello, método de autenticación, nombre de usuario, contraseña y puerta de enlace de hello seleccione:</span><span class="sxs-lookup"><span data-stu-id="ccc61-141">Enter hello Oracle server name, authentication method, username, password, and select hello gateway:</span></span>

    ![](./media/connectors-create-api-oracledatabase/create-oracle-connection.png)

6. <span data-ttu-id="ccc61-142">Una vez conectado, seleccione una tabla en la lista de Hola y especifique la tabla de tooyour de Id. de fila de Hola.</span><span class="sxs-lookup"><span data-stu-id="ccc61-142">Once connected, select a table from hello list, and enter hello row ID tooyour table.</span></span> <span data-ttu-id="ccc61-143">Necesita tabla toohello de tooknow Hola identificador.</span><span class="sxs-lookup"><span data-stu-id="ccc61-143">You need tooknow hello identifier toohello table.</span></span> <span data-ttu-id="ccc61-144">Si no sabe, póngase en contacto con el Administrador de base de datos de Oracle y obtener un resultado de hello `select * from yourTableName`.</span><span class="sxs-lookup"><span data-stu-id="ccc61-144">If you don't know, contact your Oracle DB administrator, and get hello output from `select * from yourTableName`.</span></span> <span data-ttu-id="ccc61-145">Esto deja Hola necesita tooproceed de información de identificación.</span><span class="sxs-lookup"><span data-stu-id="ccc61-145">This gives you hello identifiable information you need tooproceed.</span></span>

    <span data-ttu-id="ccc61-146">En el siguiente ejemplo de Hola, datos del trabajo que se devuelve desde una base de datos de recursos humanos:</span><span class="sxs-lookup"><span data-stu-id="ccc61-146">In hello following example, job data is being returned from a Human Resources database:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/table-rowid.png)

7. <span data-ttu-id="ccc61-147">En este paso siguiente, puede usar cualquiera de hello otro toobuild conectores el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="ccc61-147">In this next step, you can use any of hello other connectors toobuild your workflow.</span></span> <span data-ttu-id="ccc61-148">Si desea obtener los datos de Oracle tootest, envíe un correo electrónico con datos de Oracle de hello mediante uno de hello enviar conectores de correo electrónico, Office 365 o Gmail.</span><span class="sxs-lookup"><span data-stu-id="ccc61-148">If you want tootest getting data from Oracle, then send yourself an email with hello Oracle data using one of hello send email connectors, such Office 365 or Gmail.</span></span> <span data-ttu-id="ccc61-149">Usar tokens dinámica de Hola de Hola Hola de toobuild de tabla de Oracle `Subject` y `Body` de tu correo electrónico:</span><span class="sxs-lookup"><span data-stu-id="ccc61-149">Use hello dynamic tokens from hello Oracle table toobuild hello `Subject` and `Body` of your email:</span></span>

    ![](./media/connectors-create-api-oracledatabase/oracle-send-email.png)

8. <span data-ttu-id="ccc61-150">**Guarde** la aplicación lógica y, a continuación, seleccione **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="ccc61-150">**Save** your logic app, and then select **Run**.</span></span> <span data-ttu-id="ccc61-151">Cierre el Diseñador de Hola y examine Hola historial de ejecuciones para el estado de Hola.</span><span class="sxs-lookup"><span data-stu-id="ccc61-151">Close hello designer, and look at hello runs history for hello status.</span></span> <span data-ttu-id="ccc61-152">Si se produce un error, seleccione la fila de mensajes con errores de Hola.</span><span class="sxs-lookup"><span data-stu-id="ccc61-152">If it fails, select hello failed message row.</span></span> <span data-ttu-id="ccc61-153">Hola diseñador se abre y muestra qué paso no se pudo y también muestra información de error de Hola.</span><span class="sxs-lookup"><span data-stu-id="ccc61-153">hello designer opens, and shows you which step failed, and also shows hello error information.</span></span> <span data-ttu-id="ccc61-154">Si se realiza correctamente, debería recibir un correo electrónico con información de Hola que agregó.</span><span class="sxs-lookup"><span data-stu-id="ccc61-154">If it succeeds, then you should receive an email with hello information you added.</span></span>


### <a name="workflow-ideas"></a><span data-ttu-id="ccc61-155">Ideas de flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="ccc61-155">Workflow ideas</span></span>

* <span data-ttu-id="ccc61-156">Que desee toomonitor hello #oracle hashtag y coloca tweets hello en una base de datos, por lo que se pueden consultar y usar en otras aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ccc61-156">You want toomonitor hello #oracle hashtag, and put hello tweets in a database so they can be queried, and used within other applications.</span></span> <span data-ttu-id="ccc61-157">En una aplicación de lógica, agregue hello `Twitter - When a new tweet is posted` desencadenar y escriba hello **#oracle** hashtag.</span><span class="sxs-lookup"><span data-stu-id="ccc61-157">In a logic app, add hello `Twitter - When a new tweet is posted` trigger, and enter hello **#oracle** hashtag.</span></span> <span data-ttu-id="ccc61-158">A continuación, agregue hello `Oracle Database - Insert row` acción y seleccione la tabla:</span><span class="sxs-lookup"><span data-stu-id="ccc61-158">Then, add hello `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/twitter-oracledb.png)

* <span data-ttu-id="ccc61-159">Cola de Bus de servicio tooa se envían los mensajes.</span><span class="sxs-lookup"><span data-stu-id="ccc61-159">Messages are sent tooa Service Bus queue.</span></span> <span data-ttu-id="ccc61-160">Desea tooget estos mensajes y colóquelos en una base de datos.</span><span class="sxs-lookup"><span data-stu-id="ccc61-160">You want tooget these messages, and put them in a database.</span></span> <span data-ttu-id="ccc61-161">En una aplicación de lógica, agregue hello `Service Bus - when a message is received in a queue` desencadenador y seleccione Hola cola.</span><span class="sxs-lookup"><span data-stu-id="ccc61-161">In a logic app, add hello `Service Bus - when a message is received in a queue` trigger, and select hello queue.</span></span> <span data-ttu-id="ccc61-162">A continuación, agregue hello `Oracle Database - Insert row` acción y seleccione la tabla:</span><span class="sxs-lookup"><span data-stu-id="ccc61-162">Then, add hello `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/sbqueue-oracledb.png)

## <a name="common-errors"></a><span data-ttu-id="ccc61-163">Errores comunes</span><span class="sxs-lookup"><span data-stu-id="ccc61-163">Common errors</span></span>

#### <a name="error-cannot-reach-hello-gateway"></a><span data-ttu-id="ccc61-164">**Error**: no se puede alcanzar Hola puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="ccc61-164">**Error**: Cannot reach hello Gateway</span></span>

<span data-ttu-id="ccc61-165">**Causa**: puerta de enlace de datos de hello local no es capaz de tooconnect toohello en la nube.</span><span class="sxs-lookup"><span data-stu-id="ccc61-165">**Cause**: hello on-premises data gateway is not able tooconnect toohello cloud.</span></span> 

<span data-ttu-id="ccc61-166">**Mitigación**: asegúrese de que la puerta de enlace está ejecutando en la máquina de hello local donde se instaló y que TI puede conectarse toohello internet.</span><span class="sxs-lookup"><span data-stu-id="ccc61-166">**Mitigation**: Make sure your gateway is running on hello on-premises machine where you installed it, and that it can connect toohello internet.</span></span>  <span data-ttu-id="ccc61-167">Se recomienda no instalar la puerta de enlace de hello en un equipo que puede desactivarse o suspensión.</span><span class="sxs-lookup"><span data-stu-id="ccc61-167">We recommend not installing hello gateway on a computer that may be turned off or sleep.</span></span> <span data-ttu-id="ccc61-168">También puede reiniciar el servicio de puerta de enlace de datos de hello local (PBIEgwService).</span><span class="sxs-lookup"><span data-stu-id="ccc61-168">You can also restart hello on-premises data gateway service (PBIEgwService).</span></span>

#### <a name="error-hello-provider-being-used-is-deprecated-systemdataoracleclient-requires-oracle-client-software-version-817-or-greater-please-visit-httpsgomicrosoftcomfwlinkplinkid272376httpsgomicrosoftcomfwlinkplinkid272376-tooinstall-hello-official-provider"></a><span data-ttu-id="ccc61-169">**Error**: proveedor de Hola que se utiliza está en desuso: ' System.Data.OracleClient requiere la versión 8.1.7 del software cliente de Oracle o superior.'.</span><span class="sxs-lookup"><span data-stu-id="ccc61-169">**Error**: hello provider being used is deprecated: 'System.Data.OracleClient requires Oracle client software version 8.1.7 or greater.'.</span></span> <span data-ttu-id="ccc61-170">Visite [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) proveedor oficial de tooinstall Hola.</span><span class="sxs-lookup"><span data-stu-id="ccc61-170">Please visit [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) tooinstall hello official provider.</span></span>

<span data-ttu-id="ccc61-171">**Causa**: puerta de enlace de datos se ejecuta en instalaciones de cliente de Oracle Hola SDK no está instalado en el equipo de Hola donde hello.</span><span class="sxs-lookup"><span data-stu-id="ccc61-171">**Cause**: hello Oracle client SDK is not installed on hello machine where hello on-premises data gateway is running.</span></span>  

<span data-ttu-id="ccc61-172">**Resolución**: descargar e instalar el SDK de cliente de Oracle de hello en hello mismo equipo como puerta de enlace de datos de hello en local.</span><span class="sxs-lookup"><span data-stu-id="ccc61-172">**Resolution**: Download and install hello Oracle client SDK on hello same computer as hello on-premises data gateway.</span></span>

#### <a name="error-table-tablename-does-not-define-any-key-columns"></a><span data-ttu-id="ccc61-173">**Error**: La tabla '[Tablename]' no define las columnas clave.</span><span class="sxs-lookup"><span data-stu-id="ccc61-173">**Error**: Table '[Tablename]' does not define any key columns</span></span>

<span data-ttu-id="ccc61-174">**Causa**: Hola tabla no tiene ninguna clave principal.</span><span class="sxs-lookup"><span data-stu-id="ccc61-174">**Cause**: hello table does not have any primary key.</span></span>  

<span data-ttu-id="ccc61-175">**Resolución**: conector de base de datos de Oracle Hola requiere que se utilice una tabla con una columna de clave principal.</span><span class="sxs-lookup"><span data-stu-id="ccc61-175">**Resolution**: hello Oracle Database connector requires that a table with a primary key column be used.</span></span>

#### <a name="currently-not-supported"></a><span data-ttu-id="ccc61-176">Actualmente no se admite</span><span class="sxs-lookup"><span data-stu-id="ccc61-176">Currently not supported</span></span>

* <span data-ttu-id="ccc61-177">Vistas y procedimientos almacenados</span><span class="sxs-lookup"><span data-stu-id="ccc61-177">Views and stored procedures</span></span> 
* <span data-ttu-id="ccc61-178">Todas las tablas con claves compuestas</span><span class="sxs-lookup"><span data-stu-id="ccc61-178">Any table with composite keys</span></span>
* <span data-ttu-id="ccc61-179">Tipos de objetos anidados en tablas</span><span class="sxs-lookup"><span data-stu-id="ccc61-179">Nested object types in tables</span></span>
 
## <a name="connector-specific-details"></a><span data-ttu-id="ccc61-180">Detalles específicos del conector</span><span class="sxs-lookup"><span data-stu-id="ccc61-180">Connector-specific details</span></span>

<span data-ttu-id="ccc61-181">Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/oracle/).</span><span class="sxs-lookup"><span data-stu-id="ccc61-181">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/oracle/).</span></span> 

## <a name="get-some-help"></a><span data-ttu-id="ccc61-182">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="ccc61-182">Get some help</span></span>

<span data-ttu-id="ccc61-183">Hola [foro de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) es una gran colocar tooask preguntas, responda a preguntas y ver lo que hacen otros usuarios de las aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="ccc61-183">hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) is a great place tooask questions, answer questions, and see what other Logic Apps users are doing.</span></span> 

<span data-ttu-id="ccc61-184">Puede ayudar a mejorar Logic Apps y conectores al votar y enviar sus ideas en [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="ccc61-184">You can help improve Logic Apps and connectors by voting and submitting your ideas at [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish).</span></span> 


## <a name="next-steps"></a><span data-ttu-id="ccc61-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ccc61-185">Next steps</span></span>
<span data-ttu-id="ccc61-186">[Crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md)y explorar los conectores disponibles de hello en las aplicaciones lógicas en nuestro [lista de las API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="ccc61-186">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md), and explore hello available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
