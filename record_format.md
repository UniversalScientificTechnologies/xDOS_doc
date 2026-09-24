---
layout: page
parent: Tools and resources
title: UST Dosimeters file format
permalink: /xdos_format
---

# UST Detectors Output Format

# Purpose

This document specifies the format of the data files written by UST dosimeters (AIRDOS, LABDOS and SPACEDOS series). It is the reference both for the firmware that writes the files and for the software that reads or validates them: a file conforming to this specification can be interpreted unambiguously without further knowledge of the device. The format is plain text, readable by humans and simple to parse by machines.

{: .highlight }
The data format version is versioned independently of the detector firmware version. A firmware update does not necessarily change the output format, and a new format version may be introduced without a firmware version bump. This applies to all UST detectors.

# Versioning and compatibility

Starting with Version 2, each format revision is backward compatible with the previous one: a reader built for an earlier Version 2.x revision can still parse a file produced by a later one. This is achieved by construction:

- A revision may append fields to the end of an existing message, but never removes, reorders, or redefines a field already defined by an earlier revision.
- The only exception to the previous rule is a message whose format includes an explicit switch — a dedicated field that signals a changed interpretation of the fields following it. Readers must read the switch before parsing the rest of the message.
- A revision may introduce new message types (new `$` headers), but never changes the format or meaning of an existing one.
- Readers must ignore any message type they do not recognize, and must ignore any fields beyond those they know how to parse in a message they do recognize.

Format versions are numbered `MAJOR.MINOR`. The guarantee holds within one major version, i.e. within the Version 2.x series (Version 2, Version 2.1, and later revisions). A new major version (e.g. 3.0) may introduce incompatible changes. Version 1 predates this policy.

# Normative references

The following documents are referenced by this specification; where no edition is stated, the latest edition applies.

- **NMEA 0183**, *Standard for Interfacing Marine Electronic Devices* — origin of the `$`-prefixed, comma-separated line syntax used since [Version 1](#version-1).
- **ISO 8601**, *Date and time — Representations for information interchange* — basis for the date/time notation used in the `$TIME` field. Deviations are noted in the field description: a space instead of `T` separates date and time, and no time-zone designator is written because all timestamps are UTC.
- **POSIX.1 (IEEE Std 1003.1)** — definition of Unix time, used for `<current_unix_time>` and related fields in `$TIME`.
- **ISO/IEC 14977**, *Information technology — Syntactic metalanguage — Extended BNF* — basis for the notation of message formats; the symbols used and their meaning are defined in [Notation](#notation).

# Applicable documents

This specification is maintained in accordance with the software documentation and assurance framework of:

- ECSS-E-ST-40C, *Space engineering — Software*
- ECSS-Q-ST-80C, *Space product assurance — Software product assurance*

# Terms, definitions and notation

## Terms

- **Message** — one line of the file starting with `$`.
- **Message identifier** — the first field of a message, e.g. `$STOP`; determines the message type.
- **Field** — one comma-separated value of a message.
- **Header block** — the header messages at the beginning of a file, describing the device and its configuration.
- **Block** (integration block) — the data of one integration period: a `$START` line, zero or more `$E` lines and a `$STOP` line.
- **Session** (measurement session) — all data recorded from device start-up to power-off; written to one or more files.
- **Reader** — software that interprets or validates a file.
- **Tick** — the unit of the device timer; its length is given by `$TICK`.
- **Calendar RTC** — an RTC that holds the absolute time as Unix time.
- **Stopwatch RTC** — an RTC that counts seconds from a reference stored in the EEPROM (see `$TIME`).

## Abbreviations

| Abbreviation | Meaning |
|---|---|
| ADC | Analog-to-digital converter |
| EEPROM | Electrically erasable programmable read-only memory |
| FW | Firmware |
| NaN | Not a Number |
| RTC | Real-time clock |
| SD | Secure Digital (memory card) |
| UTC | Coordinated Universal Time |

## Requirement wording

- **must** — mandatory.
- **may** — permitted, not mandatory.

## Notation

Message formats throughout this document are given as a literal `$MESSAGE_NAME` followed by comma-separated fields. The notation loosely follows EBNF (ISO/IEC 14977):

- `<field_name>` — a placeholder for a value; replaced by the actual field content in the record.
- `[...]` — the enclosed field, together with its leading comma, is optional and may be omitted from the end of the line. Nesting, e.g. `[,<b>[,<c>]]`, means `<c>` may only be present if `<b>` is.
- `(A|B)` — the field takes exactly one of the literal values listed, separated by `|`.
- `...` — the preceding field is repeated; the number of repetitions is given in the message description (e.g. `<histogram_0>,<histogram_1>,...,<histogram_n>` in `$STOP`).
- Text without `<>`, `[]` or `()` is literal and appears in the record unchanged (e.g. the `reg07=` prefix in `$RTCCHK`).
- A field left empty between two commas (e.g. `,,`) is present but its value is not known; this is distinct from a field omitted per `[...]`. Which fields may be empty, and how else "not available" is represented (`NaN` for floating-point fields, or omitting the whole message — see [General rules](#general-rules)), is stated for each field individually.

## Data types

Field types used in the message catalog. Ranges are defined with reserve for future devices; a device may use only part of a range.

| Type | Range | Written as |
|---|---|---|
| U16 | 0–65 535 | decimal digits, no sign, no leading zeros |
| U32 | 0–4 294 967 295 | decimal digits, no sign, no leading zeros |
| I32 | −2 147 483 648 – 2 147 483 647 | optional `-`, then decimal digits, no leading zeros |
| DEC | at most 300 characters | optional `-`, decimal digits, optionally `.` followed by decimal digits; no exponent, no `+`. A value the device cannot provide is written as `NaN`. |
| HEX | per field | lowercase hexadecimal digits `0`–`9`, `a`–`f` |
| TEXT | per field | characters permitted by [File Structure](#file-structure) |


# Version 1

{: .note }
This version was also referred to as "Version 1.5" in some deployments. The two labels described an identical wire format — there was never a data-level distinction between them — so the documentation has been consolidated here.

## File Structure

The output file is composed of various data messages, each representing different types of data captured by the detector. The structure of these lines is adopted from [NMEA 0183](https://en.wikipedia.org/wiki/NMEA_0183). The messages are stored in a file or transmitted on the UART port. Typically, the baud rate used is 9600 with 8 databits and one stop bit. Handshake is not applicable. 

## Example:
```
$DOS,AIRDOS04X,1.0.0--Release,0,9b5cf9571b15da03150b04ad0d93ecf7ad6cea92,Release,1290c00806a200922449a000a00000c6
$DIG,BATDATUNIT01B,1290c00806a200925448a000a0000063,ffff
$ADC,USTSIPIN03A,1290c00806a200922449a000a00000c6,ffff
$HIST,0,12.3,1,255,255,255,103,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0
$HIST,1,22.28,6,255,255,255,106,2,0,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0
$HIST,2,32.54,197,255,255,255,195,53,33,24,14,11,9,4,8,6,4,3,2,3,2,1,1,1,0,1,1,1,1,2,0,1,0,2,1,0,0,0,1,1,0,0,0,0,0,1,0,0,1,0,0,0,1,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0
$HIST,3,42.79,3,255,255,255,110,0,0,0,0,0,0,0,0,0,0,0,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0
$HIST,4,53.5,4,255,255,255,102,1,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0
$HIST,5,63.32,3,255,255,255,95,2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0
$BATT,6,63.58,227,0,0,975,20.25
$HIST,6,73.63,1,255,255,255,107,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0
$HIST,7,83.87,1,255,255,255,136,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0
```

### Data format Identifier
Not implemented yet

### Detector Identifier
```
  $DOS,AIRDOS04X,1.0.0--Release,0,9b5cf9571b15da03150b04ad0d93ecf7ad6cea92,Release,1290c00806a200922449a000a00000c6
```
- **Format**: `$DOS, [DetectorModel], [FirmwareVersion], [Build number], [SerialNumber], [BuildUniqueId], [Build origin], [SN]`
- **Description**: Identifies the detector model, firmware version, a unique identifier for the device, user information, and session ID.

### Digital part identifier (applicable for AIRDOS04)
```
$DIG,BATDATUNIT01B,1290c00806a200925448a000a0000063,ffff
```
- **Format**: `$DIG, [ModuleType], [SerialNumber], [Reserved]`
- **Description**: 

### Analogue part identifies (applicable for AIRDOS04)
```
$ADC,USTSIPIN03A,1290c00806a200922449a000a00000c6,ffff
```
- **Format**: `$ADC, [SensorType], [SerialNumber], [Reserved]`
- **Description**: 

### Histogram Data
```
$HIST,4,53.5,4,255,255,255,102,1,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0
```
- **Format**: `$HIST, [message number], [time], [detected particles], [], [], [], [], [Channel 1], [Channel 2], ...`
- **Description**: A detailed histogram representing the distribution of detected events or measurements across various categories.

### Battery status
```
$BATT,6,63.58,227,0,0,975,20.25
```

### Environment data

Information about temperature, humidity, and pressure.

```
$ENV,30,309.39,23.8,45.0,24.7,44.3,23.72,984.81
```

# Version 2

Version 2 is used by AIRDOS04C and is specified in detail in [FW repository](https://github.com/UniversalScientificTechnologies/AIRDOS04/blob/AIRDOS04C/fw/AIRDOS04/OUTPUT_FORMAT.md)).

Each record is one text line. Data lines start with `$` and use comma-separated fields. Lines are terminated by newline (`\n`); within measurement blocks the firmware may use `\r\n`.

## Message types

The v2 stream can be viewed as three groups:

- **Header messages**: emitted once at the beginning of the file. They describe *what device produced the data*.
- **Particle messages**: the actual radiation/event payload, emitted repeatedly in fixed integration blocks (uasually 10 s). A block starts with `$START`, may contain many `$E` lines, and ends with `$STOP`.
- **Status messages**: emitted on a lower frequenty (or on specific service events). They carry environmental readings, battery health, and RTC/service state.


## Header messages

### `$DOS` — device identification
- **When**: once at the beginning of the file (startup header)
- **Meaning**: identifies device type (`AIRDOS04C`), firmware/build info and Git hash, and the analog board serial number.
- **Format**:

```
$DOS,<TYPE>,<FWversion>,0,<git_hash>,<build_type>,<serial_analog_16B_hex>
```

- **Example**:

```
$DOS,AIRDOS04C,2.0.0-0-User,0,a3e23b543a4de5dc3d057462bb6109bf3db0b44b,User,0910410874100851c40ba080a08000b3
```

### `$DIG` — digital module identification
- **When**: once at the beginning of the file
- **Meaning**: identifies the digital board (`BATDATUNIT01B`), its serial number and configuration bytes.
- **Format**:

```
$DIG,<DIGTYPE>,<serial_digital_16B_hex>,<DIG_EEPROM>
```

- **Example**:

```
$DIG,BATDATUNIT01B,09104108741008520c0ca080a080005e,ffff
```

### `$ADC` — analog module identification
- **When**: once at the beginning of the file
- **Meaning**: identifies the analog front-end board (`USTSIPIN03A`), its serial number and ADC configuration bytes.
- **Format**:

```
$ADC,<ADC_NAME>,<serial_analog_16B_hex>,<ADC_EEPROM>
```

- **Example**:

```
$ADC,USTSIPIN03A,0910410874100851c40ba080a08000b3,ffff
```

### `$BATP` — battery presence
- **When**: once at the beginning of the file
- **Meaning**: reports whether a battery was detected at startup and the measured battery voltage (mV).
- **Format**:

```
$BATP,<present>,<battery_mV>
```

- **Example**:

```
$BATP,1,4150
```

### `$TIME` — time and synchronization info
- **When**: potentially multiple times per file; its position within the file is not guaranteed to be at the beginning.
- **Meaning**: provides RTC seconds, last synchronization time stored in EEPROM, computed current Unix time, sync age, and human-readable UTC timestamp.
- **Format**:

```
$TIME,<rtc_seconds>,<eeprom_sync_time>,<current_unix_time>,<sync_age>,<YYYY-MM-DD HH:MM:SS>
```

- **Example**:

```
$TIME,1234567,1708862400,1708863634,0,2025-02-25 14:30:34
```


## Particle messages (integration block)

### `$START` — start of integration block
- **When**: every integration period (nominally every 10 s)
- **Meaning**: marks start of a measurement block (integration window) and provides the reference system timer value.
- **Format**:

```
$START,<count>,<event_time_0>
```

- **Example**:

```
$START,0,1
```

### `$E` — single above-threshold event
- **When**: zero or more times within an integration block
- **Meaning**: one line per event above threshold, with event time (in ticks) and the raw ADC value (used to classify the event).
- **Format**:

```
$E,<long_event_time>,<event_channel>
```

- **Example**:

```
$E,488,24
```

### `$STOP` — end of integration block
- **When**: every integration period, after the block’s `$E` lines
- **Meaning**: closes the measurement block and reports end time, total number of above-threshold events, and the histogram counters for energy channels.
- **Format**:

```
$STOP,<count>,<tm>.<tm_s100>,<systime>,<events_count>,<histogram_0>,<histogram_1>,...,<histogram_n>
```

- **Note**: the number of histogram channels (`<histogram_0>` through `<histogram_n>`) may vary between devices/configurations.

- **Example**:

```
$STOP,179,4275399681.0,31359,427,19373,11,24,7
```

## Status messages

### `$RTCCHK` — RTC check / initialization status
- **When**: on RTC check / (re)initialization (typically at startup or when needed)
- **Meaning**: records whether RTC settings were OK or had to be initialized, including selected RTC register values.
- **Format**:

```
$RTCCHK,<tm>.<tm_s100>,(OK|INIT),reg07=0x<hex>,reg28=0x<hex>
```

- **Example**:

```
$RTCCHK,1234567.50,OK,reg07=0x00,reg28=0x97
```

### `$ENV` — environmental sensors
- **When**: periodically (every ~5 minutes)
- **Meaning**: temperatures and humidities from two sensors plus temperature and pressure from a pressure sensor.
- **Format**:

```
$ENV,<count>,<tm>.<tm_s100>,<T1>,<H1>,<T2>,<H2>,<T_MS5611>,<P_MS5611>
```

- **Example**:

```
$ENV,179,4275399683.0,29.1,44.0,27.5,45.5,29.31,989.05
```

### `$BATT` — battery status
- **When**: periodically (every ~30 minutes)
- **Meaning**: battery voltage/current/capacity/temperature values from the fuel gauge.
- **Format**:

```
$BATT,<count>,<tm>.<tm_s100>,<voltage_mV>,<current_mA>,<remaining_mAh>,<full_charge_mAh>,<temperature_C>
```

- **Example**:

```
$BATT,720,12345.50,4150,-120,1800,2000,25.3
```

## Notes
- Lines starting with `#` are debug/service messages (typically on the debug serial port) and are not part of the data stream.


# Version 2.1

Version 2.1 extends [Version 2](#version-2). Every message defined in Version 2 keeps its syntax and meaning unless this section states otherwise; only new and changed messages are described here.

A Version 2.1 file is identified by the `$DATAFORMAT,VERSION_2.1` line. Readers select the parser by `$DATAFORMAT`; the device type in `$DOS` is only a fallback heuristic for files without it.

## Scope

This version of the format specifies the data written by SPACEDOS04 (firmware version 2.1 and later) to its SD card log file. SD card storage is the main data output of SPACEDOS04.

## File Structure

- **Encoding**: US-ASCII. A line consists only of printable characters `0x20`–`0x7E`; `\r` (`0x0D`) and `\n` (`0x0A`) occur only as the line terminator. Control characters, `0x7F` and bytes `0x80`–`0xFF` (including any UTF-8 sequence) do not occur.
- **Line endings**: `\n` or `\r\n` (see [General rules](#general-rules)).
- **Reserved characters**: `$`, `#` and `!` occur only as the first character of a line, where they identify the line type (see [General rules](#general-rules)). They do not occur anywhere else in the line.
- **Field separator**: `,` separates fields; a field value does not contain a comma, unless the field is explicitly documented to run to the end of the line (only `<text>` in `$ERROR` does).
- **Header and measurement block order**: the file begins with a single, uninterrupted block of header messages, then continues with an uninterrupted stream of particle and status messages for the remainder of the file. `$DIG_NAME`/`$ADC_NAME`, where present, immediately follow `$DIG`/`$ADC`. The relative order of the other header messages is otherwise not defined.
- **Sessions**: a measurement session (device start-up to power-off) is written to one or more files. Each file belongs to exactly one session and starts with its own complete header block; header messages are not repeated within a file. A device restart always begins a new file. Whether and when a running session continues in a new file depends on the device firmware.

## Maximum message length

- A line, including its line terminator, is at most 524 288 bytes (512 KiB) long. Readers must accept lines up to this length.
- `$STOP` carries at most 65 536 histogram fields; each histogram value is in the range 0–65 535.
- `<text>` in `$ERROR` is at most 512 characters long.

## Changes against Version 2

- New header message `$DATAFORMAT` naming the data format.
- New header messages `$CHAN`, `$DIODE`, `$ERNG`, `$ITIME`, `$CALIB` carrying the parameters needed to interpret the data.
- New header messages `$DIG_NAME` and `$ADC_NAME` carrying the human-readable names stored in the board EEPROMs.
- `$DOS`: the 4th field is reserved.
- `$DIG` is optional; the configuration field has a fixed width.
- New header message `$TICK` giving the length of the device timer tick.
- `$TIME`: classified as a status message; meaning of the fields stated precisely, including devices with a calendar RTC and an invalid device time; `<sync_age>` is empty when unknown.
- `$RTCCHK`: emitted in every file; `INIT` marks an invalid (relative only) device time.
- `$START`, `$E`, `$STOP`: timer values defined; `<long_event_time>` counts from the start of the block.
- `$E`: optional second channel value.
- `$STOP`: relation of `<events_count>` to the number of `$E` lines clarified.
- `$ENV`: the line always carries all fields, missing values are `NaN`.
- New message `$ERROR` with a free-text description of an error detected by the device.
- Handling of incomplete and invalid data defined.
- Maximum line length, histogram size and `$ERROR` text length defined.
- Data types defined; every message lists its fields with type, unit and range.

## General rules

- Line syntax is the same as in Version 2. Lines are terminated by `\n` or `\r\n`.
- Lines starting with `#` are debug/service messages and are not part of the data stream.
- Lines starting with `!` are reserved for commands sent **to** the device and never appear in the data stream.
- Readers must ignore `$` messages they do not know. This allows new messages to be added without a new format version.
- A known message may carry more fields than documented here if a later revision appended new ones; readers must ignore trailing fields they do not recognize (see [Versioning and compatibility](#versioning-and-compatibility)).
- A floating point value that the device cannot provide is written as `NaN`. Integer fields never carry `NaN`; if an integer value is not available, the whole message is omitted.
- Header messages are emitted once at the beginning of every file. `$DATAFORMAT` and `$DOS` are mandatory, all other header messages are optional.

## Block continuity

The `<count>` field present in `$START`, `$STOP`, `$ENV` and `$BATT` is a single block index shared by all of them. It increases by exactly 1 per integration block; `$START` and `$STOP` of one block carry the same `<count>`. `$ENV` and `$BATT` follow the `$STOP` of a block and carry that block's `<count>`.

`<count>` is not persistent: it restarts at power-up and may restart during a session. When and to which value it restarts depends on the device firmware. Apart from such a restart, consecutive blocks differ by exactly 1; any other step means that one or more blocks, and any status messages tied to them, were not recorded. `<count>` is the reliable way to confirm that no block was skipped (the actual spacing between blocks is only nominally `$ITIME`).

## Incomplete and invalid data

A file may end at any point, e.g. on power loss or a storage failure. Everything written up to that point is valid; readers apply the following rules and process the rest of the file normally:

- A line without a line terminator is discarded.
- A line whose fields do not match the definition of its message is discarded.
- A block is complete only if it has both a valid `$START` and a valid `$STOP`. An incomplete block is discarded together with its `$E` lines.

## Header messages

### `$DATAFORMAT` — data format name
- **When**: once at the beginning of the file
- **Meaning**: names the data format of the file explicitly, so a reader can select the matching parser without inferring it from the other header lines.
- **Format**:

```
$DATAFORMAT,<format_name>
```

<details markdown="1">
<summary>Fields</summary>

| Field | Type | Unit | Description |
|---|---|---|---|
| `<format_name>` | TEXT, up to 64 characters | — | Name of the data format; `VERSION_2.1` for this version. |

</details>

- **Example**:

```
$DATAFORMAT,VERSION_2.1
```

### `$DOS` — device identification (changed)
- **Format**: unchanged against Version 2.

```
$DOS,<TYPE>,<FWversion>,0,<git_hash>,<build_type>,<serial_16B_hex>
```

- **Change**: the 4th field is reserved. Devices write `0`, readers ignore its value.

<details markdown="1">
<summary>Fields</summary>

| Field | Type | Unit | Description |
|---|---|---|---|
| `<TYPE>` | TEXT, up to 64 characters | — | Device type, e.g. `AIRDOS04C`. |
| `<FWversion>` | TEXT, up to 64 characters | — | Firmware version. |
| `0` | literal | — | Reserved. |
| `<git_hash>` | TEXT, up to 64 characters | — | Git commit of the firmware build. |
| `<build_type>` | TEXT, up to 64 characters | — | Build type, e.g. `Release`, `User`. |
| `<serial_16B_hex>` | HEX, exactly 32 digits | — | Device serial number (16 bytes), see the note below. |

</details>

- **Note**: the device is identified by its analog (detector) board: `<TYPE>` and `<serial_16B_hex>` both come from the analog board if the device has one, otherwise from its only board. Replacing other boards (e.g. the digital board of AIRDOS04) does not change the device identity.

### `$DIG` — digital module identification (changed)
- **Format**: unchanged against Version 2.

```
$DIG,<DIGTYPE>,<serial_digital_16B_hex>,<DIG_EEPROM>
```

- **Change**: optional. Present only if the device has a separate digital board with its own identification.
- **Change**: `<DIG_EEPROM>` is always 4 hex digits — the first two bytes of the configuration record stored in the board EEPROM, in stored order. `ffff` means that no record is stored.

<details markdown="1">
<summary>Fields</summary>

| Field | Type | Unit | Description |
|---|---|---|---|
| `<DIGTYPE>` | TEXT, up to 64 characters | — | Digital board type, e.g. `BATDATUNIT01B`. |
| `<serial_digital_16B_hex>` | HEX, exactly 32 digits | — | Digital board serial number (16 bytes). |
| `<DIG_EEPROM>` | HEX, exactly 4 digits | — | First two bytes of the EEPROM configuration record, see above. |

</details>

### `$DIG_NAME` — digital module name
- **When**: once at the beginning of the file, right after `$DIG`; only if `$DIG` is present
- **Meaning**: the human-readable identifier stored in the configuration record of the digital board EEPROM (`device_identifier`, typically the name printed on the device enclosure). Up to 24 printable ASCII characters, none of `,` `$` `#` `!`. Empty if no record is stored.
- **Format**:

```
$DIG_NAME,<device_identifier>
```

<details markdown="1">
<summary>Fields</summary>

| Field | Type | Unit | Description |
|---|---|---|---|
| `<device_identifier>` | TEXT, up to 24 characters | — | Name stored in the digital board EEPROM, see above. May be empty. |

</details>

- **Example**:

```
$DIG_NAME,OTTER
```

### `$ADC` — analog module identification (changed)
- **Format**: unchanged against Version 2.

```
$ADC,<ADC_NAME>,<serial_analog_16B_hex>,<ADC_EEPROM>
```

- **Change**: `<ADC_EEPROM>` follows the same rule as `<DIG_EEPROM>`.

<details markdown="1">
<summary>Fields</summary>

| Field | Type | Unit | Description |
|---|---|---|---|
| `<ADC_NAME>` | TEXT, up to 64 characters | — | Analog board type, e.g. `USTSIPIN03A`. |
| `<serial_analog_16B_hex>` | HEX, exactly 32 digits | — | Analog board serial number (16 bytes). |
| `<ADC_EEPROM>` | HEX, exactly 4 digits | — | First two bytes of the EEPROM configuration record, see `$DIG`. |

</details>

### `$ADC_NAME` — analog module name
- **When**: once at the beginning of the file, right after `$ADC`; only if `$ADC` is present
- **Meaning**: the same as `$DIG_NAME`, taken from the analog board EEPROM.
- **Format**:

```
$ADC_NAME,<device_identifier>
```

<details markdown="1">
<summary>Fields</summary>

| Field | Type | Unit | Description |
|---|---|---|---|
| `<device_identifier>` | TEXT, up to 24 characters | — | Name stored in the analog board EEPROM. May be empty. |

</details>

- **Example**:

```
$ADC_NAME,OTTER
```

### `$BATP` — battery presence (clarified)
- **Format**: unchanged against Version 2.

```
$BATP,<present>,<battery_mV>
```

<details markdown="1">
<summary>Fields</summary>

| Field | Type | Unit | Description |
|---|---|---|---|
| `<present>` | `0` or `1` | — | `1` if a battery was detected at start-up, `0` otherwise. |
| `<battery_mV>` | U32 | mV | Battery voltage measured at start-up; `0` if `<present>` is `0`. |

</details>

- **Example**:

```
$BATP,1,4150
```

### `$CHAN` — spectrum channel configuration
- **When**: once at the beginning of the file
- **Meaning**: the total number of ADC channels (the channel range of both the `$STOP` histogram and the `$E` events — **not** the length of the `$STOP` histogram) and the default number of leading channels that contain noise and are excluded from the evaluation.
- **Format**:

```
$CHAN,<num_channels>,<num_noise_channels_default>
```

<details markdown="1">
<summary>Fields</summary>

| Field | Type | Unit | Description |
|---|---|---|---|
| `<num_channels>` | U32, 1–65 536 | ADC channels | Total number of ADC channels. |
| `<num_noise_channels_default>` | U32 | ADC channels | Number of leading noise channels; lower than `<num_channels>`. |

</details>

- **Example**:

```
$CHAN,65536,4
```

### `$DIODE` — silicon chip geometry
- **When**: once at the beginning of the file
- **Meaning**: the sensitive area of the silicon chip (cm²) and the depletion layer thickness (cm).
- **Format**:

```
$DIODE,<si_chip_area_cm2>,<si_chip_thickness_cm>
```

<details markdown="1">
<summary>Fields</summary>

| Field | Type | Unit | Description |
|---|---|---|---|
| `<si_chip_area_cm2>` | DEC, > 0 | cm² | Sensitive area of the silicon chip. |
| `<si_chip_thickness_cm>` | DEC, > 0 | cm | Depletion layer thickness. |

</details>

- **Example**:

```
$DIODE,0.25,0.03
```

### `$ERNG` — energy range
- **When**: once at the beginning of the file
- **Meaning**: the lower and upper bound of the deposited energy range the detector measures (MeV). Either bound may be left empty if it is not known.
- **Format**:

```
$ERNG,<energy_range_min_mev>,<energy_range_max_mev>
```

<details markdown="1">
<summary>Fields</summary>

| Field | Type | Unit | Description |
|---|---|---|---|
| `<energy_range_min_mev>` | DEC, > 0 | MeV | Lower bound of the energy range. May be empty. |
| `<energy_range_max_mev>` | DEC, > 0 | MeV | Upper bound of the energy range; greater than the lower bound. May be empty. |

</details>

- **Example**:

```
$ERNG,0.05,20
$ERNG,0.05,
```

### `$ITIME` — integration period
- **When**: once at the beginning of the file
- **Meaning**: the nominal length of one integration block (seconds), i.e. the nominal time between consecutive `$START`/`$STOP` blocks. NaN when integration block has variable length
- **Format**:

```
$ITIME,<integration_period_s>
```

<details markdown="1">
<summary>Fields</summary>

| Field | Type | Unit | Description |
|---|---|---|---|
| `<integration_period_s>` | DEC, > 0 | s | Nominal length of one integration block; `NaN` if the block length is variable. |

</details>

- **Example**:

```
$ITIME,10
```

### `$TICK` — timer tick length
- **When**: once at the beginning of the file; optional
- **Meaning**: the length of one tick of the device timer (seconds). Applies to `<event_time_0>` in `$START`, `<long_event_time>` in `$E` and `<systime>` in `$STOP`.
- **Format**:

```
$TICK,<tick_length_s>
```

<details markdown="1">
<summary>Fields</summary>

| Field | Type | Unit | Description |
|---|---|---|---|
| `<tick_length_s>` | DEC, > 0 | s | Length of one tick of the device timer. |

</details>

- **Example**:

```
$TICK,0.000128
```

### `$CALIB` — energy calibration
- **When**: once at the beginning of the file
- **Meaning**: the default energy calibration coefficients stored in the device EEPROM. `coef2` is optional and defaults to `0`. `calibration_version` is an optional identifier of the calibration (a version number, calibration type or the Unix time of the calibration); it may only be present together with `coef2`.
- **Format**:

```
$CALIB,<coef0>,<coef1>[,<coef2>[,<calibration_version>]]
```

<details markdown="1">
<summary>Fields</summary>

| Field | Type | Unit | Description |
|---|---|---|---|
| `<coef0>` | DEC | — | Calibration coefficient 0. |
| `<coef1>` | DEC | — | Calibration coefficient 1. |
| `<coef2>` | DEC | — | Optional calibration coefficient 2; `0` if absent. |
| `<calibration_version>` | TEXT, up to 64 characters | — | Optional identifier of the calibration. Present only together with `<coef2>`. |

</details>

How the coefficients are applied depends on the calibration methodology of the evaluating software. For an example interpretation see the DOSPORTAL [Visualization methodology](/dosportal/visualisation).

- **Example**:

```
$CALIB,0.01,0.002,0.0
$CALIB,0.01,0.002,0.0,1789689600
```

## Particle messages (integration block)

### `$START` — start of integration block (clarified)
- **Format**: unchanged against Version 2.

```
$START,<count>,<event_time_0>
```

<details markdown="1">
<summary>Fields</summary>

| Field | Type | Unit | Description |
|---|---|---|---|
| `<count>` | U32 | — | Block index (see [Block continuity](#block-continuity)). |
| `<event_time_0>` | U32 | tick | Raw value of the device timer at the start of the block (see `$TICK`). Informative only. |

</details>

- **Example**:

```
$START,179,31012
```

### `$E` — single above-threshold event (changed)
- **Format**:

```
$E,<long_event_time>,<event_channel>[,<event_channel_2>]
```

- **Change**: optional `<event_channel_2>`.
- **Change**: `<long_event_time>` is counted from the start of the block.

<details markdown="1">
<summary>Fields</summary>

| Field | Type | Unit | Description |
|---|---|---|---|
| `<long_event_time>` | U32 | tick | Time of the event, counted from the start of the block (see `$TICK`). |
| `<event_channel>` | U16 | ADC channel | ADC value of the event. Never lower than the number of histogram fields in `$STOP` — an event goes either to the histogram or to an `$E` line, never to both. |
| `<event_channel_2>` | U16 | — | Optional. A second ADC value of the same event. |

</details>

- **Example**:

```
$E,2514,170,108
```

### `$STOP` — end of integration block (clarified)
- **Format**: unchanged against Version 2.

```
$STOP,<count>,<tm>.<tm_s100>,<systime>,<events_count>,<histogram_0>,<histogram_1>,...,<histogram_n>
```

<details markdown="1">
<summary>Fields</summary>

| Field | Type | Unit | Description |
|---|---|---|---|
| `<count>` | U32 | — | Block index; equal to `<count>` of the block's `$START`. |
| `<tm>` | U32 | s | Device RTC time at the end of the block (see `$TIME`). |
| `<tm_s100>` | U16, 0–99 | 0.01 s | Hundredths of a second added to `<tm>`. Written as an integer. |
| `<systime>` | U32 | tick | Raw value of the device timer at the end of the block (see `$TICK`). Informative only. |
| `<events_count>` | U16 | events | Number of above-threshold events in the block. May be higher than the number of `$E` lines of the block if the device's event buffer overflowed. |
| `<histogram_0>` … `<histogram_n>` | U16 | events | Number of events in ADC channel. |

</details>

- **Example**:

```
$STOP,179,1789729204.0,31359,427,19373,11,24,7
```

## Status messages

### `$TIME` — time and synchronization info (changed)
- **When**: at any position in the file, any number of times (e.g. after the clock is (re)synchronized).
- **Change**: classified as a status message; in Version 2 it was listed among the header messages.
- **Format**: unchanged against Version 2.

```
$TIME,<rtc_seconds>,<eeprom_sync_time>,<current_unix_time>,<sync_age>,<YYYY-MM-DD HH:MM:SS>
```

<details markdown="1">
<summary>Fields</summary>

| Field | Type | Unit | Description |
|---|---|---|---|
| `<rtc_seconds>` | U32 | s | The device RTC counter. |
| `<eeprom_sync_time>` | U32 | s (Unix time) | The reference from the synchronization record in the EEPROM (`rtc_history[0].reference_timestamp`): the Unix time at which the device RTC counter was `0`. |
| `<current_unix_time>` | U32 | s (Unix time) | `<eeprom_sync_time>` + `<rtc_seconds>`. |
| `<sync_age>` | U32 | s | Seconds since the clock was last set or synchronized (`<rtc_seconds>` − `rtc_history[0].rtc_value_at_reference_timestamp`). **Empty** if the device has no valid synchronization record. |
| `<YYYY-MM-DD HH:MM:SS>` | TEXT | — | `<current_unix_time>` as a UTC date and time; exactly 19 characters, fields zero-padded (see ISO 8601 in [Normative references](#normative-references)). |

</details>

- **Devices with a calendar RTC** (the RTC holds the absolute time): the counter is the Unix time itself, so `<rtc_seconds>` equals `<current_unix_time>` and `<eeprom_sync_time>` is `0`. Consequently the time stamps `<tm>` in `$STOP`, `$ENV`, `$BATT` and `$RTCCHK` are Unix time directly.
- **Invalid device time** (e.g. the RTC lost power and was not set since): the RTC keeps counting from its reset default — typically `2000-01-01 00:00:00`, not necessarily the Unix epoch. The device reports this running value unchanged, so the time stamps stay monotonic and the relative timing within the file is preserved; only the absolute time is unknown. The invalid state is signalled by `INIT` in `$RTCCHK`. `<sync_age>` is empty. A reader may re-anchor such a file to an externally known start time.
- All times are UTC.

- **Example** (calendar RTC, last set 2026-09-18 10:00:00):

```
$TIME,1789729200,0,1789729200,3600,2026-09-18 11:00:00
```

- **Example** (stopwatch RTC, counter zero at 2024-02-25 12:00:00, last synchronized 10 minutes ago):

```
$TIME,1234567,1708862400,1710096967,600,2024-03-10 18:56:07
```

- **Example** (invalid time, RTC counting from its default of 2000-01-01, 5 minutes after power-up):

```
$TIME,946685100,0,946685100,,2000-01-01 00:05:00
```

### `$RTCCHK` — RTC check / initialization status (clarified)
- **Format**: unchanged against Version 2.

```
$RTCCHK,<tm>.<tm_s100>,(OK|INIT),reg07=0x<hex>,reg28=0x<hex>
```

- **Change**: emitted at the beginning of every file, so each file states whether its time is valid.
- **Note**: the meaning of the state is generalized to both RTC modes:
  - `INIT` — the RTC does not continue from a known time reference: it was reset by the firmware (stopwatch-mode devices) or it lost power and counts from its default value (calendar-mode devices). All time stamps in the file are relative only (see `$TIME`).
  - `OK` — the RTC continues from a known reference: for calendar-mode devices the RTC itself holds the absolute time; for stopwatch-mode devices the reference is the synchronization record reported in `$TIME`.
<details markdown="1">
<summary>Fields</summary>

| Field | Type | Unit | Description |
|---|---|---|---|
| `<tm>` | U32 | s | Device RTC time (see `$TIME`). |
| `<tm_s100>` | U16, 0–99 | 0.01 s | Hundredths of a second added to `<tm>`; written as an integer (see `$STOP`). |
| `OK` or `INIT` | literal | — | RTC state, see above. |
| `reg07=0x<hex>`, `reg28=0x<hex>` | HEX | — | RTC register values, two digits each. Informative and device specific. |

</details>

- **Example** (invalid time):

```
$RTCCHK,946684802.0,INIT,reg07=0x00,reg28=0x00
```

### `$ENV` — environmental sensors (changed)
- **Format**: unchanged against Version 2.

```
$ENV,<count>,<tm>.<tm_s100>,<T1>,<H1>,<T2>,<H2>,<T_MS5611>,<P_MS5611>
```

- **Change**: the line always carries all eight fields. Values of sensors the device does not have are `NaN`; the line is never shortened.

<details markdown="1">
<summary>Fields</summary>

| Field | Type | Unit | Description |
|---|---|---|---|
| `<count>` | U32 | — | Index of the block this message follows (see [Block continuity](#block-continuity)). |
| `<tm>` | U32 | s | Device RTC time (see `$TIME`). |
| `<tm_s100>` | U16, 0–99 | 0.01 s | Hundredths of a second added to `<tm>`; written as an integer (see `$STOP`). |
| `<T1>` | DEC | °C | Temperature, first temperature/humidity sensor. |
| `<H1>` | DEC | % RH | Relative humidity, first temperature/humidity sensor. |
| `<T2>` | DEC | °C | Temperature, second temperature/humidity sensor. |
| `<H2>` | DEC | % RH | Relative humidity, second temperature/humidity sensor. |
| `<T_MS5611>` | DEC | °C | Temperature, pressure sensor. |
| `<P_MS5611>` | DEC | hPa | Atmospheric pressure, pressure sensor. |

</details>

- **Example** (device with a single temperature/humidity sensor):

```
$ENV,179,1789729204.0,23.8,45.0,NaN,NaN,NaN,NaN
```

### `$BATT` — battery status (clarified)
- **Format**: unchanged against Version 2.

```
$BATT,<count>,<tm>.<tm_s100>,<voltage_mV>,<current_mA>,<remaining_mAh>,<full_charge_mAh>,<temperature_C>
```

<details markdown="1">
<summary>Fields</summary>

| Field | Type | Unit | Description |
|---|---|---|---|
| `<count>` | U32 | — | Index of the block this message follows (see [Block continuity](#block-continuity)). |
| `<tm>` | U32 | s | Device RTC time (see `$TIME`). |
| `<tm_s100>` | U16, 0–99 | 0.01 s | Hundredths of a second added to `<tm>`; written as an integer (see `$STOP`). |
| `<voltage_mV>` | U32 | mV | Battery voltage. |
| `<current_mA>` | I32 | mA | Battery current; positive when charging, negative when discharging. |
| `<remaining_mAh>` | U32 | mAh | Remaining battery capacity. |
| `<full_charge_mAh>` | U32 | mAh | Battery capacity when fully charged. |
| `<temperature_C>` | DEC | °C | Battery temperature. |

</details>

- **Example**:

```
$BATT,180,1789729214.0,4150,-120,1800,2000,25.3
```

### `$ERROR` — error detected by the device
- **When**: whenever the device detects an error that matters for the data; anywhere in the file, any number of times
- **Meaning**: a human-readable description of the error. Readers show it to the user and do not interpret it; it has no effect on how the other messages of the file are interpreted. The text reaches to the end of the line and may contain commas.
- **Note**: debug and service output stays on `#` lines; `$ERROR` is for errors the user of the data should see.
- **Format**:

```
$ERROR,<text>
```

<details markdown="1">
<summary>Fields</summary>

| Field | Type | Unit | Description |
|---|---|---|---|
| `<text>` | TEXT | — | Error description, up to 512 characters. Runs to the end of the line and may contain commas. |

</details>

- **Example**:

```
$ERROR,EEPROM record version 1, firmware expects 2 - measurement metadata not available
```
