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

Para llevar esto a cabo, hemos usado comandos que han resultado familiares de asignaturas como SO, en la que al igual que hemos tenido que hacer, se montaban y desmontaban particiones. Aunque es verdad que tambien había muchos comandos que resultaban nuevos como por ejemplo los que usamos para llevar a cabo la extensión deel VG almalinux desde el PV.


