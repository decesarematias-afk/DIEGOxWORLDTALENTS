# CLAUDE.md — Integración World Talents × D10S
## Maradona Landing — Perfil WT + Chat + Botonera

---

## Contexto del proyecto

Landing page interactiva sobre Diego Armando Maradona (`1776095362810_index.html`) con 3 tabs:
- **tab-maradona** — Experiencia principal: chat con Diego, perfil WT, botonera marcas
- **tab-maradoniano** — Museo interactivo con 14 salas
- **tab-hincha** — Sección para fanáticos con fixture, canciones, mapa

El archivo es HTML puro (sin framework), con React cargado via CDN solo en el archivo `index.html` del perfil WT.

---

## Transformación requerida

### ANTES (estado actual)
```
tab-maradona:
  [Hero flotante Diego + "Chateá con Diego" button]  ← REEMPLAZAR
  [Chat V1 #sala-voz]                                 ← MANTENER
  [Chat V2 #sala-voz-v2]                              ← ELIMINAR
  [Footer]

tab-maradoniano:
  [#hero-museo banner]                                ← REEMPLAZAR
  [Museo nav + 14 salas]                              ← MANTENER
```

### DESPUÉS (estado objetivo)
```
tab-maradona:
  [Perfil World Talents del Diego]                    ← NUEVO
  [Chat V1 #sala-voz]                                 ← SIN CAMBIOS
  [Botonera marcas estilo Linktree]                   ← NUEVO
  [Footer]

tab-maradoniano:
  [Hero viejo de tab-maradona movido aquí]            ← MOVER
  [Museo nav + 14 salas]                              ← SIN CAMBIOS
```

---

## Tarea 1: Mover el hero actual de tab-maradona → tab-maradoniano

### Qué mover
El bloque completo del `<section id="hero">` de **tab-maradona** (líneas ~2316 a 2410 del HTML).
Contiene: fondo con imagen de YouTube, parallax "10", foto flotante de Diego, label "HABLÁ CON:", botón WhatsApp "CHATEÁ CON DIEGO", scroll indicator.

### Dónde colocarlo
Reemplazar el `<section class="hero-museo" id="hero-museo">` en **tab-maradoniano** (líneas ~2491 a 2519).
El `#hero-museo` tiene su propia clase CSS. El hero antiguo tiene clase `#hero`. Conservar el hero antiguo con su `id="hero"` y sus estilos propios — funcionará igual en el nuevo tab.

### Ajuste de scroll indicator
El scroll indicator del hero antiguo apunta a `#sala-voz`. En su nueva ubicación en tab-maradoniano, debe apuntar a `#sala-fiorito`:
```html
<!-- CAMBIAR esto en el hero movido: -->
onclick="document.getElementById('sala-voz').scrollIntoView({behavior:'smooth'})"
<!-- POR esto: -->
onclick="document.getElementById('sala-fiorito').scrollIntoView({behavior:'smooth'})"
```

---

## Tarea 2: Eliminar Chat V2

Eliminar completamente el bloque:
```html
<!-- ═══════════════════════════════════════════
     SECCIÓN VOZ V2: DIEGO ANÉCDOTAS COMPLETAS
     ═══════════════════════════════════════════ -->
<section class="diego-v2-section" id="sala-voz-v2">
  ...
</section>
```

También eliminar del CSS todo lo que tenga clases `.diego-v2-*` (buscar en `<style>`).
También eliminar del JS toda la lógica que referencie `V2`, `diegoChatMessagesV2`, `diegoMicBtnV2`, `diegoChatInputV2`, `diegoSendBtnV2`, `diegoVoiceStatusV2`.

---

## Tarea 3: Perfil World Talents del Diego

### Posición
Va al INICIO de `tab-maradona`, antes de `#sala-voz`. Reemplaza el hero que fue movido.

### Diseño del perfil — Tema "Argentina"
Paleta extraída del sistema de temas del `index.html` WT:
```css
/* Variables del tema Argentina para este perfil */
--wt-teal:     #75AADB;   /* celeste */
--wt-teal-dk:  #2b5f8a;
--wt-teal-lt:  #a8d4f5;
--wt-neon:     #F5CB5C;   /* dorado/amarillo */
--wt-green:    #F5CB5C;   /* mismo dorado */
--wt-green-dk: #c9a020;
--wt-black:    #070b12;   /* negro noche argentina */
--wt-black-lt: #0f1520;
--wt-gold:     #D4AF37;   /* dorado Maradona */
```

### Estructura HTML del perfil WT del Diego

```html
<!-- ═══════════════════════════════════════════════
     PERFIL WORLD TALENTS — DIEGO ARMANDO MARADONA
     ═══════════════════════════════════════════════ -->
<section id="wt-profile-diego" class="wt-profile-section">

  <!-- Fondo con ambient glow celeste + dorado -->
  <div class="wt-profile-bg">
    <div class="wt-bg-glow-celeste"></div>
    <div class="wt-bg-glow-gold"></div>
    <!-- Partículas de estrellas opcionales -->
    <div class="wt-stars" aria-hidden="true"></div>
  </div>

  <!-- Container del perfil (estilo mobile-first, max 420px centrado) -->
  <div class="wt-profile-card">

    <!-- Header: contador de visitas + globo -->
    <div class="wt-profile-header-stats">
      <div class="wt-stat-badge wt-stat-left">
        <span class="wt-stat-num">35.6M</span>
        <span class="wt-stat-lbl">SEGUIDORES 🌍</span>
      </div>
      <div class="wt-stat-badge wt-stat-right">
        <span class="wt-stat-num">∞</span>
        <span class="wt-stat-lbl">ME CONOCEN 🌐</span>
      </div>
    </div>

    <!-- Avatar con borde celeste pulsante -->
    <div class="wt-avatar-wrap">
      <!-- Anillos NFC pulsantes (estilo World Talents) -->
      <div class="wt-avatar-ring wt-ring-1"></div>
      <div class="wt-avatar-ring wt-ring-2"></div>
      <div class="wt-avatar-ring wt-ring-3"></div>
      <!-- Foto de Diego -->
      <img
        class="wt-avatar-img"
        src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/2c/Maradona-Mundial_86_con_la_copa.JPG/400px-Maradona-Mundial_86_con_la_copa.JPG"
        alt="Diego Armando Maradona"
        onerror="this.src=''; this.parentElement.classList.add('wt-avatar-fallback')"
      >
      <!-- Badge verificado -->
      <div class="wt-avatar-badge" title="Perfil World Talents verificado">
        <svg width="14" height="14" viewBox="0 0 24 24" fill="white"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg>
      </div>
    </div>

    <!-- Label World Talents -->
    <div class="wt-brand-label">
      <span class="wt-brand-dot"></span>
      World Talents
    </div>

    <!-- Nombre -->
    <h1 class="wt-profile-name">Diego Armando Maradona</h1>
    <p class="wt-profile-handle">@d10s</p>

    <!-- Roles (acordeón estilo WT) -->
    <div class="wt-roles">

      <div class="wt-role-btn" onclick="wtToggleRole(this)">
        <span class="wt-role-icon">🏆</span>
        <span class="wt-role-label">CAMPEÓN DEL MUNDO</span>
        <span class="wt-role-chev">›</span>
      </div>
      <div class="wt-role-body">
        <p>Copa del Mundo México 1986 · Capitán de Argentina · Gol del Siglo · La Mano de Dios · 5 goles y 5 asistencias en un solo torneo.</p>
      </div>

      <div class="wt-role-btn" onclick="wtToggleRole(this)">
        <span class="wt-role-icon">⚽</span>
        <span class="wt-role-label">EL MEJOR DE LA HISTORIA</span>
        <span class="wt-role-chev">›</span>
      </div>
      <div class="wt-role-body">
        <p>Argentinos Juniors · Boca Juniors · FC Barcelona · SSC Napoli (2 Scudetti) · Selección Argentina (91 goles). Premio al Mejor Jugador del Siglo XX · Balón de Oro del Mundial 1986.</p>
      </div>

      <div class="wt-role-btn" onclick="wtToggleRole(this)">
        <span class="wt-role-icon">🕊️</span>
        <span class="wt-role-label">LUCHADOR DEL PUEBLO</span>
        <span class="wt-role-chev">›</span>
      </div>
      <div class="wt-role-body">
        <p>De Villa Fiorito al infinito. Símbolo de la Argentina popular. "La pelota no se mancha." 1960 — 2020.</p>
      </div>

    </div>

    <!-- Bio -->
    <p class="wt-profile-bio">
      "Yo nací en un barrio privado de Buenos Aires: privado de luz, de agua, de teléfono y de gas."
    </p>

    <!-- Redes sociales del Diego -->
    <div class="wt-social-row">
      <a class="wt-social-btn wt-social-ig"
         href="https://instagram.com/maradona" target="_blank" rel="noopener"
         title="Instagram oficial @maradona">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor">
          <rect x="2" y="2" width="20" height="20" rx="5"/>
          <circle cx="12" cy="12" r="5" fill="none" stroke="currentColor" stroke-width="1.5"/>
          <circle cx="17.5" cy="6.5" r="1.2" fill="currentColor"/>
        </svg>
      </a>
      <a class="wt-social-btn wt-social-fb"
         href="https://facebook.com/diegomaradona" target="_blank" rel="noopener"
         title="Facebook Diego Maradona">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor">
          <path d="M18 2h-3a5 5 0 00-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 011-1h3z"/>
        </svg>
      </a>
      <a class="wt-social-btn wt-social-tw"
         href="https://twitter.com/DiegoAMaradona" target="_blank" rel="noopener"
         title="Twitter @DiegoAMaradona">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor">
          <path d="M23 3a10.9 10.9 0 01-3.14 1.53 4.48 4.48 0 00-7.86 3v1A10.66 10.66 0 013 4s-4 9 5 13a11.64 11.64 0 01-7 2c9 5 20 0 20-11.5a4.5 4.5 0 00-.08-.83A7.72 7.72 0 0023 3z"/>
        </svg>
      </a>
      <a class="wt-social-btn wt-social-yt"
         href="https://youtube.com/@diegomaradona" target="_blank" rel="noopener"
         title="YouTube">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor">
          <path d="M22.54 6.42a2.78 2.78 0 00-1.95-1.96C18.88 4 12 4 12 4s-6.88 0-8.59.46A2.78 2.78 0 001.46 6.42 29 29 0 001 12a29 29 0 00.46 5.58A2.78 2.78 0 003.41 19.6C5.12 20 12 20 12 20s6.88 0 8.59-.46a2.78 2.78 0 001.95-1.95A29 29 0 0023 12a29 29 0 00-.46-5.58z"/>
          <polygon points="9.75 15.02 15.5 12 9.75 8.98 9.75 15.02" fill="#0A0E1A"/>
        </svg>
      </a>
      <a class="wt-social-btn wt-social-globe"
         href="https://m10memorial.com" target="_blank" rel="noopener"
         title="M10 Memorial">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8">
          <circle cx="12" cy="12" r="10"/>
          <line x1="2" y1="12" x2="22" y2="12"/>
          <path d="M12 2a15.3 15.3 0 014 10 15.3 15.3 0 01-4 10 15.3 15.3 0 01-4-10 15.3 15.3 0 014-10z"/>
        </svg>
      </a>
    </div>

    <!-- Botones CTA -->
    <div class="wt-cta-row">
      <button class="wt-cta-save" onclick="wtSaveContact()">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <path d="M21 15v4a2 2 0 01-2 2H5a2 2 0 01-2-2v-4"/>
          <polyline points="7 10 12 15 17 10"/>
          <line x1="12" y1="15" x2="12" y2="3"/>
        </svg>
        Guardar contacto
      </button>
      <button class="wt-cta-follow" onclick="wtFollowDiego()">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <path d="M16 21v-2a4 4 0 00-4-4H6a4 4 0 00-4 4v2"/>
          <circle cx="9" cy="7" r="4"/>
          <line x1="19" y1="8" x2="19" y2="14"/>
          <line x1="22" y1="11" x2="16" y2="11"/>
        </svg>
        + Seguir
      </button>
    </div>

    <!-- World Talents branding footer -->
    <div class="wt-profile-footer">
      <span class="wt-footer-tag">Powered by</span>
      <span class="wt-footer-brand">World Talents</span>
      <span class="wt-footer-nfc">· NFC ·</span>
      <span class="wt-footer-tag">phygital</span>
    </div>

  </div><!-- /wt-profile-card -->
</section>
```

### CSS del perfil WT del Diego

```css
/* ═══════════════════════════════════════════════
   PERFIL WORLD TALENTS — DIEGO
   Variables: celeste + dorado argentino
   ═══════════════════════════════════════════════ */

#wt-profile-diego {
  position: relative;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 40px 20px 60px;
  background: #070b12;
  overflow: hidden;
}

/* Ambient glows */
.wt-bg-glow-celeste {
  position: absolute;
  width: 500px; height: 500px;
  border-radius: 50%;
  background: radial-gradient(circle, rgba(117,170,219,0.10) 0%, transparent 70%);
  top: -100px; left: 50%;
  transform: translateX(-50%);
  pointer-events: none;
}
.wt-bg-glow-gold {
  position: absolute;
  width: 400px; height: 300px;
  border-radius: 50%;
  background: radial-gradient(circle, rgba(212,175,55,0.07) 0%, transparent 70%);
  bottom: 0; right: -100px;
  pointer-events: none;
}

/* Stars particle layer */
.wt-stars {
  position: absolute;
  inset: 0;
  background-image:
    radial-gradient(1px 1px at 20% 30%, rgba(117,170,219,0.6) 0%, transparent 100%),
    radial-gradient(1px 1px at 80% 10%, rgba(212,175,55,0.5) 0%, transparent 100%),
    radial-gradient(1px 1px at 50% 80%, rgba(117,170,219,0.4) 0%, transparent 100%),
    radial-gradient(1.5px 1.5px at 10% 60%, rgba(245,203,92,0.5) 0%, transparent 100%),
    radial-gradient(1px 1px at 90% 50%, rgba(117,170,219,0.3) 0%, transparent 100%),
    radial-gradient(1px 1px at 60% 20%, rgba(212,175,55,0.4) 0%, transparent 100%),
    radial-gradient(1px 1px at 35% 90%, rgba(117,170,219,0.3) 0%, transparent 100%);
  pointer-events: none;
}

/* Card container */
.wt-profile-card {
  position: relative;
  z-index: 2;
  width: 100%;
  max-width: 420px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0;
}

/* Header stats */
.wt-profile-header-stats {
  width: 100%;
  display: flex;
  justify-content: space-between;
  margin-bottom: 16px;
}
.wt-stat-badge {
  background: rgba(117,170,219,0.08);
  border: 1px solid rgba(117,170,219,0.20);
  border-radius: 12px;
  padding: 10px 16px;
  text-align: center;
  min-width: 110px;
}
.wt-stat-num {
  display: block;
  font-family: 'Bebas Neue', sans-serif;
  font-size: 22px;
  color: #75AADB;
  line-height: 1;
}
.wt-stat-lbl {
  display: block;
  font-family: 'Space Mono', monospace;
  font-size: 9px;
  color: rgba(255,255,255,0.45);
  text-transform: uppercase;
  letter-spacing: 1px;
  margin-top: 3px;
}

/* Avatar con anillos pulsantes */
.wt-avatar-wrap {
  position: relative;
  width: 140px; height: 140px;
  margin-bottom: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.wt-avatar-ring {
  position: absolute;
  border-radius: 50%;
  border: 1px solid #75AADB;
  animation: wtRingPulse 2.4s ease-out infinite;
}
.wt-avatar-ring.wt-ring-1 { width: 140px; height: 140px; animation-delay: 0s; }
.wt-avatar-ring.wt-ring-2 { width: 168px; height: 168px; animation-delay: 0.4s; }
.wt-avatar-ring.wt-ring-3 { width: 196px; height: 196px; animation-delay: 0.8s; }

@keyframes wtRingPulse {
  0%   { opacity: 0.7; transform: scale(0.95); }
  100% { opacity: 0;   transform: scale(1.3); }
}

.wt-avatar-img {
  width: 128px; height: 128px;
  border-radius: 50%;
  object-fit: cover;
  border: 2.5px solid #75AADB;
  box-shadow:
    0 0 0 4px rgba(7,11,18,1),
    0 0 25px rgba(117,170,219,0.35),
    0 0 50px rgba(117,170,219,0.12);
  position: relative; z-index: 1;
}
.wt-avatar-fallback {
  background: linear-gradient(135deg, #D4AF37, #75AADB);
}
.wt-avatar-fallback::after {
  content: 'D10S';
  position: absolute;
  font-family: 'Bebas Neue', sans-serif;
  font-size: 32px;
  color: white;
}

/* Badge verificado (esquina inferior derecha del avatar) */
.wt-avatar-badge {
  position: absolute;
  bottom: 4px; right: 4px;
  width: 28px; height: 28px;
  border-radius: 50%;
  background: #75AADB;
  border: 2px solid #070b12;
  display: flex; align-items: center; justify-content: center;
  z-index: 2;
}

/* Brand label */
.wt-brand-label {
  display: flex;
  align-items: center;
  gap: 6px;
  background: rgba(255,255,255,0.04);
  border: 1px solid rgba(255,255,255,0.08);
  border-radius: 20px;
  padding: 5px 14px;
  font-family: 'Space Mono', monospace;
  font-size: 10px;
  color: rgba(255,255,255,0.55);
  letter-spacing: 1px;
  margin-bottom: 10px;
}
.wt-brand-dot {
  width: 7px; height: 7px;
  border-radius: 50%;
  background: #75AADB;
  box-shadow: 0 0 6px #75AADB;
  animation: wtDotBlink 2s ease-in-out infinite;
}
@keyframes wtDotBlink {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.4; }
}

/* Nombre */
.wt-profile-name {
  font-family: 'Bebas Neue', sans-serif;
  font-size: clamp(26px, 7vw, 36px);
  color: #F0EDE6;
  letter-spacing: 0.05em;
  text-align: center;
  line-height: 1.1;
  margin: 0 0 4px;
}
.wt-profile-handle {
  font-family: 'Space Mono', monospace;
  font-size: 12px;
  color: rgba(255,255,255,0.35);
  letter-spacing: 1px;
  margin-bottom: 20px;
}

/* Roles acordeón */
.wt-roles {
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 8px;
  margin-bottom: 18px;
}
.wt-role-btn {
  display: flex;
  align-items: center;
  gap: 12px;
  background: rgba(255,255,255,0.03);
  border: 1px solid rgba(117,170,219,0.20);
  border-radius: 14px;
  padding: 14px 16px;
  cursor: pointer;
  transition: all 0.25s ease;
  user-select: none;
}
.wt-role-btn:hover {
  background: rgba(117,170,219,0.07);
  border-color: rgba(117,170,219,0.40);
}
.wt-role-btn.wt-role-open {
  background: rgba(117,170,219,0.06);
  border-color: #75AADB;
}
.wt-role-icon { font-size: 18px; }
.wt-role-label {
  flex: 1;
  font-family: 'Bebas Neue', sans-serif;
  font-size: 15px;
  color: #75AADB;
  letter-spacing: 1px;
}
.wt-role-chev {
  font-size: 18px;
  color: #75AADB;
  transition: transform 0.25s;
  line-height: 1;
}
.wt-role-btn.wt-role-open .wt-role-chev { transform: rotate(90deg); }

.wt-role-body {
  display: none;
  padding: 0 16px 14px;
  margin-top: -4px;
}
.wt-role-body.wt-role-open { display: block; }
.wt-role-body p {
  font-family: 'Inter', sans-serif;
  font-size: 13px;
  color: rgba(255,255,255,0.65);
  line-height: 1.6;
  margin: 0;
}

/* Bio */
.wt-profile-bio {
  font-family: 'Lora', serif;
  font-style: italic;
  font-size: 13px;
  color: rgba(212,175,55,0.8);
  text-align: center;
  line-height: 1.6;
  max-width: 340px;
  margin-bottom: 20px;
  padding: 0 10px;
}

/* Redes sociales */
.wt-social-row {
  display: flex;
  gap: 10px;
  margin-bottom: 16px;
  flex-wrap: wrap;
  justify-content: center;
}
.wt-social-btn {
  width: 44px; height: 44px;
  border-radius: 12px;
  display: flex; align-items: center; justify-content: center;
  text-decoration: none;
  transition: all 0.2s ease;
  border: 1px solid transparent;
}
.wt-social-btn:hover { transform: translateY(-2px); }
.wt-social-ig  { background: rgba(228,64,95,.12);  color: #E4405F; border-color: rgba(228,64,95,.25); }
.wt-social-fb  { background: rgba(24,119,242,.12); color: #1877F2; border-color: rgba(24,119,242,.25); }
.wt-social-tw  { background: rgba(29,161,242,.12); color: #1DA1F2; border-color: rgba(29,161,242,.25); }
.wt-social-yt  { background: rgba(255,0,0,.10);    color: #FF0000; border-color: rgba(255,0,0,.20); }
.wt-social-globe { background: rgba(117,170,219,.10); color: #75AADB; border-color: rgba(117,170,219,.25); }

/* CTA row */
.wt-cta-row {
  display: flex;
  gap: 10px;
  width: 100%;
  margin-bottom: 20px;
}
.wt-cta-save, .wt-cta-follow {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  padding: 13px 10px;
  border-radius: 14px;
  font-family: 'Bebas Neue', sans-serif;
  font-size: 14px;
  letter-spacing: 1px;
  cursor: pointer;
  border: none;
  transition: all 0.25s ease;
}
.wt-cta-save {
  background: rgba(117,170,219,0.12);
  border: 1px solid rgba(117,170,219,0.35);
  color: #75AADB;
}
.wt-cta-save:hover {
  background: rgba(117,170,219,0.20);
  transform: translateY(-2px);
}
.wt-cta-follow {
  background: linear-gradient(135deg, #D4AF37, #F5CB5C);
  color: #070b12;
}
.wt-cta-follow:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(212,175,55,0.35);
}

/* Footer branding */
.wt-profile-footer {
  font-family: 'Space Mono', monospace;
  font-size: 10px;
  color: rgba(255,255,255,0.25);
  letter-spacing: 1px;
  text-align: center;
  margin-top: 4px;
}
.wt-footer-brand {
  color: #75AADB;
  font-weight: bold;
}
```

### JavaScript del perfil WT

```javascript
// ─── World Talents Profile — Diego ───
function wtToggleRole(btn) {
  const body = btn.nextElementSibling;
  const isOpen = btn.classList.contains('wt-role-open');
  // Cerrar todos
  document.querySelectorAll('.wt-role-btn').forEach(b => b.classList.remove('wt-role-open'));
  document.querySelectorAll('.wt-role-body').forEach(b => b.classList.remove('wt-role-open'));
  // Abrir el clickeado si estaba cerrado
  if (!isOpen) {
    btn.classList.add('wt-role-open');
    body.classList.add('wt-role-open');
  }
}

function wtSaveContact() {
  // Generar vCard de Diego (datos públicos/conmemorativos)
  const vcard = `BEGIN:VCARD
VERSION:3.0
FN:Diego Armando Maradona
NICKNAME:D10S
ORG:Selección Argentina;Napoli
TITLE:Campeón del Mundo 1986
URL:https://instagram.com/maradona
NOTE:1960-2020. La pelota no se mancha.
END:VCARD`;
  const blob = new Blob([vcard], { type: 'text/vcard' });
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = 'diego-maradona.vcf';
  a.click();
  URL.revokeObjectURL(url);
}

function wtFollowDiego() {
  // Redirige al Instagram oficial gestionado por herederos
  window.open('https://instagram.com/maradona', '_blank', 'noopener,noreferrer');
}
```

---

## Tarea 4: Botonera Marcas Maradona (estilo Linktree)

### Posición
Va DESPUÉS de `#sala-voz` (chat V1), ANTES del `#footer`.

### Paleta de la botonera
```css
--btn-bg:       rgba(255,255,255,0.04);
--btn-border:   rgba(212,175,55,0.20);
--btn-hover-bg: rgba(212,175,55,0.08);
--btn-hover-bd: rgba(212,175,55,0.50);
--cat-color:    #D4AF37;      /* dorado para labels de categoría */
--cat-celeste:  #75AADB;     /* celeste para badges */
```

### HTML completo de la botonera

```html
<!-- ═══════════════════════════════════════════════
     BOTONERA MARCAS MARADONA — ESTILO LINKTREE
     ═══════════════════════════════════════════════ -->
<section id="marcas-diego" class="marcas-section">
  <div class="marcas-inner">

    <!-- Header -->
    <div class="marcas-header">
      <span class="marcas-tag">UNIVERSO D10S</span>
      <h2 class="marcas-title">EL LEGADO DE <span class="gold">DIEGO</span></h2>
      <p class="marcas-subtitle">Todas las marcas, experiencias y proyectos de la familia Maradona</p>
    </div>

    <!-- CATEGORÍA 1: TIENDA OFICIAL -->
    <div class="marcas-cat-label">🛍️ TIENDA OFICIAL</div>
    <div class="marcas-grid">
      <a class="marcas-btn" href="https://themaradonastore.com" target="_blank" rel="noopener">
        <span class="marcas-btn-icon">🏪</span>
        <div class="marcas-btn-info">
          <span class="marcas-btn-name">The Maradona Store</span>
          <span class="marcas-btn-desc">Tienda oficial D10S — ropa, accesorios y colecciones</span>
        </div>
        <span class="marcas-btn-arrow">›</span>
      </a>
      <a class="marcas-btn" href="https://commafootball.com" target="_blank" rel="noopener">
        <span class="marcas-btn-icon">⚡</span>
        <div class="marcas-btn-info">
          <span class="marcas-btn-name">Comma × Maradona 2026</span>
          <span class="marcas-btn-desc">Colección oficial 2026 — autorizada por los herederos</span>
        </div>
        <span class="marcas-btn-badge marcas-badge-new">NUEVO</span>
        <span class="marcas-btn-arrow">›</span>
      </a>
    </div>

    <!-- CATEGORÍA 2: INDUMENTARIA RETRO -->
    <div class="marcas-cat-label">👕 INDUMENTARIA</div>
    <div class="marcas-grid">
      <a class="marcas-btn" href="https://copafootball.com/en-us/collections/maradona" target="_blank" rel="noopener">
        <span class="marcas-btn-icon">🎽</span>
        <div class="marcas-btn-info">
          <span class="marcas-btn-name">COPA Football × Maradona</span>
          <span class="marcas-btn-desc">Camisetas retro oficiales — Boca 81, Argentina 86, Napoli 87</span>
        </div>
        <span class="marcas-btn-arrow">›</span>
      </a>
      <a class="marcas-btn" href="https://rootsoffight.com/collections/diego-maradona" target="_blank" rel="noopener">
        <span class="marcas-btn-icon">🥊</span>
        <div class="marcas-btn-info">
          <span class="marcas-btn-name">Roots of Fight</span>
          <span class="marcas-btn-desc">Colección lifestyle — hoodies, tees y accesorios</span>
        </div>
        <span class="marcas-btn-arrow">›</span>
      </a>
    </div>

    <!-- CATEGORÍA 3: MUSEOS Y EXPERIENCIAS -->
    <div class="marcas-cat-label">🏛️ MUSEOS & EXPERIENCIAS</div>
    <div class="marcas-grid">
      <a class="marcas-btn" href="https://museomaradona.com" target="_blank" rel="noopener">
        <span class="marcas-btn-icon">🇮🇹</span>
        <div class="marcas-btn-info">
          <span class="marcas-btn-name">Museo Maradona — Nápoles</span>
          <span class="marcas-btn-desc">Collezione Vignati · 100+ piezas auténticas de Diego</span>
        </div>
        <span class="marcas-btn-arrow">›</span>
      </a>
      <a class="marcas-btn" href="https://lacasaded10s.com" target="_blank" rel="noopener">
        <span class="marcas-btn-icon">🏠</span>
        <div class="marcas-btn-info">
          <span class="marcas-btn-name">La Casa de D10S — Buenos Aires</span>
          <span class="marcas-btn-desc">Lascano 2257, La Paternal · Museo en su primer hogar</span>
        </div>
        <span class="marcas-btn-arrow">›</span>
      </a>
      <a class="marcas-btn" href="https://m10memorial.com" target="_blank" rel="noopener">
        <span class="marcas-btn-icon">🕊️</span>
        <div class="marcas-btn-info">
          <span class="marcas-btn-name">M10 Memorial</span>
          <span class="marcas-btn-desc">El mausoleo y espacio de legado — Huergo 10, Buenos Aires</span>
        </div>
        <span class="marcas-btn-badge marcas-badge-soon">PRÓXIMO</span>
        <span class="marcas-btn-arrow">›</span>
      </a>
    </div>

    <!-- CATEGORÍA 4: GASTRONOMÍA -->
    <div class="marcas-cat-label">🍝 GASTRONOMÍA</div>
    <div class="marcas-grid">
      <a class="marcas-btn" href="https://instagram.com/maradona.10.restaurante" target="_blank" rel="noopener">
        <span class="marcas-btn-icon">🍕</span>
        <div class="marcas-btn-info">
          <span class="marcas-btn-name">Restaurante Maradona (10)</span>
          <span class="marcas-btn-desc">Belgrano, Buenos Aires · Horno napolitano + murales del Diego</span>
        </div>
        <span class="marcas-btn-arrow">›</span>
      </a>
      <a class="marcas-btn" href="https://pastamaradona.it" target="_blank" rel="noopener">
        <span class="marcas-btn-icon">🇮🇹</span>
        <div class="marcas-btn-info">
          <span class="marcas-btn-name">Pasta Maradona N.10 Diego</span>
          <span class="marcas-btn-desc">Pastificio Paone · Último negocio firmado por Diego</span>
        </div>
        <span class="marcas-btn-arrow">›</span>
      </a>
    </div>

    <!-- CATEGORÍA 5: STREAMING -->
    <div class="marcas-cat-label">🎬 DOCUMENTALES Y SERIES</div>
    <div class="marcas-grid">
      <a class="marcas-btn" href="https://www.primevideo.com/search?phrase=sueño+bendito" target="_blank" rel="noopener">
        <span class="marcas-btn-icon">📺</span>
        <div class="marcas-btn-info">
          <span class="marcas-btn-name">Sueño Bendito — Amazon Prime</span>
          <span class="marcas-btn-desc">Serie biográfica oficial · 10 episodios</span>
        </div>
        <span class="marcas-btn-arrow">›</span>
      </a>
      <a class="marcas-btn" href="https://www.max.com" target="_blank" rel="noopener">
        <span class="marcas-btn-icon">🎥</span>
        <div class="marcas-btn-info">
          <span class="marcas-btn-name">Diego Maradona (Kapadia) — HBO Max</span>
          <span class="marcas-btn-desc">Documental de Asif Kapadia · 90% en Rotten Tomatoes</span>
        </div>
        <span class="marcas-btn-arrow">›</span>
      </a>
      <a class="marcas-btn" href="https://www.netflix.com/search?q=maradona" target="_blank" rel="noopener">
        <span class="marcas-btn-icon">🎬</span>
        <div class="marcas-btn-info">
          <span class="marcas-btn-name">Maradona in Mexico — Netflix</span>
          <span class="marcas-btn-desc">Serie documental · Su etapa como DT en México</span>
        </div>
        <span class="marcas-btn-arrow">›</span>
      </a>
    </div>

    <!-- CATEGORÍA 6: GAMING -->
    <div class="marcas-cat-label">🎮 GAMING</div>
    <div class="marcas-grid">
      <a class="marcas-btn" href="https://www.ea.com/games/ea-sports-fc" target="_blank" rel="noopener">
        <span class="marcas-btn-icon">⚽</span>
        <div class="marcas-btn-info">
          <span class="marcas-btn-name">EA Sports FC 25/26 — ICON</span>
          <span class="marcas-btn-desc">Maradona volvió al juego en 2025 como ICON legendario</span>
        </div>
        <span class="marcas-btn-arrow">›</span>
      </a>
      <a class="marcas-btn" href="https://efootball.com" target="_blank" rel="noopener">
        <span class="marcas-btn-icon">🕹️</span>
        <div class="marcas-btn-info">
          <span class="marcas-btn-name">eFootball — Legend</span>
          <span class="marcas-btn-desc">Konami · Classic No.10 y National Legend sin interrupciones</span>
        </div>
        <span class="marcas-btn-arrow">›</span>
      </a>
    </div>

    <!-- CATEGORÍA 7: FAMILIA -->
    <div class="marcas-cat-label">❤️ FAMILIA MARADONA</div>
    <div class="marcas-grid">
      <a class="marcas-btn" href="https://fundacionmaradona.org" target="_blank" rel="noopener">
        <span class="marcas-btn-icon">🏛️</span>
        <div class="marcas-btn-info">
          <span class="marcas-btn-name">Fundación Maradona</span>
          <span class="marcas-btn-desc">Presidida por Dalma · Relanzada noviembre 2024</span>
        </div>
        <span class="marcas-btn-arrow">›</span>
      </a>
      <a class="marcas-btn" href="https://instagram.com/maradonaheirs" target="_blank" rel="noopener">
        <span class="marcas-btn-icon">👨‍👩‍👧‍👦</span>
        <div class="marcas-btn-info">
          <span class="marcas-btn-name">Herederos Maradona</span>
          <span class="marcas-btn-desc">@maradonaheirs · Instagram oficial de los 5 hijos</span>
        </div>
        <span class="marcas-btn-arrow">›</span>
      </a>
    </div>

    <!-- CATEGORÍA 8: REDES OFICIALES -->
    <div class="marcas-cat-label">📱 REDES OFICIALES DEL DIEGO</div>
    <div class="marcas-social-grid">
      <a class="marcas-social-item" href="https://instagram.com/maradona" target="_blank" rel="noopener">
        <div class="marcas-social-icon marcas-ig">
          <svg width="22" height="22" viewBox="0 0 24 24" fill="currentColor">
            <rect x="2" y="2" width="20" height="20" rx="5"/>
            <circle cx="12" cy="12" r="5" fill="none" stroke="currentColor" stroke-width="1.5"/>
            <circle cx="17.5" cy="6.5" r="1.2"/>
          </svg>
        </div>
        <span class="marcas-social-name">@maradona</span>
        <span class="marcas-social-count">8M+</span>
      </a>
      <a class="marcas-social-item" href="https://facebook.com/diegomaradona" target="_blank" rel="noopener">
        <div class="marcas-social-icon marcas-fb">
          <svg width="22" height="22" viewBox="0 0 24 24" fill="currentColor">
            <path d="M18 2h-3a5 5 0 00-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 011-1h3z"/>
          </svg>
        </div>
        <span class="marcas-social-name">Diego Maradona</span>
        <span class="marcas-social-count">12M+</span>
      </a>
      <a class="marcas-social-item" href="https://twitter.com/DiegoAMaradona" target="_blank" rel="noopener">
        <div class="marcas-social-icon marcas-tw">
          <svg width="22" height="22" viewBox="0 0 24 24" fill="currentColor">
            <path d="M23 3a10.9 10.9 0 01-3.14 1.53 4.48 4.48 0 00-7.86 3v1A10.66 10.66 0 013 4s-4 9 5 13a11.64 11.64 0 01-7 2c9 5 20 0 20-11.5a4.5 4.5 0 00-.08-.83A7.72 7.72 0 0023 3z"/>
          </svg>
        </div>
        <span class="marcas-social-name">@DiegoAMaradona</span>
        <span class="marcas-social-count">161K</span>
      </a>
    </div>

    <!-- Footer marcas -->
    <div class="marcas-footer">
      <p>Información basada en marcas y proyectos oficiales verificados · Abril 2026</p>
      <p>Derechos gestionados por los herederos vía <strong>Electa Global</strong></p>
    </div>

  </div>
</section>
```

### CSS de la botonera

```css
/* ═══════════════════════════════════════════════
   BOTONERA MARCAS MARADONA
   ═══════════════════════════════════════════════ */
#marcas-diego {
  background: linear-gradient(180deg, var(--dark) 0%, #0A0E1A 50%, var(--dark) 100%);
  padding: clamp(60px, 8vh, 100px) clamp(20px, 5vw, 60px);
}
.marcas-inner {
  max-width: 680px;
  margin: 0 auto;
}
.marcas-header {
  text-align: center;
  margin-bottom: 48px;
}
.marcas-tag {
  display: inline-block;
  font-family: 'Space Mono', monospace;
  font-size: 10px;
  letter-spacing: 3px;
  color: #75AADB;
  border: 1px solid rgba(117,170,219,0.3);
  border-radius: 20px;
  padding: 5px 14px;
  margin-bottom: 14px;
}
.marcas-title {
  font-family: var(--font-display);
  font-size: clamp(2rem, 5vw, 3.5rem);
  color: var(--white);
  letter-spacing: 0.12em;
  text-transform: uppercase;
  margin-bottom: 10px;
}
.marcas-subtitle {
  font-family: var(--font-body);
  font-size: 0.95rem;
  color: var(--white-dim);
  font-style: italic;
  line-height: 1.5;
}

/* Label de categoría */
.marcas-cat-label {
  font-family: 'Space Mono', monospace;
  font-size: 10px;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: #D4AF37;
  margin: 28px 0 10px;
  padding-left: 4px;
  border-left: 2px solid #D4AF37;
  padding-left: 10px;
}

/* Grid de botones */
.marcas-grid {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

/* Botón individual */
.marcas-btn {
  display: flex;
  align-items: center;
  gap: 14px;
  padding: 16px 18px;
  background: rgba(255,255,255,0.03);
  border: 1px solid rgba(212,175,55,0.15);
  border-radius: 14px;
  text-decoration: none;
  color: var(--white);
  transition: all 0.25s ease;
  position: relative;
  overflow: hidden;
}
.marcas-btn::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(90deg, rgba(212,175,55,0.04) 0%, transparent 100%);
  opacity: 0;
  transition: opacity 0.25s;
}
.marcas-btn:hover {
  background: rgba(212,175,55,0.07);
  border-color: rgba(212,175,55,0.40);
  transform: translateX(4px);
}
.marcas-btn:hover::before { opacity: 1; }

.marcas-btn-icon {
  font-size: 22px;
  min-width: 32px;
  text-align: center;
}
.marcas-btn-info {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 3px;
}
.marcas-btn-name {
  font-family: 'Bebas Neue', sans-serif;
  font-size: 16px;
  color: var(--white);
  letter-spacing: 0.5px;
  line-height: 1;
}
.marcas-btn-desc {
  font-family: 'Inter', sans-serif;
  font-size: 11.5px;
  color: var(--white-dim);
  line-height: 1.4;
}
.marcas-btn-arrow {
  font-size: 20px;
  color: rgba(212,175,55,0.5);
  line-height: 1;
  transition: transform 0.2s;
}
.marcas-btn:hover .marcas-btn-arrow { transform: translateX(3px); color: #D4AF37; }

/* Badges */
.marcas-btn-badge {
  font-family: 'Space Mono', monospace;
  font-size: 9px;
  letter-spacing: 1px;
  padding: 3px 8px;
  border-radius: 20px;
  font-weight: bold;
}
.marcas-badge-new {
  background: rgba(16,185,129,0.15);
  color: #10b981;
  border: 1px solid rgba(16,185,129,0.3);
}
.marcas-badge-soon {
  background: rgba(117,170,219,0.12);
  color: #75AADB;
  border: 1px solid rgba(117,170,219,0.3);
}

/* Social grid */
.marcas-social-grid {
  display: flex;
  gap: 10px;
  flex-wrap: wrap;
}
.marcas-social-item {
  flex: 1;
  min-width: 140px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
  padding: 18px 12px;
  background: rgba(255,255,255,0.03);
  border: 1px solid rgba(255,255,255,0.08);
  border-radius: 14px;
  text-decoration: none;
  color: var(--white);
  transition: all 0.25s ease;
}
.marcas-social-item:hover {
  transform: translateY(-3px);
  box-shadow: 0 8px 24px rgba(0,0,0,0.3);
}
.marcas-social-icon {
  width: 46px; height: 46px;
  border-radius: 14px;
  display: flex; align-items: center; justify-content: center;
}
.marcas-ig  { background: rgba(228,64,95,.15);  color: #E4405F; }
.marcas-fb  { background: rgba(24,119,242,.12); color: #1877F2; }
.marcas-tw  { background: rgba(29,161,242,.12); color: #1DA1F2; }
.marcas-social-name {
  font-family: 'Bebas Neue', sans-serif;
  font-size: 14px;
  letter-spacing: 0.5px;
  text-align: center;
}
.marcas-social-count {
  font-family: 'Space Mono', monospace;
  font-size: 11px;
  color: #D4AF37;
}

/* Footer marcas */
.marcas-footer {
  margin-top: 40px;
  text-align: center;
  padding-top: 24px;
  border-top: 1px solid rgba(212,175,55,0.1);
}
.marcas-footer p {
  font-family: 'Space Mono', monospace;
  font-size: 10px;
  color: var(--white-dim);
  letter-spacing: 1px;
  line-height: 1.8;
}
.marcas-footer strong { color: #75AADB; }

@media (max-width: 480px) {
  .marcas-social-grid { flex-direction: column; }
  .marcas-social-item { flex-direction: row; min-width: unset; }
}
```

---

## Orden de implementación en el archivo HTML

1. **Agregar las variables CSS** del perfil WT y la botonera en el bloque `<style>` existente
2. **Mover el `#hero`** de `tab-maradona` a `tab-maradoniano` (antes del `#museoNav`)
3. **Eliminar `#sala-voz-v2`** y todo su CSS/JS relacionado
4. **Insertar `#wt-profile-diego`** al inicio de `tab-maradona` (primer child)
5. **Insertar `#marcas-diego`** después de `#sala-voz` y antes del `#footer`
6. **Agregar las funciones JS** `wtToggleRole`, `wtSaveContact`, `wtFollowDiego` en el bloque `<script>`

## Notas importantes

- El HTML es un único archivo monolítico — todos los cambios van en el mismo archivo
- Las fuentes (`Bebas Neue`, `Space Mono`, `Inter`, `Lora`) ya están cargadas via Google Fonts en el `<head>`
- La clase `.gold` ya está definida en el CSS existente — úsarla para texto dorado
- El scroll indicator del hero movido debe apuntar a `#sala-fiorito`, no a `#sala-voz`
- El perfil WT del Diego NO usa React — es HTML/CSS/JS puro como el resto de la página
- Las funciones JS del perfil WT se agregan al bloque `<script>` existente al final del body
