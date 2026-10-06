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

const R = (...partes) => '[' + partes.join(' ') + ']'

// ── Mano izquierda ──
const lh = (r, f, o) =>
  R('[' + r + ',' + f + ']@2', f, o, o, f, r + '@2')

const bajo = '<' + [
  lh('d2','a2','d3'),
  lh('d2','a2','d3'),
  lh('e2','b2','e3'),
  lh('e2','b2','e3'),
  lh('e2','b2','e3'),
  lh('a1','e2','a2'),
  lh('d2','a2','d3'),
  lh('a1','e2','a2'),
  lh('d2','a2','d3'),
  lh('a1','e2','a2'),
  lh('e2','b2','e3'),
  lh('e2','b2','e3'),
  lh('e2','b2','e3'),
  lh('a1','e2','a2'),
].join(' ') + '>'

// ── Mano derecha ──
const c4 = R('g#4@3','~','b4','a4','g#4','[d4,g#4]')
const c5 = R(Em9+'@2','b4','g4',Em9+'@2','f#5@2')
const c6 = R(A9+'@2','b4','g4',A9+'@2','e5@2')

const armonia = '<' + [
  R(D9+'@3', D9+'@3', 'f#4@2'),
  R(Dtri+'@4','a4','d5',Dtri+'@2'),
  R(E9+'@3', E9+'@2','b4','~','g#4'),
  c4,
  c5,
  c6,
  R(E11D+'@3', E11D+'@2','~@3'),
  R(A13+'@3', A13+'@3','g4@2'),
  R(Dmaj9+'@3','a4','f#4','a4',Dmaj9+'@2'),
  R('~@4','a4','d5',A11+'@2'),
  R(E9+'@3', E9+'@2','~','~','b4'),
  c4,
  c5,
  c6,
].join(' ') + '>'

// ── Dinámica ──
const vel = '<0.7!13 0.55>'

// ─────────────────────────────
// MANO DERECHA
// ─────────────────────────────

const harmony = note(mini(armonia))
  .gain(mini(vel))
  .s('triangle')
  .visualid("harmony")
  .attack(0.005)
  .decay(0.4)
  .sustain(0.3)
  .release(0.3)
  .lpf(2100)
  .room(0.3)

// ─────────────────────────────
// MANO IZQUIERDA
// ─────────────────────────────

const bass = note(mini(bajo))
  .gain(mini(vel))
  .s('triangle')
  .visualid("bass")
  .attack(0.005)
  .decay(0.4)
  .sustain(0.3)
  .release(0.3)
  .lpf(2100)
  .room(0.3)

// ─────────────────────────────
// AUDIO + OSC
// ─────────────────────────────

$harmony: stack(
  harmony,
  harmony.osc()
)

$bass: stack(
  bass,
  bass.osc()
)
