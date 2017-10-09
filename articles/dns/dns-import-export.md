---
title: "aaaImport y exportación de una zona de dominio archivo tooAzure DNS mediante Azure CLI 1.0 | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooimport y exportar un DNS de zona DNS del archivo tooAzure mediante el uso de Azure CLI 1.0"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: f5797782-3005-4663-a488-ac0089809010
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 4c3163395e151e9934c730349b828c612491016f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-a-dns-zone-file-using-hello-azure-cli-10"></a>Importar y exportar un archivo de zona DNS mediante Hola 1.0 de CLI de Azure 

Este artículo le guiará a través de cómo tooimport y exportación de archivos de zona DNS para el uso de DNS de Azure Hola 1.0 de CLI de Azure.

## <a name="introduction-toodns-zone-migration"></a>Migración de zona tooDNS de introducción

Un archivo de zona DNS es un archivo de texto que contiene los detalles de cada registro de sistema de nombres de dominio (DNS) en la zona de Hola. Sigue un formato estándar, por lo que es adecuado para transferir registros DNS entre distintos sistemas DNS. Mediante un archivo de zona es una rápida, confiable y cómodamente tootransfer una zona DNS dentro o fuera de DNS de Azure.

DNS de Azure admite la importación y exportación de archivos de zona mediante el uso de hello Azure interfaz de línea de comandos (CLI). Importación de archivos de zona es **no** admiten a través de Azure PowerShell u Hola portal de Azure.

Hola 1.0 de CLI de Azure es una herramienta de línea de comandos multiplataforma utilizada para administrar los servicios de Azure. Está disponible para plataformas de Windows, Mac y Linux de Hola de hello [página de descargas de Azure](https://azure.microsoft.com/downloads/). La compatibilidad multiplataforma es importante para importar y exportar archivos de zona, porque Hola software más comunes del servidor de nombre, [enlazar](https://www.isc.org/downloads/bind/), normalmente se ejecuta en Linux.

> [!NOTE]
> Actualmente hay dos versiones de hello CLI de Azure. CLI1.0 se basa en Node.js y tiene comandos que comienzan por "azure".
> CLI2.0 se basa en Python y tiene comandos que empiezan por "az". Aunque se admite la importación de archivos de zona en ambas versiones, se recomienda usar comandos CLI1.0 hello, como se describe en esta página.

## <a name="obtain-your-existing-dns-zone-file"></a>Obtención del archivo de zona DNS existente

Antes de importar un archivo de zona DNS en DNS de Azure, deberá tooobtain una copia del archivo de zona de Hola. origen de Hola de este archivo depende de donde se hospeda actualmente la zona DNS Hola.

* Si la zona DNS está hospedada por un servicio de socios comerciales (como un registrador de dominios, un proveedor de hospedaje de DNS dedicado o un proveedor alternativo en la nube), que el servicio debe proporcionar el archivo de zona DNS de hello capacidad toodownload Hola.
* Si la zona DNS está hospedada en el DNS de Windows, carpeta de archivos de zona de Hola de hello predeterminada es **%systemroot%\system32\dns**. archivo de zona de tooeach de ruta de acceso completa de Hello también se muestra en hello **General** ficha de consola DNS de Hola.
* Si la zona DNS está hospedada por mediante un enlace, la ubicación de Hola Hola del archivo de zona para cada zona se especifica en el archivo de configuración de enlace de hello **named.conf**.

> [!NOTE]
> Los archivos de zona descargados de GoDaddy tienen un formato ligeramente diferente al estándar. Necesita toocorrect esto antes de importar estos archivos de zona DNS de Azure.
>
> Se especifican nombres DNS en hello RDATA de cada registro DNS como nombres completos, pero no tienen una finalización "." Esto significa que otros sistemas DNS los interpretan como nombres relativos. Debe terminar de tooedit Hola zona archivo tooappend Hola "." tootheir nombres antes de importarlos en DNS de Azure.
>
> Por ejemplo, hello registro CNAME "" www 3600 en contoso.com CNAME"debe cambiarse demasiado"www 3600 CNAME en contoso.com."
> (con una terminación ".").

## <a name="import-a-dns-zone-file-into-azure-dns"></a>Importación de un archivo de zona DNS a DNS de Azure

Si aún no existe, al importar un archivo de zona se crea una nueva zona DNS de Azure. Si ya existe una zona de hello, hello conjuntos de registros de archivo de zona de hello deben combinarse con conjuntos de registros existentes de Hola.

### <a name="merge-behavior"></a>Comportamiento de combinación

* De forma predeterminada, se combinan los conjuntos de registros nuevos y existentes. Los registros idénticos dentro de un conjunto de registros combinado se desduplican.
* O bien, mediante la especificación de hello `--force` opción, Hola reemplaza de proceso de importación conjuntos de registro existente con nuevos conjuntos de registros. Conjuntos de registros existentes que no tienen un registro correspondiente establecido en el archivo de zona importado hello no se quitará.
* Cuando se combinan los conjuntos de registros, hello tiempo toolive (TTL) de conjuntos de registros preexistentes se usa. Cuando `--force` es utilizado, se usa Hola TTL del nuevo conjunto de registros de Hola.
* Inicio de parámetros de autoridad (SOA) (excepto `host`) siempre se toman del archivo de zona importado hello, independientemente de si `--force` se utiliza. De forma similar, para establecer en vértice de la zona de Hola Hola registro de servidor de nombres, hello TTL siempre se toma del archivo de zona importado Hola.
* Un registro CNAME importado no reemplaza un CNAME existente grabar con hello mismo nombre, a menos que hello `--force` se especifica el parámetro.
* Cuando se produce un conflicto entre un registro CNAME y otro registro de hello mismo nombre pero es diferente, escriba (sin tener en cuenta que es existente o nueva), se conserva el registro existente de Hola. Este valor es independiente del uso de Hola de `--force`.

### <a name="additional-information-about-importing"></a>Información adicional sobre la importación

Hello notas siguientes proporcionan detalles técnicos adicionales acerca de la zona de hello el proceso de importación.

* Hola `$TTL` directiva es opcional y se admite. Si no `$TTL` recibe la directiva, se importan los registros sin un TTL explícito establecer tooa TTL predeterminado de 3600 segundos. Cuando dos registros en hello mismo conjunto de registros especifica TTLs diferentes, se usa un valor inferior Hola.
* Hola `$ORIGIN` directiva es opcional y se admite. Si no `$ORIGIN` se establece, el valor predeterminado de hello valor utilizado es el nombre de la zona de hello según se especifica en la línea de comandos de hello (además de terminación de Hola ".").
* Hola `$INCLUDE` y `$GENERATE` no se admiten directivas.
* Se admiten los tipos de registro siguientes: A, AAAA, CNAME, MX, NS, SOA, SRV y TXT.
* Hola registro SOA DNS de Azure se crea automáticamente cuando se crea una zona. Cuando se importa un archivo de zona, todos los parámetros SOA se toman del archivo de zona de hello *excepto* hello `host` parámetro. Este parámetro usa valor Hola proporcionada por DNS de Azure. Esto es porque este parámetro debe hacer referencia a servidor de nombre principal de toohello proporcionado por DNS de Azure.
* registro de servidor de nombres Hola establecido en vértice de la zona de hello también se crea automáticamente DNS de Azure cuando se crea la zona de Hola. Solo hello TTL de este conjunto de registros se importa. Estos registros contienen nombres de servidor de nombre de hello proporcionados por DNS de Azure. valores de hello contenidos en el archivo de zona importado hello no sobrescribe los datos de registro de Hello.
* Durante la versión preliminar pública, DNS de Azure admite solamente registros TXT de cadena única. MultiString registros TXT se pueden too255 concatenados y el truncado caracteres.

### <a name="cli-format-and-values"></a>Valores y formato de la CLI

formato de Hola de tooimport de comando de CLI de Azure de hello una zona DNS es:

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

Valores:

* `<resource group>`es el nombre de Hola Hola del grupo de recursos para la zona de hello en DNS de Azure.
* `<zone name>`es el nombre de Hola de zona de Hola.
* `<zone file name>`es Hola/nombre de ruta de hello zona archivo toobe importado.

Si una zona con este nombre no existe en el grupo de recursos de hello, se crea automáticamente. Si hello zona ya existe, hello conjuntos de registros importados se combinan con los conjuntos de registros existentes. toooverwrite Hola existente conjuntos de registros, usar hello `--force` opción.

formato de hello tooverify de un archivo de zona sin realmente importarlo, use hello `--parse-only` opción.

### <a name="step-1-import-a-zone-file"></a>Paso 1. Importación de un archivo de zona

un archivo de zona para la zona de hello tooimport **contoso.com**.

1. Inicie sesión en tooyour suscripción de Azure mediante Hola 1.0 de CLI de Azure.

    ```azurecli
    azure login
    ```

2. Seleccione la suscripción de Hola donde desea toocreate la nueva zona DNS.

    ```azurecli
    azure account set <subscription name>
    ```

3. DNS de Azure es un servicio de Azure solo el Administrador de recursos, por lo que Hola CLI de Azure debe ser el modo de administrador tooResource desactivados.

    ```azurecli
    azure config mode arm
    ```

4. Antes de usar el servicio DNS de Azure de hello, debe registrar el proveedor de recursos de Microsoft.Network de suscripción toouse Hola. (Se trata de una operación única para cada suscripción).

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. Si no tiene ninguno todavía, también deberá toocreate un grupo de recursos del Administrador de recursos.

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. zona de hello tooimport **contoso.com** desde archivo hello **contoso.com.txt** en una nueva zona DNS en el grupo de recursos de hello **myresourcegroup**, ejecute el comando de hello `azure network dns zone import`.<BR>Este comando carga el archivo de zona de hello y analizarlo. una serie de comandos ejecuta el comando de Hello en zona de hello Azure DNS servicio toocreate hello y todos los registros de Hola se establece en la zona de Hola. Hola comando informa del progreso en la ventana de la consola de hello, junto con los errores o advertencias. Como conjuntos de registros se crean en serie, puede tardar unos tooimport minutos un archivo de zona de gran tamaño.

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-hello-zone"></a>Paso 2: Compruebe la zona de Hola

tooverify Hola zona de DNS después de importar el archivo hello, puede usar cualquiera de los siguientes métodos de hello:

* Puede enumerar los registros de hello mediante Hola siguiente comando de CLI de Azure:

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* Puede enumerar los registros de hello mediante cmdlet de PowerShell de hello `Get-AzureRmDnsRecordSet`.
* Puede usar `nslookup` tooverify la resolución de nombres para los registros de Hola. Como zona de hello no delega todavía, deberá servidores de nombres de DNS de Azure correcta de toospecify Hola explícitamente. Hello en el ejemplo siguiente muestra cómo nombres de servidor de nombre de tooretrieve Hola asignan toohello zona. TI también muestra cómo grabar utilizando tooquery Hola "www" `nslookup`.

        C:\>azure network dns record-set show myresourcegroup contoso.com @ NS
        info:Executing command network dns record-set show
        + Looking up hello DNS Record Set "@" of type "NS"
        data:Id: /subscriptions/.../resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com/NS/@
        data:Name: @
        data:Type: Microsoft.Network/dnszones/NS
        data:Location: global
        data:TTL : 3600
        data:NS records
        data:Name server domain name : ns1-01.azure-dns.com
        data:Name server domain name : ns2-01.azure-dns.net
        data:Name server domain name : ns3-01.azure-dns.org
        data:Name server domain name : ns4-01.azure-dns.info
        data:
        info:network dns record-set show command OK

        C:\> nslookup www.contoso.com ns1-01.azure-dns.com

        Server: ns1-01.azure-dns.com
        Address:  40.90.4.1

        Name:www.contoso.com
        Addresses:  134.170.185.46
        134.170.188.221

### <a name="step-3-update-dns-delegation"></a>Paso 3: Actualización de la delegación de DNS

Después de comprobar que la zona de Hola se ha importado correctamente, necesita tooupdate Hola DNS delegación toopoint toohello servidores de nombres DNS de Azure. Para obtener más información, vea el artículo de hello [actualizar delegación DNS de hello](dns-domain-delegation.md).

## <a name="export-a-dns-zone-file-from-azure-dns"></a>Exportación de un archivo de zona DNS de DNS de Azure

formato de Hola de tooimport de comando de CLI de Azure de hello una zona DNS es:

```azurecli
azure network dns zone export [options] <resource group> <zone name> <zone file name>
```

Valores:

* `<resource group>`es el nombre de Hola Hola del grupo de recursos para la zona de hello en DNS de Azure.
* `<zone name>`es el nombre de Hola de zona de Hola.
* `<zone file name>`es Hola/nombre de ruta de toobe de archivo de zona Hola exportado.

Como con la importación de la zona de hello, primero debe toosign en, elija su suscripción y configurar el modo de administrador de recursos de toouse de hello CLI de Azure.

### <a name="tooexport-a-zone-file"></a>tooexport un archivo de zona

1. Inicie sesión en tooyour suscripción de Azure mediante Hola CLI de Azure.

    ```azurecli
    azure login
    ```

2. Seleccione la suscripción de Hola donde desea toocreate la zona DNS.

    ```azurecli
    azure account set <subscription name>
    ```

3. DNS de Azure es un servicio exclusivo del Administrador de recursos de Azure. Hola CLI de Azure debe ser el modo de administrador tooResource desactivados.

    ```azurecli
    azure config mode arm
    ```

4. tooexport Hola zona DNS de Azure existente **contoso.com** en grupo de recursos **myresourcegroup** toohello archivo **contoso.com.txt** (en la carpeta actual de hello), ejecute `azure network dns zone export`. Este comando llama Hola tooenumerate del servicio DNS de Azure conjuntos de registros en la zona de Hola y Exportar archivo de zona de hello resultados tooa compatible con el enlace.

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
