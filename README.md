# Practicas-ISE
- *Alumno:* Manuel Cazorla Chica
- *Grupo de prácticas:* B1 
- *Usuario:* manucazorla69
- *Curso:* 2025 / 2026
---

# Sesión 1 24/09/2025: 
## Creación de la bitácora

He creado un repositorio privado en GitHub llamado practicas-ISE con un archivo README.md para llevar mi bitácora e invité al profesor como colaborador. Después hice un fork del repositorio bitacoras-ISE-25-26, añadí mi fichero con el enlace a mi repo y confirmé los cambios. Finalmente, envié un Pull Request para que el profesor pudiera aprobarlo e incluir mi enlace en el repositorio original.

## Inicio Práctica 1

Antes de empezar la práctica tuve que descargar Debian y VirtualBox, ya que nunca había trabjado con ellos y no los tenia instalados en mi ordeador. No obstante a la hora de empezar la práctica, una serie de problemas que tras importar las maquinas no me dejaban que arranacaran correctamente debido a la configuración de mi ordenador. Sin embargo con ayuda de algunos compañeros que habían tenido el mismo problema, conseguí finalmente dejar la aplicación bien para poder utilizar las maquinas. Para solucionarlo tuve que entrar en la bios del ordenador y desactivar una de las configuraciones que tenia activadas por defecto.

Como no pude arrancar la maquina durante la hora, tuve que realizar la práctica con ayuda del video del profesor que duraba alrederdor de 1h. Sin embargo este me vino muy bien, ya que a pesar de que podía perderme en alguno de los pasos con facilidad, gracias al video era muy fácil, volver a atrás para ver donde habías tenido el problema. Se agradece tener este tipo de contenidos audiovisuales, ya que si en clase tienes algún problema que surja de manera expontanea, puedes seguir la clase atendiendo a todo lo que hace aunque sea sin hacerlo, y posteriormente hacer lo mismo con ayuda del video.


Tras seguir paso a paso el video, obtuve por fin la instalacion de Debian con las correspondientes particiones que debiamos hacer en los discos, la configuracion de un RAID1 gestionado con LVM. Tomé esta captura de los comandos que había que ejecutar tras haber completado todo el proceso.

<img width="1283" height="880" alt="image" src="https://github.com/user-attachments/assets/a1ce4cb5-49ae-4e8e-b51c-eafa7b033616" />

Tras haber hecho esto, tome una instantanea de la máquina para poder cargar el estado de la maquina guardado, por si algún dia el estado de la maquina me diera algun problema, poder tener una copia y no tener que configurar la máquina desde el principio


---

# Sesion 2 01/10/2025

## Prática 2

En esta práctica hemos trabajado con almalinux, un sistema operativo que me resultaba nuevo. Tras su instalación, debimos instalar una nueva versión de la maquina virtual, a una version mas moderna, ya que sino podriamos encontrarnos con problemas y que no funcionara bien la misma. Sin embargo tras la instalacion de la misma, comenzamos con la instalación del nuevo sistema operativo.


Al principio tras completar la instalación, solo teniamos creado un usuario, el root, por tanto lo primero que tuvimos que hacer fue realizar la creacion de nuestro propio usuario con contraseña. Tras esto, pudimos emepzar con la practica de verdad, en la que debiamos asignarle un LV exclusivamente al directorio /var. Para ello incluimos un nuevo disco y configuramos LVM para que /var se montara en el nuevo VL que creamos para él.

Para llevar esto a cabo, hemos usado comandos en la terminal que han resultado familiares de asignaturas como SO, en la que al igual que hemos tenido que hacer, se montaban y desmontaban particiones. Aunque es verdad que tambien había muchos comandos que resultaban nuevos como por ejemplo los que usamos para llevar a cabo la extensión deel VG almalinux desde el volumen físico.


# Sesión 3 08/10/2025

## Práctica 3

En la práctica, hemos llevado a cabo la configuracion de un RAID 1 a partir de una de la instantaneas que habíamos tomado en la práctica anterior. Para ello lo primero que hicimos fue con ayuda del comando fdisk, crear dos particiones de los discos fisicos de 2G que habiamos recuperado de la instantanea sdb y sdc, a los que llamamos sdb1 y sdc1. Posteriormente llevamos a cabo la creacion de un dispositivo RAID 1 a través del comando mdadm, al que llamaremos md0. Este RAID 1, nos permitirá duplicar los datos en los discos (mirroring)..

Tras esto creamos el volumen físico desde el md0, y sobre esto crearemos el VG con ayuda del comando vgcreate. Este VG lo llamamos vg_raid1. Por último llevé a cabo la creación del LV llamado new-var desde el VG, y tras esto comprobé que todo fuera de manera correcta.
<img width="553" height="260" alt="image" src="https://github.com/user-attachments/assets/6f1c889c-71fe-4a17-9b2b-6513518a7566" />

Asimismo el siguiente pasó que llevamos a cabo fue la encriptación con ayuda del comando cryptsetup, aunque para ellos tuvimos primero que llevar a cabo la instalción de algunos paquetes necesarios. Modificamos después el fichero y tras esto el sistema activará el LV new_var en el arranque del sistema tras pedirnos la contraseña.

<img width="601" height="92" alt="image" src="https://github.com/user-attachments/assets/67251f17-a811-495b-a2ce-ad46a89e6626" />

Por último en la práctica montamos el sistema de ficheros en /var libreando en primer lugar el espacio del antiguo /var y después creamos un nuevo /var y montamos.


<img width="664" height="749" alt="image" src="https://github.com/user-attachments/assets/97553855-3515-4243-9c2a-54dead8bffab" />



# Sesión 4 15/10/2025

## Práctica 4

Para poder empezar esta práctica, hemos tenido en primer lugar que cambiar el tipo de red de nuestras maquinas virtuales para poner ambas en adaptador solo de afitrión y asi permimtir la conectividad entre ellas.

Posteriormente, tanto en Debian como en Alma, hemos asigando con el comando "ip addr add 192.168.56.XXX/24 dev enp0s8" a cada una de las maquinas una ip distinta para la interfaz de red enp0s8, usando la máscara de red /24.  Tras haberlo hecho, hemos comprobado que la comunicación era correcta. 
<img width="1280" height="800" alt="debian conexiones" src="https://github.com/user-attachments/assets/4be690fc-5195-4383-8443-34d5cfe11b4f" />

Después hemos tenido que modificar unos archivos en debian para intetrar un demonio en el dispositivo de red, y mediante algunos procesos de instalación y de modificación del servicio, hemos podido conectarnos desde una máquina a la otra y también a nuestro propio ordenador.

Por último, hemos llevado a cabo la deshabilitación del root y el cambio de puerto meidante la modificacion de unos de los archivos que pertenecen a la configuracion del sshd, esto nos ha permitido poder acceder a la máquina mediante un ssh. En esta foto se puede ver como hemos tenido que llevar a cabo la modificación del arcvhio para hacer lo anteriormente dicho.


<img width="1280" height="800" alt="modificacion debian archivo" src="https://github.com/user-attachments/assets/9bc0b1c2-2d3b-4ff2-96e3-294e2ad5dbbe" />

Además, en la prática hemos podido encontrar algunas nociones que nos hablan de difetencias entre debian y alma, y también diferencias entre comandos (cuando debemos usar cada uno) que podemos encontrar entre las dos maquinas.



# Sesión 5 22/10/2025

## Práctica 5

En la pŕactica de hoy hemos atendido a una lección relacionada con las copias de seguridad y Git 


# Sesión 6 29/10/2025

## Práctica 6

En esta práctica, hemos aprendido en primer lugar, a poder conectarnos desde el pc propio a cada una de las maquinas virtuales con el comando ssh. Para ello el primero de los pasos era hacer un ssh a cada una de las maquinas seleccionando el puerto 22022, que fue el que habíamos cambiado en la practica anterior. Sin embargo, tras esto cada vez que queriamos a acceder a alguna de las maquinas virtuales, estas nos pedian la constraseña del usuario, por lo que próximo que hicimos fue generar claves en las respectivas máquinas además de en nuestro propio pc, de tal forma que después al compartir esa clave entre ellas y cambiar el parametro de uno de los ficheros del ordenador usados para el servicio ssh (/etc/ssh/sshd_config) para que por defecto no pidiera la constraseña al acceder (PasswordAuthentication no), podiamos conectarnos entre las maquinas (excepto desde las virtuales al anfitrión). 
En la imagen podemos ver un ejemplo de como nos conectamos desde el pc propio a debian a traves de ssh, y ademas podemos apreciar como no nos pide la contraseña del usuario al establecer la conexión porque hemos compartido la clave pública desde el anfitrión a debian (si usas Windows no te dejara enviar las claves públicas directamente, por lo que tenemos que copiar la clave pública del ordenador y pegarla en el fichero authtorized_keys de la máquina a la que queramos conectarnos)
<img width="735" height="324" alt="imagen" src="https://github.com/user-attachments/assets/93e9482b-7802-438a-90be-9f81007c240c" />


También vimos de manera express que había otras maneras de permitir y restringir usuarios a traves del acceso mediante ssh modificando en el fichero anteriormente mencionado (/etc/ssh/sshd_config) los parámetros respectivos a AllowUser. Asimismo vimos el uso de fail2ban en alma desde el cual creabamos una jaula de tal manera que este nos permitía monitorizar los accesos que se hacian mediante el sshd de tal manera que podía bloquear ataques maliciosos e IPs.


Después vimos algunas utilidades (screen y tmux) de ambas máquinas que nos permitian recuperar sesiones que habíamos dejado abiertas y que han sido cerradas inesperadamente o por fuerza bruta.


POr último vimos como se hacía la instalación del servidor web (LAMP), para ello instalamos la pila LAMP entera a través del comando "dnf install httpd php mariadb mariadb-server php-mysqlnd" sin embargo este contiene muchos paquetes distintos por lo que es necesario configurar y habilitar los servivios de cada uno de los paquetes con ayuda del comando "systemctl [status | enable | start] <paquete_que_queramos_comprobar>". Tras haber comprobado los paquetes, modificamos el fichero /var/www/html/index.php con el fin de crear una página web en php, y tras hacerlo obtenemos este resultado al buscar la ip del ordenador en el buscador.
<img width="990" height="515" alt="imagen" src="https://github.com/user-attachments/assets/9cf14ec6-8f56-40b6-8662-084d4a596a50" />


# Sesión 7 5/11/2025

## Práctica 7

En esta práctica, hemos llevado a cabo una partición del disco, tal y como hicimos en la primera práctica. Es decir, para comenzar la práctica hemos hecho lo mismo que hicimos en las primeras prácticas a modo de recordartorio. 
Además hemos, estado viendo que es la monitorización y observación, y hemos visto de la misma manera muchas aplicaciones que nos facilitan hacer eso. Aunque en esta práctica nos hemos centrado mas en  Zabbix.

Esta clase, ha sido un poco más teorica, sin embargo tenemos que realizar un ejercicio de monitorización desde Zabbix en debian a alma, a través de shh y http.

# Sesión 8 12/11/2025

## Práctica 3

Durante esta sesión de prácticas hemos tenido tiempo para llevar a cabo la realización del ejercicio anteriormente comentado en la práctica de la semana 7.
Para llevar a cabo este ejercicio lo que tenemos que hacer en primer lugar, es agregar el repositorio de Zabbix 7.4 a la
máquina de Debian a través de los siguientes comandos:

wget https://repo.zabbix.com/zabbix/7.4/release/debian/pool/main/z/zabbix-release/zabbix-release_latest_7.4+debian13_all.deb
sudo dpkg -i zabbix-release_latest_7.4+debian13_all.deb
sudo apt update

Posteriormente, instalamos Zabbix Server, frontend y agente a través de este comando:​

sudo apt install zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf
zabbix-agent

Siguiendo el guion que proporciona la página oficial de Zabbix, accedemos a la base de datos de MariaDB que previamente habíamos instalado. Tras acceder a ella, creamos la tabla de datos de Zabbix, en la cuál creamos el usuario “zabbix” al que podemos acceder con la contraseña “practicas,ise”. Asimismo, le otorgamos todos los privilegios a dicho usuario y cerramos la base de datos. Todo ello lo llevamos a cabo con estos comandos:
​
sudo mysql -u root -p ← Acceder a la base de datos dde MariaDB
DROP DATABASE IF EXISTS zabbix; ← Dropear por si acaso existe
CREATE DATABASE zabbix CHARACTER SET utf8mb4 COLLATE utf8mb4_bin;
CREATE USER 'zabbix'@'localhost' IDENTIFIED BY 'practicas,ise';
GRANT ALL PRIVILEGES ON zabbix.* TO 'zabbix'@'localhost';
FLUSH PRIVILEGES;
EXIT;

Tras esto, importamos el esquema en la base de datos a través del comando:​

sudo zcat /usr/share/zabbix-sql-scripts/mysql/server.sql.gz | mysql -u zabbix -pzabbix

Para terminar con la instalación en Debian 13 de Zabbix, es necesario modificar uno de los documentos que se originan en el directorio /etc/zabbix/. Lo que hacemos a continuación es modificar el archivo /etc/zabbix/zabbix_server.conf, de tal manera que modificamos las líneas del mismo de esta manera:​
​
DBName=zabbix
DBUser=zabbix
DBPassword=practicas,ise

Hacemos esto porque los datos que se introducen en la creación de tablas en MariaDB deben concordar con los datos que se encuentran en el documento, es decir, el nombre de usuario y la contraseña que elegimos cuando creamos la tabla de Zabbix en MariaDB deben ser los mismos que aparezcan en dicho documento.

Tras esto, se finaliza la parte de instalación de Zabbix casi al completo, ya que solo queda buscar la IP que tenemos asignada a nuestra máquina de Debian (en nuestro caso,192.168.56.105) en internet, a través de http y la ruta /zabbix → http://192.168.56.105/zabbix
<img width="1126" height="646" alt="imagen" src="https://github.com/user-attachments/assets/e43dde49-3543-46a6-a99f-7af7f34352e9" />


Al acceder a dicha página, nos aparecerá un inicio de sesión en Zabbix que nos permitirá completar la instalación del mismo. Aunque, deberemos de logearnos posteriormente con  usuario: Admin y contraseña: zabbix que son los que propone Zabbix por defecto.Ahora, deberemos modificar los ficheros de Zabbix, en concreto el fichero /etc/zabbix/zabbix_agentd.conf y tenemos que modifcar las líneas en las que pone Server, ServerActive y Hostname y dejarlo de esta manera:

Server=127.0.0.1
ServerActive=127.0.0.1
Hostname=Zabbix server

Y posteriormente se reiniciará el agente a través del comando:

sudo systemctl restart zabbix-agent

Ahora es necesario crear un equipo dentro de la interfaz web de Zabbix, para ello le pondremos el nombre de AlmaLinux y la IP de la misma, además de las plantillas Linux by Zabbix agent y Apache by Zabbix agent.​
Tras esto hacemos un cambio a la máquina de alma, en la que deberemos de instalar el agente 2 de Zabbix a través de los comandos:​

sudo rpm -Uvh
https://repo.zabbix.com/zabbix/7.4/rhel/9/x86_64/zabbix-release-7.4-1.el9.noarch.rpm
sudo dnf clean all
sudo dnf install zabbix-agent2

Y configuramos el agente de la misma manera que hemos hecho en Debian, es decir modificando el archivo /etc/zabbix/zabbix_agent2.conf y cambiando el Server, ServerActive y Hostname de tal manera:​

Server=192.168.56.105
ServerActive=192.168.56.105
Hostname=AlmaLinux

Antes de terminar es necesario abrir el puerto 10050 de Alma, que será el necesario para poder establecer una monitorización a través de Zabbix. Esto lo haremos a través de estos comandos:

sudo firewall-cmd --add-port=10050/tcp --permanent
sudo firewall-cmd --reload

Por último para establecer el servidor ssh y el http es necesario en dicho host que hemos creado específico para Alma (llamado AlmaLinux) añadir items de monitorización, los cuales serán ambos simple check con claves net.tcp.service[ssh,192.168.56.110,22022] (con puerto 22022 como tenemos en las máquinas) y net.tcp.service[http,192.168.56.110,80] respectivamente.

Con todo lo anterior, obtenemos esto si por ejemplo monitorizamos los mensajes enviados
desde Alma (haciendo un ping a Debian)
<img width="1245" height="431" alt="imagen" src="https://github.com/user-attachments/assets/543a53d7-ceb5-4aaa-859b-5a650ceef509" />


# Sesión 9 19/11/2025

## Práctica 4

En esta práctica, hemos conocido que es el benchmarking y alguno de sus usos. Para ello, vimos algunas aplicaciones que tenian disponibilidad para el uso de benchamrkings como Phoronix, ab y Jmeter, aunque la práctica fue mas enfocada en el uso de Jmeter. Además de dichas aplicaciones, estuvimos viendo una breve introdución a los dockers, y a algunas de las ventajas que estos nos pueden aportar.

Tras esa breve introducción a la práctica, llebamos a cabo la instalación de Jmeter y haremos una breve comprobación de benchmark para mnuestro ordenador
<img width="950" height="934" alt="Captura desde 2025-11-19 15-52-00" src="https://github.com/user-attachments/assets/9d4c0abc-5fba-4a3c-a1cf-339006643ca6" />

Esta aplicación, nos permitirá conocer algunos benchmarks de nuestro ordenador y además nos dara una comparación de las características del mismo frente a otros ordenadores que dicha aplicación tiene guardados desde 2011 
<img width="950" height="934" alt="Captura desde 2025-11-19 15-59-11" src="https://github.com/user-attachments/assets/974eca58-1eca-4d07-bbfb-a4c30ea8d368" />


Después de esto, será necesario instalar algunas herramientas de hhtpd con el propósito de comprobar la velocidad que tiene nuestro ordenador, por ejemplo, probamos a eviarle a la ip de alma 50 peticiones por parte de 5 usuarios, para ver cuanto es el tiempo que tarda nuestro ordenador en llevar a cabo dichas peticiones.

<img width="945" height="933" alt="Captura desde 2025-11-19 16-03-44" src="https://github.com/user-attachments/assets/f41cdf3d-e7ca-4522-9c4c-597d1638f101" />

Por último, hemos llevado a cabo trabajos con dockers enfocado en el uso de Jmter 
<img width="954" height="932" alt="Captura desde 2025-11-19 17-02-39" src="https://github.com/user-attachments/assets/ed1ece14-3d47-442b-8039-4d18dabf266e" />


Además de la práctica, hemos llevado a cabo la realizacion de un ejercicio del guión, que nos pertmite realizar una benchmark de alma, aunque para ello es necesario que descarguemos la interfaz gráfica en nuestro ordenador própio, y que tras esto lo pasemos a alma y ejecutemos el benchmark, que podemos ver con el ordenador própio a traves de un archivo html, los resultados del mismo 





# Sesión 10 26/11/2025

## Práctica 4


En esta práctica, hemos partido desde la aplicación que instalamos (como ejercicio de la práctica anterior). 
En primer lugar, lo que hicimos fue desde dicha aplicación crear un gestor de autorizacion http, de tal manera que con los datos que se nos proporcionaban teniamos que rellenar una serie de paramétros que llevaran a cabo dicho gestor, como por ejemplo la url base, para la cual ibamos a usar la ip de debian añadiendo :3000 al final de la misma. Tras esto, deberiamos de llevar a cabo la petición http que configurariamos de la siguiente manera.
<img width="880" height="518" alt="imagen" src="https://github.com/user-attachments/assets/d105bdc8-31ab-44fc-9859-added71af2e2" />

Después de todo esto, ejecutaremos el comando docker exec -it ise-p4app-mongodb-2 mongosh con el fin de acceder al contenedor de la práctica 4 con la consola de mongosh abierta. En ella ejecutaremos estos comandos, que nos permitiran conocer una lista de usuarios que pertenecen a dicha base de datos. Cogeremos uno de los usuarios junto con sus contraseñas, y lo añadiremos a dicha app (añdiendo un gestor de cabecera http), y añadiremos un extractor de expresiones regualares que usaremos para guardar el token que cuando dicho usuario pide la petición para conocer datos ha de meterse. Para terminar esta parte añadiremos un árbol de resultados para obtener los resultados de las peticiones que vamos a lanzar con dicho usuario. En este momento contemplamos que cuando un usuaior mete su contraseña correcta, en el árbol de expresiones su login sera correcto, pero no lo sera en caso de que la contraseña no sea correcta.
Todo lo realizado hasta el momento quedaria así:
<img width="861" height="492" alt="imagen" src="https://github.com/user-attachments/assets/a612e645-8e80-4f61-921c-ccf5b20e008b" />

Después de esto, realizaremos a traves de estos comandos crearemos un plan de pruebas (hay que ejecutar tambien sudo dnf install mc) 
<img width="902" height="449" alt="imagen" src="https://github.com/user-attachments/assets/825703b2-f571-4b38-aa42-9159cc7df8d0" />
<img width="892" height="139" alt="imagen" src="https://github.com/user-attachments/assets/e0475d23-26de-4193-b99e-998e155e64e5" />

