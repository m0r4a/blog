---
title: "Guía rápida de Python"
draft: false
date: 2024-10-04
description: Este es un tutorial muy pequeño y compacto de Python, esto es solamente un archivo de prueba para testear funciones .md relacionadas a código.
summary: Este es otro post de prueba en donde hice una simple y resumida guía de python.
---

## 1. Variables y Tipos de Datos

Las variables en Python se declaran simplemente asignándoles un valor:

```python
nombre = "Ana"  # String
edad = 25       # Integer
altura = 1.65   # Float
es_estudiante = True  # Boolean
```

## 2. Estructuras de Control

### Condicionales

```python
if edad >= 18:
    print("Eres mayor de edad")
elif edad >= 13:
    print("Eres adolescente")
else:
    print("Eres menor de edad")
```

### Bucles

#### For

```python
for i in range(5):
    print(i)  # Imprime del 0 al 4
```

#### While

```python
contador = 0
while contador < 5:
    print(contador)
    contador += 1
```

## 3. Funciones

Definición y uso de funciones:

```python
def saludar(nombre):
    return f"Hola, {nombre}!"

mensaje = saludar("María")
print(mensaje)  # Imprime: Hola, María!
```

## 4. Listas y Diccionarios

### Listas

```python
frutas = ["manzana", "banana", "cereza"]
frutas.append("damasco")
print(frutas[1])  # Imprime: banana
```

### Diccionarios

```python
persona = {
    "nombre": "Carlos",
    "edad": 30,
    "ciudad": "Madrid"
}
print(persona["ciudad"])  # Imprime: Madrid
```

## 5. Módulos

Importación y uso de módulos:

```python
import random

numero = random.randint(1, 10)
print(f"Número aleatorio: {numero}")
```

## 6. Manejo de Excepciones

```python
try:
    resultado = 10 / 0
except ZeroDivisionError:
    print("Error: División por cero")
finally:
    print("Operación finalizada")
```

## 7. Comprensión de Listas

```python
cuadrados = [x**2 for x in range(5)]
print(cuadrados)  # Imprime: [0, 1, 4, 9, 16]
```

---

**Nota**: Esta guía cubre los conceptos básicos de Python. Para más información, consulte la [documentación oficial de Python](https://docs.python.org/).
