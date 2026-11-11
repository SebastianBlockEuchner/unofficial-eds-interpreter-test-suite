# EDS Test Cases

This document describes the EDS (Electronic Data Sheet) test files used to verify how an EDS interpreter parses and displays EDS content. These test files are unofficial and are not an ODVA publication; see the [README](README.md) for details. Each test case has its own EDS file, located in the [`eds/`](eds/) folder, and focuses on a specific set of EDS keywords or data types.

## File naming convention

Each EDS file name is built from the device identity in hexadecimal, in the form `VVVVTTTTCCCCMMmm.eds`:

| Part | Meaning | Example (`0018002B00140100.eds`) |
|---|---|---|
| `VVVV` | Vendor ID | `0018` = 24 (ODVA Inc) |
| `TTTT` | Product Type | `002B` = 43 (Generic Device) |
| `CCCC` | Product Code | `0014` = 20 |
| `MM` | Major revision | `01` = 1 |
| `mm` | Minor revision | `00` = the minor revision doesn't affect anything related to the use of the EDS file |

## Test cases

| Test | EDS file | Vendor ID | Product Type | Product Code |
|---|---|---:|---:|---:|
| [Minimal Requirements](#minimal-requirements) | [`0018002B00010100.eds`](eds/0018002B00010100.eds) | 24 | 43 | 1 |
| [Param BOOL](#param-bool) | [`0018002B00020100.eds`](eds/0018002B00020100.eds) | 24 | 43 | 2 |
| [Param USINT](#param-usint) | [`0018002B00030100.eds`](eds/0018002B00030100.eds) | 24 | 43 | 3 |
| [Param UINT](#param-uint) | [`0018002B00040100.eds`](eds/0018002B00040100.eds) | 24 | 43 | 4 |
| [Param UDINT](#param-udint) | [`0018002B00050100.eds`](eds/0018002B00050100.eds) | 24 | 43 | 5 |
| [Param SINT](#param-sint) | [`0018002B00060100.eds`](eds/0018002B00060100.eds) | 24 | 43 | 6 |
| [Param INT](#param-int) | [`0018002B00070100.eds`](eds/0018002B00070100.eds) | 24 | 43 | 7 |
| [Param DINT](#param-dint) | [`0018002B00080100.eds`](eds/0018002B00080100.eds) | 24 | 43 | 8 |
| [Param All Data Types](#param-all-data-types) | [`0018002B00090100.eds`](eds/0018002B00090100.eds) | 24 | 43 | 9 |
| [Param Enumeration](#param-enumeration) | [`0018002B00140100.eds`](eds/0018002B00140100.eds) | 24 | 43 | 20 |
| [Assem SINT](#assem-sint) | [`0018002B000A0100.eds`](eds/0018002B000A0100.eds) | 24 | 43 | 10 |
| [Assem USINT](#assem-usint) | [`0018002B000B0100.eds`](eds/0018002B000B0100.eds) | 24 | 43 | 11 |
| [Assem INT](#assem-int) | [`0018002B000C0100.eds`](eds/0018002B000C0100.eds) | 24 | 43 | 12 |
| [Assem UINT](#assem-uint) | [`0018002B000D0100.eds`](eds/0018002B000D0100.eds) | 24 | 43 | 13 |
| [Assem DINT](#assem-dint) | [`0018002B000E0100.eds`](eds/0018002B000E0100.eds) | 24 | 43 | 14 |
| [Assem UDINT](#assem-udint) | [`0018002B000F0100.eds`](eds/0018002B000F0100.eds) | 24 | 43 | 15 |
| [Assem Mix Aligned](#assem-mix-aligned) | [`0018002B00100100.eds`](eds/0018002B00100100.eds) | 24 | 43 | 16 |
| [Assem Mix Unaligned](#assem-mix-unaligned) | [`0018002B00110100.eds`](eds/0018002B00110100.eds) | 24 | 43 | 17 |
| [Assem Config Aligned](#assem-config-aligned) | [`0018002B00120100.eds`](eds/0018002B00120100.eds) | 24 | 43 | 18 |
| [Assem Config Indirect Basic](#assem-config-indirect-basic) | [`0018002B00130100.eds`](eds/0018002B00130100.eds) | 24 | 43 | 19 |
| [Assem Config Indirect Zero](#assem-config-indirect-zero) | [`0018002B00150100.eds`](eds/0018002B00150100.eds) | 24 | 43 | 21 |
| [Assem Config Indirect Size](#assem-config-indirect-size) | [`0018002B00160100.eds`](eds/0018002B00160100.eds) | 24 | 43 | 22 |

---

## Minimal Requirements

| Field | Value |
|---|---|
| EDS file | [`0018002B00010100.eds`](eds/0018002B00010100.eds) |
| Vendor ID | 24 |
| Product Type | 43 |
| Product Code | 1 |

### Description

Tests an EDS file that contains only the bare minimum of required keywords for a device EDS file, with no optional sections or keywords.

Verifies that:

- The tool parses the file without errors or warnings.
- The required `[File]` section keywords (DescText, CreateDate, CreateTime, ModDate, ModTime, and Revision) are read and displayed correctly.
- The required `[Device]` section keywords (VendCode, VendName, ProdType, ProdTypeStr, ProdCode, MajRev, MinRev, and ProdName) are read and displayed correctly.
- The `[Device Classification]` section is read correctly, with the device classified as EtherNetIP.
- The tool doesn't depend on any optional sections or keywords, and doesn't report their absence as an error.

---

## Param BOOL

| Field | Value |
|---|---|
| EDS file | [`0018002B00020100.eds`](eds/0018002B00020100.eds) |
| Vendor ID | 24 |
| Product Type | 43 |
| Product Code | 2 |

### Description

Tests the use of ParamN entry keywords with data type BOOL (0xC1).

Verifies that:

- The tool correctly parses the parameter definition.
- The full value range (0–1) is displayed correctly, including default values.
- The data type is shown as BOOL with a data size of 1 byte.
- The parameter name, units, and help string are displayed as defined in the EDS.

---

## Param USINT

| Field | Value |
|---|---|
| EDS file | [`0018002B00030100.eds`](eds/0018002B00030100.eds) |
| Vendor ID | 24 |
| Product Type | 43 |
| Product Code | 3 |

### Description

Tests the use of ParamN entry keywords with data type USINT (0xC6).

Verifies that:

- The tool correctly parses the parameter definition.
- The full value range (0–255) is displayed correctly, including the minimum, maximum, and default values.
- Values specified in hexadecimal notation (0x00–0xFF) are parsed correctly and displayed as their equivalent values.
- The data type is shown as USINT with a data size of 1 byte.
- The parameter name, units, and help string are displayed as defined in the EDS.
- Scaling and decimal precision is used as defined in the EDS.

---

## Param UINT

| Field | Value |
|---|---|
| EDS file | [`0018002B00040100.eds`](eds/0018002B00040100.eds) |
| Vendor ID | 24 |
| Product Type | 43 |
| Product Code | 4 |

### Description

Tests the use of ParamN entry keywords with data type UINT (0xC7).

Verifies that:

- The tool correctly parses the parameter definition.
- The full value range (0–65535) is displayed correctly, including the minimum, maximum, and default values.
- Values specified in hexadecimal notation (0x0000–0xFFFF) are parsed correctly and displayed as their equivalent values.
- The data type is shown as UINT with a data size of 2 bytes.
- The parameter name, units, and help string are displayed as defined in the EDS.

---

## Param UDINT

| Field | Value |
|---|---|
| EDS file | [`0018002B00050100.eds`](eds/0018002B00050100.eds) |
| Vendor ID | 24 |
| Product Type | 43 |
| Product Code | 5 |

### Description

Tests the use of ParamN entry keywords with data type UDINT (0xC8).

Verifies that:

- The tool correctly parses the parameter definition.
- The full value range (0–4294967295) is displayed correctly, including the minimum, maximum, and default values.
- Values specified in hexadecimal notation (0x00000000–0xFFFFFFFF) are parsed correctly and displayed as their equivalent values.
- The data type is shown as UDINT with a data size of 4 bytes.
- The parameter name, units, and help string are displayed as defined in the EDS.

---

## Param SINT

| Field | Value |
|---|---|
| EDS file | [`0018002B00060100.eds`](eds/0018002B00060100.eds) |
| Vendor ID | 24 |
| Product Type | 43 |
| Product Code | 6 |

### Description

Tests the use of ParamN entry keywords with data type SINT (0xC2).

Verifies that:

- The tool correctly parses the parameter definition.
- The full signed value range (−128 to 127) is displayed correctly, including the minimum, maximum, and default values.
- Negative values are displayed with the correct sign.
- The data type is shown as SINT with a data size of 1 byte.
- The parameter name, units, and help string are displayed as defined in the EDS.

---

## Param INT

| Field | Value |
|---|---|
| EDS file | [`0018002B00070100.eds`](eds/0018002B00070100.eds) |
| Vendor ID | 24 |
| Product Type | 43 |
| Product Code | 7 |

### Description

Tests the use of ParamN entry keywords with data type INT (0xC3).

Verifies that:

- The tool correctly parses the parameter definition.
- The full signed value range (−32768 to 32767) is displayed correctly, including the minimum, maximum, and default values.
- Negative values are displayed with the correct sign.
- The data type is shown as INT with a data size of 2 bytes.
- The parameter name, units, and help string are displayed as defined in the EDS.

---

## Param DINT

| Field | Value |
|---|---|
| EDS file | [`0018002B00080100.eds`](eds/0018002B00080100.eds) |
| Vendor ID | 24 |
| Product Type | 43 |
| Product Code | 8 |

### Description

Tests the use of ParamN entry keywords with data type DINT (0xC4).

Verifies that:

- The tool correctly parses the parameter definition.
- The full signed value range (−2147483648 to 2147483647) is displayed correctly, including the minimum, maximum, and default values.
- Negative values are displayed with the correct sign.
- The data type is shown as DINT with a data size of 4 bytes.
- The parameter name, units, and help string are displayed as defined in the EDS.

---

## Param All Data Types

| Field | Value |
|---|---|
| EDS file | [`0018002B00090100.eds`](eds/0018002B00090100.eds) |
| Vendor ID | 24 |
| Product Type | 43 |
| Product Code | 9 |

### Description

Tests the use of ParamN entry keywords across all CIP elementary data types from BOOL (0xC1) to TIME (0xDB) in a single EDS file. The following data types are covered:

- **Boolean:** BOOL
- **Signed integers:** SINT, INT, DINT, LINT
- **Unsigned integers:** USINT, UINT, UDINT, ULINT
- **Floating point:** REAL, LREAL
- **Date and time:** STIME, DATE, TIME_OF_DAY, DATE_AND_TIME
- **Durations:** FTIME, LTIME, ITIME, TIME
- **Strings:** STRING, STRING2, SHORT_STRING
- **Bit strings:** BYTE, WORD, DWORD, LWORD

Verifies that:

- The tool correctly parses each parameter definition and displays the default value in the correct format for each data type.
- Negative values are displayed with the correct sign for signed integer, floating-point, and duration types.
- The maximum values of the unsigned integer types (including 64-bit ULINT) are displayed correctly.
- String defaults, including Unicode characters and escape sequences, are displayed correctly.
- Bit string defaults specified in binary notation are parsed correctly.
- STIME defaults specified in decimal, formatted (`yyyy-mm-dd-hh:nn:ss.iii.jjj.kkk`), and hexadecimal notation are parsed correctly, and all three display the same date and time (2025-11-12 02:14:00 UTC).
- The DATE, TIME_OF_DAY, and DATE_AND_TIME defaults are displayed as the dates and times stated in their help strings: 2025-12-14, 08:46:00, and 2025-12-14 08:51:00. The display format may differ between tools, but the date and time shown must be the same.
- The data type and data size are shown correctly for each parameter.
- The parameter name, units, and help string are displayed as defined in the EDS.

> **Note:** Minimum and maximum values are not tested in this file. Value ranges for BOOL, SINT, INT, DINT, USINT, UINT, and UDINT are covered by the individual data type tests.

---

## Param Enumeration

| Field | Value |
|---|---|
| EDS file | [`0018002B00140100.eds`](eds/0018002B00140100.eds) |
| Vendor ID | 24 |
| Product Type | 43 |
| Product Code | 20 |

### Description

Tests the use of EnumN entry keywords together with ParamN entries for integer and bit string data types. Each data type is tested with two parameters: one with a default value of zero, and one with a non-zero default value that matches an enumerated name or, for bit strings, sets several named bits.

Verifies that:

- The tool correctly associates each EnumN entry with its corresponding ParamN entry and displays the enumerated names in place of the numeric values.
- For the integer types (BOOL, SINT, INT, USINT, and UINT), each enumerated value is matched to the correct name, including negative values for the signed types (SINT and INT).
- For the bit string types (BYTE, WORD, DWORD, and LWORD), the enumerated values are interpreted as bit positions, and the lowest, second lowest, second highest, and highest bits are named correctly for each data size, up to bit 63 for LWORD.
- The default value of each parameter is displayed using its enumerated name where one is defined, including negative defaults for the signed types (for example, −100 shown as "Minus one hundred").
- Bit string defaults with several bits set display the enumerated name of each set bit, including the highest bit of each data size.
- Bit string defaults specified in binary notation are parsed correctly.
- The data type, data size, parameter name, units, and help string are displayed as defined in the EDS.

---

## Assem SINT

| Field | Value |
|---|---|
| EDS file | [`0018002B000A0100.eds`](eds/0018002B000A0100.eds) |
| Vendor ID | 24 |
| Product Type | 43 |
| Product Code | 10 |

### Description

Tests the use of ParamN entry keywords with data type SINT (0xC2) as members of AssemN entry keywords. The EDS defines two AssemN entries, one for O→T data (Assem1) and one for T→O data (Assem2), each referencing two ParamN entries with unique names (SINT 1 and SINT 2 for O→T, SINT 3 and SINT 4 for T→O). The assemblies are used by an exclusive-owner connection (Connection1), with the RPI defined by Param1000.

Verifies that:

- The tool correctly resolves each ParamN reference in the AssemN entries and displays the corresponding parameter name for each assembly member.
- The member size is shown as 8 bits per SINT member.
- The members are displayed in the order defined in the EDS.
- The size of each assembly is calculated as 16 bits (2 bytes), since no size is declared in the AssemN entries.
- The connection references the correct O→T and T→O assemblies, and the RPI range (1000–100000 µs) and default (10000 µs) are shown as defined by Param1000.

---

## Assem USINT

| Field | Value |
|---|---|
| EDS file | [`0018002B000B0100.eds`](eds/0018002B000B0100.eds) |
| Vendor ID | 24 |
| Product Type | 43 |
| Product Code | 11 |

### Description

Tests the use of ParamN entry keywords with data type USINT (0xC6) as members of AssemN entry keywords. The EDS defines two AssemN entries, one for O→T data (Assem1) and one for T→O data (Assem2), each referencing two ParamN entries with unique names (USINT 1 and USINT 2 for O→T, USINT 3 and USINT 4 for T→O). The assemblies are used by an exclusive-owner connection (Connection1), with the RPI defined by Param1000.

Verifies that:

- The tool correctly resolves each ParamN reference in the AssemN entries and displays the corresponding parameter name for each assembly member.
- The member size is shown as 8 bits per USINT member.
- The members are displayed in the order defined in the EDS.
- The size of each assembly is calculated as 16 bits (2 bytes), since no size is declared in the AssemN entries.
- The connection references the correct O→T and T→O assemblies, and the RPI range (1000–100000 µs) and default (10000 µs) are shown as defined by Param1000.

---

## Assem INT

| Field | Value |
|---|---|
| EDS file | [`0018002B000C0100.eds`](eds/0018002B000C0100.eds) |
| Vendor ID | 24 |
| Product Type | 43 |
| Product Code | 12 |

### Description

Tests the use of ParamN entry keywords with data type INT (0xC3) as members of AssemN entry keywords. The EDS defines two AssemN entries, one for O→T data (Assem1) and one for T→O data (Assem2), each referencing two ParamN entries with unique names (INT 1 and INT 2 for O→T, INT 3 and INT 4 for T→O). The assemblies are used by an exclusive-owner connection (Connection1), with the RPI defined by Param1000.

Verifies that:

- The tool correctly resolves each ParamN reference in the AssemN entries and displays the corresponding parameter name for each assembly member.
- The member size is shown as 16 bits per INT member.
- The members are displayed in the order defined in the EDS.
- The size of each assembly is calculated as 32 bits (4 bytes), since no size is declared in the AssemN entries.
- The connection references the correct O→T and T→O assemblies, and the RPI range (1000–100000 µs) and default (10000 µs) are shown as defined by Param1000.

---

## Assem UINT

| Field | Value |
|---|---|
| EDS file | [`0018002B000D0100.eds`](eds/0018002B000D0100.eds) |
| Vendor ID | 24 |
| Product Type | 43 |
| Product Code | 13 |

### Description

Tests the use of ParamN entry keywords with data type UINT (0xC7) as members of AssemN entry keywords. The EDS defines two AssemN entries, one for O→T data (Assem1) and one for T→O data (Assem2), each referencing two ParamN entries with unique names (UINT 1 and UINT 2 for O→T, UINT 3 and UINT 4 for T→O). The assemblies are used by an exclusive-owner connection (Connection1), with the RPI defined by Param1000.

Verifies that:

- The tool correctly resolves each ParamN reference in the AssemN entries and displays the corresponding parameter name for each assembly member.
- The member size is shown as 16 bits per UINT member.
- The members are displayed in the order defined in the EDS.
- The size of each assembly is calculated as 32 bits (4 bytes), since no size is declared in the AssemN entries.
- The connection references the correct O→T and T→O assemblies, and the RPI range (1000–100000 µs) and default (10000 µs) are shown as defined by Param1000.

---

## Assem DINT

| Field | Value |
|---|---|
| EDS file | [`0018002B000E0100.eds`](eds/0018002B000E0100.eds) |
| Vendor ID | 24 |
| Product Type | 43 |
| Product Code | 14 |

### Description

Tests the use of ParamN entry keywords with data type DINT (0xC4) as members of AssemN entry keywords. The EDS defines two AssemN entries, one for O→T data (Assem1) and one for T→O data (Assem2), each referencing two ParamN entries with unique names (DINT 1 and DINT 2 for O→T, DINT 3 and DINT 4 for T→O). The assemblies are used by an exclusive-owner connection (Connection1), with the RPI defined by Param1000.

Verifies that:

- The tool correctly resolves each ParamN reference in the AssemN entries and displays the corresponding parameter name for each assembly member.
- The member size is shown as 32 bits per DINT member.
- The members are displayed in the order defined in the EDS.
- The size of each assembly is calculated as 64 bits (8 bytes), since no size is declared in the AssemN entries.
- The connection references the correct O→T and T→O assemblies, and the RPI range (1000–100000 µs) and default (10000 µs) are shown as defined by Param1000.

---

## Assem UDINT

| Field | Value |
|---|---|
| EDS file | [`0018002B000F0100.eds`](eds/0018002B000F0100.eds) |
| Vendor ID | 24 |
| Product Type | 43 |
| Product Code | 15 |

### Description

Tests the use of ParamN entry keywords with data type UDINT (0xC8) as members of AssemN entry keywords. The EDS defines two AssemN entries, one for O→T data (Assem1) and one for T→O data (Assem2), each referencing two ParamN entries with unique names (UDINT 1 and UDINT 2 for O→T, UDINT 3 and UDINT 4 for T→O). The assemblies are used by an exclusive-owner connection (Connection1), with the RPI defined by Param1000.

Verifies that:

- The tool correctly resolves each ParamN reference in the AssemN entries and displays the corresponding parameter name for each assembly member.
- The member size is shown as 32 bits per UDINT member.
- The members are displayed in the order defined in the EDS.
- The size of each assembly is calculated as 64 bits (8 bytes), since no size is declared in the AssemN entries.
- The connection references the correct O→T and T→O assemblies, and the RPI range (1000–100000 µs) and default (10000 µs) are shown as defined by Param1000.

---

## Assem Mix Aligned

| Field | Value |
|---|---|
| EDS file | [`0018002B00100100.eds`](eds/0018002B00100100.eds) |
| Vendor ID | 24 |
| Product Type | 43 |
| Product Code | 16 |

### Description

Tests the use of ParamN entry keywords with the elementary integer data types (SINT, USINT, INT, UINT, DINT, and UDINT) as members of AssemN entry keywords. The EDS defines two AssemN entries, one for O→T data (Assem1) and one for T→O data (Assem2). Each contains two members of each data type, arranged so that every 16-bit and 32-bit member starts on a 16-bit boundary without padding. The assemblies are used by an exclusive-owner connection (Connection1), with the RPI defined by Param1000.

Both AssemN entries have the following structure. Each ParamN entry has a unique name, as shown in the O→T and T→O member columns:

| Offset (bits) | Size (bits) | Data type | O→T member (Assem1) | T→O member (Assem2) |
|---:|---:|---|---|---|
| 0 | 8 | SINT | SINT 1 | SINT 3 |
| 8 | 8 | SINT | SINT 2 | SINT 4 |
| 16 | 8 | USINT | USINT 1 | USINT 3 |
| 24 | 8 | USINT | USINT 2 | USINT 4 |
| 32 | 16 | INT | INT 1 | INT 3 |
| 48 | 16 | INT | INT 2 | INT 4 |
| 64 | 16 | UINT | UINT 1 | UINT 3 |
| 80 | 16 | UINT | UINT 2 | UINT 4 |
| 96 | 32 | DINT | DINT 1 | DINT 3 |
| 128 | 32 | DINT | DINT 2 | DINT 4 |
| 160 | 32 | UDINT | UDINT 1 | UDINT 3 |
| 192 | 32 | UDINT | UDINT 2 | UDINT 4 |
| **Total** | **224 (28 bytes)** | | | |

Verifies that:

- The tool correctly resolves each ParamN reference in the AssemN entries and displays the corresponding parameter name for each member.
- The size and bit offset of each member are shown correctly.
- The members are displayed in the order defined in the EDS.
- No padding is inserted.
- The size of each assembly is calculated as 224 bits (28 bytes), since no size is declared in the AssemN entries.
- The connection references the correct O→T and T→O assemblies, and the RPI range (1000–100000 µs) and default (10000 µs) are shown as defined by Param1000.

---

## Assem Mix Unaligned

| Field | Value |
|---|---|
| EDS file | [`0018002B00110100.eds`](eds/0018002B00110100.eds) |
| Vendor ID | 24 |
| Product Type | 43 |
| Product Code | 17 |

### Description

Tests the use of ParamN entry keywords with the unsigned elementary integer data types (USINT, UINT, and UDINT) as members of AssemN entry keywords. The EDS defines two AssemN entries, one for O→T data (Assem1) and one for T→O data (Assem2). Each contains two members of each data type, packed without alignment or padding, so that some 16-bit and 32-bit members do not start on their natural alignment boundary. The assemblies are used by an exclusive-owner connection (Connection1), with the RPI defined by Param1000.

Both AssemN entries have the following structure. Each ParamN entry has a unique name, as shown in the O→T and T→O member columns:

| Offset (bits) | Size (bits) | Data type | O→T member (Assem1) | T→O member (Assem2) | Value (T→O) |
|---:|---:|---|---|---|---:|
| 0 | 8 | USINT | USINT 1 | USINT 3 | 8 |
| 8 | 16 | UINT | UINT 1 | UINT 3 | 16 |
| 24 | 32 | UDINT | UDINT 1 | UDINT 3 | 32 |
| 56 | 8 | USINT | USINT 2 | USINT 4 | 8 |
| 64 | 16 | UINT | UINT 2 | UINT 4 | 16 |
| 80 | 32 | UDINT | UDINT 2 | UDINT 4 | 32 |
| **Total** | **112 (14 bytes)** | | | | |

Verifies that:

- The tool correctly resolves each ParamN reference in the AssemN entries and displays the corresponding parameter name for each member.
- The size and bit offset of each member are shown correctly.
- The members are displayed in the order defined in the EDS.
- No padding is inserted.
- The size of each assembly is calculated as 112 bits (14 bytes), since no size is declared in the AssemN entries.
- The connection references the correct O→T and T→O assemblies, and the RPI range (1000–100000 µs) and default (10000 µs) are shown as defined by Param1000.
- The data sent by the reference implementation in the T→O direction is decoded correctly, with each member showing the value listed in the table.

---

## Assem Config Aligned

| Field | Value |
|---|---|
| EDS file | [`0018002B00120100.eds`](eds/0018002B00120100.eds) |
| Vendor ID | 24 |
| Product Type | 43 |
| Product Code | 18 |

### Description

Tests the use of ParamN entry keywords with the elementary integer data types (SINT, USINT, INT, UINT, DINT, and UDINT) as members of an AssemN entry keyword that is delivered as the target configuration. The EDS defines three AssemN entries with the same aligned structure:

- **Assem1 (O→T)** and **Assem2 (T→O)**, which intentionally reference the same ParamN entries (SINT 1, SINT 2, and so on).
- **Assem99 (configuration)**, which references separate ParamN entries (Cfg SINT 1, Cfg SINT 2, and so on).

The assemblies are used by an exclusive-owner connection (Connection1), which references Assem99 as the target configuration and uses configuration instance 99 in its path. The RPI is defined by Param1000. Each assembly contains two members of each data type, arranged so that every 16-bit and 32-bit member starts on a 16-bit boundary without padding. The reference implementation returns the configuration data it receives in the T→O direction, so that the delivered values can be checked.

The AssemN entries have the following structure:

| Offset (bits) | Size (bits) | Data type | I/O member (Assem1 and Assem2) | Configuration member (Assem99) | Configuration default and expected T→O value |
|---:|---:|---|---|---|---:|
| 0 | 8 | SINT | SINT 1 | Cfg SINT 1 | 1 |
| 8 | 8 | SINT | SINT 2 | Cfg SINT 2 | −1 |
| 16 | 8 | USINT | USINT 1 | Cfg USINT 1 | 1 |
| 24 | 8 | USINT | USINT 2 | Cfg USINT 2 | 255 |
| 32 | 16 | INT | INT 1 | Cfg INT 1 | 1 |
| 48 | 16 | INT | INT 2 | Cfg INT 2 | −1 |
| 64 | 16 | UINT | UINT 1 | Cfg UINT 1 | 1 |
| 80 | 16 | UINT | UINT 2 | Cfg UINT 2 | 65535 |
| 96 | 32 | DINT | DINT 1 | Cfg DINT 1 | 1 |
| 128 | 32 | DINT | DINT 2 | Cfg DINT 2 | −1 |
| 160 | 32 | UDINT | UDINT 1 | Cfg UDINT 1 | 1 |
| 192 | 32 | UDINT | UDINT 2 | Cfg UDINT 2 | 4294967295 |
| **Total** | **224 (28 bytes)** | | | | |

Verifies that:

- The tool correctly resolves each ParamN reference in the AssemN entries and displays the corresponding parameter name for each member.
- The size and bit offset of each member are shown correctly in all three assemblies.
- The members are displayed in the order defined in the EDS.
- No padding is inserted.
- The size of each assembly is calculated as 224 bits (28 bytes), since no size is declared in the AssemN entries.
- The tool accepts the same ParamN entries being referenced by both the O→T and T→O assemblies.
- The connection references the correct O→T, T→O, and configuration assemblies, and the RPI range (1000–100000 µs) and default (10000 µs) are shown as defined by Param1000.
- The configuration data is built from the configured parameter values and delivered to the target, and the values returned by the reference implementation in the T→O direction match the configured values (by default, the values listed in the table).

---

## Assem Config Indirect Basic

| Field | Value |
|---|---|
| EDS file | [`0018002B00130100.eds`](eds/0018002B00130100.eds) |
| Vendor ID | 24 |
| Product Type | 43 |
| Product Code | 19 |

### Description

Tests the use of ParamN entry keywords together with the Indirect Parameter Reference (Descriptor bit 10). The values of the ParamN entries in the target configuration assembly select which ParamN entry is used for each member of the AssemN entry describing the T→O data. Each enumerated value is the number of the referenced ParamN entry.

The EDS defines three AssemN entries, used by an exclusive-owner connection (Connection1) with the RPI defined by Param1000:

- **Assem1 (O→T):** one 16-bit member, UINT Dummy (Param5).
- **Assem2 (T→O):** two 16-bit members, resolved indirectly through Param1001 and Param1002.
- **Assem99 (configuration):** Param1001 and Param1002, delivered as the target configuration.

The target configuration assembly has the following structure:

| Entry | ParamN | Name | Data type | Offset (bits) | Size (bits) | Default | Selects |
|---|---|---|---|---:|---:|---|---|
| 1 | Param1001 | UINT 1 or UINT 2 | USINT | 0 | 8 | 1 (UINT 1) | First T→O entry |
| 2 | Param1002 | INT or UINT | USINT | 8 | 8 | 3 (INT) | Second T→O entry |
| **Total** | | | | | **16 (2 bytes)** | | |

The AssemN entry describing the T→O data always contains two 16-bit entries. The first entry is always a UINT, while the second entry may be either INT or UINT, depending on the selections:

| Configuration entry | Selection (value) | Referenced ParamN | T→O entry | Data type | Value (T→O) |
|---|---|---|---|---|---:|
| 1 | UINT 1 (1) | Param1 | 1 | UINT | 0x1111 |
| 1 | UINT 2 (2) | Param2 | 1 | UINT | 0x2222 |
| 2 | INT (3) | Param3 | 2 | INT | −10000 |
| 2 | UINT (4) | Param4 | 2 | UINT | 10000 |

With the default configuration, the T→O data consists of UINT 1 (0x1111) followed by INT (−10000).

Verifies that:

- The tool recognizes the Indirect Parameter Reference (Descriptor bit 10) and offers the enumerated choices for each configuration ParamN entry.
- For each selection, the tool uses the referenced ParamN entry for the corresponding T→O member and displays its name and data type.
- The default configuration results in the T→O layout UINT 1 followed by INT.
- The T→O assembly size is calculated as 32 bits (4 bytes) for all combinations, and the O→T assembly size as 16 bits (2 bytes).
- The configuration data delivered to the target reflects the selected values.
- The data sent by the reference implementation in the T→O direction is decoded according to the selected data types, with each member showing the value listed in the table, including −10000 as a negative value when INT is selected.

---

## Assem Config Indirect Zero

| Field | Value |
|---|---|
| EDS file | [`0018002B00150100.eds`](eds/0018002B00150100.eds) |
| Vendor ID | 24 |
| Product Type | 43 |
| Product Code | 21 |

### Description

Tests the use of ParamN entry keywords together with the Indirect Parameter Reference (Descriptor bit 10), including a parameter value of 0, which means no reference. The values of the ParamN entries in the target configuration assembly select which ParamN entry is used for each member of the AssemN entry describing the T→O data. Each enumerated value is the number of the referenced ParamN entry, and 0 means that the member is omitted.

The EDS defines three AssemN entries, used by an exclusive-owner connection (Connection1) with the RPI defined by Param1000:

- **Assem1 (O→T):** one 16-bit member, UINT Dummy (Param5).
- **Assem2 (T→O):** three members, resolved indirectly through Param1001, Param1002, and Param1003. The size of the second member is not declared, since it is either 0 or 16 bits depending on the selection.
- **Assem99 (configuration):** Param1001, Param1002, and Param1003, delivered as the target configuration.

The target configuration assembly has the following structure:

| Entry | ParamN | Name | Data type | Offset (bits) | Size (bits) | Default | Selects |
|---|---|---|---|---:|---:|---|---|
| 1 | Param1001 | UINT 1 or UINT 2 | USINT | 0 | 8 | 1 (UINT 1) | First T→O entry |
| 2 | Param1002 | None - INT or UINT | USINT | 8 | 8 | 3 (INT) | Second T→O entry |
| 3 | Param1003 | INT or UINT | USINT | 16 | 8 | 6 (INT) | Third T→O entry |
| **Total** | | | | | **24 (3 bytes)** | | |

The AssemN entry describing the T→O data contains either two or three 16-bit entries. The first entry is always a UINT, the second entry may be omitted, INT, or UINT, and the third entry may be either INT or UINT, depending on the selections:

| Configuration entry | Selection (value) | Referenced ParamN | T→O entry | Data type |
|---|---|---|---|---|
| 1 | UINT 1 (1) | Param1 (UINT 1) | 1 | UINT |
| 1 | UINT 2 (2) | Param2 (UINT 2) | 1 | UINT |
| 2 | None (0) | — | 2 | Omitted |
| 2 | INT (3) | Param3 (None - INT) | 2 | INT |
| 2 | UINT (4) | Param4 (None - UINT) | 2 | UINT |
| 3 | INT (6) | Param6 (INT) | 3 | INT |
| 3 | UINT (7) | Param7 (UINT) | 3 | UINT |

With the default configuration, the T→O data consists of the parameters UINT 1 (Param1), None - INT (Param3), and INT (Param6), for a total of 48 bits (6 bytes).

Verifies that:

- The tool recognizes the Indirect Parameter Reference (Descriptor bit 10) and offers the enumerated choices for each configuration ParamN entry, including None.
- A value of 0 (None) is treated as no reference: the second T→O entry is omitted, and the tool doesn't report it as an error or an invalid reference.
- The tool handles the second T→O member having no declared size, and uses the size of the referenced ParamN entry when one is selected.
- When the second entry is omitted, the third entry follows directly after the first entry, at bit offset 16 instead of 32.
- The T→O assembly size is calculated as 32 bits (4 bytes) when None is selected, and as 48 bits (6 bytes) otherwise. The O→T assembly size is 16 bits (2 bytes).
- The default configuration results in the T→O layout UINT 1 (Param1), None - INT (Param3), and INT (Param6).
- For each selection, the tool uses the referenced ParamN entry for the corresponding T→O member and displays its name and data type.
- The configuration data delivered to the target reflects the selected values.
- The data sent by the reference implementation in the T→O direction is decoded according to the selected data types and structure.

---

## Assem Config Indirect Size

| Field | Value |
|---|---|
| EDS file | [`0018002B00160100.eds`](eds/0018002B00160100.eds) |
| Vendor ID | 24 |
| Product Type | 43 |
| Product Code | 22 |

### Description

Tests the use of ParamN entry keywords together with the Indirect Parameter Reference (Descriptor bit 10), where the referenced ParamN entries have different sizes, so that the size of the T→O data changes with the selections. The values of the ParamN entries in the target configuration assembly select which ParamN entry is used for each member of the AssemN entry describing the T→O data. Each enumerated value is the number of the referenced ParamN entry.

The EDS defines three AssemN entries, used by an exclusive-owner connection (Connection1) with the RPI defined by Param1000:

- **Assem1 (O→T):** one 16-bit member, UINT Dummy (Param5).
- **Assem2 (T→O):** two members, resolved indirectly through Param1001 and Param1002. Neither member has a declared size, since each is either 16 or 32 bits depending on the selection.
- **Assem99 (configuration):** Param1001 and Param1002, delivered as the target configuration.

The target configuration assembly has the following structure:

| Entry | ParamN | Name | Data type | Offset (bits) | Size (bits) | Default | Selects |
|---|---|---|---|---:|---:|---|---|
| 1 | Param1001 | UINT 1 or UDINT 1 | USINT | 0 | 8 | 1 (UINT 1) | First T→O entry |
| 2 | Param1002 | UINT 2 or UDINT 2 | USINT | 8 | 8 | 3 (UINT 2) | Second T→O entry |
| **Total** | | | | | **16 (2 bytes)** | | |

The AssemN entry describing the T→O data always contains two entries, each of which may be either UINT or UDINT, depending on the selections:

| Configuration entry | Selection (value) | Referenced ParamN | T→O entry | Data type | Size (bits) |
|---|---|---|---|---|---:|
| 1 | UINT 1 (1) | Param1 (UINT 1) | 1 | UINT | 16 |
| 1 | UDINT 1 (2) | Param2 (UDINT 1) | 1 | UDINT | 32 |
| 2 | UINT 2 (3) | Param3 (UINT 2) | 2 | UINT | 16 |
| 2 | UDINT 2 (4) | Param4 (UDINT 2) | 2 | UDINT | 32 |

This results in the following T→O layouts:

| First entry | Second entry | Second entry offset (bits) | Total size (bits) |
|---|---|---:|---:|
| UINT 1 | UINT 2 | 16 | 32 (4 bytes) |
| UINT 1 | UDINT 2 | 16 | 48 (6 bytes) |
| UDINT 1 | UINT 2 | 32 | 48 (6 bytes) |
| UDINT 1 | UDINT 2 | 32 | 64 (8 bytes) |

With the default configuration, the T→O data consists of UINT 1 followed by UINT 2, for a total of 32 bits (4 bytes).

Verifies that:

- The tool recognizes the Indirect Parameter Reference (Descriptor bit 10) and offers the enumerated choices for each configuration ParamN entry.
- For each selection, the tool uses the referenced ParamN entry for the corresponding T→O member and displays its name and data type.
- The tool handles T→O members with no declared size, and uses the size of the referenced ParamN entry.
- The bit offset of the second entry and the total T→O assembly size are recalculated when a selection changes, as listed in the layout table. The O→T assembly size is 16 bits (2 bytes).
- The default configuration results in the T→O layout UINT 1 followed by UINT 2.
- The configuration data delivered to the target reflects the selected values.
- The data sent by the reference implementation in the T→O direction is decoded according to the selected data types.
