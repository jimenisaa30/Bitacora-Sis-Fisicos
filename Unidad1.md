setcpm(30)
//batería y percusión
let drum = stack(
  s("oh").beat("14",16), //closed hat
  s("hh").beat("1,5,9,13",16), //closed hat
  s("cp").beat("3,13",16), //clap
  s("bd").beat("0,4,6,10,14",16), //kick
).bank("RhythmAce"); //sample - archivos de audio

$drum: drum // guarda la información en la variable luego del stack

//melodías y harmonías
$melody: note("[48 55]*4, 72 79 82 84").sound("gm_blown_bottle").legato(1) // melodía
$melody: note("[61, 60 ] [65, 68] [77, 79] [64, 68]").sound("gm_electric_guitar_muted").legato(1)
$wind: note("[39 41]*3").sound("wind").lpf(470) //viento

//bajo
$bass: note("[54 56 58 61]/4").sound("sawtooth").lpf(700)
