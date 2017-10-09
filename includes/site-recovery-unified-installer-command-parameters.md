|Nombre de parámetro| Escriba | Descripción| Valores posibles|
|-|-|-|-|
| /ServerMode|Obligatorio|Especifica si se deben instalar los servidores de configuración y proceso de Hola o sólo servidor de procesos de Hola|CS<br>PS|
|/InstallLocation|Obligatorio|carpeta de Hello en qué Hola se instalan componentes| Cualquier carpeta de equipo de Hola|
|/MySQLCredsFilePath|Obligatorio|ruta de acceso de archivo de Hello en qué Hola MySQL se almacenan las credenciales del servidor|archivo Hello debe tener formato de hello especificado más abajo|
|/VaultCredsFilePath|Obligatorio|ruta de acceso de Hello del archivo de credenciales de almacén de hello|Ruta de acceso de archivo válido|
|/EnvType|Obligatorio|Tipo de entorno que desea tooprotect |VMware<br>NonVMware|
|/PSIP|Obligatorio|Dirección IP de hello NIC toobe utilizado para la transferencia de datos de replicación| Cualquier dirección IP válida|
|/CSIP|Obligatorio|dirección IP de Hola de NIC de hello en qué Hola está escuchando el servidor de configuración en| Cualquier dirección IP válida|
|/PassphraseFilePath|Obligatorio|Hola toolocation de ruta de acceso completa del archivo de frase de contraseña de hello|Ruta de acceso de archivo válido|
|/BypassProxy|Opcional|Especifica que el servidor configuración Hola conecta tooAzure sin un servidor proxy|toodo obtener este valor desde Venu|
|/ProxySettingsFilePath|Opcional|Configuración de proxy (proxy predeterminado de hello requiere autenticación, o un proxy personalizado)|archivo Hello debe estar en formato de hello especificado más abajo|
|DataTransferSecurePort|Opcional|Número de puerto en hello PSIP toobe utilizado para los datos de replicación| Número de puerto válido (el valor predeterminado es 9433)|
|/SkipSpaceCheck|Opcional|Omitir comprobación de espacio para disco de caché| |
|/AcceptThirdpartyEULA|Obligatorio|La marca implica la aceptación de los términos de licencia de terceros| |
|/ShowThirdpartyEULA|Opcional|Muestra los términos de licencia de terceros. Si se proporciona como entrada, se omiten todos los demás parámetros| |
