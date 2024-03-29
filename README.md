# HexTools 

## TableWriter 



### Default Settings

By default the `TableWriter` writes 8 columns of 2 hex bytes, 
with the byte offset in the first column, 
and the ASCII representation in the last column.




#### Printing all bytes

```csharp
using (var writer = new HexTools.TableWriter(Console.Out))
{
    writer.Write(asciiTable);
}
```
Output:
```
   0 0001 0203 0405 0607 0809 0A0B 0C0D 0E0F ................
  16 1011 1213 1415 1617 1819 1A1B 1C1D 1E1F ................
  32 2021 2223 2425 2627 2829 2A2B 2C2D 2E2F .!"#$%&'()*+,-./
  48 3031 3233 3435 3637 3839 3A3B 3C3D 3E3F 0123456789:;<=>?
  64 4041 4243 4445 4647 4849 4A4B 4C4D 4E4F @ABCDEFGHIJKLMNO
  80 5051 5253 5455 5657 5859 5A5B 5C5D 5E5F PQRSTUVWXYZ[\]^_
  96 6061 6263 6465 6667 6869 6A6B 6C6D 6E6F `abcdefghijklmno
 112 7071 7273 7475 7677 7879 7A7B 7C7D 7E7F pqrstuvwxyz{|}~.
 128 8081 8283 8485 8687 8889 8A8B 8C8D 8E8F ................
 144 9091 9293 9495 9697 9899 9A9B 9C9D 9E9F ................
 160 A0A1 A2A3 A4A5 A6A7 A8A9 AAAB ACAD AEAF ................
 176 B0B1 B2B3 B4B5 B6B7 B8B9 BABB BCBD BEBF ................
 192 C0C1 C2C3 C4C5 C6C7 C8C9 CACB CCCD CECF ................
 208 D0D1 D2D3 D4D5 D6D7 D8D9 DADB DCDD DEDF ................
 224 E0E1 E2E3 E4E5 E6E7 E8E9 EAEB ECED EEEF ................
 240 F0F1 F2F3 F4F5 F6F7 F8F9 FAFB FCFD FEFF ................
```

#### Printing a table where the last row isn't full

```csharp
using (var writer = new HexTools.TableWriter(Console.Out))
{
    writer.Write(asciiTable);
}
```
Output:
```
   0 6E6F 7071 7273 7475 7677 7879 7A7B 7C7D nopqrstuvwxyz{|}
  16 7E7F 8081 8283 8485 8687 8889 8A8B 8C8D ~...............
  32 8E8F 9091 9293 9495                     ........        
```

#### Change layout to 3 columns of 3 bytes

```csharp
using (var writer = new HexTools.TableWriter(Console.Out)
{
    ColumnCount = 3,
    ColumnWidth = 3,
})
{
    writer.Write(asciiTable);
}
```
Output:
```
   0 6E6F70 717273 747576 nopqrstuv
   9 777879 7A7B7C 7D7E7F wxyz{|}~.
  18 808182 838485 868788 .........
  27 898A8B 8C8D8E 8F9091 .........
  36 929394 95            ....     
```

#### remove the offset column

```csharp
using (var writer = new HexTools.TableWriter(Console.Out)
{
    ShowOffsetColumn = false,
})
{
    writer.Write(asciiTable);
}
```
Output:
```
6E6F 7071 7273 7475 7677 7879 7A7B 7C7D nopqrstuvwxyz{|}
7E7F 8081 8283 8485 8687 8889 8A8B 8C8D ~...............
8E8F 9091 9293 9495                     ........        
```

#### Remove the ascii column

```csharp
using (var writer = new HexTools.TableWriter(Console.Out)
{
    ShowAsciiColumn = false,
})
{
    writer.Write(asciiTable);
}
```
Output:
```
   0 6E6F 7071 7273 7475 7677 7879 7A7B 7C7D
  16 7E7F 8081 8283 8485 8687 8889 8A8B 8C8D
  32 8E8F 9091 9293 9495                    
```

#### change hex to lower case

```csharp
using (var writer = new HexTools.TableWriter(Console.Out)
{
    ByteFormat = "{0:x2}"
})
{
    writer.Write(asciiTable);
}
```
Output:
```
   0 6e6f 7071 7273 7475 7677 7879 7a7b 7c7d nopqrstuvwxyz{|}
  16 7e7f 8081 8283 8485 8687 8889 8a8b 8c8d ~...............
  32 8e8f 9091 9293 9495                     ........        
```

#### print bytes as decimal

```csharp
using (var writer = new HexTools.TableWriter(Console.Out)
{
    ByteFormat = "{0,4}" // no hex conversion, but write byte with a fixed width to 4
})
{
    writer.Write(asciiTable);
}
```
Output:
```
   0  110 111  112 113  114 115  116 117  118 119  120 121  122 123  124 125 nopqrstuvwxyz{|}
  16  126 127  128 129  130 131  132 133  134 135  136 137  138 139  140 141 ~...............
  32  142 143  144 145  146 147  148 149                                     ........        
```

#### print bytes as binary (.NET 8+)

```csharp
using (var writer = new HexTools.TableWriter(Console.Out)
{
    ByteFormat = "{0:B8}",
    ColumnWidth = 1,
    ColumnCount = 4,
})
{
    writer.Write(asciiTable);
}
```
Output:
```
   0 01101110 01101111 01110000 01110001 nopq
   4 01110010 01110011 01110100 01110101 rstu
   8 01110110 01110111 01111000 01111001 vwxy
  12 01111010 01111011 01111100 01111101 z{|}
  16 01111110 01111111 10000000 10000001 ~...
  20 10000010 10000011 10000100 10000101 ....
  24 10000110 10000111 10001000 10001001 ....
  28 10001010 10001011 10001100 10001101 ....
  32 10001110 10001111 10010000 10010001 ....
  36 10010010 10010011 10010100 10010101 ....
```

#### change column separator

```csharp
using (var writer = new HexTools.TableWriter(Console.Out)
{
    ColumnSeparator = " | ",
})
{
    writer.Write(asciiTable);
}
```
Output:
```
   0 | 6E6F | 7071 | 7273 | 7475 | 7677 | 7879 | 7A7B | 7C7D | nopqrstuvwxyz{|}
  16 | 7E7F | 8081 | 8283 | 8485 | 8687 | 8889 | 8A8B | 8C8D | ~...............
  32 | 8E8F | 9091 | 9293 | 9495 |      |      |      |      | ........        
```

#### Prefix every row with >>>

```csharp
using (var writer = new HexTools.TableWriter(Console.Out)
{
    RowStart = ">>> ",
})
{
    writer.Write(asciiTable);
}
```
Output:
```
>>>    0 6E6F 7071 7273 7475 7677 7879 7A7B 7C7D nopqrstuvwxyz{|}
>>>   16 7E7F 8081 8283 8485 8687 8889 8A8B 8C8D ~...............
>>>   32 8E8F 9091 9293 9495                     ........        
```

#### End every row with <<<

```csharp
using (var writer = new HexTools.TableWriter(Console.Out)
{
    RowEnd = " <<<",
})
{
    writer.Write(asciiTable);
}
```
Output:
```
   0 6E6F 7071 7273 7475 7677 7879 7A7B 7C7D nopqrstuvwxyz{|} <<<
  16 7E7F 8081 8283 8485 8687 8889 8A8B 8C8D ~............... <<<
  32 8E8F 9091 9293 9495                     ........         <<<
```

#### Make it a markdown table

```csharp

Console.Out.WriteLine("| offset | byte 0-1 | byte 2-3 | byte 4-5 | byte 6-7 | byte 8-9 | byte 10-11 | byte 12-13 | byte 14-15 | ASCII |");
Console.Out.WriteLine("|--------|----------|----------|----------|----------|----------|------------|------------|------------|-------|");
using (var writer = new HexTools.TableWriter(Console.Out)
{
    ColumnSeparator = " | ",
    RowStart = "| ",
    RowEnd = " |",
    AsciiFormat = "`{0}`",
})
{
    writer.Write(asciiTable);
}
```
Output:


| offset | byte 0-1 | byte 2-3 | byte 4-5 | byte 6-7 | byte 8-9 | byte 10-11 | byte 12-13 | byte 14-15 | ASCII |
|--------|----------|----------|----------|----------|----------|------------|------------|------------|-------|
|    0 | 6E6F | 7071 | 7273 | 7475 | 7677 | 7879 | 7A7B | 7C7D | `nopqrstuvwxyz{|}` |
|   16 | 7E7F | 8081 | 8283 | 8485 | 8687 | 8889 | 8A8B | 8C8D | `~...............` |
|   32 | 8E8F | 9091 | 9293 | 9495 |      |      |      |      | `........`         |

#### Generate some code 

```csharp
Console.Out.WriteLine("public static readonly byte[] bytes = {");
using (var writer = new HexTools.TableWriter(Console.Out)
{
    RowStart = "    ",
    OffsetFormat = "/* {0,4} */",
    ColumnSeparator = ", ",
    ColumnWidth = 1,
    ByteFormat = "0x{0:X2}",
    AsciiFormat = "// ascii bytes: {0}",
    OmitMissingByteColumns = true,
})
{
    writer.Write(asciiTable);
}
Console.Out.WriteLine("};");
```
Output:
```csharp
public static readonly byte[] bytes = {
    /*    0 */, 0x6E, 0x6F, 0x70, 0x71, 0x72, 0x73, 0x74, 0x75, // ascii bytes: nopqrstu
    /*    8 */, 0x76, 0x77, 0x78, 0x79, 0x7A, 0x7B, 0x7C, 0x7D, // ascii bytes: vwxyz{|}
    /*   16 */, 0x7E, 0x7F, 0x80, 0x81, 0x82, 0x83, 0x84, 0x85, // ascii bytes: ~.......
    /*   24 */, 0x86, 0x87, 0x88, 0x89, 0x8A, 0x8B, 0x8C, 0x8D, // ascii bytes: ........
    /*   32 */, 0x8E, 0x8F, 0x90, 0x91, 0x92, 0x93, // ascii bytes: ......  
};
```
