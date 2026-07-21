setcpm(30)
//batería 
let drum = stack(
  s("oh").beat("14",16), //closed hat
  s("hh").beat("1,5,9,13",16), //closed hat
  s("cp").beat("3,13",16), //clap
  s("bd").beat("0,4,6,10,14",16), //kick
).bank("RhythmAce"); //sample - archivos de audio

$drum: drum // guarda la información en la variable luego del stack

$melody: note("36 43, 52 59 62 64").sound("gm_blown_bottle").legato(1) // melodía
