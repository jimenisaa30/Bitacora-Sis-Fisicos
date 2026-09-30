const { visualid } = createParams('visualid')

setcps(119/60/4)

// ── Voicings de mano derecha ──
const D9    = '[f#4,a4,c5,e5]'
const E9    = '[g#4,b4,d5,f#5]'
const Em9   = '[g4,b4,d5,f#5]'
const A9    = '[g4,b4,c#5,e5]'
const E11D  = '[g#4,a4,b4,d5]'      
const A13   = '[g4,c#5,e5,f#5]'
const Dmaj9 = '[f#4,a4,c#5,e5]'
const A11   = '[g4,c#5,d5,e5]'
const Dtri  = '[d4,f#4,a4]'

// Une eventos en un compás: R('a@3','b@3','c@2') → '[a@3 b@3 c@2]'
const R = (...partes) => '[' + partes.join(' ') + ']'

// ── Mano izquierda: [raíz+quinta]@2, quinta, octava, octava, quinta, raíz@2 ──
const lh = (r, f, o) => R('[' + r + ',' + f + ']@2', f, o, o, f, r + '@2')

const bajo = '<' + [
  lh('d2','a2','d3'),  // 1  D9
  lh('d2','a2','d3'),  // 2  D9
  lh('e2','b2','e3'),  // 3  E9
  lh('e2','b2','e3'),  // 4  E9
  lh('e2','b2','e3'),  // 5  Em9
  lh('a1','e2','a2'),  // 6  A9
  lh('d2','a2','d3'),  // 7  E11/D
  lh('a1','e2','a2'),  // 8  A13
  lh('d2','a2','d3'),  // 9  Dmaj9
  lh('a1','e2','a2'),  // 10 A11
  lh('e2','b2','e3'),  // 11 E9
  lh('e2','b2','e3'),  // 12 E9
  lh('e2','b2','e3'),  // 13 Em9
  lh('a1','e2','a2'),  // 14 A9
].join(' ') + '>'

// ── Mano derecha (@n = duración en corcheas, 8 por compás) ──
const c4 = R('g#4@3','~','b4','a4','g#4','[d4,g#4]')       // compases 4 y 12
const c5 = R(Em9+'@2','b4','g4',Em9+'@2','f#5@2')          // compases 5 y 13
const c6 = R(A9+'@2','b4','g4',A9+'@2','e5@2')             // compases 6 y 14

const armonia = '<' + [
  R(D9+'@3', D9+'@3', 'f#4@2'),                     // 1  D9
  R(Dtri+'@4','a4','d5',Dtri+'@2'),                 // 2  D9
  R(E9+'@3', E9+'@2','b4','~','g#4'),               // 3  E9
  c4,                                               // 4  E9
  c5,                                               // 5  Em9
  c6,                                               // 6  A9
  R(E11D+'@3', E11D+'@2','~@3'),                    // 7  E11/D
  R(A13+'@3', A13+'@3','g4@2'),                     // 8  A13
  R(Dmaj9+'@3','a4','f#4','a4',Dmaj9+'@2'),         // 9  Dmaj9
  R('~@4','a4','d5',A11+'@2'),                      // 10 A11
  R(E9+'@3', E9+'@2','~','~','b4'),                 // 11 E9
  c4,                                               // 12 E9
  c5,                                               // 13 Em9
  c6,                                               // 14 A9
].join(' ') + '>'

// ── Dinámica: mf en los compases 1–13, mp en el 14 ──
const vel = '<0.7!13 0.55>'

// mini(...) convierte las cadenas armadas con JS en patrones
stack(
  // Bloque 1: mano derecha
  note(mini(armonia)).gain(mini(vel))
    .s('triangle').visualid("harmony")
    .attack(0.005)
    .decay(0.4)
    .sustain(0.3)
    .release(0.3)
    .lpf(2200)
    .room(0.3),

  // Bloque 2: mano izquierda
  note(mini(bajo)).gain(mini(vel))
    .s('triangle').visualid("bass")
    .attack(0.005)
    .decay(0.4)
    .sustain(0.3)
    .release(0.3)
    .lpf(2200)
    .room(0.3)
)
