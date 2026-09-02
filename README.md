# Nand-2-Tetris
#XOR
CHIP Xor {
    IN a, b;
    OUT out;

    PARTS:
    Or(a=a, b=b, out=orAB);
    And(a=a, b=b, out=andAB);
    Not(in=andAB, out=notAnd);
    And(a=orAB, b=notAnd, out=out);
}


#2-WAYMUX
CHIP Mux {
    IN a, b, sel;
    OUT out;

    PARTS:
    Not(in=sel, out=notSel);
    And(a=a, b=notSel, out=aSelected);
    And(a=b, b=sel, out=bSelected);
    Or(a=aSelected, b=bSelected, out=out);
}
#4-WAYMUX
CHIP Mux4Way16 {
    IN a[16], b[16], c[16], d[16], sel[2];
    OUT out[16];

    PARTS:
    Mux16(a=a, b=b, sel=sel[0], out=ab);
    Mux16(a=c, b=d, sel=sel[0], out=cd);
    Mux16(a=ab, b=cd, sel=sel[1], out=out);
}
#DMUX
CHIP DMux {
    IN in, sel;
    OUT a, b;

    PARTS:
    Not(in=sel, out=notSel);
    And(a=in, b=notSel, out=a);
    And(a=in, b=sel, out=b);
}
