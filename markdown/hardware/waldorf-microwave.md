# OS 1.25

Tuning tables doesn't appear in the specification.

# OS v2.0

It appears in `MicrowaveSysex 2_0.txt` as TUNR and TUND messages:

  
## TUNR
--------------------------------------------
IDM: 06h (Tuning Table Dump Request)

Requests a dump of a user Tuning table.

    Byte #   Value

      0     F0h (EXC)
      1     IDW
      2     IDE
      3     DEV
      4     IDM

            Data:
      5     Tuning Table # (0...3)
      6     CHKSUM (=Byte 5)
      7     EOX (F7h)

TUND
------------------------------------------------------
IDM: 46h (User Tuning Table Dump)

Will be issued after recieving a TUNR request.

When recieving a Tuning table dump, the table will be stored
according to it's number.

Already existing tables will be erased and replaced.

Tables 0..1 are internal RAM tables,
       2..3 are Card-RAM tables.

    Byte #   Value

      0     F0h (EXC)
      1     IDW
      2     IDE
      3     DEV
      4     IDM

            Data:
      5       Tuning Table # (0...3)
      6...261 Tablepositions 0...127, first Semitone (0...127),
              followed by Detune (0...127, equals -64...0...+63)

    262     CHKSUM over Bytes 5...261
    263     EOX (F7h)
