UnifiedSetup.exe [/ ServerMode < CS/PS >] [/ InstallDrive <DriveLetter>] [/ MySQLCredsFilePath <MySQL credentials file path>] [/ VaultCredsFilePath <Vault credentials file path>] [/ EnvType < VMWare/NonVMWare >] [/ PSIP < toobe de dirección IP utilizada para la transferencia de datos] [/CSIP <IP address of CS toobe registered with>] [/ PassphraseFilePath <Passphrase file path>]

Parámetros:

* /ServerMode: Obligatorio. Especifica si se deben instalar los servidores de configuración y proceso de Hola o sólo servidor de procesos de Hola. Valores de entrada: CS, PS.
* InstallLocation: Obligatorio. carpeta de Hello en qué Hola se instalan los componentes.
* /MySQLCredsFilePath. Obligatorio. ruta de acceso de Hello en qué Hola MySQL se almacenan las credenciales del servidor. archivo Hello debe tener este formato:
* [MySQLCredentials]
* MySQLRootPassword = "<Password>"
* MySQLUserPassword = "<Password>"
* /VaultCredsFilePath. Obligatorio. ubicación de Hello del archivo de credenciales de almacén de hello
* /EnvType. Obligatorio. tipo de Hola de instalación. Valores: VMware, NonVMware
* /PSIP y /CSIP. Obligatorio. dirección IP de Hello del servidor de procesos de Hola y el servidor de configuración.
* /PassphraseFilePath. Obligatorio. ubicación de Hello del archivo de frase de contraseña de Hola.
* /ByPassProxy. Opcional. Especifica que el servidor configuración Hola conecta tooAzure sin un servidor proxy.
* /ProxySettingsFilePath. Opcional. Configuración de proxy (proxy predeterminado de hello requiere autenticación, o un proxy personalizado). archivo Hello debe tener este formato:
* [ProxySettings]
* ProxyAuthentication = "Sí/No"
* Proxy IP = "dirección IP >"
* ProxyPort = "<Port>"
* ProxyUserName="<User Name>"
* ProxyPassword="<Password>"
* DataTransferSecurePort. Opcional. número de puerto de Hola para datos de replicación.
* SkipSpaceCheck. Opcional. Omitir comprobación de espacio en memoria caché.
* AcceptThirdpartyEULA. Obligatorio. Acepta los términos de licencia de terceros de Hola.
* ShowThirdpartyEULA. Obligatorio. Muestra los términos de licencia de terceros. Si se proporciona como entrada, se omiten todos los demás parámetros.
