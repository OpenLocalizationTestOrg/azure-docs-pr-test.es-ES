<!--author=jgerend last changed: 03/16/16-->

## <a name="preparing-for-updates"></a>Preparación de las actualizaciones
Necesitará hello tooperform siguiendo los pasos antes de examinar y aplique la actualización de hello:

1. Tome una instantánea de nube de los datos del dispositivo Hola.
2. Asegúrese de que la IP fijas del controlador sean enrutable y pueden conectarse toohello Internet. IP fijas serán tooyour dispositivo de tooservice usa las actualizaciones. Puede probarlo mediante la ejecución de hello siguientes cmdlet en cada controlador de interfaz de Windows PowerShell de hello de dispositivo de hello:
   
     `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter network> `
   
    **Resultados de ejemplo para la conexión de prueba cuando IP fijas puedan conectarse toohello Internet**

        Controller0>Test-Connection -Source 10.126.173.91 -Destination bing.com

        Source      Destination     IPV4Address      IPV6Address
        ----------------- -----------  -----------
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200

        Controller0>Test-Connection -Source 10.126.173.91 -Destination  204.79.197.200

        Source      Destination       IPV4Address    IPV6Address
        ----------------- -----------  -----------
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200

Después de haber completado correctamente estas comprobaciones previas manuales, puede continuar tooscan e instalar actualizaciones de Hola.

