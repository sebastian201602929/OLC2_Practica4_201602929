# Practica 4

**Sebastián Gómez Lavarreda - 201602929**

Ejercicio 1

~~~
S -> L                                                                       { imprimir(concat("[", L.cad, "]")); }
L -> D ; { L'.cad_h = D.cad; } L'                                            { L.cad = L'.cad; }
L' -> D ; { L'1.cad_h = concat(L'.cad_h, ",", D.cad); } L'                   { L'.cad = L'1.cad; }
    | ε                                                                      { L'.cad = L'.cad_h; }
D -> T id { D'.tipo = T.tipo;
            D'.cad_h = concat("(", id, ",", T.tipo, ")"); } D'               { D.cad = D'.cad; }
D' -> , id { D'1.tipo = D'.tipo;
             D'1.cad_h = concat(D'.cad_h, ",(", id, ",", D'.tipo, ")"); } D' { D'.cad = D'1.cad; }
    | ε                                                                      { D'.cad = D'.cad_h; }
T -> int                                                                     { T.tipo = "int"; }
   | char                                                                    { T.tipo = "char"; }
~~~
