---
title: "clústeres de HDInsight Unidos a un dominio de aaaManage - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomanage Unidos al dominio HDInsight clústeres"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 6ebc4d2f-2f6a-4e1e-ab6d-af4db6b4c87c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 233ddf0953e981f9a24b77d9dde194d590e5e6d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-domain-joined-hdinsight-clusters-preview"></a>Administración de clústeres de HDInsight unidos a dominio (versión preliminar)
Obtenga información acerca de usuarios de Hola y roles de hello en HDInsight Unidos a un dominio y cómo toomanage HDInsight Unidos a un dominio los clústeres.

## <a name="users-of-domain-joined-hdinsight-clusters"></a>Usuarios de clústeres de HDInsight unidos a dominio
Un clúster de HDInsight no está unido al dominio tiene dos cuentas de usuario que se crean durante la creación del clúster hello:

* **Administrador de Ambari**: esta cuenta es también conocida como *usuario de Hadoop* o *usuario de HTTP*. Esta cuenta puede ser usado toolog en tooAmbari en https://&lt;clustername >. azurehdinsight.net. También puede ser usado toorun consultas en las vistas de Ambari, ejecutar los trabajos a través de herramientas externas (es decir, PowerShell, Templeton, Visual Studio) y autenticarse con el controlador de ODBC de Hive de Hola y herramientas de BI (es decir, Excel, Power BI o Tableau).
* **Usuario de SSH**: esta cuenta se puede usar con SSH y permite ejecutar comandos de sudo. Tiene privilegios de raíz toohello máquinas virtuales de Linux.

Un clúster de HDInsight Unidos a un dominio tiene tres nuevos usuarios en usuario de administrador y SSH tooAmbari adición.

* **Administración de Cazador**: esta cuenta es cuenta de administrador de Apache Cazador local Hola. No es un usuario de dominio de Active Directory. Esta cuenta puede ser usado toosetup directivas y realizar otros administradores de usuarios o administradores delegados (para que los usuarios puedan administrar las directivas). De forma predeterminada, es el nombre de usuario de hello *administración* y contraseña de hello es Hola igual Hola Ambari contraseña de administrador. contraseña de Hello puede actualizarse desde la página de configuración de Hola de Cazador.
* **Usuario de dominio del Administrador de clúster**: esta cuenta es un usuario de dominio de active directory designado como Hola administración de clúster de Hadoop incluidos Ambari y Cazador. Se deben proporcionar las credenciales del usuario durante la creación del clúster. Este usuario tiene Hola siguientes privilegios:

  * Unirse a dominio de toohello máquinas y colocarlos en hello OU que especifique durante la creación del clúster.
  * Crear a entidades de servicio dentro de hello OU que especifique durante la creación del clúster.
  * Crear entradas de DNS inversas.

    Hola tenga en cuenta otros usuarios de AD tienen también estos privilegios.

    Hay algunos puntos finales en el clúster de hello (por ejemplo, Templeton) que no están administrados por Cazador y, por lo tanto, no son seguras. Estos extremos están bloqueados para todos los usuarios excepto el usuario de dominio de administración de clúster de Hola.
* **Normal**: durante la creación del clúster, puede proporcionar varios grupos de Active Directory. los usuarios de Hello en estos grupos será tooRanger sincronizado y Ambari. Estos usuarios son usuarios de dominio y tendrán acceso tooonly administrado Cazador puntos de conexión (por ejemplo, Hiveserver2). Todas las directivas RBAC de Hola y auditoría serán los usuarios toothese aplicables.

## <a name="roles-of-domain-joined-hdinsight-clusters"></a>Roles de clústeres de HDInsight unidos a dominio
HDInsight Unidos a un dominio tienen Hola siguientes roles:

* Administrador de clústeres
* Operador de clústeres
* Administrador de servicios
* Operador de servicio
* Usuario del clúster

**permisos de hello toosee de estos roles**

1. Abra Hola interfaz de usuario de administración de Ambari.  Vea [Hola abrir interfaz de usuario de administración de Ambari](#open-the-ambari-management-ui).
2. Hola menú izquierdo, haga clic en **Roles**.
3. Haga clic en permisos de Hola de toosee de signo de interrogación azul hello:

    ![Permisos de roles de HDInsight unidos a dominio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-roles-permissions.png)

## <a name="open-hello-ambari-management-ui"></a>Abra Hola interfaz de usuario de administración de Ambari
1. Inicio de sesión toohello [portal de Azure](https://portal.azure.com).
2. Abra el clúster de HDInsight en una hoja. Consulte [Enumeración y visualización de clústeres](hdinsight-administer-use-management-portal.md#list-and-show-clusters).
3. Haga clic en **panel** de hello menú superior tooopen Ambari.
4. Inicie sesión en tooAmbari con nombre de usuario de dominio de administrador de clúster de hello y una contraseña.
5. Haga clic en hello **administración** menú desplegable de la esquina superior derecha de hello y, a continuación, haga clic en **Ambari administrar**.

    ![Administración de Ambari para HDInsight unido a un dominio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-manage-ambari.png)

    Hola interfaz de usuario tiene el siguiente aspecto:

    ![IU de administración de Ambari para HDInsight unido a dominio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui.png)

## <a name="list-hello-domain-users-synchronized-from-your-active-directory"></a>Lista de usuarios de dominio de hello sincronizados desde Active Directory
1. Abra Hola interfaz de usuario de administración de Ambari.  Vea [Hola abrir interfaz de usuario de administración de Ambari](#open-the-ambari-management-ui).
2. Hola menú izquierdo, haga clic en **usuarios**. Verá todos los usuarios de hello sincronizados desde el clúster de HDInsight de toohello de Active Directory.

    ![IU de administración de Ambari para HDInsight unido a dominio: enumeración de usuarios](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-users.png)

## <a name="list-hello-domain-groups-synchronized-from-your-active-directory"></a>Lista de grupos de dominio de hello sincronizados desde Active Directory
1. Abra Hola interfaz de usuario de administración de Ambari.  Vea [Hola abrir interfaz de usuario de administración de Ambari](#open-the-ambari-management-ui).
2. Hola menú izquierdo, haga clic en **grupos**. Verá todos los grupos de hello sincronizados desde el clúster de HDInsight de toohello de Active Directory.

    ![IU de administración de Ambari para HDInsight unido a dominio: enumeración de grupos](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-groups.png)

## <a name="configure-hive-views-permissions"></a>Configuración de permisos de vistas de Hive
1. Abra Hola interfaz de usuario de administración de Ambari.  Vea [Hola abrir interfaz de usuario de administración de Ambari](#open-the-ambari-management-ui).
2. Hola menú izquierdo, haga clic en **vistas**.
3. Haga clic en **HIVE** detalles de hello tooshow.

    ![IU de administración de Ambari para HDInsight unido a dominio: vistas de Hive](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views.png)
4. Haga clic en hello **vista Hive** vincular tooconfigure Hive vistas.
5. Desplácese hacia abajo toohello **permisos** sección.

    ![IU de administración de Ambari para HDInsight unido a dominio: vistas de Hive, configuración de permisos](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views-permissions.png)
6. Haga clic en **Agregar usuario** o **Agregar grupo**y, a continuación, especifique Hola usuarios o grupos que pueden utilizar las vistas de Hive.

## <a name="configure-users-for-hello-roles"></a>Configurar los usuarios para los roles de Hola
 toosee una lista de funciones y sus permisos, consulte [clústeres de HDInsight Unidos a Roles de dominios](#roles-of-domain---joined-hdinsight-clusters).

1. Abra Hola interfaz de usuario de administración de Ambari.  Vea [Hola abrir interfaz de usuario de administración de Ambari](#open-the-ambari-management-ui).
2. Hola menú izquierdo, haga clic en **Roles**.
3. Haga clic en **Agregar usuario** o **Agregar grupo** tooassign a los usuarios y grupos de roles de toodifferent.

## <a name="next-steps"></a>Pasos siguientes
* Para configurar un clúster de HDInsight unido a dominio, consulte [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Configuración de clústeres de HDInsight unidos a un dominio).
* Para configurar directivas de Hive y ejecución de consultas de Hive, consulte [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md) (Configuración de directivas de los clústeres de HDInsight unidos a dominio).
* Para ejecutar consultas de Hive mediante SSH en clústeres de HDInsight unidos a un dominio, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).
