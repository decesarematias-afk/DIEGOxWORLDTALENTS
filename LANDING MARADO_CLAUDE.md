# CLAUDE.md — D10S: La Experiencia Interactiva de Diego Armando Maradona

## PROYECTO
Landing page interactiva premium tipo "museo digital privado" sobre Diego Armando Maradona. No es una wiki ni una biografía — es una **experiencia emocional 360** que hace que la gente lo conozca de verdad y se reenamore de él. Enfoque: lado humano, anécdotas exclusivas, frases poco conocidas, Argentina como eje.

## CARPETA
`~/Desktop/LANDING MARADO/`

## STACK TÉCNICO
- **Single-file HTML** (index.html) — autocontenido para deploy en Netlify
- HTML5 + CSS3 + Vanilla JS (o React si se necesita para complejidad)
- Google Fonts (Bebas Neue + Cormorant Garamond + Space Mono)
- YouTube embeds (lazy load, click-to-play)
- Spotify embeds (iframes de tracks/playlists)
- CSS animations + IntersectionObserver para scroll-triggered reveals
- 100% responsive (mobile first)
- NO frameworks pesados. NO dependencias npm. Deploy = arrastrar carpeta a Netlify.

## ESTÉTICA / DIRECCIÓN DE ARTE

### Concepto Visual: "Museo Nocturno de D10S"
Imaginar un museo de arte contemporáneo de noche, con paredes negras y piezas iluminadas con luz dorada focalizada. Cada sección es una "sala" del museo.

### Paleta
```
--dark: #0A0A0F (fondo principal)
--dark-card: #12121A (cards/paneles)
--dark-surface: #1A1A25 (superficies elevadas)
--gold: #D4AF37 (acento principal, bordes, títulos)
--gold-light: #F5D76E (highlights)
--celeste: #75AADB (acento Argentina)
--celeste-bright: #87CEEB
--white: #F0EDE6 (texto principal)
--white-dim: #A0A0A0 (texto secundario)
--neon-blue: #00D4FF (links, botones interactivos)
--fire: #FF4500 (hitos, momentos cumbre)
```

### Tipografía
- **Display/Títulos:** Bebas Neue (mayúsculas, tracking amplio, dorado)
- **Body/Narrativa:** Cormorant Garamond (serif, itálica para citas, elegante)
- **Data/Tags/UI:** Space Mono (monospace, pequeño, celeste/dim)

### Texturas
- Grain overlay sutil (SVG noise filter, opacity 0.03)
- Gradientes radiales sutiles en secciones
- Fade-to-black en bordes de imágenes
- Box-shadows dorados en hover (glow effect)

## ESTRUCTURA DE LA PÁGINA (Secciones = "Salas del Museo")

### SALA 0: HERO / PORTADA
- Imagen hero full-width: Diego levantando la Copa del Mundo 1986 (ya tenemos el base64, reutilizar del proyecto anterior o pedir al usuario que suba)
- Fade-to-black gradiente inferior
- Título: "D10S" en tipografía gigante con stroke dorado
- Subtítulo: "El lado que nunca te contaron de Diego Armando Maradona"
- Tagline en mono: "1960 — 2020 · ETERNO"
- Scroll indicator animado
- Parallax suave en el número 10

### SALA 1: VILLA FIORITO — "Donde Nació Todo"
**Formato: Storytelling con scroll + tarjetas flip**

Contenido narrativo (basado en investigación):
- La casa de Azamor 523: chapa, madera, sin agua, sin luz, sin gas
- Frase icónica: "Yo nací en un barrio privado de Buenos Aires: privado de luz, de agua, de teléfono y de gas"
- Los tachos de aceite para el agua
- Las tormentas y los tachitos bajo las goteras
- La primera pelota a los 3 años (regalo del primo Beto Zárate)
- La caída al pozo ciego persiguiendo una pelota
- "Soñaba con comer" — lo que pedía de chico
- La carta a los Reyes Magos que nunca llegó
- "En Fiorito a veces faltaba plata, pero nunca felicidad"

**Funcionalidad interactiva:**
- **Flip cards** (6 tarjetas): Frente = imagen/ícono + título corto. Reverso = anécdota completa + cita textual
- Animación: las cards aparecen con stagger al hacer scroll
- La casa fue declarada "Lugar Histórico Nacional" en 2021 (dato al final)

### SALA 2: DOÑA TOTA Y DON DIEGO — "El Amor que Sostuvo Todo"
**Formato: Línea dual (madre/padre) con paneles expandibles**

**Doña Tota (columna izquierda):**
- "No voy a comer, ando mal del estómago" (se saltaba comidas para que coman los hijos)
- Diego tardó hasta los 13 años en entender que nunca le había dolido nada
- Primer sueldo → Pizzería La Rumba: "Parecíamos Bill Gates y mi vieja la Reina Sofía"
- "Sos la primera mujer de mi vida, mi novia eterna"
- Tatuaje "Tota, te amo" en la espalda
- "Yo juego para vos, mamá" — llamada post goles a Inglaterra 1986
- Fallecimiento 19 noviembre 2011, Diego no llegó desde Dubái

**Don Diego "Chitoro" (columna derecha):**
- Nacido en Esquina, Corrientes. Vendió su barca llorando para emigrar a Buenos Aires
- Trabajaba en Tritumol (molienda de huesos) desde las 4-5 AM
- Se quedaba dormido parado en el colectivo, Diego lo sostenía en puntas de pie
- Le lustraba los botines con betún antes de cada partido
- Ruggeri: "Don Diego nos hacía los asados y nos servía él. Nunca lo escuché decir 'jugaron mal'"
- La mamá en cambio: "Jugaron mal, así no se juega" (brava, dura)

**Funcionalidad:** Panel izquierdo/derecho que se expande al click. En mobile, tabs Tota/Chitoro.

### SALA 3: FRASES DEL DIEGO — "En Sus Propias Palabras"
**Formato: Carrusel de citas con categorías filtrables**

Categorías (tabs/filtros):
1. **Identidad & Orígenes**
2. **Fútbol & Pasión**
3. **Familia & Amor**
4. **Filosofía & Vida**
5. **Humor & Picardía**

Frases (mínimo 20, organizadas por categoría):

**Identidad & Orígenes:**
- "Yo nací en un barrio privado de Buenos Aires: privado de luz, de agua, de teléfono y de gas"
- "Soy un cabecita negra, ¿cuál es el problema? Nunca renegué de mis orígenes"
- "Yo no soy ningún mago. Los magos son los que viven en Fiorito con mil pesos por mes"
- "¿Quién soy? El pibe de Villa Fiorito que una tarde de 1986 se puso a llorar cuando recibió la Copa del Mundo"

**Fútbol & Pasión:**
- "Si me muero, quiero volver a nacer y quiero ser futbolista. Y quiero volver a ser Diego Armando Maradona"
- "Cuando estás en la cancha, la vida se va, los problemas se van, todo se va"
- "La pelota no se mancha"
- "Lo que más me gusta del fútbol es la pelota. Todo lo demás, cansa"
- "Boca, sos el beso de mi mamá"

**Familia & Amor:**
- "Lo único que quiero es que mi viejo no trabaje más" (a los 15 años)
- "Yo juego para vos, mamá"
- "Yo siempre digo que mi viejo llegó primero, sino yo me casaba con ella" (sobre Doña Tota)

**Filosofía & Vida:**
- "La droga es un pacman que se come a toda tu familia"
- "¿Sabés qué jugador hubiese sido si no hubiese tomado droga? Un jugador de la puta madre"
- "Les pido que me dejen vivir mi vida. Nunca quise ser un ejemplo"
- "Ayuden a comer a la gente. Lo mío no es show, porque yo la pasé"

**Humor & Picardía:**
- "Me peleé con el Papa porque fui al Vaticano y vi los techos de oro"
- "Me siento más solo que Kung Fu" (en Cuba)

**Funcionalidad:**
- Cards con efecto typewriter al aparecer
- Filtro por categoría (tabs arriba)
- Fondo de cada cita con gradiente sutil diferente por categoría
- Click en card → se expande con contexto (cuándo lo dijo, a quién, en qué circunstancia)

### SALA 4: ANÉCDOTAS DEL VESTUARIO — "Lo Que Cuentan Los Que Estuvieron"
**Formato: Cards testimoniales con foto placeholder del narrador**

Testimonios (cada uno es una card expandible):

1. **Valdano — "La locomotora"**: En la final del 86, después del 2-0, Maradona le susurró "Quedate tranquilo, que de la locomotora me encargo yo". Luego marcó personalmente a Briegel porque entendió que Valdano estaba muerto.

2. **Valdano — El Gol del Siglo**: "Mirá cómo son las cosas. Yo estuve toda la jugada buscándote para darte la pelota, pero siempre se aparecía un inglés que me obligaba a cambiar de idea."

3. **Ruggeri — La Copa en el avión**: Después de ganar el Mundial, Maradona no soltaba la Copa. "Lo dormimos", confesó Ruggeri, para que el resto pudiera sacarse fotos.

4. **Ruggeri — Los regalos**: Diego compraba regalos para todos en los aeropuertos. En las concentraciones les daba vuelta la cama y les tiraba el colchón: "¿Sabés los gritos que pegaba?"

5. **Ruggeri — El funeral**: "Reaccioné cuando vi que el cajón decía Diego Armando Maradona. Empecé a llorar solo."

6. **Troglio — Primera concentración**: Compartía habitación con Maradona. "Maradona no debe ni saber quién soy yo", pensó. Diego entró: "Hola Pedrito." Al día siguiente lo invitó a comer a su casa.

7. **Bilardo (via Troglio)**: "Acá hay 21 jugadores que hacen lo que yo digo y uno que puede hacer lo que quiere." Diego, avergonzado: "No Carlos, no es así."

8. **Caniggia — Mundial 90**: Bilardo no quería llevar a Caniggia. Diego: "Si no va Claudio, yo tampoco." Bilardo lo convocó.

9. **Ferrara (Napoli)**: "Empecé a amar a Maradona a los 17 y no lo tuteaba. Seguí así 30 años. Era un Dios, pero nadie fue más humano."

10. **Careca (Napoli)**: "Maradona peleaba por todos. Por el utilero, por el masajista, por el último del banco."

11. **Lineker (Inglaterra)**: "Fue tan bueno ese segundo gol que por única vez en mi carrera pensaba aplaudir, aunque estuviera jugando en el equipo rival."

12. **Signorini (preparador físico)**: "Con Diego iría al fin del mundo. Pero con Maradona, no daría ni un paso."

**Funcionalidad:** 
- Grid de cards con foto placeholder (silueta dorada) + nombre + club/contexto
- Click → flip o expand con el testimonio completo
- Categorías: Selección 86 | Selección 90 | Napoli | Rivales

### SALA 5: EL DIEGO SOLIDARIO — "Lo Que Hizo en Silencio"
**Formato: Timeline vertical con íconos de corazón**

Historias:
1. **Bebé prematura (1987)**: Cuando nació Dalma, pagó la internación de una bebé prematura en la misma clínica. Nunca lo contó. Lo leyó Dalma décadas después, llorando.
2. **Niño de Acerra (1984, Nápoles)**: Jugó benéfico en campo embarrado ante 12.000 personas. Puso de su bolsillo los 15 millones de liras faltantes. El niño Luca dijo: "Él me dio la vida."
3. **Tarantini (campeón 78)**: Le pagó el colegio de los hijos cuando estaba en crisis.
4. **Hernán Fonseca (arquero en silla de ruedas)**: Viajó a jugar un benéfico. Pidió que la ovación fuera para Fonseca.
5. **Video Corazones Solidarios (2020)**: Se quebró ante cámara: "Ayuden a comer a la gente. Yo la pasé." No pudo terminar.
6. **Los remedios**: En su casa, gente llegaba a buscar medicamentos. Diego mandaba a sus hermanas a la farmacia con las recetas.
7. **Los pescadores de Esquina**: Invitó a los amigos de su padre a Buenos Aires. "Chicharra" Pérez se convirtió en un hermano más.

**Funcionalidad:** Scroll-triggered, cada historia aparece con fade-in + ícono animado (corazón que late una vez).

### SALA 6: FIORITO → AZTECA — "El Cuento de Hadas Argentino"
**Formato: Sección cinematográfica con parallax + video embed**

Contenido:
- La profecía del pibe de 12 años en TV: "Mis sueños son jugar en primera, vestir la camiseta de la Selección y ganar un Mundial" → CUMPLIÓ TODOS
- Debutó con un solo pantalón de corderoy en pleno calor
- Contexto Malvinas 1982: 649 soldados muertos. Herida abierta.
- "De alguna manera culpábamos a los jugadores ingleses por todo lo que había sufrido el pueblo argentino"
- La Mano de Dios: viveza criolla, no trampa
- El Gol del Siglo: 60 metros, 44 pasos, 12 toques, 10.87 segundos, 5 ingleses en el piso
- Relato de Víctor Hugo Morales: "¡Barrilete cósmico! ¿De qué planeta viniste?"
- Bielsa: "El mito que es esa persona nos hace creer que nosotros también podemos hacerlo"
- Peter Reid: "Me levanto transpirado de noche, con pesadillas"

**Video embed:** ARG vs ENG 1986 full match (YouTube: Pl3AnYCeTrU)

**Funcionalidad:** Background parallax con gradiente celeste/blanco → dorado. Contadores animados (60m, 44 pasos, 12 toques, 10.87s).

### SALA 7: D10S COMO RELIGIÓN — "Por Qué Argentina Lo Convirtió en Dios"
**Formato: Infografía interactiva**

Contenido:
- Cuarteto de mitos argentinos: Gardel, Evita, el Che, Maradona
- **Iglesia Maradoniana** (fundada 1998, Rosario): 500.000+ fieles, 60+ países
  - 10 mandamientos (el 1ro: "La pelota no se mancha")
  - Navidad Maradoniana: 30 de octubre
  - Pascua Maradoniana: 22 de junio
  - Calendario d.D. (después de Diego)
  - Rezo: "Diego nuestro que estás en el cielo, santificada sea tu zurda..."
- Canciones dedicadas (con Spotify embeds):
  - Rodrigo Bueno — "La Mano de Dios" (la favorita de Diego)
  - Las Pastillas del Abuelo — "Es Dios"
  - Manu Chao — "Santa Maradona" / "La Vida Tombola"
  - Andrés Calamaro — referencia a Diego
  - Calle 13 — "Latinoamérica" ("Soy Maradona contra Inglaterra anotándote dos goles")
- Murales:
  - Buenos Aires: Martín Ron (14 pisos), Alfredo Segatori (La Boca), Bagnasco (visible desde Ezeiza)
  - La Paternal: 17 murales consecutivos de Victor Marley
  - Villa Fiorito: pintados el día de su muerte
  - Nápoles: Mario Filardi (Quartieri Spagnoli, 1990) — 6 millones de visitantes/año

**Funcionalidad:**
- Spotify iframes embebidos (previews de 30s)
- Grid de murales con hover zoom
- Los 10 mandamientos en accordion/collapsible

### SALA 8: NÁPOLES — "La Ciudad que Lo Amó Como Ninguna"
**Formato: Sección con fondo azul Napoli + cards**

Contenido clave (resumen, no protagonista):
- Llegó en helicóptero, 70.000 personas lo esperaban
- "Yo quería ser el ídolo de los chicos pobres de Nápoles, porque son como yo fui en Buenos Aires"
- Pancarta: "Berlusconi, ahora los ricos también lloran"
- Figuritas de Diego en los pesebres navideños junto al Papa
- Bar Nilo: frasco con "las lágrimas de Maradona"
- Estadio renombrado "Diego Armando Maradona" (dic 2020)
- Mural de Quartieri Spagnoli: santuario con altar y ofrendas

### SALA 9: EL ADIÓS — "La Tarde que Argentina Se Detuvo"
**Formato: Sección emotiva, fondo negro puro, tipografía grande**

Contenido:
- 30 octubre 2020: último cumpleaños. Estadio de Gimnasia. Caminando sostenido. A los 3 minutos pidió irse.
- Signorini: "A Diego habría que festejarle los días en vez de los cumpleaños"
- 25 noviembre 2020: paro cardíaco en Tigre. Corazón de 503 gramos.
- Féretro en Casa Rosada (Salón de los Patriotas Latinoamericanos). Bandera argentina + camiseta de Boca + camiseta de Argentinos + pañuelos de Madres de Plaza de Mayo.
- Fila de 1.6 km. ~1 millón de personas rompieron cuarentena.
- Primer visitante: Nahuel De Lima, de Villa Fiorito, con muletas: "Quien habla de Maradona también habla de Argentina"
- Gases lacrimógenos DENTRO de la Casa Rosada
- Cortejo por 9 de Julio. Banderas en puentes. Todos los clubes unidos.
- Messi: "Se nos va pero no se va, porque el Diego es eterno"
- Galeano: "El más humano de los dioses"
- Pancarta argentina: "No importa lo que hayas hecho con tu vida. Importa lo que hiciste con nuestras vidas."

**Funcionalidad:** Texto que aparece línea por línea con scroll. Minimalista. Sin cards. Solo texto grande y espacio negro.

### SALA 10: FOOTER / CIERRE
- Cita final: "Si me muero, quiero volver a nacer y quiero ser futbolista. Y quiero volver a ser Diego Armando Maradona."
- "Cumplido, Diego. Todo cumplido."
- Créditos: D10S · DE FIORITO AL INFINITO · 1960–2020
- Links: Playlist FIFA YouTube, Spotify playlist, documental Kapadia

---

## FUNCIONALIDADES INTERACTIVAS (CHECKLIST)

### Obligatorias:
- [ ] **Flip cards** (CSS 3D transform) — en Sala 1 (Fiorito) y Sala 4 (Vestuario)
- [ ] **Collapsible/accordion** — en Sala 2 (Familia) y Sala 7 (Mandamientos)
- [ ] **Carrusel filtrable de frases** — Sala 3 (tabs por categoría)
- [ ] **YouTube embeds lazy-load** — click-to-play con thumbnail preview
- [ ] **Spotify embeds** — iframes de tracks específicos (30s preview)
- [ ] **Contadores animados** — Sala 6 (60m, 44 pasos, 12 toques, 10.87s del Gol del Siglo)
- [ ] **Scroll-triggered animations** — IntersectionObserver en todas las secciones
- [ ] **Parallax** — Hero + Sala 6
- [ ] **Expand/Collapse all** — botón global
- [ ] **Responsive** — mobile first, breakpoint 768px

### Deseables (si el archivo no se hace gigante):
- [ ] **Barra de progreso** de lectura (top sticky, dorada, 2px)
- [ ] **Navegación lateral** — dots/bullets fijos que indican en qué sala estás
- [ ] **Easter egg**: Konami code o click en el "10" del hero → reproduce audio del relato de Víctor Hugo Morales
- [ ] **Modo "Luces apagadas"**: botón que pone todo en negro absoluto excepto el texto (modo lectura nocturna extrema)
- [ ] **Share cards**: botón en cada cita para copiar como imagen/texto

## VIDEOS DE YOUTUBE A EMBEDER
```
- Final Mundial U-20 1979 (ARG vs URSS): eXFeaQLc42M
- Batalla del Bernabéu 1984: tLHK9bSZpkg
- ARG vs ENG 1986 (FIFA Full Match): Pl3AnYCeTrU
- Napoli vs Milan 86/87: V1iXExcKeXI
- Playlist FIFA Maradona: PLCGIzmTE4d0i50BeizuDk6K1YbbRkPh1I
- FIFA+ ARG-ENG 1986: https://www.plus.fifa.com/en/content/argentina-v-england-quarter-finals-1986-fifa-world-cup-mexico-full-match-replay/3e760034-8966-404b-9c4c-214a2dec6bf1
```

## CANCIONES SPOTIFY A EMBEDER
```
- Rodrigo Bueno — "La Mano de Dios": spotify:track:1dNmjzGKb0BFGHOT8rE9B4
- Las Pastillas del Abuelo — "Es Dios": spotify:track:2Q4bUjBpi9xFL8w9g8BJUA
- Manu Chao — "La Vida Tombola": spotify:track:5QY0EERd2eqFhqBdFnxtHi
- Andrés Calamaro — "Maradona": buscar en Spotify
- Calle 13 — "Latinoamérica": spotify:track:3PuHGMxqXeNEJatqbjbwN2
```
Para embeds de Spotify usar formato:
```html
<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/TRACK_ID?theme=0" width="100%" height="80" frameBorder="0" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>
```

## INSTRUCCIONES PARA CLAUDE CODE

1. **Crear `index.html`** en `~/Desktop/LANDING MARADO/`
2. **Todo en un solo archivo** (CSS inline en `<style>`, JS inline en `<script>`)
3. **Imágenes**: Usar thumbnails de YouTube como placeholders (img.youtube.com/vi/VIDEO_ID/hqdefault.jpg). No necesitamos imágenes propias salvo el hero (que el usuario subirá).
4. **Performance**: Lazy load en todo. No cargar iframes de YouTube/Spotify hasta que el usuario haga click o scroll a esa sección.
5. **Tamaño target**: < 500KB el HTML (sin contar imágenes base64 que se agreguen después)
6. **Deploy**: Solo arrastrar la carpeta a Netlify. Sin build step.
7. **Mobile**: Todo tiene que funcionar y verse perfecto en iPhone SE hasta desktop 1920px.
8. **Accesibilidad**: Aria labels en botones interactivos. Contraste suficiente.

## PRIORIDAD DE CONSTRUCCIÓN
1. Hero + estructura de secciones + navegación
2. Sala 1 (Fiorito) con flip cards
3. Sala 3 (Frases) con carrusel filtrable
4. Sala 4 (Vestuario) con cards expandibles
5. Sala 5 (Solidario) con timeline
6. Sala 6 (Azteca) con contadores + video
7. Sala 2 (Familia) con paneles duales
8. Sala 7 (Religión) con Spotify + mandamientos
9. Sala 8 (Nápoles) resumida
10. Sala 9 (Adiós) minimalista
11. Footer + navegación lateral + progreso

## TONO DEL CONTENIDO
- Celebratorio, emotivo, íntimo
- Escrito en español argentino
- Sin spoilers de momentos tristes hasta el final
- Cada sala tiene que terminar con una frase/cita que cierre emocionalmente
- No es una enciclopedia: es un viaje emocional de principio a fin
