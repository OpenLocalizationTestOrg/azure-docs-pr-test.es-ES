---
title: "aaaHow toogenerate y transferencia de claves protegidas con HSM para el almacén de claves de Azure | Documentos de Microsoft"
description: "Utilice este toohelp artículo planear, generar y, a continuación, transferir su propios toouse claves protegidas con HSM al almacén de claves de Azure. También se denomina BYOK o \"traiga su propia clave\"."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 51abafa1-812b-460f-a129-d714fdc391da
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: ambapat
ms.openlocfilehash: 3bb234bd1c4b81770542ccf7110e256385ca3309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogenerate-and-transfer-hsm-protected-keys-for-azure-key-vault"></a>¿Cómo toogenerate y transferencia de claves protegidas con HSM para el almacén de claves de Azure
## <a name="introduction"></a>Introducción
Para mayor seguridad, cuando se utiliza el almacén de claves de Azure, puede importar o generar claves en módulos de seguridad de hardware (HSM) que no dejan nunca el límite de HSM Hola. Este escenario es a menudo denominado tooas *traiga su propia clave*, o BYOK. Hola HSM son FIPS 140-2 nivel 2 validado. Almacén de claves de Azure usa familia Thales nShield de HSM tooprotect sus claves.

Utilice la información de hello en este tema toohelp planear, generar y, a continuación, transferir su propios toouse claves protegidas con HSM al almacén de claves de Azure.

Esta funcionalidad no está disponible para Azure China.

> [!NOTE]
> Para obtener más información sobre el Almacén de claves de Azure, consulte [¿Qué es el Almacén de claves de Azure?](key-vault-whatis.md)  
>
> Para ver tutorial introductorio, que incluye la creación de un almacén de claves para claves protegidas con HSM, consulte [Introducción al Almacén de claves de Azure](key-vault-get-started.md).
>
>

Obtener más información sobre cómo generar y transferir una clave protegida por HSM a través de Internet de hello:

* Generar clave de Hola desde una estación de trabajo sin conexión, lo que reduce la superficie expuesta a ataques Hola.
* clave de Hola se cifra con una clave de intercambio de claves (KEK), que permanece cifrada hasta que se transfieren toohello HSM del almacén de claves de Azure. Solo Hola versión cifrada de la clave deja de estación de trabajo original Hola.
* conjunto de herramientas de Hello establece propiedades en su clave de inquilino que enlaza su clave toohello mundo de seguridad del almacén de claves de Azure. Modo que, después de HSM del almacén de claves de hello Azure reciban y descifren su clave, solamente dichos HSM los pueden usarla. La clave no se puede exportar. Este enlace es impuesto por hello HSM de Thales.
* Hola clave de intercambio de claves (KEK) que es tooencrypt usa la clave se genera dentro de HSM del almacén de claves de Azure de hello y no es exportable. Hola HSM exigen que no puede haber ninguna versión neta de hello KEK fuera Hola HSM. Además, el conjunto de herramientas de hello incluye la atestación desde Thales ese Hola KEK no es exportable y se generó dentro de un HSM genuino que fabricó Thales.
* conjunto de herramientas de Hello incluye la atestación desde Thales ese Hola mundo de seguridad también se generó en un HSM genuino fabricado por Thales el almacén de claves de Azure. Este atestación demuestra tooyou que Microsoft usa hardware genuino.
* Microsoft usa KEK independientes y separa los espacios de seguridad de las distintas regiones geográficas. Esta separación garantiza que su clave pueda usarse solamente en centros de datos en la región de hello en el que se ha cifrado. Por ejemplo, una clave de un cliente europeo no se puede utilizar en centros de datos de América del Norte o Asia.

## <a name="more-information-about-thales-hsms-and-microsoft-services"></a>Más información acerca de los HSM de Thales y los servicios de Microsoft
Thales e-Security es una principales proveedores mundiales de cifrado de datos y ciberseguridad seguridad soluciones toohello servicios financieros, tecnología punta, fabricación, gobierno y sectores tecnológicos. Con una información de gobierno y 40 años trayectoria de protección corporativa, se utilizan las soluciones de Thales por cuatro de hello cinco empresas más grandes el sector energético y aeroespacial. También las utilizan 22 países de la OTAN y protegen más del 80 por ciento de las transacciones de pago mundiales.

Microsoft ha colaborado con el estado de Hola de Thales tooenhance de carátulas de HSM. Estas mejoras permiten beneficios típico de hello tooget de servicios hospedados sin abandonar control sobre las claves. En concreto, estas mejoras permiten que Microsoft administre Hola HSM para que no es necesario. Como una nube de que almacén de claves de servicio, Azure se amplía en muy poco tiempo toomeet picos de uso de su organización. Hola al mismo tiempo, la clave está protegida dentro de los HSM de Microsoft: mantener el control sobre el ciclo de vida de clave de Hola porque generar clave de Hola y transferir los HSM del tooMicrosoft.

## <a name="implementing-bring-your-own-key-byok-for-azure-key-vault"></a>Implementación del método Aportar tu propia clave (BYOK) en el Almacén de claves de Azure
Hola de uso después de obtener información y procedimientos si va a generar su propia clave protegida por HSM y, a continuación, transferirla tooAzure el almacén de claves: Hola aportar su propia escenario clave (BYOK).

## <a name="prerequisites-for-byok"></a>Requisitos previos de BYOK
Vea Hola siguiente tabla para obtener una lista de requisitos previos para aportar su propia clave (BYOK) para el almacén de claves de Azure.

| Requisito | Más información |
| --- | --- |
| Un tooAzure de suscripción |toocreate un almacén de claves de Azure, se necesita una suscripción a Azure: [suscribirse a la versión de prueba gratuita](https://azure.microsoft.com/pricing/free-trial/) |
| Hola claves protegidas con HSM en el toosupport nivel de servicio Premium de almacén de claves de Azure |Para obtener más información sobre los niveles de servicio de Hola y las capacidades de almacén de claves de Azure, vea hello [precios de Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/) sitio Web. |
| HSM de Thales, tarjetas inteligentes y software compatible |Debe tener acceso a tooa módulo de seguridad de Hardware de Thales y al conocimiento operacional básico de HSM de Thales. Vea [módulo de seguridad de Hardware de Thales](https://www.thales-esecurity.com/msrms/buy) de lista de Hola de modelos compatibles o toopurchase un HSM si no tiene uno. |
| Hola después de hardware y software:<ol><li>Una estación de trabajo x64 sin conexión con un sistema operativo Windows 7 y software Thales nShield versión 11.50 o superior.<br/><br/>Si esta estación de trabajo ejecuta Windows 7, debe [instalar Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</li><li>Una estación de trabajo que está conectado toohello Internet y tiene un sistema operativo mínimo de Windows 7 y [Azure PowerShell](/powershell/azure/overview) **versión mínima 1.1.0** instalado.</li><li>Una unidad USB u otro dispositivo de almacenamiento portátil con al menos 16 MB de espacio libre.</li></ol> |Por motivos de seguridad, se recomienda que Hola primera estación de trabajo no está conectado tooa red. Sin embargo, esta recomendación no es de obligado cumplimiento.<br/><br/>Tenga en cuenta que en las instrucciones de Hola que siguen, esta estación de trabajo es estación de trabajo que se hace referencia tooas Hola desconectado.</p></blockquote><br/>Además, si la clave de inquilino es para una red de producción, se recomienda que realice una segunda estación de trabajo independiente toodownload Hola conjunto de herramientas y la carga Hola clave de inquilino. Pero con fines de prueba, puede usar Hola misma estación de trabajo como Hola primero.<br/><br/>Tenga en cuenta que en las instrucciones de Hola que siguen, esta segunda estación de trabajo conectada a Internet la estación de trabajo del hello tooas que se hace referencia.</p></blockquote><br/> |

## <a name="generate-and-transfer-your-key-tooazure-key-vault-hsm"></a>Generar y transferir su clave tooAzure HSM del almacén de claves
Utilizará Hola siguiendo cinco toogenerate de pasos y transferir su clave tooan HSM del almacén de claves de Azure:

* [Paso 1: preparación de la estación de trabajo conectada a Internet](#step-1-prepare-your-internet-connected-workstation)
* [Paso 2: preparación de la estación de trabajo desconectada](#step-2-prepare-your-disconnected-workstation)
* [Paso 3: generación de la clave](#step-3-generate-your-key)
* [Paso 4: preparación de la clave para la transferencia](#step-4-prepare-your-key-for-transfer)
* [Paso 5: Transferir su clave tooAzure el almacén de claves](#step-5-transfer-your-key-to-azure-key-vault)

## <a name="step-1-prepare-your-internet-connected-workstation"></a>Paso 1: preparación de la estación de trabajo conectada a Internet
Este primer paso, Hola seguir los procedimientos descritos en la estación de trabajo que está conectado toohello Internet.

### <a name="step-11-install-azure-powershell"></a>Paso 1.1: instalación de Azure PowerShell
Hola conectada a Internet estación de trabajo, descargue e instale el módulo de PowerShell de Azure de Hola que incluye cmdlets de hello toomanage el almacén de claves de Azure. Esto requiere una versión mínima de 0.8.13.

Para obtener instrucciones de instalación, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).

### <a name="step-12-get-your-azure-subscription-id"></a>Paso 1.2: especificación del identificador de la suscripción a Azure
Inicie una sesión de PowerShell de Azure e inicie sesión en tooyour cuenta de Azure mediante el siguiente comando de hello:

        Add-AzureAccount
En la ventana emergente del explorador de hello, escriba el nombre de usuario de cuenta de Azure y la contraseña. A continuación, usar hello [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) comando:

        Get-AzureSubscription
De salida de hello, busque el identificador de hello para la suscripción de Hola que se va a utilizar para el almacén de claves de Azure. Lo necesitará más adelante.

No cierre la ventana de PowerShell de Azure de hello.

### <a name="step-13-download-hello-byok-toolset-for-azure-key-vault"></a>Paso 1.3: Descargar el conjunto de herramientas BYOK de hello para el almacén de claves de Azure
Vaya toohello Microsoft Download Center y [descargar el conjunto de herramientas de BYOK de almacén de claves de Azure de hello](http://www.microsoft.com/download/details.aspx?id=45345) para su región geográfica o la instancia de Azure. Utilice siguiente hello toodownload de nombre de paquete de información tooidentify hello y su correspondiente SHA-256 hash del paquete:

- - -
**Estados Unidos:**

KeyVault-BYOK-Tools-UnitedStates.zip

760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B

- - -
**Europa:**

KeyVault-BYOK-Tools-Europe.zip

7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D

- - -
**Asia:**

KeyVault-BYOK-Tools-AsiaPacific.zip

813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8

- - -
**América Latina:**

KeyVault-BYOK-Tools-LatinAmerica.zip

3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0

- - -
**Japón:**

KeyVault-BYOK-Tools-Japan.zip

453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90

- - -
**Corea:**

KeyVault-BYOK-Tools-Korea.zip

C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A

- - -
**Australia:**

KeyVault-BYOK-Tools-Australia.zip

4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B

- - -
[**Azure Government:**](https://azure.microsoft.com/features/gov/)

KeyVault-BYOK-Tools-USGovCloud.zip

3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64

- - -
**DoD del Gobierno de Estados Unidos:**

KeyVault-BYOK-Tools-USGovernmentDoD.zip

A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D

- - -
**Canadá:**

KeyVault-BYOK-Tools-Canada.zip

30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7

- - -
**Alemania:**

KeyVault-BYOK-Tools-Germany.zip

5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261

- - -
**India:**

KeyVault-BYOK-Tools-India.zip

136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7

- - -
**Reino Unido:**

KeyVault-BYOK-Tools-UnitedKingdom.zip

ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268

- - -

integridad de hello toovalidate de su conjunto de herramientas BYOK descargado, desde la sesión de PowerShell de Azure, use hello [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet.

    Get-FileHash KeyVault-BYOK-Tools-*.zip

conjunto de herramientas de Hello incluye siguiente hello:

* Un paquete de clave de intercambio de claves (KEK) cuyo nombre comienza por **BYOK-KEK-pkg-.**
* Un paquete de espacio de seguridad cuyo nombre comienza por **BYOK-SecurityWorld-pkg-.**
* Un script Python denominado **verifykeypackage.py.**
* Un archivo ejecutable de línea de comandos denominado **KeyTransferRemote.exe** y asociado a las DLL.
* Un paquete redistribuible de Visual C++ denominado **vcredist_x64.exe**.

Unidad USB de tooa de copia Hola paquete u otro almacenamiento portátil.

## <a name="step-2-prepare-your-disconnected-workstation"></a>Paso 2: preparación de la estación de trabajo desconectada
Para este segundo paso: Hola seguir los procedimientos descritos en la estación de trabajo de Hola que no está conectado tooa red (Hola Internet o la red interna).

### <a name="step-21-prepare-hello-disconnected-workstation-with-thales-hsm"></a>Paso 2.1: Preparar la estación de trabajo de hello desconectada con HSM de Thales
Instalar software de soporte de hello nCipher (Thales) en un equipo de Windows y, a continuación, adjunte un equipo de toothat HSM de Thales.

Asegúrese de que Hola herramientas de Thales se encuentran en la ruta de acceso (**%nfast_home%\bin**). Por ejemplo, escriba el siguiente hello:

        set PATH=%PATH%;"%nfast_home%\bin"

Para obtener más información, consulte la Guía de usuario de hello incluida con hello HSM de Thales.

### <a name="step-22-install-hello-byok-toolset-on-hello-disconnected-workstation"></a>Paso 2.2: Conjunto de herramientas BYOK de Hola instalación en la estación de trabajo de hello desconectado
Copie el paquete de conjunto de herramientas BYOK de Hola de unidad USB de Hola o de otro almacenamiento portátil y, a continuación, Hola siguientes:

1. Extraiga los archivos de hello del paquete de descarga de Hola en cualquier carpeta.
2. En esa carpeta, ejecute vcredist_x64.exe.
3. Siga las instrucciones de hello toohello instalar los componentes de tiempo de ejecución de Visual C++ de Hola para Visual Studio 2013.

## <a name="step-3-generate-your-key"></a>Paso 3: generación de la clave
Para el tercer paso, Hola seguir los procedimientos descritos en la estación de trabajo de hello desconectado. toocomplete este paso HSM debe estar en modo de inicialización. 


### <a name="step-31-change-hello-hsm-mode-tooi"></a>Paso 3.1: Cambiar Hola HSM modo too'I'
Si usas Thales nShield Edge, modo de Hola toochange: 1. Utilice Hola modo toohighlight botón Hola modo requerido. 2. Dentro de unos segundos, mantenga presionada botón Borrar Hola para un par de segundos. Si se cambia el modo de hello, Hola nuevo modo se detiene de LED parpadea y permanece encendido. Hola el LED de estado podría flash irregular durante unos segundos y, a continuación, parpadeará con regularidad al dispositivo de hello está listo. En caso contrario, Hola dispositivo permanece en el modo actual hello, con el modo adecuado de hello LED encendido.

### <a name="step-32-create-a-security-world"></a>Paso 3.2: creación de un espacio de seguridad
Inicie un símbolo del sistema y ejecute hello programa del nuevo mundo de Thales.

    new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3

Este programa crea un **mundo de seguridad** archivos en % NFAST_KMDATA%\local\world, que corresponde a toohello C:\ProgramData\nCipher\Key Management Data\local carpeta. Puede usar valores diferentes para el quórum de hello pero en nuestro ejemplo, le tooenter solicitadas tres las tarjetas en blanco y PIN de cada uno de ellos. A continuación, dos tarjetas cualesquiera proporcionarán mundo de seguridad de acceso completo toohello. Estas tarjetas convierten hello **conjunto de tarjetas de administrador** para Hola mundo de seguridad nuevo.

A continuación, Hola siguientes:

* Realizar una copia de archivo de hello world. Proteger y proteger el archivo de hello world, tarjetas de administrador de Hola y sus anclajes y asegúrese de que ninguna persona tiene acceso toomore que una tarjeta.

### <a name="step-33-change-hello-hsm-mode-tooo"></a>Paso 3.3: Cambiar Hola HSM modo too'O'
Si usas Thales nShield Edge, modo de Hola toochange: 1. Utilice Hola modo toohighlight botón Hola modo requerido. 2. Dentro de unos segundos, mantenga presionada botón Borrar Hola para un par de segundos. Si se cambia el modo de hello, Hola nuevo modo se detiene de LED parpadea y permanece encendido. Hola el LED de estado podría flash irregular durante unos segundos y, a continuación, parpadeará con regularidad al dispositivo de hello está listo. En caso contrario, Hola dispositivo permanece en el modo actual hello, con el modo adecuado de hello LED encendido.


### <a name="step-34-validate-hello-downloaded-package"></a>Paso 3.4: Validar el paquete de descarga de Hola
Este paso es opcional pero se recomienda para que pueda validar siguiente hello:

* Clave de intercambio que se incluye en el conjunto de herramientas de Hola Hola se ha generado desde un HSM de Thales genuino.
* hash de Hola Hola mundo de seguridad que se incluye en el conjunto de herramientas de Hola se ha generado desde un HSM de Thales genuino.
* Hola clave de intercambio no es exportable.

> [!NOTE]
> Hola toovalidate descargó el paquete, hello HSM debe estar conectado, encendida y debe tener un mundo de seguridad en él (por ejemplo, Hola uno que acaba de crear).
>
>

paquete de hello descargado toovalidate:

1. Ejecutar script de Hola verifykeypackage.py escribiendo uno de los siguientes de hello, según la región geográfica o la instancia de Azure:

   * Norteamérica:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
   * Europa:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
   * Asia:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
   * América Latina:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-LATAM-1 -w BYOK-SecurityWorld-pkg-LATAM-1
   * Japón:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-JPN-1 -w BYOK-SecurityWorld-pkg-JPN-1
   * Para Corea:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-KOREA-1 -w BYOK-SecurityWorld-pkg-KOREA-1
   * Para Australia:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AUS-1 -w BYOK-SecurityWorld-pkg-AUS-1
   * Para [Azure Government](https://azure.microsoft.com/features/gov/), que utiliza la instancia de gobierno de hello Estados Unidos de Azure:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USGOV-1 -w BYOK-SecurityWorld-pkg-USGOV-1
   * Para DoD del Gobierno de Estados Unidos:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USDOD-1 -w BYOK-SecurityWorld-pkg-USDOD-1
   * Para Canadá:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-CANADA-1 -w BYOK-SecurityWorld-pkg-CANADA-1
   * Para Alemania:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-GERMANY-1 -w BYOK-SecurityWorld-pkg-GERMANY-1
   * Para India:

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-INDIA-1 -w BYOK-SecurityWorld-pkg-INDIA-1
     > [!TIP]
     > Hola software de Thales incluye un script python en %NFAST_HOME%\python\bin
     >
     >
2. Confirme que ve a continuación hello, que indica la validación correcta: **resultado: correcto**

Este script valida la cadena del firmante Hola seguridad toohello clave raíz de Thales. hash de Hola de esta clave raíz está incrustada en el script de Hola y su valor debe ser **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**. También puede confirmar este valor independiente visitando hello [sitio Web de Thales](http://www.thalesesec.com/).

Ahora está listo toocreate una nueva clave.

### <a name="step-35-create-a-new-key"></a>Paso 3.5: creación de una nueva clave
Genere una clave mediante hello Thales **generatekey** programa.

Ejecute hello después la tecla de comando toogenerate hello:

    generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=

Cuando ejecute este comando, siga estas instrucciones:

* Hola parámetro *proteger* se debe establecer el valor de toohello **módulo**, tal y como se muestra. Esto crea una clave protegida por el módulo. conjunto de herramientas BYOK de Hello no admite claves protegidas por OCS.
* Reemplazar el valor de Hola de *contosokey* para hello **ident** y **plainname** con cualquier valor de cadena. toominimize de sobrecargas administrativas y reducir los riesgos de Hola de errores, se recomienda que use Hola mismo valor para ambos. Hola **ident** valor debe contener solo números, guiones y minúsculas.
* Hola pubexp se deja en blanco (valor predeterminado) en este ejemplo, pero puede especificar valores específicos. Para obtener más información, vea Hola documentación de Thales.

Este comando crea un archivo de clave acortada en la carpeta %NFAST_KMDATA%\local con un nombre que comienza con **key_simple_**, seguido de hello **ident** que se especificó en el comando de Hola. Por ejemplo: **key_simple_contosokey**. Este archivo contiene una clave cifrada.

Realice una copia del archivo tokenizado en una ubicación segura.

> [!IMPORTANT]
> Cuando posteriormente transfiera su clave tooAzure el almacén de claves, Microsoft no exportar esta clave tooyou atrás así que tiene mucha importancia que haga una copia el clave y seguridad del mundo de forma segura. Póngase en contacto con Thales si necesita guía y procedimientos recomendados para realizar copias de seguridad de una clave.
>
>

Se está ahora listo tootransfer su clave tooAzure el almacén de claves.

## <a name="step-4-prepare-your-key-for-transfer"></a>Paso 4: preparación de la clave para la transferencia
Para este paso cuarto, Hola seguir los procedimientos descritos en la estación de trabajo de hello desconectado.

### <a name="step-41-create-a-copy-of-your-key-with-reduced-permissions"></a>Paso 4.1: creación de una copia de la clave con menos permisos

Abra un nuevo símbolo y cambie Hola actual toohello ubicación del directorio donde descomprimió el archivo zip de hello BYOK. permisos de Hola de tooreduce en su clave, desde un símbolo del sistema, ejecutan uno de los siguientes de hello, según la región geográfica o la instancia de Azure:

* Norteamérica:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
* Europa:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
* Asia:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
* América Latina:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1
* Japón:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1
* Para Corea:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1
* Para Australia:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1
* Para [Azure Government](https://azure.microsoft.com/features/gov/), que utiliza la instancia de gobierno de hello Estados Unidos de Azure:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1
* Para DoD del Gobierno de Estados Unidos:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1
* Para Canadá:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1
* Para Alemania:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1
* Para India:

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1

Cuando ejecute este comando, reemplace *contosokey* con hello mismo valor que especificó en **3.5 paso: crear una nueva clave** de hello [generar su clave de](#step-3-generate-your-key) paso.

Se le preguntará tooplug sus tarjetas de administrador del mundo de seguridad.

Cuando se completa el comando de hello, verá **resultado: correcto** y copia de Hola de su clave con permisos reducidos se encuentran en el archivo de hello llamado key_xferacId_<contosokey>.

Puede inspecciona Hola ACL con los siguientes comandos mediante Hola utilidades de Thales:

* aclprint.py:

        "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
* kmfile-dump.exe:

        "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
  Cuando ejecute estos comandos, reemplace contosokey con hello mismo valor que especificó en **3.5 paso: crear una nueva clave** de hello [generar su clave de](#step-3-generate-your-key) paso.

### <a name="step-42-encrypt-your-key-by-using-microsofts-key-exchange-key"></a>Paso 4.2: cifrado de la clave mediante la clave de intercambio de claves de Microsoft
Ejecute uno de hello siga los comandos, según la región geográfica o la instancia de Azure:

* Norteamérica:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Europa:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Asia:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* América Latina:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Japón:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Para Corea:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Para Australia:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Para [Azure Government](https://azure.microsoft.com/features/gov/), que utiliza la instancia de gobierno de hello Estados Unidos de Azure:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Para DoD del Gobierno de Estados Unidos:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Para Canadá:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Para Alemania:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Para India:

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey

Cuando ejecute este comando, siga estas instrucciones:

* Reemplace *contosokey* con el identificador de Hola que usó toogenerate clave de hello en **3.5 paso: crear una nueva clave** de hello [generar su clave de](#step-3-generate-your-key) paso.
* Reemplace *SubscriptionID* con el Id. de Hola de hello suscripción de Azure que contiene el almacén de claves. Recuperar este valor anteriormente, en **paso 1.2: obtener el identificador de suscripción de Azure** de hello [preparar su estación de trabajo conectada a Internet](#step-1-prepare-your-internet-connected-workstation) paso.
* Reemplace *ContosoFirstHSMKey* por una etiqueta que se usará para el nombre del archivo de salida.

Cuando se complete correctamente, muestra **resultado: correcto** y hay un nuevo archivo en la carpeta actual de Hola que tiene Hola después de nombre: KeyTransferPackage -*ContosoFirstHSMkey*.byok

### <a name="step-43-copy-your-key-transfer-package-toohello-internet-connected-workstation"></a>Paso 4.3: Copie la transferencia de claves paquete toohello conectada a Internet estación de trabajo
Use una unidad USB u otro archivo de salida de almacenamiento portátil toocopy Hola Hola anterior paso (KeyTransferPackage-ContosoFirstHSMkey.byok) tooyour conectada a Internet estación de trabajo.

## <a name="step-5-transfer-your-key-tooazure-key-vault"></a>Paso 5: Transferir su clave tooAzure el almacén de claves
Para este último paso, Hola conectada a Internet estación de trabajo, use hello [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) paquete de transferencia de clave de Hola de tooupload de cmdlet que copió de hello desconectado toohello de estación de trabajo HSM del almacén de claves de Azure:

    Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMkey' -KeyFilePath 'c:\KeyTransferPackage-ContosoFirstHSMkey.byok' -Destination 'HSM'

Si carga hello es correcta, verá las propiedades de muestra de Hola de clave de Hola que acaba de agregar.

## <a name="next-steps"></a>Pasos siguientes
Ahora puede usar esta clave protegida con HSM en el almacén de claves. Para obtener más información, vea hello **si desea que un módulo de seguridad de hardware (HSM) de toouse** sección Hola [Introducción al almacén de claves de Azure](key-vault-get-started.md) tutorial.
