.. -*- coding: utf-8 -*-

.. _rcs_subversion:
  
Clase 02 - POO 2024
===================
(Fecha: 13 de marzo)


Registro en video de algunos temas de la clase de hoy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

`std namespace vector list 2022 <https://www.youtube.com/watch?v=7ORVHLxFvRM>`_ 

`vector 2021 <https://www.youtube.com/watch?v=mUWIo9uKW5c>`_ 


Problema para las próximas semanas
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

:Una empresa que se dedica al desarrollo de software ofrece soluciones y utiliza las siguientes tecnologías y herramientas:
		- QtCreator como IDE
		- Biblioteca Qt con C++ para aplicaciones Desktop
		- MongoDB para base de datos
		- FastAPI en Python para la API

Necesidad 
^^^^^^^^^

- Se desea una aplicación desktop en Qt que tenga un login de usuarios 
- Cuando un usuario en la aplicación desktop ingrese un usuario válido obtendrá un access token desde la API desarrollada con FastAPI
- Cuando se obtiene el access token, el usuario ya estará logueado, y podrá utilizar este token para próximas consultas a la API
- Los usuarios se almacenarán en una colección de MongoDB
- Se quiere montar todo esto en el localhost para tener un entorno de desarrollo y testing





Utilidades de la biblioteca estándar de C++
===========================================

vector
^^^^^^

- Mantiene sus elementos en un área contigua de memoria.
- El acceso aleatorio es eficiente.
- La inserción en cualquier posición distinta a la última es ineficiente.
- Se encuentra en #include <vector> en el namespace std

.. code-block:: c

	vector< int > v1;                     // vector vacío
	vector< int > v2( 15 );               // vector de 15 elementos
	vector< string > v3( 18, "cadena" );  // 18 elemento con valor inicial
	vector< string > v4( v3 );            // v4 es una copia v3

**Algunas operaciones**

.. code-block:: c

	size()          // Tamaño
	bool empty()    // Está vacío?
	void clear()    // Limpia el vector
	front()         // Acceso al primero
	back()          // Al último
	push_back( x )  // Inserción al último
	pop_back()      // Elimina
	w = v           // Asignación
	v == w   v < w  // Comparaciones
	v.at( i )       // Acceso con verificación de rango (lanza out_of_range)
	v[ i ]          // Acceso sin verificación de rango

