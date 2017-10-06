---
title: aaaConnect tooAzure Analysis Services | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooconnect tooand obtener datos desde un servidor de Analysis Services en Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: b37f70a0-9166-4173-932d-935d769539d1
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 5df94492feb48034f156b72e83e1009683988fc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-azure-analysis-services-server"></a><span data-ttu-id="bf2ce-103">Conectar el servidor de Analysis Services de Azure de tooan</span><span class="sxs-lookup"><span data-stu-id="bf2ce-103">Connect tooan Azure Analysis Services server</span></span>

<span data-ttu-id="bf2ce-104">Este artículo describe conexión server tooa mediante modelado de datos y aplicaciones de administración como SQL Server Management Studio (SSMS) o SQL Server Data Tools (SSDT).</span><span class="sxs-lookup"><span data-stu-id="bf2ce-104">This article describes connecting tooa server by using data modeling and management applications like SQL Server Management Studio (SSMS) or SQL Server Data Tools (SSDT).</span></span> <span data-ttu-id="bf2ce-105">O bien, con aplicaciones cliente de generación de informes, como Microsoft Excel, Power BI Desktop o aplicaciones personalizadas.</span><span class="sxs-lookup"><span data-stu-id="bf2ce-105">Or, with client reporting applications like Microsoft Excel, Power BI Desktop, or custom applications.</span></span> <span data-ttu-id="bf2ce-106">Las conexiones tooAzure Analysis Services usa HTTPS.</span><span class="sxs-lookup"><span data-stu-id="bf2ce-106">Connections tooAzure Analysis Services use HTTPS.</span></span>

## <a name="client-libraries"></a><span data-ttu-id="bf2ce-107">Bibliotecas de clientes</span><span class="sxs-lookup"><span data-stu-id="bf2ce-107">Client libraries</span></span>
[<span data-ttu-id="bf2ce-108">Obtener bibliotecas de cliente más recientes de Hola</span><span class="sxs-lookup"><span data-stu-id="bf2ce-108">Get hello latest Client libraries</span></span>](analysis-services-data-providers.md)

<span data-ttu-id="bf2ce-109">Todos los servidores de tooa de conexiones, independientemente del tipo, requieren actualizada AMO, ADOMD.NET y OLEDB bibliotecas tooconnect tooand interfaz de cliente con un servidor de Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="bf2ce-109">All connections tooa server, regardless of type, require updated AMO, ADOMD.NET, and OLEDB client libraries tooconnect tooand interface with an Analysis Services server.</span></span> <span data-ttu-id="bf2ce-110">Para obtener SSMS, SSDT, Excel 2016 y Power BI, bibliotecas de cliente más recientes de Hola se instalan o se actualizan con las versiones mensuales.</span><span class="sxs-lookup"><span data-stu-id="bf2ce-110">For SSMS, SSDT, Excel 2016, and Power BI, hello latest client libraries are installed or updated with monthly releases.</span></span> <span data-ttu-id="bf2ce-111">Sin embargo, en algunos casos, es posible que una aplicación no puede tener hello más reciente.</span><span class="sxs-lookup"><span data-stu-id="bf2ce-111">However, in some cases, it's possible an application may not have hello latest.</span></span> <span data-ttu-id="bf2ce-112">Por ejemplo, cuando actualiza el retraso de directivas o actualizaciones de Office 365 son en hello canal diferida.</span><span class="sxs-lookup"><span data-stu-id="bf2ce-112">For example, when policies delay updates, or Office 365 updates are on hello Deferred Channel.</span></span>

## <a name="server-name"></a><span data-ttu-id="bf2ce-113">Nombre de servidor</span><span class="sxs-lookup"><span data-stu-id="bf2ce-113">Server name</span></span>

<span data-ttu-id="bf2ce-114">Cuando se crea un servidor de Analysis Services en Azure, especifique un único hello y nombre de la región donde servidor Hola se toobe creado.</span><span class="sxs-lookup"><span data-stu-id="bf2ce-114">When you create an Analysis Services server in Azure, you specify a unique name and hello region where hello server is toobe created.</span></span> <span data-ttu-id="bf2ce-115">Cuando se especifica el nombre del servidor de hello en una conexión, es el esquema de nomenclatura del servidor hello:</span><span class="sxs-lookup"><span data-stu-id="bf2ce-115">When specifying hello server name in a connection, hello server naming scheme is:</span></span>

```
<protocol>://<region>/<servername>
```
 <span data-ttu-id="bf2ce-116">Donde el protocolo es cadena **asazure**, región es hello Uri donde se creó el servidor hello (por ejemplo, westus.asazure.windows.net) y nombreServidor es Hola nombre del servidor único dentro de la región de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf2ce-116">Where protocol is string **asazure**, region is hello Uri where hello server was created (for example, westus.asazure.windows.net) and servername is hello name of your unique server within hello region.</span></span>

### <a name="get-hello-server-name"></a><span data-ttu-id="bf2ce-117">Obtener el nombre del servidor hello</span><span class="sxs-lookup"><span data-stu-id="bf2ce-117">Get hello server name</span></span>
<span data-ttu-id="bf2ce-118">En **portal de Azure** > servidor > **Introducción** > **nombre del servidor**, nombre de servidor completo de Hola de copia.</span><span class="sxs-lookup"><span data-stu-id="bf2ce-118">In **Azure portal** > server > **Overview** > **Server name**, copy hello entire server name.</span></span> <span data-ttu-id="bf2ce-119">Si otros usuarios de su organización va a conectar el servidor de toothis demasiado, puede compartir este nombre de servidor con ellos.</span><span class="sxs-lookup"><span data-stu-id="bf2ce-119">If other users in your organization are connecting toothis server too, you can share this server name with them.</span></span> <span data-ttu-id="bf2ce-120">Al especificar un nombre de servidor, debe usarse la ruta de acceso completa de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf2ce-120">When specifying a server name, hello entire path must be used.</span></span>

![Obtención del nombre del servidor en Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)


## <a name="connection-string"></a><span data-ttu-id="bf2ce-122">Cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="bf2ce-122">Connection string</span></span>

<span data-ttu-id="bf2ce-123">Cuando se conecte tooAzure Analysis Services mediante Hola modelo de objetos tabulares, Hola de uso después de formatos de cadena de conexión:</span><span class="sxs-lookup"><span data-stu-id="bf2ce-123">When connecting tooAzure Analysis Services using hello Tabular Object Model, use hello following connection string formats:</span></span>

###### <a name="integrated-azure-active-directory-authentication"></a><span data-ttu-id="bf2ce-124">Autenticación integrada de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bf2ce-124">Integrated Azure Active Directory authentication</span></span>
<span data-ttu-id="bf2ce-125">La autenticación integrada recoge Hola caché de credenciales de Azure Active Directory si está disponible.</span><span class="sxs-lookup"><span data-stu-id="bf2ce-125">Integrated authentication picks up hello Azure Active Directory credential cache if available.</span></span> <span data-ttu-id="bf2ce-126">De lo contrario, se muestra la ventana de inicio de sesión Azure hello.</span><span class="sxs-lookup"><span data-stu-id="bf2ce-126">If not, hello Azure login window is shown.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;"
```


###### <a name="azure-active-directory-authentication-with-username-and-password"></a><span data-ttu-id="bf2ce-127">Autenticación de Azure Active Directory con el nombre de usuario y la contraseña</span><span class="sxs-lookup"><span data-stu-id="bf2ce-127">Azure Active Directory authentication with username and password</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;User ID=<user name>;Password=<password>;Persist Security Info=True; Impersonation Level=Impersonate;";
```

###### <a name="windows-authentication-integrated-security"></a><span data-ttu-id="bf2ce-128">Autenticación de Windows (seguridad integrada)</span><span class="sxs-lookup"><span data-stu-id="bf2ce-128">Windows authentication (Integrated security)</span></span>
<span data-ttu-id="bf2ce-129">Utilizar cuenta de Windows hello ejecutando el proceso actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf2ce-129">Use hello Windows account running hello current process.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>; Integrated Security=SSPI;Persist Security Info=True;"
```



## <a name="connect-using-an-odc-file"></a><span data-ttu-id="bf2ce-130">Conexión mediante un archivo .odc</span><span class="sxs-lookup"><span data-stu-id="bf2ce-130">Connect using an .odc file</span></span>
<span data-ttu-id="bf2ce-131">En versiones anteriores de Excel, los usuarios pueden conectarse tooan servidor de Analysis Services de Azure mediante un archivo de conexión de datos de Office (.odc).</span><span class="sxs-lookup"><span data-stu-id="bf2ce-131">With older versions of Excel, users can connect tooan Azure Analysis Services server by using an Office Data Connection (.odc) file.</span></span> <span data-ttu-id="bf2ce-132">más información, consulte toolearn [crear un archivo de conexión de datos de Office (.odc)](analysis-services-odc.md).</span><span class="sxs-lookup"><span data-stu-id="bf2ce-132">toolearn more, see [Create an Office Data Connection (.odc) file](analysis-services-odc.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="bf2ce-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bf2ce-133">Next steps</span></span>
<span data-ttu-id="bf2ce-134">[Connect with Excel](analysis-services-connect-excel.md)   (Conexión con Excel)</span><span class="sxs-lookup"><span data-stu-id="bf2ce-134">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
<span data-ttu-id="bf2ce-135">[Connect with Power BI](analysis-services-connect-pbi.md)  (Conexión con Power BI)</span><span class="sxs-lookup"><span data-stu-id="bf2ce-135">[Connect with Power BI](analysis-services-connect-pbi.md) </span></span>  
[<span data-ttu-id="bf2ce-136">Administración del servidor</span><span class="sxs-lookup"><span data-stu-id="bf2ce-136">Manage your server</span></span>](analysis-services-manage.md)   

