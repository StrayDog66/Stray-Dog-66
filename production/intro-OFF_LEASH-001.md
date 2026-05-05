# OFF LEASH · INTRO · EPISODIO 001
## Production Brief · v1.0

> **Decisiones aprobadas:**
> · Show: OFF LEASH · Idioma voz: ESPAÑOL · Voz: robótica/sintética distorsionada · Ladrido signature: SÍ
> Duración objetivo: 30 segundos · BPM: 138 · Key: F# minor · Loudness target: -14 LUFS integrated

---

## 1 · CREATIVE BRIEF

**Propósito:** Sello sonoro recurrente que abre cada episodio de OFF LEASH. La meta es que el oyente, después de 5-6 episodios, reconozca los primeros 3 segundos sin ver el título.

**Principios:**
1. La intro es **idéntica todas las semanas**. Solo cambia el número de episodio.
2. **Brand-locked:** menciona "Stray Dog", "Off Leash" y la triada "Sin correa. Sin dueño. Sin piedad."
3. **Coherente con la estética del sitio:** brutalista, oscuro, industrial.
4. La intro debe **funcionar a bajo volumen** (alguien escuchando en el auto o el gym a las 8am).

**Anti-patterns (lo que NO va):**
- Voz inglés con acento neutro (suena genérico, EDM)
- Música melodic / synth lead / future house
- Frases largas o explicativas
- Risas, FX cómicos, "drop bait" tipo TikTok

---

## 2 · SCRIPT DE LA VOZ (ES)

**Versión final · 22 segundos hablados:**

```
[ambient drone 4s]

VOZ:  "Pilar, Paraguay."
      [pausa 0.3s]
      "Ciudad de Panamá."
      [pausa 0.5s]

[kick 909 entra · 4s]

VOZ:  "Stray Dog."
      [pausa 0.5s]
      "Esto es Off Leash."
      [pausa 0.8s]
      "Episodio cero uno."
      [pausa 1s]

[build 6s]

VOZ:  "Sin correa."
      [pausa 0.4s]
      "Sin dueño."
      [pausa 0.4s]
      "Sin piedad."
      [pausa 0.3s]

[DROP · ladrido procesado · 4s]
[transición al primer track]
```

**Total con música y silencios:** ~30 segundos.

**Nota de dirección de actuación (para el TTS):**
- Sin emoción de marketing radial
- Tono grave, pausado, declarativo
- Cero interrogación ni énfasis ascendente
- Como si estuviera leyendo en voz baja un manifiesto, no presentando un programa

---

## 3 · SUNO · PROMPT PARA EL BED MUSICAL

Pegá esto exacto en https://suno.com/create (modo Custom):

**Style of Music:**
```
dark industrial hard techno intro, warehouse atmosphere, dystopian,
TR-909 distorted kick, sub bass F# minor, metallic riser,
pitched-down siren, vinyl crackle, no melody, no lead synth,
no vocals, cinematic build, late-night Berlin warehouse,
references: Surgeon, Regis, Ansome, Birmingham techno,
138 BPM, F# minor key
```

**Title:**
```
OFF LEASH 001 INTRO BED
```

**Lyrics:** dejarlo en blanco · marcar `Instrumental: ON`

**Settings:**
- Model: v4 o v4.5
- Length: 30 segundos (si Suno genera más, recortar después)
- Generar 4-6 variantes y elegir la mejor

**Criterio de selección entre las 4-6 variantes:**
- ✓ Kick distorsionado audible desde segundo 4-5
- ✓ Sub bass continuo en F# (no melodías)
- ✓ Build evidente entre segundo 18-25
- ✓ Espacio limpio en el medio (300-3000 Hz) para que entre la voz
- ✗ Descartar si tiene synth lead melódico o coro
- ✗ Descartar si suena "EDM" / future bass / progressive

**Backup si Suno no convence:** Udio con el mismo prompt o Stable Audio 2.0.

---

## 4 · ELEVENLABS · CONFIGURACIÓN DE LA VOZ

URL: https://elevenlabs.io/app/speech-synthesis

**Voz recomendada (free tier):**
| Voice ID | Nombre | Por qué |
|---|---|---|
| `pNInz6obpgDQGcFmaJgB` | **Adam** (multilingual v2) | Grave, neutral, soporta español bien |
| `TxGEqnHWrfWFTfGW9XjX` | **Josh** | Más oscuro, ideal para tono manifiesto |
| `2EiwWnXFnvU5JabPnv8n` | **Clyde** | Más maduro, autoridad |

Mi pick: **Adam** con multilingual v2.

**Settings (importante):**
```
Model:           Eleven Multilingual v2
Stability:       0.35     ← bajo = más variación dramática
Similarity:      0.80     ← alto = consistencia entre takes
Style exaggeration: 0.20  ← bajo = sin teatralidad
Speaker boost:   ON
```

**Cómo escribir el script en el textarea (con marcas de pausa SSML-light):**

```
Pilar, Paraguay. <break time="0.3s" /> Ciudad de Panamá. <break time="0.5s" />

Stray Dog. <break time="0.5s" /> Esto es Off Leash. <break time="0.8s" /> Episodio cero uno. <break time="1s" />

Sin correa. <break time="0.4s" /> Sin dueño. <break time="0.4s" /> Sin piedad.
```

**Generar 3 takes** y elegir el que tenga mejor tono grave y menos respiración audible.

**Export:** MP3 192kbps mínimo (44.1 kHz). Si tu plan permite, WAV.

---

## 5 · FX CHAIN · PROCESAMIENTO DE LA VOZ

Este es el secreto. El TTS sale "limpio" y nosotros lo convertimos en **voz robótica de pirata radio**.

**Cadena en orden (Audacity tiene todos estos plugins gratis):**

```
INPUT: voz_eleven.wav
      │
      ├─ 1. HIGH-PASS FILTER  · 80 Hz (corta el rumble)
      │
      ├─ 2. EQ subtractive    · -3 dB en 250-400 Hz (sacar boomy)
      │                       · +2 dB en 2-4 kHz (presencia)
      │                       · -6 dB en 8 kHz+ (corta sibilancia)
      │
      ├─ 3. COMPRESOR         · threshold -18 dB · ratio 4:1
      │                       · attack 5ms · release 80ms
      │
      ├─ 4. BITCRUSHER        · sample rate: 16 kHz
      │                       · bit depth: 12 bit
      │                       · mix wet: 35%   ← clave del color "robótico"
      │
      ├─ 5. TAPE SATURATION   · drive 25% (Audacity: "Distortion: Soft Clipping")
      │                       · agrega calidez analógica + grit
      │
      ├─ 6. SLAP DELAY        · 1/8 dotted (~163ms a 138 BPM)
      │                       · feedback 25% · mix 18%
      │                       · pan ligero L/R alternado
      │
      ├─ 7. PLATE REVERB      · decay 1.8s · pre-delay 30ms
      │                       · damping 50% · mix 22%
      │
      └─ 8. STEREO WIDENING   · 110-115% (NO MÁS o pierde mono compatibility)

OUTPUT: voz_processed.wav
```

**Reglas de oro:**
- Solo procesar la VOZ. NO aplicar a la música ni al ladrido (ya tienen su carácter).
- Después de procesar, normalizar pico a -3 dB para tener headroom.
- Si la voz "pelea" con el kick, automatizar un duck de -3 dB en la voz cuando entra el kick.

---

## 6 · LADRIDO · SAMPLE LIBRARY GRATUITA

**Opción A · Freesound.org (recomendada · gratis · CC0):**

Buscar: `dog bark deep aggressive`
URL: https://freesound.org/search/?q=dog+bark+deep&f=license:%22Creative+Commons+0%22

**Picks específicos (testeados):**
- `Dog_Bark_Loud.wav` por user `acclivity` — 0.7s, brutal
- `pitbull-bark.wav` por user `Jaggy` — 1.2s, grave
- `german-shepherd.wav` por user `markedit` — 0.9s, agresivo

**Opción B · Tu propio perro (si tenés acceso):**
- Grabar con celular en habitación silenciosa
- Provocar 5-10 ladridos con saludo o jugando
- Elegir el más limpio (sin ruido de fondo)
- Procesar en Audacity (limpieza con Adobe Podcast Enhance gratis)

**Procesamiento del ladrido (FX chain corta):**

```
1. HIGH-PASS    · 100 Hz
2. PITCH SHIFT  · -3 semitones (lo hace más grave / amenazante)
3. BITCRUSHER   · 14 bit · mix 50%
4. REVERB       · plate 2.5s · mix 35%
5. DELAY        · 1/4 note feedback 40% (le da el "reverb largo industrial")
```

El ladrido va al final, sobre el drop, panneado al centro pero con stereo width grande.

---

## 7 · AUDACITY · TUTORIAL DE MEZCLA (PASO A PASO)

Audacity gratis: https://www.audacityteam.org/

**Setup inicial:**
- Project rate: **48000 Hz**
- Default sample format: **32-bit float**
- Tracks → New Track → Mono x4

**Pista 1 · BED MUSICAL (de Suno):**
1. File → Import → Audio → seleccionar `bed_musical.mp3`
2. Si dura más de 30s, usar Effect → Truncate Silence o cortar manual
3. Volumen: -3 dB (leave headroom)

**Pista 2 · VOZ (de ElevenLabs ya procesada con FX chain):**
1. Importar `voz_processed.wav`
2. Posicionar el primer "Pilar, Paraguay." en el segundo **4.0**
3. Volumen: 0 dB (ducked -3dB cuando entra el kick — ver paso 4)

**Pista 3 · LADRIDO (procesado):**
1. Importar `bark_processed.wav`
2. Posicionar exactamente en segundo **25.5** (justo antes del drop)
3. Volumen: -2 dB

**Pista 4 · NOISE TEXTURE (opcional pero recomendada):**
1. Generate → Noise → White Noise · 30s · amplitude 0.3
2. Effect → High-pass · 4000 Hz
3. Effect → Amplify · -28 dB
4. Le da "vinyl hiss" continuo de fondo

**Step 4 · Automatización de volumen (envelope):**
- Click en la pista de voz → Envelope Tool (icono de campana)
- Crear automation que baje -3dB cuando entra el kick (segundo 8) y vuelva a 0 cuando para
- Esto hace que la voz "respire" con la música en lugar de pelear

**Step 5 · Master bus (sobre todo):**
- Effect → Compressor: threshold -12 dB · ratio 2.5:1 (gluing)
- Effect → Limiter: -1 dB ceiling, threshold -6 dB
- Verificar peak meter no pase de -1 dB

**Step 6 · Export:**
- File → Export → Export as WAV · 48 kHz · 24 bit · `OFF_LEASH_001_intro_master.wav`
- File → Export → Export as MP3 · 320 kbps · `OFF_LEASH_001_intro.mp3`

---

## 8 · VARIANTES A/B (RECOMENDADAS PARA TESTEAR)

**Variante A · "DRY"**  · más al frente
- Reverb voz: 12% (en vez de 22%)
- Slap delay: 8% (en vez de 18%)
- Voz suena más cercana, "al oído"

**Variante B · "WET"**  · cinematográfica
- Reverb voz: 35% (en vez de 22%)
- Plate más larga: 2.5s
- Add: granular reverb tail post-último "piedad"
- Voz suena en un warehouse vacío

**Cómo decidir cuál usar:**
Mostrale las dos a 5 personas distintas (no DJs). Preguntá "¿cuál te dan más ganas de seguir escuchando?". La que gane 3+ es la oficial.

---

## 9 · EXPORT · DELIVERABLES

Al final del proceso, debés tener estos 4 archivos:

```
production/
└── intro-OFF_LEASH-001/
    ├── OFF_LEASH_001_intro_master.wav    ← 48k/24bit · archivo madre
    ├── OFF_LEASH_001_intro.mp3           ← 320 kbps · para SoundCloud
    ├── OFF_LEASH_001_intro_vox_only.wav  ← solo voz procesada · útil para variantes futuras
    └── OFF_LEASH_001_intro_no_vox.wav    ← solo música + ladrido · útil para shows en vivo
```

**Loudness check final (importante para SoundCloud / Spotify):**
- Subir el MP3 a https://www.loudness.app/ (gratis)
- Verificar Integrated LUFS entre **-14 y -12**
- Si está más fuerte (-9), bajar el master bus -2dB y re-exportar
- Si está más bajo (-18), subir +3dB y re-exportar

---

## 10 · CHECKLIST FINAL ANTES DE PUBLICAR

```
[ ] Bed musical generado en Suno (4-6 variantes, elegida la mejor)
[ ] Voz generada en ElevenLabs (3 takes, elegido el mejor)
[ ] FX chain aplicada a la voz en Audacity
[ ] Ladrido seleccionado y procesado
[ ] Mezcla en Audacity (4 pistas alineadas)
[ ] Automation de volumen aplicada
[ ] Master bus con compressor + limiter
[ ] Loudness check: -14 LUFS integrated
[ ] Export WAV master + MP3 320
[ ] Variante A vs B testeada con 5 personas
[ ] Subir a SoundCloud como "OFF LEASH · INTRO TAG"
[ ] Guardar el .aup3 (proyecto Audacity) para futuros episodios
[ ] Para episodio 002: solo regenerar voz cambiando "cero uno" por "cero dos"
```

---

## 11 · TIMELINE REALISTA

| Tarea | Tiempo |
|---|---|
| Generar bed en Suno (4-6 intentos) | 25-40 min |
| Voz en ElevenLabs (3 takes + comparación) | 15 min |
| FX chain a la voz en Audacity | 25 min |
| Conseguir y procesar ladrido | 15 min |
| Mezcla principal | 30 min |
| Mastering + loudness | 20 min |
| Exports | 10 min |
| **TOTAL primer intro** | **~2.5 horas** |
| Episodio 002 (solo cambia "uno"→"dos") | **~10 minutos** |

La inversión grande es la primera. Las siguientes 50 intros son gratis.

---

## 12 · NEXT STEPS POST-INTRO

Una vez tengas la intro lista:

1. **Subila a SoundCloud** como track separado: `OFF LEASH · INTRO TAG · 0:30`
   - Sirve para que otros DJs/shows puedan usarla con permiso
   - SoundCloud la indexa: cuando alguien busca "Stray Dog" la encuentra

2. **Compactala como sample en tu DAW** para usar como cierre de sets en vivo

3. **Versión THE GROWLER** (calmada, dub) usando este mismo brief con cambios:
   - Bed musical: Suno prompt cambia a `dub techno, deep, atmospheric, 110 BPM, A minor`
   - Sin ladrido (no encaja con tono pausado)
   - Voz con MENOS bitcrush, MÁS reverb largo

4. **Versión 5-segundos** (para reels IG/TikTok):
   - Solo "Stray Dog · Off Leash" + ladrido
   - Sin bed musical largo
   - Para usar como tag en clips

5. **Sting de transición** (3 segundos):
   - Solo el ladrido procesado + sub drop
   - Para meter entre tracks dentro del set

---

## 13 · CONTACTO PRODUCCIÓN

Si en cualquier paso necesitás ajuste de mezcla, balanceo de frecuencias o prompt alternativo, volvé al chat con:
- El archivo `.wav` en cuestión (subido a un drive con link)
- Tu duda específica (ej: "la voz se pelea con el kick en el segundo 12")
- Yo te doy el ajuste exacto

---

**EST. 2026 · 66 RECORDS · STRAY DOG**
**SIN CORREA · SIN DUEÑO · SIN PIEDAD**
