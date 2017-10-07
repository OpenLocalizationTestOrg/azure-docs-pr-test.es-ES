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
# <a name="install-and-configure-postgresql-on-azure"></a><span data-ttu-id="ec0d5-103">Instalación y configuración de PostgreSQL en Azure</span><span class="sxs-lookup"><span data-stu-id="ec0d5-103">Install and configure PostgreSQL on Azure</span></span>
<span data-ttu-id="ec0d5-104">PostgreSQL es una base de datos de código abierto avanzados similares tooOracle y DB2.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-104">PostgreSQL is an advanced open-source database similar tooOracle and DB2.</span></span> <span data-ttu-id="ec0d5-105">Incluye características preparadas para el ámbito empresarial, como el cumplimiento de ACID completo, un procesamiento transaccional confiable y un control de simultaneidad de múltiples versiones.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-105">It includes enterprise-ready features such as full ACID compliance, reliable transactional processing, and multi-version concurrency control.</span></span> <span data-ttu-id="ec0d5-106">También admite estándares como ANSI SQL y SQL/MED (incluidos los contenedores de datos externos para Oracle, MySQL, MongoDB y muchas otras).</span><span class="sxs-lookup"><span data-stu-id="ec0d5-106">It also supports standards such as ANSI SQL and SQL/MED (including foreign data wrappers for Oracle, MySQL, MongoDB, and many others).</span></span> <span data-ttu-id="ec0d5-107">Es altamente extensible al admitir más de 12 lenguajes procedimentales, índices GIN y GiST, datos espaciales y múltiples características NoSQL para JSON o aplicaciones basadas en clave-valor.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-107">It is highly extensible with support for over 12 procedural languages, GIN and GiST indexes, spatial data support, and multiple NoSQL-like features for JSON or key-value-based applications.</span></span>

<span data-ttu-id="ec0d5-108">En este artículo, aprenderá cómo tooinstall y configurar PostgreSQL en una máquina virtual de Azure ejecutan Linux.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-108">In this article, you will learn how tooinstall and configure PostgreSQL on an Azure virtual machine running Linux.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-postgresql"></a><span data-ttu-id="ec0d5-109">Instalación de PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="ec0d5-109">Install PostgreSQL</span></span>
> [!NOTE]
> <span data-ttu-id="ec0d5-110">Ya debe tener una máquina virtual con Linux en orden toocomplete este tutorial.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-110">You must already have an Azure virtual machine running Linux in order toocomplete this tutorial.</span></span> <span data-ttu-id="ec0d5-111">toocreate y configurar una VM Linux antes de continuar, consulte la [tutorial de la máquina virtual de Linux de Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ec0d5-111">toocreate and set up a Linux VM before proceeding, see the [Azure Linux VM tutorial](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

<span data-ttu-id="ec0d5-112">En este caso, utilice puerto 1999 como Hola puerto PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-112">In this case, use port 1999 as hello PostgreSQL port.</span></span>  

<span data-ttu-id="ec0d5-113">Conectar toohello VM de Linux que creó mediante PuTTY.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-113">Connect toohello Linux VM you created via PuTTY.</span></span> <span data-ttu-id="ec0d5-114">Si se trata de hello primera vez que se está utilizando una VM de Linux de Azure, consulte [cómo tooUse SSH con Linux en Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toolearn cómo PuTTY toouse tooconnect tooa VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-114">If this is hello first time you're using an Azure Linux VM, see [How tooUse SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toolearn how toouse PuTTY tooconnect tooa Linux VM.</span></span>

1. <span data-ttu-id="ec0d5-115">Siguiente ejecución Hola comando tooswitch toohello raíz (Administrador):</span><span class="sxs-lookup"><span data-stu-id="ec0d5-115">Run hello following command tooswitch toohello root (admin):</span></span>
   
        # sudo su -
2. <span data-ttu-id="ec0d5-116">Algunas distribuciones tienen dependencias que se deben instalar antes de instalar PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-116">Some distributions have dependencies that you must install before installing PostgreSQL.</span></span> <span data-ttu-id="ec0d5-117">Busque la distribución en esta lista y ejecute el comando adecuado de hello:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-117">Check for your distro in this list and run hello appropriate command:</span></span>
   
   * <span data-ttu-id="ec0d5-118">Linux basado en Red Hat:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-118">Red Hat base Linux:</span></span>
     
           # yum install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
   * <span data-ttu-id="ec0d5-119">Linux basado en Debian:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-119">Debian base Linux:</span></span>
     
            # apt-get install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam libxslt-devel tcl-devel python-devel -y  
   * <span data-ttu-id="ec0d5-120">Linux SUSE:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-120">SUSE Linux:</span></span>
     
           # zypper install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
3. <span data-ttu-id="ec0d5-121">Descargar PostgreSQL en el directorio raíz de hello y, a continuación, descomprima el paquete de hello:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-121">Download PostgreSQL into hello root directory, and then unzip hello package:</span></span>
   
        # wget https://ftp.postgresql.org/pub/source/v9.3.5/postgresql-9.3.5.tar.bz2 -P /root/
   
        # tar jxvf  postgresql-9.3.5.tar.bz2
   
    <span data-ttu-id="ec0d5-122">Hola anterior es un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-122">hello above is an example.</span></span> <span data-ttu-id="ec0d5-123">Puede encontrar Hola más detallada descargar dirección Hola [índicede/pub/origen/](https://ftp.postgresql.org/pub/source/).</span><span class="sxs-lookup"><span data-stu-id="ec0d5-123">You can find hello more detailed download address in hello [Index of /pub/source/](https://ftp.postgresql.org/pub/source/).</span></span>
4. <span data-ttu-id="ec0d5-124">compilación hello toostart, ejecute estos comandos:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-124">toostart hello build, run these commands:</span></span>
   
        # cd postgresql-9.3.5
   
        # ./configure --prefix=/opt/postgresql-9.3.5
5. <span data-ttu-id="ec0d5-125">Si desea toobuild todo lo que pueden crearse, incluida documentación hello (páginas HTML y man) y módulos adicionales (hogar), ejecute hello siguiente comando en su lugar:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-125">If  you want toobuild everything that can be built, including hello documentation (HTML and man pages) and additional modules (contrib), run hello following command instead:</span></span>
   
        # gmake install-world
   
    <span data-ttu-id="ec0d5-126">Debería recibir Hola siguiente mensaje de confirmación:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-126">You should receive hello following confirmation message:</span></span>
   
        PostgreSQL, contrib, and documentation successfully made. Ready tooinstall.

## <a name="configure-postgresql"></a><span data-ttu-id="ec0d5-127">Configuración de PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="ec0d5-127">Configure PostgreSQL</span></span>
1. <span data-ttu-id="ec0d5-128">(Opcional) Crear un hello tooshorten de vínculo simbólico PostgreSQL referencia toonot incluyen el número de versión de hello:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-128">(Optional) Create a symbolic link tooshorten hello PostgreSQL reference toonot include hello version number:</span></span>
   
        # ln -s /opt/pgsql9.3.5 /opt/pgsql
2. <span data-ttu-id="ec0d5-129">Cree un directorio de base de datos de hello:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-129">Create a directory for hello database:</span></span>
   
        # mkdir -p /opt/pgsql_data
3. <span data-ttu-id="ec0d5-130">Cree un usuario no raíz y modifique el perfil del usuario.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-130">Create a non-root user and modify that user’s profile.</span></span> <span data-ttu-id="ec0d5-131">A continuación, cambie toothis nuevo usuario (denominado *postgres* en nuestro ejemplo):</span><span class="sxs-lookup"><span data-stu-id="ec0d5-131">Then, switch toothis new user (called *postgres* in our example):</span></span>
   
        # useradd postgres
   
        # chown -R postgres.postgres /opt/pgsql_data
   
        # su - postgres
   
   > [!NOTE]
   > <span data-ttu-id="ec0d5-132">Por motivos de seguridad, PostgreSQL utiliza un tooinitialize de usuario no es de raíz, iniciar o cerrar la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-132">For security reasons, PostgreSQL uses a non-root user tooinitialize, start, or shut down hello database.</span></span>
   > 
   > 
4. <span data-ttu-id="ec0d5-133">Editar hello *bash_profile* archivo escribiendo los siguientes comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-133">Edit hello *bash_profile* file by entering hello commands below.</span></span> <span data-ttu-id="ec0d5-134">Estas líneas se agregarán toohello final de hello *bash_profile* archivo:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-134">These lines will be added toohello end of hello *bash_profile* file:</span></span>
   
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
5. <span data-ttu-id="ec0d5-135">Ejecute hello *bash_profile* archivo:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-135">Execute hello *bash_profile* file:</span></span>
   
        $ source .bash_profile
6. <span data-ttu-id="ec0d5-136">Validar la instalación mediante el uso de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-136">Validate your installation by using hello following command:</span></span>
   
        $ which psql
   
    <span data-ttu-id="ec0d5-137">Si la instalación se realiza correctamente, verá Hola después de respuesta:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-137">If your installation is successful, you will see hello following response:</span></span>
   
        /opt/pgsql/bin/psql
7. <span data-ttu-id="ec0d5-138">También puede comprobar la versión de Hola PostgreSQL:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-138">You can also check hello PostgreSQL version:</span></span>
   
        $ psql -V
8. <span data-ttu-id="ec0d5-139">Inicializar base de datos de hello:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-139">Initialize hello database:</span></span>
   
        $ initdb -D $PGDATA -E UTF8 --locale=C -U postgres -W
   
    <span data-ttu-id="ec0d5-140">Debería recibir Hola después de salida:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-140">You should receive hello following output:</span></span>

![imagen](./media/postgresql-install/no1.png)

## <a name="set-up-postgresql"></a><span data-ttu-id="ec0d5-142">Configuración de PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="ec0d5-142">Set up PostgreSQL</span></span>
<!--    [postgres@ test ~]$ exit -->

<span data-ttu-id="ec0d5-143">Ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-143">Run hello following commands:</span></span>

    # cd /root/postgresql-9.3.5/contrib/start-scripts

    # cp linux /etc/init.d/postgresql

<span data-ttu-id="ec0d5-144">Modificar dos variables en el archivo de hello /etc/init.d/postgresql.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-144">Modify two variables in hello /etc/init.d/postgresql file.</span></span> <span data-ttu-id="ec0d5-145">prefijo de Hola se establece la ruta de instalación de toohello de PostgreSQL: **pgsql/opt/**.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-145">hello prefix is set toohello installation path of PostgreSQL: **/opt/pgsql**.</span></span> <span data-ttu-id="ec0d5-146">PGDATA se establece toohello ruta de acceso de almacenamiento de datos de PostgreSQL: **pgsql_data/opt/**.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-146">PGDATA is set toohello data storage path of PostgreSQL: **/opt/pgsql_data**.</span></span>

    # sed -i '32s#usr/local#opt#' /etc/init.d/postgresql

    # sed -i '35s#usr/local/pgsql/data#opt/pgsql_data#' /etc/init.d/postgresql

![imagen](./media/postgresql-install/no2.png)

<span data-ttu-id="ec0d5-148">Cambiar Hola archivo toomake lo ejecutable:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-148">Change hello file toomake it executable:</span></span>

    # chmod +x /etc/init.d/postgresql

<span data-ttu-id="ec0d5-149">Inicie PostgreSQL:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-149">Start PostgreSQL:</span></span>

    # /etc/init.d/postgresql start

<span data-ttu-id="ec0d5-150">Compruebe si el extremo de Hola de PostgreSQL se encuentra en:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-150">Check if hello endpoint of PostgreSQL is on:</span></span>

    # netstat -tunlp|grep 1999

<span data-ttu-id="ec0d5-151">Debería ver Hola después de salida:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-151">You should see hello following output:</span></span>

![imagen](./media/postgresql-install/no3.png)

## <a name="connect-toohello-postgres-database"></a><span data-ttu-id="ec0d5-153">Conectar la base de datos de toohello Postgres</span><span class="sxs-lookup"><span data-stu-id="ec0d5-153">Connect toohello Postgres database</span></span>
<span data-ttu-id="ec0d5-154">Cambiar una vez más toohello postgres usuario:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-154">Switch toohello postgres user once again:</span></span>

    # su - postgres

<span data-ttu-id="ec0d5-155">Cree una base de datos de Postgres:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-155">Create a Postgres database:</span></span>

    $ createdb events

<span data-ttu-id="ec0d5-156">Conectar la base de datos de eventos de toohello que acaba de crear:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-156">Connect toohello events database that you just created:</span></span>

    $ psql -d events

## <a name="create-and-delete-a-postgres-table"></a><span data-ttu-id="ec0d5-157">Creación y eliminación de una tabla de Postgres</span><span class="sxs-lookup"><span data-stu-id="ec0d5-157">Create and delete a Postgres table</span></span>
<span data-ttu-id="ec0d5-158">Ahora que ha conectado toohello base de datos, puede crear tablas en ella.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-158">Now that you have connected toohello database, you can create tables in it.</span></span>

<span data-ttu-id="ec0d5-159">Por ejemplo, puede crear una nueva tabla de ejemplo Postgres mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-159">For example, create a new example Postgres table by using hello following command:</span></span>

    CREATE TABLE potluck (name VARCHAR(20),    food VARCHAR(30),    confirmed CHAR(1), signup_date DATE);

<span data-ttu-id="ec0d5-160">Ahora ha configurado una tabla de cuatro columnas con hello siguiendo los nombres de columna y restricciones:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-160">You have now set up a four-column table with hello following column names and restrictions:</span></span>

1. <span data-ttu-id="ec0d5-161">Hola "name" columna ha sido limitado por hello VARCHAR comando toobe en 20 caracteres de longitud.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-161">hello “name” column has been limited by hello VARCHAR command toobe under 20 characters long.</span></span>
2. <span data-ttu-id="ec0d5-162">columna de "food" Hello indica alimento de Hola que mostrará cada persona.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-162">hello “food” column indicates hello food item that each person will bring.</span></span> <span data-ttu-id="ec0d5-163">VARCHAR limita este toobe texto en 30 caracteres.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-163">VARCHAR limits this text toobe under 30 characters.</span></span>
3. <span data-ttu-id="ec0d5-164">Hola "confirmado" registros de columna si persona Hola ha para RSVP Fiesta americana toohello.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-164">hello “confirmed” column records whether hello person has RSVP’d toohello potluck.</span></span> <span data-ttu-id="ec0d5-165">los valores aceptables de Hello son "S" y "N".</span><span class="sxs-lookup"><span data-stu-id="ec0d5-165">hello acceptable values are "Y" and "N".</span></span>
4. <span data-ttu-id="ec0d5-166">fecha"Hello" columna se muestra cuando registró para eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-166">hello “date” column shows when they signed up for hello event.</span></span> <span data-ttu-id="ec0d5-167">Postgres requiere que las fechas se escriban como aaaa-mm-dd.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-167">Postgres requires that dates be written as yyyy-mm-dd.</span></span>

<span data-ttu-id="ec0d5-168">Debería ver Hola siguiente si la tabla se ha creado correctamente:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-168">You should see hello following if your table has been successfully created:</span></span>

![imagen](./media/postgresql-install/no4.png)

<span data-ttu-id="ec0d5-170">También puede comprobar estructura de la tabla de hello mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-170">You can also check hello table structure by using hello following command:</span></span>

![imagen](./media/postgresql-install/no5.png)

### <a name="add-data-tooa-table"></a><span data-ttu-id="ec0d5-172">Agregar datos tooa tabla</span><span class="sxs-lookup"><span data-stu-id="ec0d5-172">Add data tooa table</span></span>
<span data-ttu-id="ec0d5-173">En primer lugar, inserte información en una fila:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-173">First, insert information into a row:</span></span>

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('John', 'Casserole', 'Y', '2012-04-11');

<span data-ttu-id="ec0d5-174">Debería ver este resultado:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-174">You should see this output:</span></span>

![imagen](./media/postgresql-install/no6.png)

<span data-ttu-id="ec0d5-176">Puede agregar un par más personas toohello tabla así.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-176">You can add a couple more people toohello table as well.</span></span> <span data-ttu-id="ec0d5-177">Estas son algunas opciones, o bien puede crear las suyas propias:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-177">Here are some options, or you can create your own:</span></span>

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Sandy', 'Key Lime Tarts', 'N', '2012-04-14');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES ('Tom', 'BBQ','Y', '2012-04-18');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Tina', 'Salad', 'Y', '2012-04-18');

### <a name="show-tables"></a><span data-ttu-id="ec0d5-178">Visualización de tablas</span><span class="sxs-lookup"><span data-stu-id="ec0d5-178">Show tables</span></span>
<span data-ttu-id="ec0d5-179">Usar hello después tooshow una tabla de comandos:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-179">Use hello following command tooshow a table:</span></span>

    select * from potluck;

<span data-ttu-id="ec0d5-180">salida de Hello es:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-180">hello output is:</span></span>

![imagen](./media/postgresql-install/no7.png)

### <a name="delete-data-in-a-table"></a><span data-ttu-id="ec0d5-182">Eliminación de datos de una tabla</span><span class="sxs-lookup"><span data-stu-id="ec0d5-182">Delete data in a table</span></span>
<span data-ttu-id="ec0d5-183">Usar hello comando toodelete datos en una tabla siguientes:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-183">Use hello following command toodelete data in a table:</span></span>

    delete from potluck where name=’John’;

<span data-ttu-id="ec0d5-184">Esto elimina toda la información de Hola Hola fila "John".</span><span class="sxs-lookup"><span data-stu-id="ec0d5-184">This deletes all hello information in hello "John" row.</span></span> <span data-ttu-id="ec0d5-185">salida de Hello es:</span><span class="sxs-lookup"><span data-stu-id="ec0d5-185">hello output is:</span></span>

![imagen](./media/postgresql-install/no8.png)

### <a name="update-data-in-a-table"></a><span data-ttu-id="ec0d5-187">Actualización de los datos de una tabla</span><span class="sxs-lookup"><span data-stu-id="ec0d5-187">Update data in a table</span></span>
<span data-ttu-id="ec0d5-188">Usar hello comando tooupdate datos siguientes en una tabla.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-188">Use hello following command tooupdate data in a table.</span></span> <span data-ttu-id="ec0d5-189">En este primer lugar, Sandy ha confirmado que asista a, por lo que se cambiará su RSVP de "N" demasiado "Y":</span><span class="sxs-lookup"><span data-stu-id="ec0d5-189">For this one, Sandy has confirmed that she is attending, so we will change her RSVP from "N" too"Y":</span></span>

     UPDATE potluck set confirmed = 'Y' WHERE name = 'Sandy';


## <a name="get-more-information-about-postgresql"></a><span data-ttu-id="ec0d5-190">Obtener más información sobre PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="ec0d5-190">Get more information about PostgreSQL</span></span>
<span data-ttu-id="ec0d5-191">Ahora que ha completado la instalación de Hola de PostgreSQL en una máquina virtual Linux de Azure, puede disfrutar de su uso en Azure.</span><span class="sxs-lookup"><span data-stu-id="ec0d5-191">Now that you have completed hello installation of PostgreSQL in an Azure Linux VM, you can enjoy using it in Azure.</span></span> <span data-ttu-id="ec0d5-192">toolearn más información acerca de PostgreSQL, visite hello [sitio Web de PostgreSQL](http://www.postgresql.org/).</span><span class="sxs-lookup"><span data-stu-id="ec0d5-192">toolearn more about PostgreSQL, visit hello [PostgreSQL website](http://www.postgresql.org/).</span></span>

