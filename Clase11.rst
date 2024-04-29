.. -*- coding: utf-8 -*-

.. _rcs_subversion:

Clase 11 - POO 2024
===================
(Fecha: 29 de abril)


Registro en video de algunos temas de la clase de hoy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

`Polimorfismo función virtual 2021 <https://youtu.be/wT_LfW-Ao0A>`_

`Polimorfismo - QtDesigner y métodos virtuales de QWidget 2023 <https://youtu.be/idc1aCpYUgg>`_


Vista obligatoria
^^^^^^^^^^^^^^^^^

`Funciones virtuales 2023 <https://youtu.be/a5-p12-jscc>`_


Polimorfismo
============

- Lo utilizamos con punteros.
- Nos permite acceder a objetos de la clase derivada usando un puntero a la clase base.
- Sin embargo, sólo podemos acceder a datos y funciones que existan en la clase base.
- Los datos y funciones propias de la derivada quedan inaccesibles.

.. code-block::

	class Persona  {
	public:
	    Persona( QString nombre ) : nombre( nombre )  {  }
	    QString verNombre()  {  return "Nombre: " + nombre;  }

	protected:  // Para acceso desde las clases derivadas
	    QString nombre;
	};

	class Empleado : public Persona  {
	public:
	    Empleado( QString nombre ) : Persona( nombre )  {  }
	    QString verNombre()  {  return "Empleado: " + nombre;  }
	    void mostrarAlgo()  {  qDebug() << "Algo";  }
	};

	class Estudiante : public Persona  {
	public:
	    Estudiante( QString nombre ) : Persona( nombre )  {  }
	    QString verNombre()  {  return "Estudiante: " + nombre;  }
	};


	#include <QApplication>
	#include "persona.h"
	#include <QDebug>

	int main( int argc, char** argv )  {
	    QApplication a(argc, argv);

	    {
	    Persona * jose = new Estudiante( "Jose" );
	    Persona * carlos = new Empleado( "Carlos" );

	    qDebug() << carlos->verNombre();
	    qDebug() << jose->verNombre();
	    carlos->mostrarAlgo();  // Muestra algo? 

	    delete jose;
	    delete carlos;
	    }

	    return a.exec();
	}
	


Funciones virtuales
===================

- Puede ser interesante llamar a la función de la derivada (en polimorfismo).
- Al declarar una función como virtual en la clase base, si se superpone en la derivada, al invocar usando el puntero a la clase base, se ejecuta la versión de la derivada.

.. code-block::

	class Persona  {
	public:
	    Persona( QString nombre ) : nombre( nombre )  {  }
	    virtual QString verNombre()  {  return "Persona: " + nombre;  }  // Y si no fuera virtual?

	protected:  
	    QString nombre;
	};

	class Empleado : public Persona  {
	public:
	    Empleado( QString nombre ) : Persona( nombre )  {  }
	    QString verNombre()  {  return "Empleado: " + nombre;  }
	};


	#include <QApplication>
	#include "personal.h"
	#include <QDebug>

	int main( int argc, char** argv )  {
	    QApplication a( argc, argv) ;

	    {
	    Persona *carlos = new Empleado( "Carlos" );

	    qDebug() << carlos->verNombre();  // Qué publica?

	    delete carlos;
	    }

	    return a.exec();
	}




Uso de Qt Designer
==================

- Nuevo proyecto -> Qt Widgets Application
- Utilizar el puntero ``ui`` para acceder a los objetos del diseño


**Ejemplo**

.. code-block::
	
	// ventana.h
	#ifndef VENTANA_H
	#define VENTANA_H

	#include <QWidget>

	namespace Ui {
	    class Ventana;
	}

	class Ventana : public QWidget  {
	    Q_OBJECT

	public:
	    explicit Ventana( QWidget * parent = 0 );
	    ~Ventana();

	private:
	    Ui::Ventana *ui;
	};

	#endif // VENTANA_H

.. code-block::

	// ventana.cpp
	#include "ventana.h"
	#include "ui_ventana.h"

	Ventana::Ventana( QWidget * parent ) : QWidget( parent ), ui( new Ui::Ventana )  {
	    ui->setupUi( this );
	}

	Ventana::~Ventana()  {
	    delete ui;
	}


Métodos virtuales de QWidget para capturar eventos
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Estos métodos pueden ser reimplementados en una clase derivada para recibir los eventos.

.. code-block::

	virtual void mouseDoubleClickEvent( QMouseEvent * event );
	virtual void mouseMoveEvent( QMouseEvent * event );
	virtual void mousePressEvent( QMouseEvent * event );
	virtual void mouseReleaseEvent( QMouseEvent * event );
	virtual void keyPressEvent( QKeyEvent * event );
	virtual void keyReleaseEvent( QKeyEvent * event );
	virtual void resizeEvent( QResizeEvent * event );
	virtual void moveEvent( QMoveEvent * event );
	virtual void closeEvent( QCloseEvent * event );
	virtual void hideEvent( QHideEvent * event );
	virtual void showEvent( QShowEvent * event );
	virtual void paintEvent( QPaintEvent * event );



Ejercicio 19
============

- Crear una clase Pintura que herede de QWidget y que permita dibujar a mano alzada con el mouse.
- Con el scroll permitirá ampliar y disminuir el tamaño del trazo del pincel.
- Con las teclas R, G y B se cambia el color del pincel.
- Con Escape se borra todo lo que esté dibujado.


 







