.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 19 - POO 2024
===================
(Fecha: 3 de junio)


Simulacro de examen parcial
===========================


Ejercicio A
^^^^^^^^^^^

- Definir una ventana vacía en la clase Principal, que herede de QWidget y diseñado con QtDesigner.
- Agregar a este proyecto la clase AdminDB para permitir el uso de una base de datos. 
- Instanciar un único objeto de AdminDB en la aplicación.
- Definir una clase Linea con las siguientes características:
	- En los archivos fuente linea.h y linea.cpp
	- Atributos privados: int x_inicial, y_inicial, x_final, y_final
	- Con sus getters y setters.
	- Utilizar en esta clase todos los const que son recomendables
- Definir una tabla "lineas" en la base de datos con los siguientes campos: id, x_inicial, y_inicial, x_final, y_final
- Cargar en la base de datos un único registro, es decir, los datos de una única línea.
- Desde la clase Principal se podrá leer este único registro y crear un objeto Linea con esos datos.
- Dibujar con paintEvent esta línea dentro de la ventana con las coordenadas leídas de la base.


Ejercicio B
^^^^^^^^^^^

- Definir un formulario en la clase Formulario usando QtDesigner. 
- En Formulario se darán de alta instrumentos en un negocio de instrumentos musicales.
- Los instrumentos que se pueden cargar serán: guitarras, vientos y teclados.
- Definir las clases Instrumento, Guitarra, Viento y Teclado.
- Cada clase en sus correspondientes archivos .h y .cpp
- Instrumento será una clase abstracta con la función virtual pura ``void afinar()``
- Que esa función virtual pura simplemente publique un texto por consola, por ejemplo "Afinando guitarra".
- El formulario tendrá un botón que agregará un instrumento nuevo a un ``QVector< Instrumento * >``
- El formulario tendrá un QComboBox en el cual tendrá el siguiente listado: Guitarra, Viento y Teclado.
- El formulario también tendrá un botón "Ver stock" que publicará por consola todos los instrumentos cargados.
- Los Instrumentos tendrán los siguientes atributos: marca, precio, cantidad_de_cuerdas, cantidad_de_teclas, metal_usado.
- Cuando en el QComboBox se seleccione Guitarra, se deberá permitir ingresar sólo la marca, el precio y la cantidad de cuerdas.


Ejercicio C
^^^^^^^^^^^

- Usar la clase Manager para gestionar todas las ventanas de una nueva aplicación.
- Usar un login (clase Login) que valide usuarios contra la tabla usuarios usando AdminDB.
- Para el campo clave usar MD5.
- La base de datos debe estar en el archivo base.sqlite
- Login y AdminDB que sean singleton.
- Cada clase en sus correspondientes archivos .h y .cpp
- Cuando un usuario ingrese correctamente, mostrar una ventana vacía.


Ejercicio D
^^^^^^^^^^^

- Crear una clase Lienzo que herede de QWidget, creado con QtDesigner y que permita dibujar con paintEvent.
- Cuando se presiona la tecla A (Activar) se comenzará a dibujar cada posición en donde se encuentra el mouse. No depende de que se presione algún bóton del mouse para comenzar a dibujar.
- Cuando se presiona la tecla D (Desactivar) se dejará de dibujar.
- La clase Lienzo recibe una enumeración que puede ser: TrazoFino, TrazoMediano, TrazoGrueso que determinará el grosor de lo que se dibuja.
- Dentro de Lienzo y ubicado abajo a la derecha, se ubicará un objeto de MiLabel, que hereda de QLabel, con una señal propia para detectar el click del mouse.
- Cuando se presione este MiLabel, se borrará todo lo dibujado.




