Cómo usar Proxychains para redirigir el tráfico a través del servidor proxy
=============================================================================

A veces instalamos un servidor proxy, pero solo ciertos programas como Firefox y Google Chrome proporcionan configuraciones de proxy. Afortunadamente, podemos usar una utilidad de línea de comandos llamada proxychains para redirigir cualquier programa para que pase por nuestro servidor proxy. Este tutorial le mostrará cómo configurarlo en Debian, Ubuntu, OpenSUSE, Fedora, CentOS / Redhat, Arch Linux y sus derivados.

Si no sabe cómo configurar un servidor proxy, consulte esta publicación para conocer el proxy shadowsocks . Después de eso, vuelve aquí.

https://www.linuxbabe.com/ubuntu/shadowsocks-libev-proxy-server-ubuntu-16-04-17-10


Debian/Ubuntu OS
++++++++++++++++++
::

	sudo apt-get install proxychains

CentOS/Redhat
+++++++++++++++
::

	sudo yum instalar proxychains

Agregar un servidor proxy a Proxychains
++++++++++++++++++++++++++++++++++++++++++

Abre el archivo de configuración.::

	vi /etc/proxychains.conf
	
Al final del archivo, agregue su proxy como este

	calcetines5 127.0.0.1 1080

socks5 es el tipo de proxy, puede agregar otros tipos, como http , https , socks4 , etc., según su situación. 127.0.0.1 es el host proxy y 1080 es el puerto en el que escucha el servidor proxy. Nuevamente, cámbielos a su situación específica.

El proxy predeterminado es el socks4 127.0.0.1 9050 que puede eliminar de forma segura.

Establecer un servidor DNS predeterminado
++++++++++++++++++++++++++++++++++++++++++++++++++
Se recomienda encarecidamente que cambie el servidor DNS predeterminado 4.4.2.2 a otro, como el servidor DNS de Google 8.8.8.8/8.8.4.4 . O servidor OpenDNS 203.67.222.222/203.67.220.220 . Abra el archivo de configuración resolv .

Debian/Ubuntu
+++++++++++++
::

	vi /usr/lib/proxyresolv

Fedora/CentOS/Redhat/OpenSUSE
++++++++++++++++++++++++++
::

	vi /usr/bin/proxyresolv
	
Encuentra la siguiente línea::

	DNS_SERVER = 4.4.2.2
	
Cambie su valor a algo como 8.8.8.8 . Luego guarde y cierre el archivo. En Arch Linux, no hay un archivo de configuración proxyresolv.

Prueba
+++++++++
Simplemente anteponga proxychains a cualquier comando que ejecute como el siguiente.::

	proxychains youtube-dl -citw https://www.youtube.com/channel/<channel-id>

Si está utilizando youtube-dl, entonces puede saber que no tiene soporte incorporado para proxy de calcetines, pero Proxychains redirigirá youtube-dl para que pase por el servidor proxy.

Si desea redirigir todo el tráfico de su terminal a través del servidor proxy, ingrese iniciar un nuevo programa de shell con proxychains, como a continuación.::

	proxychains bash
	
Este comando iniciará otro shell bash con proxychains en su terminal y de ahora en adelante no tendrá que anteponer proxychains a su comando. Su tráfico en este nuevo shell será redirigido automáticamente a través del servidor proxy.

Nota: El  terminal es diferente del shell . Terminal es el dispositivo que le permite conectarse a una computadora host, mientras que Shell es una pieza de software en la computadora host. Shell es un intérprete de línea de comandos , que traduce su comando a ceros y unos para que la computadora pueda entender su comando. Cuando un terminal se conecta a una computadora host, se iniciará automáticamente un programa de shell para que los comandos del usuario puedan ser interpretados por el shell y la computadora pueda entender los comandos del usuario.

Modo silencioso
+++++++++++++++++++++
Por defecto, proxychains enviará su actividad al terminal. Si no desea ver esta información, puede desactivarla editando el /etc/proxychains.confarchivo.::

	vi /etc/proxychains.conf
	
Encuentra la siguiente línea::

	#Modo silencioso
	
Eliminar el hashtag. Guarde y cierre el archivo. Ahora solo verá el resultado de la aplicación que se está redirigiendo.