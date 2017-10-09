---
title: aaaManage datos personales en Microsoft Azure | Documentos de Microsoft
description: "instrucciones sobre cómo toocorrect, actualizar, eliminar y exportar datos personales en Azure Active Directory y la base de datos de SQL Azure"
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.openlocfilehash: 032f70d32377cb9395cb2c35c27dad05001537c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-personal-data-in-microsoft-azure"></a>Administración de datos personales en Microsoft Azure

Este artículo proporciona instrucciones sobre cómo toocorrect, actualizar, eliminar y exportar datos personales en Azure Active Directory y la base de datos de SQL Azure.

## <a name="scenario"></a>Escenario

Una empresa de Dublin proporciona todo lo necesario para bodas de destino de gama alta Irlanda y alrededor de Hola a todos para una base de clientes local e internacional. Tienen oficinas, clientes, empleados y proveedores ubicados en todo recintos hello world toofully servicio Hola ofrecen.

Entre otros muchos aspectos, empresa Hola realiza un seguimiento de confirmaciones de asistencia que incluyen alergias y las preferencias de la. Los invitados novia pueden registrar para varias actividades como explorar, botes a caballo conducir, llevar a, etc. e incluso interactúan entre sí en una página web central durante los meses de hello conduzcan toohello eventos. empresa Hola recopila información personal de empleados, proveedores, los clientes y los invitados novia. Debido a Hola naturaleza internacional de empresa de hello business Hola debe cumplir con varios niveles de la normativa.

## <a name="problem-statement"></a>Declaración del problema

- Administradores de datos deben ser capaz de toocorrect correcta actualización e información incompleta o que cambian personal información personal.

- Necesidad de administradores de datos debe ser capaz de toodelete información personal tras la solicitud de Hola de un asunto de datos.

- Administradores de datos necesitan los datos de tooexport y proporcionan a tooa asunto de datos en un formato común y estructurado en su solicitud.

## <a name="company-goals"></a>Objetivos de la empresa

- La información personal poco precisa o incompleta de clientes, invitados, empleados y proveedores debe corregirse o actualizarse en Azure Active Directory y Azure SQL Database.

- Información personal debe eliminarse en Azure Active Directory y la base de datos de SQL Azure tras la solicitud de saludo de un asunto de datos.

- Datos personales deben exportarse en un formato común y estructurado tras la solicitud de saludo de un asunto de datos.

## <a name="solutions"></a>Soluciones

### <a name="azure-active-directory-rectifycorrect-inaccurate-or-incomplete-personal-data-and-erasedelete-personal-datauser-profiles"></a>Azure Active Directory: rectificación o corrección de datos personales poco precisos o incompletos y eliminación o borrado de perfiles de usuario o datos personales.

[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) es el directorio multiinquilino basado en la nube y el servicio de administración de identidades de Microsoft.
Puede corregir, actualizar o eliminar los perfiles de usuario de clientes y empleados y la información de trabajo de usuario que contienen datos personales, como nombre, título de trabajo, dirección o número de teléfono, un usuario en su [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) entorno con hello [portal de Azure](https://portal.azure.com/).

Debe iniciar sesión con una cuenta que sea un administrador global para el directorio de Hola.

#### <a name="how-do-i-correct-or-update-user-profile-and-work-information-in-azure-active-directory"></a>¿Cómo puedo corregir o actualizar el perfil de usuario y la información laboral en Azure Active Directory?

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que sea un administrador global para el directorio de Hola.

2. Seleccione **más servicios**, escriba **usuarios y grupos** en Hola cuadro de texto y, a continuación, seleccione **ENTRAR**.

    ![media/image1.png](media/manage-personal-data-azure/image001.png)

3. En hello **usuarios y grupos** hoja, seleccione **usuarios**.

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. En hello **a los usuarios y grupos: los usuarios** hoja, seleccione un usuario de la lista de hello y, a continuación, en la hoja de hello para el usuario seleccionado de hello, seleccione **perfil** tooview información de perfil de usuario de Hola que necesita toobe corregido o actualizados.

    ![media/image3.png](media/manage-personal-data-azure/image005.png)

5. Corregir o actualizar la información de hello y, a continuación, en la barra de comandos de hello, seleccione **guardar.**

6.  En la hoja de hello para el usuario seleccionado de hello, seleccione **de trabajo información** información tooview de trabajo del usuario que necesita toobe corrección o actualización.

    ![media/image4.png](media/manage-personal-data-azure/image007.png)

7. Corregir o actualizar la información de trabajo de usuario de hello y, a continuación, en la barra de comandos de hello, seleccione **guardar.**

#### <a name="how-do-i-delete-a-user-profile-in-azure-active-directory"></a>¿Cómo elimino un perfil de usuario en Azure Active Directory?

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que sea un administrador global para el directorio de Hola.

2. Seleccione **más servicios**, escriba **usuarios y grupos** en Hola cuadro de texto y, a continuación, seleccione **ENTRAR**.

    ![](media/manage-personal-data-azure/image001.png)

3. En hello **usuarios y grupos** hoja, seleccione **usuarios**.

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. En hello **a los usuarios y grupos: los usuarios** hoja, seleccione un usuario de la lista de Hola.

    ![media/image3.png](media/manage-personal-data-azure/image007.png)

5. En la hoja de hello para el usuario seleccionado de hello, seleccione **Introducción**y, a continuación, en la barra de comandos de hello, seleccione **eliminar**.

    ![](media/manage-personal-data-azure/image013.png)

### <a name="sql-database-rectifycorrect-inaccurate-or-incomplete-personal-data-erasedelete-personal-data-export-personal-data"></a>SQL Database: rectificación o corrección de datos personales poco precisos o incompletos, eliminación o borrado de datos personales y exportación de información personal 

[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) es una base de datos en la nube que ayuda a los desarrolladores a crear y mantener aplicaciones.

Los datos personales pueden actualizarse en [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) mediante consultas SQL estándares, y también se pueden eliminar. Además, los datos personales pueden exportarse desde la base de datos de SQL con una variedad de métodos, incluidos Hola importación de Azure SQL Server y el Asistente para exportación y en una variedad de formatos, incluido un archivo BACPAC.

#### <a name="how-do-i-correct-update-or-erase-personal-data-in-sql-database"></a>¿Cómo puedo corregir, actualizar o borrar datos personales en SQL Database?

toolearn cómo toocorrect o actualización de datos personales en la base de datos de SQL, visite hello [actualización (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [actualizar texto](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [actualizar con la expresión de tabla común](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), o [ Actualizar texto escribir](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) documentación.

toolearn cómo toodelete datos personales en la base de datos de SQL, visite hello [eliminar (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) documentación.

#### <a name="how-do-i-export-personal-data-tooa-bacpac-file-in-sql-database"></a>¿Cómo se puede exportar archivo BACPAC de tooa de datos personales en la base de datos SQL?

Un archivo BACPAC incluye los metadatos y datos de la base de datos SQL de Hola y es un archivo zip con una extensión BACPAC. Esto puede hacerse mediante hello [portal de Azure](https://portal.azure.com/), Hola utilidad de línea de comandos SQLPackage, SQL Server Management Studio (SSMS) o PowerShell.

toolearn cómo archivo BACPAC tooa tooexport datos, visite hello [exportar un archivo BACPAC de tooa de base de datos de SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-export) página, que incluye instrucciones detalladas para cada método mencionado anteriormente.

¿Cómo se puede exportar datos personales de la base de datos de SQL con SQL Server Import hello y Asistente para exportación?

Este asistente le ayuda a copiar los datos de un origen tooa destino. Para que un asistente de toohello introducción, incluido cómo tooget, información sobre permisos, y cómo ayudar tooget con la herramienta de hello, visitan Hola [importar y exportar datos con SQL Server Import hello y Asistente para exportación de](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) página web.

Para obtener información general de las etapas de Asistente de hello, visite hello [los pasos de hello importación de SQL Server y el Asistente para exportación de](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) página web.

## <a name="next-steps"></a>Pasos siguientes:

[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) 

[Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

