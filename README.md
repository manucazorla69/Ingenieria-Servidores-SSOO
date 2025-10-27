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


# Sesión  08/10/2025

## Práctica 3

En la práctica, hemos llevado a cabo la configuracion de un RAID 1 a partir de una de la instantaneas que habíamos tomado en la práctica anterior. Para ello lo primero que hicimos fue con ayuda del comando fdisk, crear dos particiones de los discos fisicos de 2G que habiamos recuperado de la instantanea sdb y sdc, a los que llamamos sdb1 y sdc1. Posteriormente llevamos a cabo la creacion de un dispositivo RAID 1 a través del comando mdadm, al que llamaremos md0. Este RAID 1, nos permitirá duplicar los datos en los discos (mirroring)..

Tras esto creamos el volumen físico desde el md0, y sobre esto crearemos el VG con ayuda del comando vgcreate. Este VG lo llamamos vg_raid1. Por último llevé a cabo la creación del LV llamado new-var desde el VG, y tras esto comprobé que todo fuera de manera correcta.
<img width="553" height="260" alt="image" src="https://github.com/user-attachments/assets/6f1c889c-71fe-4a17-9b2b-6513518a7566" />

Asimismo el siguiente pasó que llevamos a cabo fue la encriptación con ayuda del comando cryptsetup, aunque para ellos tuvimos primero que llevar a cabo la instalción de algunos paquetes necesarios. Modificamos después el fichero y tras esto el sistema activará el LV new_var en el arranque del sistema tras pedirnos la contraseña.

<img width="601" height="92" alt="image" src="https://github.com/user-attachments/assets/67251f17-a811-495b-a2ce-ad46a89e6626" />

Por último en la práctica montamos el sistema de ficheros en /var libreando en primer lugar el espacio del antiguo /var y después creamos un nuevo /var y montamos.


<img width="664" height="749" alt="image" src="https://github.com/user-attachments/assets/97553855-3515-4243-9c2a-54dead8bffab" />



# Sesión 15/10/2025

## Práctica 4

Para poder empezar esta práctica, hemos tenido en primer lugar que cambiar el tipo de red de nuestras maquinas virtuales para poner ambas en adaptador solo de afitrión y asi permimtir la conectividad entre ellas.

Posteriormente, tanto en Debian como en Alma, hemos asigando con el comando "ip addr add 192.168.56.XXX/24 dev enp0s8" a cada una de las maquinas una ip distinta para la interfaz de red enp0s8, usando la máscara de red /24.  Tras haberlo hecho, hemos comprobado que la comunicación era correcta. 
<img width="1280" height="800" alt="debian conexiones" src="https://github.com/user-attachments/assets/4be690fc-5195-4383-8443-34d5cfe11b4f" />

Después hemos tenido que modificar unos archivos en debian para intetrar un demonio en el dispositivo de red, y mediante algunos procesos de instalación y de modificación del servicio, hemos podido conectarnos desde una máquina a la otra y también a nuestro propio ordenador.

Por último, hemos llevado a cabo la deshabilitación del root y el cambio de puerto meidante la modificacion de unos de los archivos que pertenecen a la configuracion del sshd, esto nos ha permitido poder acceder a la máquina mediante un ssh. En esta foto se puede ver como hemos tenido que llevar a cabo la modificación del arcvhio para hacer lo anteriormente dicho.


<img width="1280" height="800" alt="modificacion debian archivo" src="https://github.com/user-attachments/assets/9bc0b1c2-2d3b-4ff2-96e3-294e2ad5dbbe" />

Además, en la prática hemos podido encontrar algunas nociones que nos hablan de difetencias entre debian y alma, y también diferencias entre comandos (cuando debemos usar cada uno) que podemos encontrar entre las dos maquinas.



# Sesión 22/10/2025

## Práctica 5

En la pŕactica de hoy hemos atendido a una lección relacionada con las copias de seguridad y Git 



