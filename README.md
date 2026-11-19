# Momias de Guanajuato

Juego de plataformas hecho con Flutter. Camina y salta para derrotar momias,
recolectar calaveritas y llegar al final del nivel.

## 6. Cómo ejecutar todo

Desde la raíz del proyecto:

1. Ejecuta las pruebas:

   ```bash
   flutter test
   ```

2. Inicia el juego:

   ```bash
   flutter run
   ```

3. Mantén presionados los botones de izquierda o derecha para caminar y el
   botón de arriba para saltar.
4. Salta encima de las momias para derrotarlas, recolecta las calaveritas y
   llega al final del nivel.

> **Estado de pruebas:** en la rama `tdd-capturas-vscode`, `flutter test` pasa
> completo: **23 pruebas en verde** en los cinco archivos de prueba del manual.
> Ver la sección *Evidencia de cada prueba en VS Code*.

## 7. Checklist de este proyecto TDD

| Verificación | Estado |
| --- | :---: |
| La colisión AABB (`Rectangulo`) se probó de forma aislada antes de usarse en cualquier otra parte. | ✓ |
| `resolverColisionConPiso` usa la posición anterior del personaje, no solo la actual. | ✓ |
| El criterio de *stomp* exige caer y estar en la mitad superior de la momia, no solo intersectar. | ✓ |
| `patrullar()`, la aleatoriedad (`agregarFichaAleatoria`-style) y demás lógica sensible al tiempo son deterministas en las pruebas. | ✓ |
| `MotorJuego.mover()` es el único lugar que decide el orden de física, combate, recolección y meta. | ✓ |
| La interfaz no decide colisiones ni puntajes; solo traduce el estado de `MotorJuego` a píxeles. | ✓ |

## Evidencia

La captura muestra el juego en ejecución, con el personaje, las momias, las
calaveritas, las plataformas y los controles:

![Captura de evidencia del juego en ejecución](evidencia/captura-juego.png)

## Evidencia de cada prueba en VS Code

Rama: `tdd-capturas-vscode` · Usuario de GitHub: [Diegue83](https://github.com/Diegue83)

El código se copió del manual ronda por ronda y, en cada paso, se ejecutó en VS Code
(Terminal → Ejecutar tarea → **TDD: todas las pruebas**):

```bash
flutter test --reporter expanded
```

Cada captura muestra el resultado en la terminal y la cuenta **Diegue83 (GitHub)** con sesión iniciada en VS Code.

| Paso | Resultado | Captura |
| ---- | --------- | :-----: |
| Ronda 1 – Rojo | ❌ No compila: `Rectangulo` no existe | [01](evidencia/capturas_vscode/01_ronda1_rojo.jpg) |
| Ronda 1 – Verde | ✅ 2/2 | [02](evidencia/capturas_vscode/02_ronda1_verde.jpg) |
| Ronda 2 – Rojo | ❌ No compila: `Personaje` y `MotorFisica` no existen | [03](evidencia/capturas_vscode/03_ronda2_rojo.jpg) · [03b](evidencia/capturas_vscode/03b_ronda2_rojo_detalle.jpg) |
| Ronda 2 – Verde | ✅ 5/5 | [04](evidencia/capturas_vscode/04_ronda2_verde.jpg) |
| Ronda 3 – Rojo | ❌ No compila: `resolverColisionConPiso` no existe | [05](evidencia/capturas_vscode/05_ronda3_rojo.jpg) · [05b](evidencia/capturas_vscode/05b_ronda3_rojo_detalle.jpg) |
| Ronda 3 – Verde (código del manual) | ❌ 6 pasan, 1 falla: la prueba de aterrizaje espera `true` y obtiene `false` | [06](evidencia/capturas_vscode/06_ronda3_verde.jpg) |
| Ronda 3 – Corrección | ✅ 7/7 | [07](evidencia/capturas_vscode/07_ronda3_correccion.jpg) |
| Ronda 4 – Rojo | ❌ No compila: `moverHorizontal` no existe | [08](evidencia/capturas_vscode/08_ronda4_rojo.jpg) |
| Ronda 4 – Verde | ✅ 10/10 | [09](evidencia/capturas_vscode/09_ronda4_verde.jpg) |
| Ronda 5 – Rojo | ❌ No compila: `Momia` no existe | [10](evidencia/capturas_vscode/10_ronda5_rojo.jpg) |
| Ronda 5 – Verde | ✅ 13/13 | [11](evidencia/capturas_vscode/11_ronda5_verde.jpg) |
| Ronda 6 – Rojo | ❌ No compila: `MotorCombate` no existe | [12](evidencia/capturas_vscode/12_ronda6_rojo.jpg) |
| Ronda 6 – Verde (código del manual) | ❌ 15 pasan, 1 falla: el *stomp* espera `momiaDerrotada` y obtiene `ninguna` | [13](evidencia/capturas_vscode/13_ronda6_verde.jpg) · [13b](evidencia/capturas_vscode/13b_ronda6_verde_detalle.jpg) |
| Ronda 6 – Corrección | ✅ 16/16 | [14](evidencia/capturas_vscode/14_ronda6_correccion.jpg) |
| Ronda 7 – Rojo | ❌ No compila: `Calaverita` y `MotorJuego` no existen | [15](evidencia/capturas_vscode/15_ronda7_rojo.jpg) |
| Ronda 7 – Verde | ✅ 18/18 | [16](evidencia/capturas_vscode/16_ronda7_verde.jpg) |
| Ronda 8 – Rojo | ❌ No compila: `haLlegadoALaMeta` no existe | [17](evidencia/capturas_vscode/17_ronda8_rojo.jpg) |
| Ronda 8 – Verde | ✅ 20/20 | [18](evidencia/capturas_vscode/18_ronda8_verde.jpg) |
| Ronda 9 – Rojo | ❌ No compila: `EstadoJuego` y el constructor de `MotorJuego` no existen | [19](evidencia/capturas_vscode/19_ronda9_rojo.jpg) |
| Ronda 10 – Verde | ✅ 22/22 | [20](evidencia/capturas_vscode/20_ronda10_verde.jpg) |
| Integración | ✅ 23/23 | [21](evidencia/capturas_vscode/21_integracion.jpg) |

### Correcciones a las pruebas del manual

Dos pruebas del manual fallan aunque el código esté bien, porque sus datos no representan el caso que describen.
Solo se cambiaron los datos de esas pruebas; el código de `lib/logica/` es idéntico al del manual.

- **Ronda 3, aterrizaje:** con `y: 90` y `yAnterior: 85`, el pie anterior (117) ya estaba debajo de la plataforma (100), así que no es una caída desde arriba. Se usa `y: 70` y `yAnterior: 65`.
- **Ronda 6, *stomp*:** con `y: 68`, el pie del personaje queda justo en `y = 100` y la colisión AABB (estricta) no lo cuenta como intersección. Se usa `y: 70`.
- **`widget_test.dart`:** es la plantilla de `flutter create` (usa `MyApp`, que no existe) y el manual no la incluye; se eliminó.

#### Ronda 1 – Rojo
![Ronda 1 – Rojo](evidencia/capturas_vscode/01_ronda1_rojo.jpg)

#### Ronda 1 – Verde
![Ronda 1 – Verde](evidencia/capturas_vscode/02_ronda1_verde.jpg)

#### Ronda 2 – Rojo
![Ronda 2 – Rojo](evidencia/capturas_vscode/03_ronda2_rojo.jpg)
![Ronda 2 – Rojo](evidencia/capturas_vscode/03b_ronda2_rojo_detalle.jpg)

#### Ronda 2 – Verde
![Ronda 2 – Verde](evidencia/capturas_vscode/04_ronda2_verde.jpg)

#### Ronda 3 – Rojo
![Ronda 3 – Rojo](evidencia/capturas_vscode/05_ronda3_rojo.jpg)
![Ronda 3 – Rojo](evidencia/capturas_vscode/05b_ronda3_rojo_detalle.jpg)

#### Ronda 3 – Verde (código del manual)
![Ronda 3 – Verde (código del manual)](evidencia/capturas_vscode/06_ronda3_verde.jpg)

#### Ronda 3 – Corrección
![Ronda 3 – Corrección](evidencia/capturas_vscode/07_ronda3_correccion.jpg)

#### Ronda 4 – Rojo
![Ronda 4 – Rojo](evidencia/capturas_vscode/08_ronda4_rojo.jpg)

#### Ronda 4 – Verde
![Ronda 4 – Verde](evidencia/capturas_vscode/09_ronda4_verde.jpg)

#### Ronda 5 – Rojo
![Ronda 5 – Rojo](evidencia/capturas_vscode/10_ronda5_rojo.jpg)

#### Ronda 5 – Verde
![Ronda 5 – Verde](evidencia/capturas_vscode/11_ronda5_verde.jpg)

#### Ronda 6 – Rojo
![Ronda 6 – Rojo](evidencia/capturas_vscode/12_ronda6_rojo.jpg)

#### Ronda 6 – Verde (código del manual)
![Ronda 6 – Verde (código del manual)](evidencia/capturas_vscode/13_ronda6_verde.jpg)
![Ronda 6 – Verde (código del manual)](evidencia/capturas_vscode/13b_ronda6_verde_detalle.jpg)

#### Ronda 6 – Corrección
![Ronda 6 – Corrección](evidencia/capturas_vscode/14_ronda6_correccion.jpg)

#### Ronda 7 – Rojo
![Ronda 7 – Rojo](evidencia/capturas_vscode/15_ronda7_rojo.jpg)

#### Ronda 7 – Verde
![Ronda 7 – Verde](evidencia/capturas_vscode/16_ronda7_verde.jpg)

#### Ronda 8 – Rojo
![Ronda 8 – Rojo](evidencia/capturas_vscode/17_ronda8_rojo.jpg)

#### Ronda 8 – Verde
![Ronda 8 – Verde](evidencia/capturas_vscode/18_ronda8_verde.jpg)

#### Ronda 9 – Rojo
![Ronda 9 – Rojo](evidencia/capturas_vscode/19_ronda9_rojo.jpg)

#### Ronda 10 – Verde
![Ronda 10 – Verde](evidencia/capturas_vscode/20_ronda10_verde.jpg)

#### Integración
![Integración](evidencia/capturas_vscode/21_integracion.jpg)
