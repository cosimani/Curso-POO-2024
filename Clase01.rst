.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 01 - POO 2024
===================
(Fecha: 11 de marzo)


Metodología didáctica
=====================

- A continuación se resume el conjunto de estrategias, procedimientos y acciones para facilitar el aprendizaje y el logro de nuestros objetivos. 

:Teoría: 
	- En la primer parte de cada clase se expondrán los contenidos teóricos.
	- Este contenido también está disponible en grabaciones de años anteriores, cuyos links se colocarán a medida que se avance en las clases.

:Práctica: 
	- La segunda parte de cada clase estará destinado a la resolución de ejercicios e incorporación de esos contenidos.

:Regularidad, promoción y examen final: 
	- Primer y segundo parcial: Problema para resolver en 2 horas
	- La materia se promociona bajo la modalidad de la UBP.
	- El examen final sigue `esta modalidad <https://github.com/cosimani/Curso-POO-2024/blob/main/Desafios.rst>`_ .


Registro en video de algunos temas de la clase de hoy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

`Library, Librería, Biblioteca 2021 <https://www.youtube.com/watch?v=k9ZZSSWuX6E>`_ 

`std C y std C++ 2021 <https://www.youtube.com/watch?v=GrOLHLHcZqg>`_ 


Instalación de herramientas
===========================

:QtCreator: 
	- Si hay instaladas versiones anteriores de Qt, desinstalarlas con C:\\Qt\\MaintenanceTool.exe y tildando Uninstall only 
	- Se recomienda este instalador Offline: `https://download.qt.io/archive/qt/5.14/5.14.1 <https://download.qt.io/archive/qt/5.14/5.14.1>`_
	- Importante la instalación de: 'Biblioteca Qt 5.14.1'  'Qt Creator'  'MinGW 7.3.0 64-bit'

:OpenSSL: 
	- Descargar instalador desde la `Página de descarga <https://slproweb.com/products/Win32OpenSSL.html>`_
	- Seleccionar el instalador `Win64 OpenSSL v3.1.0 <https://slproweb.com/download/Win64OpenSSL-3_1_0.exe>`_


Biblioteca estándar de C++
==========================

- Está en el espacio de nombres ``std``
- En la biblioteca estándar de C, los archivos de cabecera X.h se reemplazan por cX o X. Por ejemplo:

.. code-block:: c

	#include <stdlib.h>                   #include <cstdlib>    

	    int atoi( const char * )  // Convierte a int un número expresado en cadena
	    int abs( int )            // Devuleve el valor absoluto
	    int rand()                // Devuelve un número pseudo aleatorio entre 0 y 32767


	#include <stdio.h>                   #include <cstdio>    

	    // Borra un archivo. Devuelve 0 o un código de error.
	    int remove( const char * filename )

	    // Imprime por pantalla. Recibe un número indefinido de argumentos.
	    int printf( const char * format, ... )

	#include <iostream.h>                   #include <iostream>    

	    cout
	    cin
	    endl
