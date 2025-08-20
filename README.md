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

Ejercicio 2

~~~
S -> { L.iden = 0; } L                                                          { imprimir(L.cad); }
L -> { T.iden = L.iden; } T { L'.iden = L.iden;
                              L'.cad_h = T.cad; } L'                            { L.cad = L'.cad; }
L' -> { T.iden = L.iden; } T { L'1.iden = L'.iden;
                               L'1.cad_h = concat(L'.cad_h, "\n", T.cad); } L'  { L'.cad = L'1.cad; }
    | ε                                                                         { L'.cad = L'.cad_h; }
T -> { P.iden = T.iden; } P ;                                                   { T.cad = concat(P.cad, ";"); }
   | { I.iden = T.iden; } I                                                     { T.cad = I.cad; }
P -> print ( E )                                                                { P.cad = concat(gen_espacios(P.iden * 4), "print(", E.cad, ")"); }
I -> if ( C ) then { L.iden = I.iden + 1; } L                                   { I.cad = concat(gen_espacios(I.iden * 4), "if(", C.cad, ") then\n");
                                                                                  I.cad = concat(I.cad, L.cad); }
   | if ( C ) then { L1.iden = I.iden + 1; } L else { L2.iden = I.iden + 1; } L { I.cad = concat(gen_espacios(I.iden * 4), "if(", C.cad, ") then\n");
                                                                                  I.cad = concat(I.cad, L1.cad, "\n");
                                                                                  I.cad = concat(I.cad, gen_espacios(I.iden * 4), "else\n");
                                                                                  I.cad = concat(I.cad, L2.cad); }
C -> E < E                                                                      { C.cad = concat(E1.cad, "<", E2.cad); }
   | E <= E                                                                     { C.cad = concat(E1.cad, "<=", E2.cad); }
   | E > E                                                                      { C.cad = concat(E1.cad, ">", E2.cad); }
   | E >= E                                                                     { C.cad = concat(E1.cad, ">=", E2.cad); }
E -> id                                                                         { E.cad = id; }
   | num                                                                        { E.cad = num; }
~~~
