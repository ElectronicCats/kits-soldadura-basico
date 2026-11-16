# Kits de soldadura básico · Electronic Cats

Cuatro gatos para aprender a soldar componentes de inserción (through hole): **Gatito Esotérico**, **Robocat**,
**Mariachi Meow** y **Gato Alebrije**. Al terminar y poner la pila, los ojos del gato parpadean alternados.

Se regalaron 100 kits en la Villa del Hardware de BugCON 2026 (CDMX), con el patrocinio de UNIT Electronics.

**Guía en video paso a paso:** https://youtu.be/u02vvQnGIQA

## Qué trae cada kit

| Cant. | Pieza | Referencia en la placa |
|---|---|---|
| 1 | PCB del gato | — |
| 2 | LED amarillo 3 mm | D1, D2 |
| 2 | Capacitor electrolítico 100 µF / 16 V | C3, C4 |
| 2 | Resistencia axial 330 Ω | R1, R4 |
| 2 | Resistencia axial 1 kΩ | R2, R3 |
| 2 | Transistor NPN BC547 | Q1, Q2 (en el Robocat: Q3, Q4) |
| 1 | Portapilas CR2032 | BT1 (va por detrás) |
| 1 | Switch SMD | SW2 (va por detrás) |

La pila CR2032 no viene en la lista de materiales del kit.

## Cómo se arma

1. **LED** (D1, D2). Tienen polaridad: la pata larga va en **+**.
2. **Capacitores** (C3, C4). Tienen polaridad: la franja va en **−**. Corta las patitas que sobran.
3. **Resistencias**: 330 Ω en R1 y R4, 1 kΩ en R2 y R3. No tienen polaridad.
4. **Transistores** (Q1, Q2). La cara plana va como en el dibujo de la placa.
5. **La vuelta**: portapilas.
6. **La vuelta**: switch. Fíjalo con pinzas y suelda una patita primero.
7. Pon la pila CR2032 con el **+** hacia afuera y mueve el switch a **ON**.

## Cómo funciona

Es un oscilador de dos transistores (multivibrador astable). Cada LED va **en paralelo** con su transistor, del
colector a tierra, y se alimenta por su resistencia de 330 Ω: cuando el transistor conduce, apaga su LED; cuando se
corta, el LED enciende. Los capacitores cruzan cada colector con la base del otro transistor y las resistencias de
1 kΩ cargan las bases, así que los dos LED se alternan unas seis veces por segundo.

**Por qué 1 kΩ y 100 µF (y no 100 kΩ y 10 µF):** para apagar su LED, cada transistor debe hundir unos 9 mA
(3.3 V / 330 Ω). Con 100 kΩ en la base sólo le entran ~26 µA y un BC547 no se satura: el colector apenas baja,
el LED amarillo fija el nivel alto en ~2 V y el salto que pasa al otro transistor (~0.4 V) no alcanza para cortarlo.
Los dos se quedan a medias y el circuito no oscila. Con 1 kΩ la base recibe ~2.6 mA, el transistor se satura y
conmuta limpio; el capacitor sube a 100 µF para que el parpadeo no sea demasiado rápido.

## Hardware

Diseñado en KiCad 9. Cada gato tiene su proyecto en `hardware/Kit_<gato>/` (esquemático, PCB y vistas frontal y
trasera en SVG). Los archivos de fabricación se generan con KiBot (`.github/workflows/kicad_fabrication_files.yml`).

Diseño: Electronic Cats.
