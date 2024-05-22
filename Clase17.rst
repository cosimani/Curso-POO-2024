.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 17 - POO 2024
===================
(Fecha: 22 de mayo)


Registro en video de algunos temas de la clase de hoy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

`Sobrecarga de operadores 2021 <https://youtu.be/QGTNAjeRdNg>`_

`Singleton 2021 <https://youtu.be/RNAZ0pu-Ybc>`_


Sobrecarga de operadores 
========================

- Supongamos los siguientes objetos de la clase Poste:

.. code-block:: c

	Poste p1;  // Su único miembro dato es un float para la altura del Poste
	Poste p2;

- Necesitamos unir estos Postes para obtener un único Poste con sus alturas sumadas.
- ¿Podemos hacer lo siguiente?

.. code-block:: c

	Poste unidos = p1 + p2;

**Otro ejemplo**

.. code-block:: c

	class Cliente  {
	private:
	    int saldo;

	public:
	    Cliente() : saldo( 0 )  {
	    }

	    void operator+( int sumando )  {
	        this->saldo += sumando;
	    }

	    void operator-( int sustraendo )  {
	        this->saldo -= sustraendo;
	    }

	    bool operator<( Cliente otroCliente )  {
	        if ( this->saldo < otroCliente.saldo )
	            return true;
	        return false;
	    }
	};

	int main( int argc, char ** argv )  {
	    Cliente juan;

	    Cliente carlos;

	    juan + 50;  // Suma 50 a su cuenta

	    carlos + 100;  // Quita 100 a carlos

	    if ( juan < carlos )  {
	        qDebug() << "juan tiene menos";
	    }

	    return 0;
	}




static
======

**Variables estáticas**

- Al salir de su ámbito no pierde su valor
- Sólo son conocidas dentro de su ámbito (pero igual "recuerdan su valor")
- Se inicializan sólo la primera vez

.. code-block:: c

	#include <QApplication>
	#include <QDebug>

	int funcion( int a = 2 )  {
	    static int suma = 0;
	    return ( suma += a );
	}

	int main( int argc, char ** argv )  {
	    QApplication a( argc, argv );

	    qDebug() << funcion();	    
	    qDebug() << funcion( 10 );	
	    qDebug() << funcion();	    

	    return 0;
	}

**Miembros estáticos**

- Para cada instancia de una clase existe una copia de los miembros no-estáticos.
- Pero hay una única copia de los estáticos para todas las instancias.
- Pueden ser accedidas sin referencia a ninguna instancia concreta de la clase.
- Los miembros estáticos no dependen de ninguna instancia para su existencia.
- Existen incluso antes que la primera instancia de una clase.

**¿Qué problema tiene este código?**

.. code-block:: c

	#include <QApplication>
	#include <QDebug>

	class A  {
	public:
	    static int x;
	};

	int main( int argc, char ** argv )  {
	    QApplication a( argc, argv );

	    A a1;
	    qDebug() << a1.x;		// No reconoce x

	    return 0;
	}

**¿Qué se publica?**

.. code-block:: c

	#include <QApplication>
	#include <QDebug>

	class A  {
	public:
	    static int x;
	};

	int A::x = 5;

	int main( int argc, char ** argv )  {
	    QApplication a( argc, argv );

	    A a1, a2;
	    qDebug() << a1.x;		
	    qDebug() << a2.x;		

	    a1.x = 9;
	    qDebug() << a1.x;		
	    qDebug() << a2.x;		

	    return 0;
	}

- La modificación del valor ``x`` en el objeto a1 cambia dicha propiedad ``x`` en ``a2``.
- La definición ``int A::x = 5;`` solo son permitidas para miembros estáticos.

**¿Qué error tiene el siguiente código?**

.. code-block:: c

	class B  {
	    static const char * p1;        // privado por defecto

	public:
	    static const char * p2;        // declaración
	    const char* p3;
	};

	const char * B::p1 = "Adios";     // Ok.  Definición
	const char * B::p2 = "mundo";     // Ok
	const char * B::p3 = "cruel";     // Error. No es estática. No se puede definir así.


- No significa que las propiedades estáticas (privadas o protegidas) puedan ser accedidas directamente desde el exterior. Depende del modificador de acceso:

.. code-block:: c

	int main( int argc, char ** argv ) {
	    QApplication a( argc, argv );

	    qDebug() << B::p1;    // Error: no accesible!
	    qDebug() << B::p2;    // Ok: -> "mundo"

	    return 0;
	}

**Definición de miembros estáticos**

- Si los miembros estáticos existen antes de cualquier instancia, entonces hay que definirlos. 
- Los métodos estáticos sólo pueden acceder a miembros estáticos.

**¿Qué problema tiene el siguiente código?**

.. code-block:: c

	class C  {
	    static int y;

	public: 
	    int x;
	    static int * p;
	    static const char * c;
	    static int getY()  { return y; }
	    static int getX()  { return x; }	// No compila. x no es estático.
	};

	int C::y = 1;          		// no se debe poner static
	int * C::p = &C::y;     		
	const char * C::c = "ABC";   

**El constructor y miembros estáticos**

- La inclusión de un constructor no evita tener que definir los miembros estáticos.
- Recordar que el constructor es invocado cuando se instancia.
- El constructor puede modificar los valores de los miembros estáticos pero no inicializarlos.

**¿El siguiente código compila?**

.. code-block:: c

	class D  {
	    static int y;

	public: 
	    int x;

	    // El constructor no puede modificar así los miembros estáticos
	    D() : y( 10 ), x( 20 )  {  }  
	};

	int D::y = 1;

- Se debería usar un constructor como el que sigue:

.. code-block:: c

	D() : x( 20 )  {
	    y = 10;
	}

**Particularidades de la notación**

- Los miembros estáticos pueden ser accedidos con :: con la notación C::miembro.
- No es necesario utilizar ninguna instancia concreta de la clase.

**¿Qué publicaría el siguiente código?**

.. code-block:: c

	#include <QApplication>
	#include <QDebug>

	class E  {
	public:
	    static int x;  // miembro estático
	    E( int i = 12 )  {  x = i;  }   

	};

	int E::x = 13;  // definicion de miembro

	int main( int argc, char ** argv )  {
	    QApplication( argc, argv );

	    qDebug() << E::x;   
	    E e1;
	    qDebug() << E::x;  

	    return 0;
	}



Singleton
=========

- Un singleton es un patrón de diseño que restringe la creación de instancias de una clase a una única instancia.


Ejemplo de AdminDB como singleton
=================================

.. code-block:: c++

	#ifndef ADMINDB_H
	#define ADMINDB_H

	class AdminDB  {

	private:
	    static AdminDB * instancia;
	    AdminDB();

	public:
	    static AdminDB * getInstancia();

	    void conectar();
	};

	#endif // ADMINDB_H


.. code-block:: c++

	#include "admindb.h"
	#include <QDebug>

	AdminDB * AdminDB::instancia = nullptr;

	AdminDB::AdminDB()  {
	}

	AdminDB * AdminDB::getInstancia()  {
	    if( instancia == nullptr )  {
	        instancia = new AdminDB;
	    }
	    return instancia;
	}

	void AdminDB::conectar()  {
	    qDebug() << "La base se encuentra conectada...";
	}


.. code-block:: c++

	#include "admindb.h"

	int main( int, char ** )  {

	    AdminDB::getInstancia()->conectar();

	    return 0;
	}




Ejercicio 25:
=============

- Construir un nuevo proyecto que tenga un Login independiente, es decir, que no dependa de otra clase GUI.
- El Login tenga un QLabel que funciona como botón que sea para registrar un nuevo usuario.
- Cuando se presiona el QLabel que funciona como botón, se abrirá una ventana para dar de alta un usuario.
- Usar SQLite con AdminDB como singleton.
- Cuando un usuario válido ingresa correctamente se mostrará otra ventana que visualizará todos los usuarios cargados en la base.
- Para la visualización de los usuarios se puede usar QTreeWidget. Agregar la funcionalidad para que en esta misma ventana se puedan editar los campos como si fuera una planilla tipo excel.
- Seguir las recomendaciones que se comentaron durante el dictado de clases para construir las clases.
