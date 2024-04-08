.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 07 - POO 2024
===================
(Fecha: 8 de abril)


Registro en video de algunos temas de la clase de hoy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

`Sutileza con punteros - octal - arrays como parámetros 2021 <https://www.youtube.com/watch?v=XQOBvBVkffM>`_

`QNetworkAccessManager y colocar imagen en login 2023 <https://youtu.be/PFSWwS-RHyI>`_




Sutilezas con punteros
^^^^^^^^^^^^^^^^^^^^^^

.. code-block::

	char cadena[ 10 ] = "hola";  
	// Funciona? sí. Qué hace con el sobrante?
	// Los completa a todos con \000

	char cadena[ 4 ] = "hola";   // Por qué no compila?

	char cadena[ 5 ] = "hola";   // Y por qué esto sí compila?

	// Porque la última posición se usa para el carácter nulo que el
	// compilador lo agrega (si tiene lugar).

	//    \000  (octal)
	//    \x0   (hexadecimal)    

Usando puntero para cadenas
^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block::

	char * cadena = "hola";      // el compilador agrega \000
	char * cadena = "ho\000la";  // Imprime  ho

- Asignamos memoria dinámicamente.
- No necesitamos especificar la longitud máxima.

Notación octal y hexadecimal
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block::

	cout << 3 + 4 + 11;      // Imprime 18
	cout << 3 + 4 + 011;     // ?

	//    octal    hexadecimal    decimal
	//    0121     0x51           81
	//    011      0x9            9
	//    '\000'   '\x0'          nulo
	//    '\063'   '\x33'         carácter 3




Obtener una imagen desde internet
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block::

	void Principal::slot_descargaFinalizada( QNetworkReply * reply )  {
	    QImage image = QImage::fromData( reply->readAll() );
	}



Ejercicio 14 (continuación):
============================

- Publicar en la ventana de Login, la temperatura actual en la Ciudad de Córdoba. Usar alguna API disponible.
- Agregar un método en Login que permita mostrar u ocultar la información de la temperatura.
- Además que la ventana de Login tenga como background una imagen descargada de interner, centrada y adaptada en tamaño, sin deformar su aspecto y que permita al usuario que modifique el tamaño del Login y que se siga viendo correctamente la imagen.
- Agregar un método en Login que permita indicar la URL de la imagen que se mostrará en el background. En caso que nunca se invoque a este método, ninguna imagen se mostrará.


Ejercicio 16 (continuación):
============================

- Que el endpoint para validar a los usuarios sea con un POST y que devuelva "denegado" o que devuelva el nombre y el apellido del usuario en el siguiente formato: "Juan Carlos::Ponce"
- Probar el funcionamiento de este endpoint mediante la web de prueba de FastAPI.



Ejercicio 17
============

- Diseñar un login que cargue como fondo, una imagen descargada de internet
- Cuando un usuario sea válido, que se abra en full screen otra ventana (definida en la clase Ventana) y que tenga otra imagen descargada de internet en su interior, abarcando toda la ventana.
- Esta ventana no deberá abrirse hasta tanto se haya descargado la imagen.
- La imagen no se debe deformar al visualizarse.


Aclaraciones
============

- Acondicionar la publicación de los ejercicios en el GitHub de manera que puedan ser explorados fácilmente.
- Colocar el enunciado de cada ejercicio para una cómoda exploración.
