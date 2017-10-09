---
title: "aaaOverview de control de acceso en el almacén de Data Lake | Documentos de Microsoft"
description: "Descripción de cómo funciona el control de acceso en Azure Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d16f8c09-c954-40d3-afab-c86ffa8c353d
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 1cc5d578f22ef0a123a1547abebfb4795ea09139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="access-control-in-azure-data-lake-store"></a>Control de acceso en Azure Data Lake Store

Almacén de Azure Data Lake implementa un modelo de control de acceso que se deriva de HDFS, que a su vez deriva de modelo de control de acceso de hello POSIX. En este artículo se resume los conceptos básicos de hello del modelo de control de acceso de hello para el almacén de Data Lake. vea toolearn más información sobre el modelo de control de acceso HDFS de hello [HDFS permisos guía](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).

## <a name="access-control-lists-on-files-and-folders"></a>Listas de control de acceso en archivos y carpetas

Hay dos tipos de listas de control de acceso (ACL): **ACL de acceso** y **ACL predeterminadas**.

* **Obtener acceso a ACL**: estos objetos de tooan de acceso de control. Tanto los archivos como las carpetas tienen ACL de acceso.

* **ACL predeterminadas**: "Plantilla" de ACL asociada a una carpeta que determinan Hola acceso ACL para los elementos secundarios que se crean en esa carpeta. Los archivos no tienen ACL predeterminadas.

![ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-1.png)

ACL de acceso y ACL predeterminada tienen Hola misma estructura.

![ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-2.png)



> [!NOTE]
> Hola cambiante ACL predeterminada de un elemento primario no afecta a Hola acceso ACL o ACL predeterminada de los elementos secundarios que ya existen.
>
>

## <a name="users-and-identities"></a>Usuarios e identidades

Todos los archivos y carpetas tienen permisos distintos para estas identidades:

* Hola propietaria de usuario del archivo hello
* grupo de propietario de Hola
* Usuarios designados
* Grupos designados
* Los restantes usuarios

identidades de Hola de usuarios y grupos son las identidades de Azure Active Directory (Azure AD). Por lo que, a menos que se indique lo contrario, un "usuario", en el contexto de hello Lake del almacén de datos, puede ya sea significar que un usuario de Azure AD o un grupo de seguridad de Azure AD.

## <a name="permissions"></a>Permisos

Hola permisos en un objeto de sistema de archivos son **lectura**, **escribir**, y **Execute**, y puede utilizarse en archivos y carpetas como se muestra en hello en la tabla siguiente:

|            |    Archivo     |   Carpeta |
|------------|-------------|----------|
| **Lectura (R)** | Puede leer el contenido de Hola de un archivo | Requiere **lectura** y **Execute** contenido de hello toolist de carpeta Hola|
| **Escritura (W)** | Puede escribir o anexar archivo tooa | Requiere **escribir** y **Execute** toocreate los elementos secundarios en una carpeta |
| **Ejecución (X)** | No significa nada en el contexto de Hola de almacén de Data Lake | Elementos secundarios de tootraverse necesario Hola de una carpeta |

### <a name="short-forms-for-permissions"></a>Formas abreviadas de los permisos

**RWX** es usado tooindicate **lectura + escribir y ejecutar**. Existe un formato numérico más reducido en el que **lectura = 4**, **escribir = 2**, y **Execute = 1**, suma Hola de los cuales representa los permisos de Hola. A continuación se muestran algunos ejemplos.

| Formato numérico | Formato abreviado |      Qué significa     |
|--------------|------------|------------------------|
| 7            | RWX        | Lectura + Escritura + Ejecución |
| 5            | R-X        | Lectura + ejecución         |
| 4            | R--        | Lectura                   |
| 0            | ---        | Sin permisos         |


### <a name="permissions-do-not-inherit"></a>Los permisos no se heredan

Modelo de estilo de POSIX Hola utilizado por el almacén de Data Lake, permisos para un elemento se almacenan en el propio elemento Hola. En otras palabras, no pueden heredarse los permisos para un elemento de elementos primarios de Hola.

## <a name="common-scenarios-related-toopermissions"></a>Toopermissions relacionados de escenarios comunes

Estos son algunos toohelp escenarios comunes que comprenda qué permisos son necesarios tooperform determinadas operaciones en una cuenta de almacén de Data Lake.

### <a name="permissions-needed-tooread-a-file"></a>Permisos necesarios tooread un archivo

![ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-3.png)

* Para leer el toobe de archivo hello, Hola llamador necesidades **lectura** permisos.
* Para todos hello carpetas en la estructura de carpetas de Hola que contienen el archivo hello, Hola llamador necesidades **Execute** permisos.

### <a name="permissions-needed-tooappend-tooa-file"></a>Permisos necesarios tooappend tooa archivo

![ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-4.png)

* Para hello toobe de archivo se anexa a, Hola llamador necesidades **escribir** permisos.
* Para todos hello las carpetas que contienen el archivo hello, Hola llamador necesidades **Execute** permisos.

### <a name="permissions-needed-toodelete-a-file"></a>Permisos necesarios toodelete un archivo

![ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-5.png)

* Para la carpeta principal de hello, Hola llamador necesidades **escribir + ejecutar** permisos.
* Para todos los hello otras carpetas en la ruta de acceso del archivo de hello, Hola llamador necesidades **Execute** permisos.



> [!NOTE]
> Escribir permisos en el archivo hello no son necesario toodelete, siempre y cuando Hola dos condiciones anteriores son ciertas.
>
>

### <a name="permissions-needed-tooenumerate-a-folder"></a>Permisos necesarios tooenumerate una carpeta

![ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-6.png)

* Para tooenumerate de la carpeta de hello, Hola llamador necesidades **lectura + Execute** permisos.
* Para todos los hello carpetas antecesor, Hola llamador necesidades **Execute** permisos.

## <a name="viewing-permissions-in-hello-azure-portal"></a>Ver permisos en hello portal de Azure

De hello **Explorador de datos** hoja de hello cuenta de almacén de Data Lake, haga clic en **acceso** toosee hello las ACL para un archivo o una carpeta. Haga clic en **acceso** toosee hello las ACL para hello **catálogo** carpeta bajo hello **mydatastore** cuenta.

![ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-1.png)

En esta hoja, la sección superior hello muestra un resumen de los permisos de Hola que tiene. (En la captura de pantalla de hello, usuario de hello es Bob). A continuación, se muestran los permisos de acceso de Hola. Después de eso, de hello **acceso** hoja, haga clic en **vista Simple** toosee Hola vista más sencilla.

![ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-simple-view.png)

Haga clic en **vista avanzada** toosee hello más vista avanzada, donde se muestran los conceptos de Hola de ACL predeterminada, la máscara y superusuario.

![ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-advance-view.png)

## <a name="hello-super-user"></a>superusuario de Hola

Un superusuario tiene Hola la mayoría de los derechos de todos los usuarios de Hola Hola almacén de Data Lake. Un superusuario:

* Tiene permisos de RWX demasiado**todos los** archivos y carpetas.
* Puede cambiar los permisos de Hola en cualquier archivo o carpeta.
* Puede cambiar Hola posee el usuario o grupo de cualquier archivo o carpeta propietario.

En Azure, una cuenta de Data Lake Store tiene varios roles de Azure, incluidos:

* Propietarios
* Colaboradores
* Lectores

Todas las personas de hello **propietarios** rol para una cuenta de almacén de Data Lake automáticamente es un superusuario para esa cuenta. más información, consulte toolearn [el control de acceso basado en roles](../active-directory/role-based-access-control-configure.md).
Si desea toocreate una función de control de acceso basados en roles (RBAC) personalizado que tenga permisos de superusuario, necesita hello toohave los siguientes permisos:
- Microsoft.DataLakeStore/accounts/Superuser/action
- Microsoft.Authorization/roleAssignments/write


## <a name="hello-owning-user"></a>usuario propietario de Hola

usuario de Hola que ha creado el elemento de hello automáticamente es hello propietaria de usuario del elemento de Hola. Un usuario propietario puede:

* Cambiar los permisos de Hola de un archivo que pertenece.
* Cambiar Hola propietaria de grupo de un archivo de propiedad, como usuario propietario de hello también es miembro del grupo de destino de Hola.

> [!NOTE]
> Hola propietaria usuario *no se puede* cambiar Hola propietaria de usuario de otro archivo de propiedad. Solo los usuarios superobligatorios pueden cambiar Hola propietaria de usuario de un archivo o carpeta.
>
>

## <a name="hello-owning-group"></a>grupo de propietario de Hola

Hola POSIX ACL, cada usuario está asociado con un "grupo principal". Por ejemplo, el usuario "alice" podría pertenecer toohello grupo de "Finanzas". Alice también es posible que pertenezca a grupos de toomultiple, pero un grupo siempre se designa como su grupo principal. En POSIX, cuando Alice crea un archivo, Hola propietaria de grupo de ese archivo se establece tooher grupo primario, que en este caso es "Finanzas".

Cuando se crea un nuevo elemento de sistema de archivos, almacén de Data Lake asigna un toohello valor grupo propietario.

* **Caso 1**: carpeta de raíz de Hola "/". Esta carpeta se crea cuando se crea una cuenta de Data Lake Store. En este caso, grupo de propietario de Hola se establece toohello usuario que creó la cuenta de hello.
* **Caso 2** (los demás casos): cuando se crea un nuevo elemento, grupo de propietario de Hola se copia desde la carpeta principal de Hola.

grupo de propietario de Hello puede cambiarse mediante:
* Cualquier superusuario.
* Hola posee el usuario, si el usuario propietario de hello también es miembro del grupo de destino de Hola.

## <a name="access-check-algorithm"></a>Algoritmo de comprobación de acceso

Hola siguiente ilustración representa el algoritmo de comprobación de acceso de Hola para las cuentas de almacén de Data Lake.

![Algoritmo de ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-algorithm.png)


## <a name="hello-mask-and-effective-permissions"></a>máscara de Hola y "permisos efectivos"

Hola **máscara** es un RWX valor que es acceso toolimit usado para **denominado usuarios**, hello **grupo propietario**, y **con grupos con nombre** cuando esté listo realizar el algoritmo de comprobación de acceso de Hola. Estos son conceptos clave de Hola de máscara de Hola.

* máscara de Hello crea "permisos efectivos". Es decir, modifica los permisos de hello en tiempo de Hola de comprobación de acceso.
* máscara de Hello puede modificarse directamente por el propietario del archivo hello y a los usuarios superobligatorios.
* máscara de Hello puede quitar el permiso efectivo de permisos toocreate Hola. máscara de Hello *no* agregar permiso efectivo de permisos toohello.

Veamos algunos ejemplos. En el siguiente ejemplo de Hola, máscara de Hola se establece demasiado**RWX**, lo que significa que esa máscara hello no quite los permisos. permisos efectivos de Hola para hello con el nombre de usuario, grupo de propietario y con el nombre de grupo no se modifican durante la comprobación de acceso de Hola.

![ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-mask-1.png)

En el siguiente ejemplo de Hola, máscara de Hola se establece demasiado**R-X**. Esto significa que **desactiva los permisos de escritura de hello** para **con el nombre de usuario**, **grupo propietario**, y **denominado grupo** en tiempo de Hola de acceso comprobación.

![ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-mask-2.png)

Como referencia, es aquí donde la máscara de Hola para un archivo o una carpeta aparece en hello portal de Azure.

![ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-mask-view.png)

> [!NOTE]
> Para una nueva cuenta de almacén de Data Lake, Hola para hello ACL de acceso y de máscara ACL predeterminada de raíz de hello predeterminado tooRWX de la carpeta ("/").
>
>

## <a name="permissions-on-new-files-and-folders"></a>Permisos en los archivos y carpetas nuevos

Cuando se crea un nuevo archivo o carpeta en una carpeta existente, determina Hola ACL predeterminada en la carpeta principal de hello:

- La ACL predeterminada y la ACL de acceso de una carpeta secundaria.
- La ACL de acceso de un archivo secundario (los archivos no tienen ninguna ACL predeterminada).

### <a name="hello-access-acl-of-a-child-file-or-folder"></a>Hola acceso ACL de un archivo secundario o una carpeta

Cuando se crea un archivo secundario o una carpeta, predeterminado ACL del elemento primario de hello se copiará como Hola acceso ACL de archivos secundarios de Hola o una carpeta. Además, si **otros** usuario tiene permisos de RWX predeterminado del elemento primario de hello ACL, se quita de la ACL de acceso del elemento de hello secundarios.

![ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-child-items-1.png)

En la mayoría de los escenarios, información anterior de hello es todo lo que necesita tooknow acerca de cómo se determinan los ACL de acceso de un elemento secundario. Sin embargo, si está familiarizado con los sistemas POSIX y detallados desee toounderstand cómo se consigue esta transformación, vea la sección de hello [rol del Umask en la creación de hello acceso ACL para los nuevos archivos y carpetas](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) más adelante en este artículo.


### <a name="a-child-folders-default-acl"></a>ACL predeterminada de una carpeta secundaria.

Cuando se crea una carpeta secundaria en una carpeta primaria, ACL predeterminada de la carpeta principal Hola se copió sea ACL predeterminada de la carpeta de toohello secundarios.

![ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-child-items-2.png)

## <a name="advanced-topics-for-understanding-acls-in-data-lake-store"></a>Temas avanzados para entender las ACL en Data Lake Store

Los siguientes son algunos toohelp temas avanzados que comprenda cómo se determinan las ACL para el almacén de Data Lake archivos o carpetas.

### <a name="umasks-role-in-creating-hello-access-acl-for-new-files-and-folders"></a>Rol del umask en la creación de hello acceso ACL para los nuevos archivos y carpetas

En un sistema compatible con POSIX, concepto general de hello es ese umask es un valor de 9 bits en carpeta principal de Hola que ha usado el permiso de hello tootransform para **propietario usuario**, **grupo propietario**, y  **otros** en hello acceso ACL de un archivo secundario nuevo o una carpeta. bits de Hola de un umask identifican qué tooturn bits off en ACL de acceso del elemento de hello secundarios. Por lo tanto se utiliza tooselectively evitar la propagación de Hola de permisos para **propietaria de usuario**, **grupo propietario**, y **otros**.

En un sistema HDFS, Hola umask suele ser una opción de configuración en todo el sitio que está controlada por los administradores. Data Lake Store usa una **umask para toda la cuenta** que no se puede cambiar. Hola siguiente tabla muestra hello desenmascara almacén de Data Lake.

| Grupo de usuarios  | Configuración | Efecto en la ACL de acceso de un nuevo elemento secundario |
|------------ |---------|---------------------------------------|
| usuario propietario | ---     | Sin efecto                             |
| grupo propietario| ---     | Sin efecto                             |
| otro       | RWX     | Se elimina lectura + escritura + ejecución         |

Hola sigue en la ilustración muestra este umask en acción. efecto neto de Hello es tooremove **lectura + escribir y ejecutar** para **otros** usuario. Porque Hola umask no especificó los bits de **propietario usuario** y **grupo propietario**, esos permisos no se transforman.

![ACL de Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-umask.png)

### <a name="hello-sticky-bit"></a>bit rápidas Hola

bit rápidas de Hello es una característica avanzada más de un sistema de archivos POSIX. En contexto de hello Lake del almacén de datos, es poco probable que se necesitarán ese bit rápidas Hola.

Hello tabla siguiente muestra cómo funciona el bit rápidas de hello en el almacén de Data Lake.

| Grupo de usuarios         | Archivo    | Carpeta |
|--------------------|---------|-------------------------|
| Sticky Bits **DESACTIVADO** | Sin efecto   | Sin efecto.           |
| Sticky Bits **ACTIVADO**  | Sin efecto   | Impide que nadie excepto **usuarios superobligatorios** hello y **propietaria de usuario** de un elemento secundario de eliminar o cambiar el nombre de ese elemento secundario.               |

bit rápidas Hello no se muestra en hello portal de Azure.

## <a name="common-questions-about-acls-in-data-lake-store"></a>Preguntas frecuentes sobre las ACL en Data Lake Store

Estas son algunas preguntas que surgen a menudo con respecto a las ACL en Data Lake Store.

### <a name="do-i-have-tooenable-support-for-acls"></a>¿Tengo que tooenable compatibilidad con las ACL?

No. El control de acceso mediante las ACL siempre está activado en las cuentas de Data Lake Store.

### <a name="which-permissions-are-required-toorecursively-delete-a-folder-and-its-contents"></a>¿Qué permisos están toorecursively necesario eliminar una carpeta y su contenido?

* debe tener la carpeta principal de Hello **escribir + ejecutar** permisos.
* Hola toobe carpeta eliminado, y requiere que todas las carpetas dentro de él, **lectura + escribir y ejecutar** permisos.

> [!NOTE]
> No es necesario escribir permisos toodelete archivos en carpetas. Además, Hola carpeta raíz "/" puede **nunca** puede eliminar.
>
>

### <a name="who-is-hello-owner-of-a-file-or-folder"></a>¿Quién es el propietario de Hola de un archivo o carpeta?

creador de Hola de un archivo o carpeta se convierte en propietario de Hola.

### <a name="which-group-is-set-as-hello-owning-group-of-a-file-or-folder-at-creation"></a>¿El grupo al que se establece como Hola grupo de un archivo o carpeta en la creación del propietario?

grupo de propietario de Hola se copia desde Hola posee el grupo de la carpeta principal de hello en qué Hola se crea un nuevo archivo o carpeta.

### <a name="i-am-hello-owning-user-of-a-file-but-i-dont-have-hello-rwx-permissions-i-need-what-do-i-do"></a>Soy Hola propietaria de usuario de un archivo pero no tengo permisos de RWX Hola que necesito. ¿Qué puedo hacer?

usuario propietario de Hello puede cambiar Hola permisos de hello archivo toogive ellos mismos los permisos RWX que necesitan.

### <a name="when-i-look-at-acls-in-hello-azure-portal-i-see-user-names-but-through-apis-i-see-guids-why-is-that"></a>Si se observan las ACL en hello portal de Azure ver nombres de usuario pero a través de API, veo GUID, ¿por qué?

Las entradas de las ACL de Hola se almacenan como GUID correspondientes toousers en Azure AD. Hola API devuelven Hola GUID tal cual. Hola portal de Azure intenta toomake ACL más fácil toouse por traducción Hola GUID en nombres descriptivos siempre que sea posible.

### <a name="why-do-i-sometimes-see-guids-in-hello-acls-when-im-using-hello-azure-portal"></a>¿Por qué a veces aparece GUID en las ACL de hello cuando utilizo Hola portal de Azure?

Un GUID se muestra al usuario de hello no existe en Azure AD ya. Normalmente esto sucede cuando el usuario de hello ha dejado la empresa de Hola o si se ha eliminado su cuenta en Azure AD.

### <a name="does-data-lake-store-support-inheritance-of-acls"></a>¿Admite Data Lake Store la herencia de ACL?

No.

### <a name="what-is-hello-difference-between-mask-and-umask"></a>¿Cuál es la diferencia de hello entre máscara y umask?

| mask | umask|
|------|------|
| Hola **máscara** propiedad está disponible en todos los archivos y carpetas. | Hola **umask** es una propiedad de hello cuenta de almacén de Data Lake. Por lo que hay solo un único umask Hola almacén de Data Lake.    |
| propiedad de máscara de Hello en un archivo o carpeta puede ser modificado por hello posee el usuario o grupo de un archivo o un superusuario propietario. | no se puede modificar la propiedad de umask Hola por cualquier usuario, incluso un superusuario. Es un valor constante y que no puede cambiarse.|
| propiedad de máscara de Hola se utiliza durante el algoritmo de comprobación de acceso de hello en tiempo de ejecución toodetermine si un usuario tiene tooperform derecho hello en la operación en un archivo o carpeta. rol de Hola de máscara de hello es toocreate "permisos efectivos" en tiempo de Hola de comprobación de acceso. | Hola umask no se utiliza durante la comprobación de acceso en absoluto. Hola umask es toodetermine usado Hola acceso ACL de nuevos elementos secundarios de una carpeta. |
| máscara de Hello es un valor RWX de 3 bits que se aplica toonamed usuario, nombre de grupo y usuario propietario en tiempo de Hola de comprobación de acceso.| umask Hello es un valor de 9 bits que se aplica toohello posee el usuario, grupo, propietario y **otros** de un nuevo elemento secundario.|

### <a name="where-can-i-learn-more-about-posix-access-control-model"></a>¿Dónde puedo obtener más información sobre el modelo de control de acceso POSIX?

* [POSIX Access Control Lists on Linux](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html) (Listas de control de acceso de POSIX en Linux)

* [HDFS Permission Guide](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html) (Guía de permisos de HDFS)

* [POSIX FAQ (PREGUNTAS MÁS FRECUENTES SOBRE POSIX)](http://www.opengroup.org/austin/papers/posix_faq.html)

* [POSIX 1003.1 2008](http://standards.ieee.org/findstds/standard/1003.1-2008.html)

* [POSIX 1003.1 2013](http://pubs.opengroup.org/onlinepubs/9699919799.2013edition/)

* [POSIX 1003.1 2016](http://pubs.opengroup.org/onlinepubs/9699919799.2016edition/)

* [ACL de POSIX en Ubuntu](https://help.ubuntu.com/community/FilePermissionsACLs)

* [ACL: Using Access Control Lists on Linux](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/) (ACL: uso de listas de control de acceso en Linux)

## <a name="see-also"></a>Consulte también

* [Información general del Almacén de Azure Data Lake](data-lake-store-overview.md)
