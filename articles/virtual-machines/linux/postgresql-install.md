---
title: aaaSet seguridad PostgreSQL en una VM Linux | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooinstall y configurar PostgreSQL en una máquina virtual de Linux en Azure"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 1a747363-0cc5-4ba3-9be7-084dfeb04651
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: mingzhan
ms.openlocfilehash: 40209647924dffce11500705eb2d9f41c14df6ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-postgresql-on-azure"></a>Instalación y configuración de PostgreSQL en Azure
PostgreSQL es una base de datos de código abierto avanzados similares tooOracle y DB2. Incluye características preparadas para el ámbito empresarial, como el cumplimiento de ACID completo, un procesamiento transaccional confiable y un control de simultaneidad de múltiples versiones. También admite estándares como ANSI SQL y SQL/MED (incluidos los contenedores de datos externos para Oracle, MySQL, MongoDB y muchas otras). Es altamente extensible al admitir más de 12 lenguajes procedimentales, índices GIN y GiST, datos espaciales y múltiples características NoSQL para JSON o aplicaciones basadas en clave-valor.

En este artículo, aprenderá cómo tooinstall y configurar PostgreSQL en una máquina virtual de Azure ejecutan Linux.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-postgresql"></a>Instalación de PostgreSQL
> [!NOTE]
> Ya debe tener una máquina virtual con Linux en orden toocomplete este tutorial. toocreate y configurar una VM Linux antes de continuar, consulte la [tutorial de la máquina virtual de Linux de Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

En este caso, utilice puerto 1999 como Hola puerto PostgreSQL.  

Conectar toohello VM de Linux que creó mediante PuTTY. Si se trata de hello primera vez que se está utilizando una VM de Linux de Azure, consulte [cómo tooUse SSH con Linux en Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toolearn cómo PuTTY toouse tooconnect tooa VM de Linux.

1. Siguiente ejecución Hola comando tooswitch toohello raíz (Administrador):
   
        # sudo su -
2. Algunas distribuciones tienen dependencias que se deben instalar antes de instalar PostgreSQL. Busque la distribución en esta lista y ejecute el comando adecuado de hello:
   
   * Linux basado en Red Hat:
     
           # yum install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
   * Linux basado en Debian:
     
            # apt-get install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam libxslt-devel tcl-devel python-devel -y  
   * Linux SUSE:
     
           # zypper install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
3. Descargar PostgreSQL en el directorio raíz de hello y, a continuación, descomprima el paquete de hello:
   
        # wget https://ftp.postgresql.org/pub/source/v9.3.5/postgresql-9.3.5.tar.bz2 -P /root/
   
        # tar jxvf  postgresql-9.3.5.tar.bz2
   
    Hola anterior es un ejemplo. Puede encontrar Hola más detallada descargar dirección Hola [índicede/pub/origen/](https://ftp.postgresql.org/pub/source/).
4. compilación hello toostart, ejecute estos comandos:
   
        # cd postgresql-9.3.5
   
        # ./configure --prefix=/opt/postgresql-9.3.5
5. Si desea toobuild todo lo que pueden crearse, incluida documentación hello (páginas HTML y man) y módulos adicionales (hogar), ejecute hello siguiente comando en su lugar:
   
        # gmake install-world
   
    Debería recibir Hola siguiente mensaje de confirmación:
   
        PostgreSQL, contrib, and documentation successfully made. Ready tooinstall.

## <a name="configure-postgresql"></a>Configuración de PostgreSQL
1. (Opcional) Crear un hello tooshorten de vínculo simbólico PostgreSQL referencia toonot incluyen el número de versión de hello:
   
        # ln -s /opt/pgsql9.3.5 /opt/pgsql
2. Cree un directorio de base de datos de hello:
   
        # mkdir -p /opt/pgsql_data
3. Cree un usuario no raíz y modifique el perfil del usuario. A continuación, cambie toothis nuevo usuario (denominado *postgres* en nuestro ejemplo):
   
        # useradd postgres
   
        # chown -R postgres.postgres /opt/pgsql_data
   
        # su - postgres
   
   > [!NOTE]
   > Por motivos de seguridad, PostgreSQL utiliza un tooinitialize de usuario no es de raíz, iniciar o cerrar la base de datos de Hola.
   > 
   > 
4. Editar hello *bash_profile* archivo escribiendo los siguientes comandos de Hola. Estas líneas se agregarán toohello final de hello *bash_profile* archivo:
   
        cat >> ~/.bash_profile <<EOF
        export PGPORT=1999
        export PGDATA=/opt/pgsql_data
        export LANG=en_US.utf8
        export PGHOME=/opt/pgsql
        export PATH=\$PATH:\$PGHOME/bin
        export MANPATH=\$MANPATH:\$PGHOME/share/man
        export DATA=`date +"%Y%m%d%H%M"`
        export PGUSER=postgres
        alias rm='rm -i'
        alias ll='ls -lh'
        EOF
5. Ejecute hello *bash_profile* archivo:
   
        $ source .bash_profile
6. Validar la instalación mediante el uso de hello siguiente comando:
   
        $ which psql
   
    Si la instalación se realiza correctamente, verá Hola después de respuesta:
   
        /opt/pgsql/bin/psql
7. También puede comprobar la versión de Hola PostgreSQL:
   
        $ psql -V
8. Inicializar base de datos de hello:
   
        $ initdb -D $PGDATA -E UTF8 --locale=C -U postgres -W
   
    Debería recibir Hola después de salida:

![imagen](./media/postgresql-install/no1.png)

## <a name="set-up-postgresql"></a>Configuración de PostgreSQL
<!--    [postgres@ test ~]$ exit -->

Ejecute hello siguientes comandos:

    # cd /root/postgresql-9.3.5/contrib/start-scripts

    # cp linux /etc/init.d/postgresql

Modificar dos variables en el archivo de hello /etc/init.d/postgresql. prefijo de Hola se establece la ruta de instalación de toohello de PostgreSQL: **pgsql/opt/**. PGDATA se establece toohello ruta de acceso de almacenamiento de datos de PostgreSQL: **pgsql_data/opt/**.

    # sed -i '32s#usr/local#opt#' /etc/init.d/postgresql

    # sed -i '35s#usr/local/pgsql/data#opt/pgsql_data#' /etc/init.d/postgresql

![imagen](./media/postgresql-install/no2.png)

Cambiar Hola archivo toomake lo ejecutable:

    # chmod +x /etc/init.d/postgresql

Inicie PostgreSQL:

    # /etc/init.d/postgresql start

Compruebe si el extremo de Hola de PostgreSQL se encuentra en:

    # netstat -tunlp|grep 1999

Debería ver Hola después de salida:

![imagen](./media/postgresql-install/no3.png)

## <a name="connect-toohello-postgres-database"></a>Conectar la base de datos de toohello Postgres
Cambiar una vez más toohello postgres usuario:

    # su - postgres

Cree una base de datos de Postgres:

    $ createdb events

Conectar la base de datos de eventos de toohello que acaba de crear:

    $ psql -d events

## <a name="create-and-delete-a-postgres-table"></a>Creación y eliminación de una tabla de Postgres
Ahora que ha conectado toohello base de datos, puede crear tablas en ella.

Por ejemplo, puede crear una nueva tabla de ejemplo Postgres mediante Hola siguiente comando:

    CREATE TABLE potluck (name VARCHAR(20),    food VARCHAR(30),    confirmed CHAR(1), signup_date DATE);

Ahora ha configurado una tabla de cuatro columnas con hello siguiendo los nombres de columna y restricciones:

1. Hola "name" columna ha sido limitado por hello VARCHAR comando toobe en 20 caracteres de longitud.
2. columna de "food" Hello indica alimento de Hola que mostrará cada persona. VARCHAR limita este toobe texto en 30 caracteres.
3. Hola "confirmado" registros de columna si persona Hola ha para RSVP Fiesta americana toohello. los valores aceptables de Hello son "S" y "N".
4. fecha"Hello" columna se muestra cuando registró para eventos de Hola. Postgres requiere que las fechas se escriban como aaaa-mm-dd.

Debería ver Hola siguiente si la tabla se ha creado correctamente:

![imagen](./media/postgresql-install/no4.png)

También puede comprobar estructura de la tabla de hello mediante Hola siguiente comando:

![imagen](./media/postgresql-install/no5.png)

### <a name="add-data-tooa-table"></a>Agregar datos tooa tabla
En primer lugar, inserte información en una fila:

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('John', 'Casserole', 'Y', '2012-04-11');

Debería ver este resultado:

![imagen](./media/postgresql-install/no6.png)

Puede agregar un par más personas toohello tabla así. Estas son algunas opciones, o bien puede crear las suyas propias:

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Sandy', 'Key Lime Tarts', 'N', '2012-04-14');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES ('Tom', 'BBQ','Y', '2012-04-18');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Tina', 'Salad', 'Y', '2012-04-18');

### <a name="show-tables"></a>Visualización de tablas
Usar hello después tooshow una tabla de comandos:

    select * from potluck;

salida de Hello es:

![imagen](./media/postgresql-install/no7.png)

### <a name="delete-data-in-a-table"></a>Eliminación de datos de una tabla
Usar hello comando toodelete datos en una tabla siguientes:

    delete from potluck where name=’John’;

Esto elimina toda la información de Hola Hola fila "John". salida de Hello es:

![imagen](./media/postgresql-install/no8.png)

### <a name="update-data-in-a-table"></a>Actualización de los datos de una tabla
Usar hello comando tooupdate datos siguientes en una tabla. En este primer lugar, Sandy ha confirmado que asista a, por lo que se cambiará su RSVP de "N" demasiado "Y":

     UPDATE potluck set confirmed = 'Y' WHERE name = 'Sandy';


## <a name="get-more-information-about-postgresql"></a>Obtener más información sobre PostgreSQL
Ahora que ha completado la instalación de Hola de PostgreSQL en una máquina virtual Linux de Azure, puede disfrutar de su uso en Azure. toolearn más información acerca de PostgreSQL, visite hello [sitio Web de PostgreSQL](http://www.postgresql.org/).

