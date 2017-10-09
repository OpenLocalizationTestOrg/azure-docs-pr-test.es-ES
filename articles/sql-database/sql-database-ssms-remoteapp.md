---
title: aaaConnect tooSQL base de datos mediante SQL Server Management Studio en Azure RemoteApp | Documentos de Microsoft
description: "Use este tutorial toolearn cómo toouse SQL Server Management Studio en Azure RemoteApp para la seguridad y rendimiento al conectarse tooSQL base de datos"
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
ms.openlocfilehash: 73994f9a1eb3e48efa5d7c4f976b00cfcbc88d75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-tooconnect-toosql-database"></a>Usar SQL Server Management Studio en Azure RemoteApp tooconnect tooSQL base de datos

> [!IMPORTANT]
> Azure RemoteApp va a dejar de estar disponible. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
>

## <a name="introduction"></a>Introducción
Este tutorial muestra cómo toouse SQL Server Management Studio (SSMS) en Azure RemoteApp tooconnect tooSQL base de datos. Le guía a través del proceso de Hola de configuración de SQL Server Management Studio en Azure RemoteApp, explica las ventajas de Hola y muestra las características de seguridad que puede usar en Azure Active Directory.

**Estimado toocomplete de tiempo:** 45 minutos

## <a name="ssms-in-azure-remoteapp"></a>SSMS en Azure RemoteApp
Azure RemoteApp es un servicio RDS de Azure que ofrece aplicaciones. Puede obtener más información sobre esta herramienta aquí: [¿Qué es RemoteApp?](../remoteapp/remoteapp-whatis.md)

SSMS que se ejecuta en Azure RemoteApp proporciona Hola misma experiencia que ejecute SSMS localmente.

![Captura de pantalla que muestra a SSMS ejecutándose en Azure RemoteApp][1]

## <a name="benefits"></a>Ventajas
Hay muchas ventajas toousing SSMS en Azure RemoteApp, incluido:

* El puerto 1433 en el servidor de SQL Azure no tiene toobe expone externamente (fuera de Azure).
* No hay tookeep necesidad de agregar y quitar direcciones IP en firewall de servidor de SQL Azure Hola.
* Todas las conexiones de Azure RemoteApp se realizan a través de HTTPS en el puerto 443 mediante un protocolo cifrado de escritorio remoto
* Es multiusuario y se puede escalar.
* Hay un aumento del rendimiento de con SSMS en hello misma región que Hola base de datos SQL.
* Puede auditar el uso de RemoteApp de Azure con la edición Premium Hola de Azure Active Directory que tiene informes de actividad de usuario.
* Puede habilitar la autenticación multifactor (MFA).
* SSMS en cualquier lugar al usar cualquiera de hello admite el acceso los clientes de Azure RemoteApp que incluye iOS, Android, Mac, Windows Phone y equipos que ejecutan Windows.

## <a name="create-hello-azure-remoteapp-collection"></a>Crear la colección de RemoteApp de Azure de Hola
Estos es Hola pasos toocreate la colección de RemoteApp de Azure con SSMS:

### <a name="1-create-a-new-windows-vm-from-image"></a>1. Cree una nueva máquina virtual de Windows desde una imagen
Usar hello "Windows Server remoto escritorio sesión Host Windows Server 2012 R2" imagen de hello Galería toomake la nueva máquina virtual.

### <a name="2-install-ssms-from-sql-express"></a>2. Instale SSMS desde SQL Express
Vaya a Hola nueva máquina virtual y navegar por la página de descarga de toothis: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)

Hay una descarga de tooonly opción SSMS. Después de la descarga, vaya al directorio de instalación de Hola y ejecute el programa de instalación tooinstall SSMS.

También debe tooinstall SQL Server 2014 Service Pack 1. Puede descargarlo aquí: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)

El Service Pack 1 de SQL Server 2014 incluye funciones esenciales para trabajar con la Base de datos SQL de Azure.

### <a name="3-run-validate-script-and-sysprep"></a>3. Ejecute un script Validate y Sysprep
En hello escritorio de hello VM es un script de PowerShell denominado validar. Ejecútelo haciendo doble clic. Comprobará que hello VM es listo toobe que se usa para hospedar remota de aplicaciones. Una vez completada la comprobación, le preguntará toorun sysprep - elija toorun lo.

Cuando sysprep finalice, se apagará Hola máquina virtual.

toolearn más información acerca de cómo crear una imagen de Azure RemoteApp, consulte: [cómo toocreate una plantilla de RemoteApp de la imagen en Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)

### <a name="4-capture-image"></a>4. Capture la imagen
Cuando Hola VM ha dejado de ejecutarse, disponible en el portal actual de Hola y capturarlo.

toolearn más acerca de cómo capturar una imagen, vea [capturar una imagen de una máquina virtual de Windows Azure creada con el modelo de implementación clásica de Hola](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="5-add-tooazure-remoteapp-template-images"></a>5. Agregar imágenes de plantilla de RemoteApp tooAzure
Hola Azure RemoteApp sección del portal actual de hello, vaya la ficha de imágenes de plantilla toohello y haga clic en Agregar. En el cuadro emergente de hello, seleccione "Importar una imagen de la biblioteca de máquinas virtuales" y, a continuación, elija Hola imagen que acaba de crear.

### <a name="6-create-cloud-collection"></a>6. Cree una colección en la nube
En el portal actual de hello, cree una nueva colección de nube de RemoteApp de Azure. Elija Hola imagen de plantilla que acaba de importar con SSMS instalado en él.

![Creación de una nueva colección en la nube][2]

### <a name="7-publish-ssms"></a>7. Publique SSMS
En hello publicar pestaña de la nueva colección de nube, seleccione Publicar una aplicación de Hola menú Inicio y luego elija SSMS de lista Hola.

![Aplicación de publicación][5]

### <a name="8-add-users"></a>8. Agregar usuarios
En la ficha acceso de usuario de hello puede seleccionar usuarios Hola que tendrán acceso toothis Azure RemoteApp colección que solo incluye SSMS.

![Agregar usuario][6]

### <a name="9-install-hello-azure-remoteapp-client-application"></a>9. Instalar la aplicación de cliente de hello Azure RemoteApp
Puede descargar e instalar un cliente de Azure RemoteApp aquí: [Descargar | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)

## <a name="configure-azure-sql-server"></a>Configuración de un servidor Azure SQL
Hola solo configuración necesaria es tooensure que da servicio a Azure está habilitado firewall de Hola. Si utiliza esta solución, no deberá tooadd cualquier firewall de Hola de tooopen de direcciones IP. tráfico de red de Hola que se permite toohello SQL Server es de otros servicios de Azure.

![Permiso de Azure][4]

## <a name="multi-factor-authentication-mfa"></a>Multi-Factor Authentication (MFA)
MFA se puede habilitar específicamente para esta aplicación. Vaya a toohello de pestaña de las aplicaciones de Azure Active Directory. Encontrará una entrada para Microsoft Azure RemoteApp. Si hace clic en esa aplicación y, a continuación, configura, verá Hola página donde puede habilitar MFA para esta aplicación.

![Habilitar MFA][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a>Auditoría de actividad de usuario con Azure Active Directory Premium
Si no tiene Azure AD Premium, tendrá que tooturn encenderlo en Hola sección de licencias de su directorio. Con Premium habilitado, puede asignar a usuarios a nivel de toohello Premium.

Cuando algún usuario tooa en Azure Active Directory, a continuación, puede ir toohello actividad pestaña toosee inicio de sesión información tooAzure RemoteApp.

## <a name="next-steps"></a>Pasos siguientes
Después de completar todos los Hola por encima de los pasos, se pueda toorun hello Azure RemoteApp cliente y el registro de con un usuario asignado. Se le mostrará con SSMS como uno de sus aplicaciones y ejecutarla como lo haría si se instalaron en el equipo con acceso a tooAzure SQL server.

Para obtener más información sobre cómo toomake Hola conexión tooSQL base de datos, vea [conectarse tooSQL base de datos con SQL Server Management Studio y realizar una consulta de T-SQL de ejemplo](sql-database-connect-query-ssms.md).

Eso es todo por ahora. ¡Disfrute!

<!--Image references-->
[1]: ./media/sql-database-ssms-remoteapp/ssms.png
[2]: ./media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: ./media/sql-database-ssms-remoteapp/mfa.png
[4]: ./media/sql-database-ssms-remoteapp/allowazure.png
[5]: ./media/sql-database-ssms-remoteapp/publish.png
[6]: ./media/sql-database-ssms-remoteapp/user.png