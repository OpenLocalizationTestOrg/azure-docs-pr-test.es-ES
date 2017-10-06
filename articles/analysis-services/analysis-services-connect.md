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
# <a name="connect-tooan-azure-analysis-services-server"></a>Conectar el servidor de Analysis Services de Azure de tooan

Este artículo describe conexión server tooa mediante modelado de datos y aplicaciones de administración como SQL Server Management Studio (SSMS) o SQL Server Data Tools (SSDT). O bien, con aplicaciones cliente de generación de informes, como Microsoft Excel, Power BI Desktop o aplicaciones personalizadas. Las conexiones tooAzure Analysis Services usa HTTPS.

## <a name="client-libraries"></a>Bibliotecas de clientes
[Obtener bibliotecas de cliente más recientes de Hola](analysis-services-data-providers.md)

Todos los servidores de tooa de conexiones, independientemente del tipo, requieren actualizada AMO, ADOMD.NET y OLEDB bibliotecas tooconnect tooand interfaz de cliente con un servidor de Analysis Services. Para obtener SSMS, SSDT, Excel 2016 y Power BI, bibliotecas de cliente más recientes de Hola se instalan o se actualizan con las versiones mensuales. Sin embargo, en algunos casos, es posible que una aplicación no puede tener hello más reciente. Por ejemplo, cuando actualiza el retraso de directivas o actualizaciones de Office 365 son en hello canal diferida.

## <a name="server-name"></a>Nombre de servidor

Cuando se crea un servidor de Analysis Services en Azure, especifique un único hello y nombre de la región donde servidor Hola se toobe creado. Cuando se especifica el nombre del servidor de hello en una conexión, es el esquema de nomenclatura del servidor hello:

```
<protocol>://<region>/<servername>
```
 Donde el protocolo es cadena **asazure**, región es hello Uri donde se creó el servidor hello (por ejemplo, westus.asazure.windows.net) y nombreServidor es Hola nombre del servidor único dentro de la región de Hola.

### <a name="get-hello-server-name"></a>Obtener el nombre del servidor hello
En **portal de Azure** > servidor > **Introducción** > **nombre del servidor**, nombre de servidor completo de Hola de copia. Si otros usuarios de su organización va a conectar el servidor de toothis demasiado, puede compartir este nombre de servidor con ellos. Al especificar un nombre de servidor, debe usarse la ruta de acceso completa de Hola.

![Obtención del nombre del servidor en Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)


## <a name="connection-string"></a>Cadena de conexión

Cuando se conecte tooAzure Analysis Services mediante Hola modelo de objetos tabulares, Hola de uso después de formatos de cadena de conexión:

###### <a name="integrated-azure-active-directory-authentication"></a>Autenticación integrada de Azure Active Directory
La autenticación integrada recoge Hola caché de credenciales de Azure Active Directory si está disponible. De lo contrario, se muestra la ventana de inicio de sesión Azure hello.

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;"
```


###### <a name="azure-active-directory-authentication-with-username-and-password"></a>Autenticación de Azure Active Directory con el nombre de usuario y la contraseña

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;User ID=<user name>;Password=<password>;Persist Security Info=True; Impersonation Level=Impersonate;";
```

###### <a name="windows-authentication-integrated-security"></a>Autenticación de Windows (seguridad integrada)
Utilizar cuenta de Windows hello ejecutando el proceso actual de Hola.

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>; Integrated Security=SSPI;Persist Security Info=True;"
```



## <a name="connect-using-an-odc-file"></a>Conexión mediante un archivo .odc
En versiones anteriores de Excel, los usuarios pueden conectarse tooan servidor de Analysis Services de Azure mediante un archivo de conexión de datos de Office (.odc). más información, consulte toolearn [crear un archivo de conexión de datos de Office (.odc)](analysis-services-odc.md).


## <a name="next-steps"></a>Pasos siguientes
[Connect with Excel](analysis-services-connect-excel.md)   (Conexión con Excel)  
[Connect with Power BI](analysis-services-connect-pbi.md)  (Conexión con Power BI)  
[Administración del servidor](analysis-services-manage.md)   

