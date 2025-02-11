# KMyacc Documentation

## Introduction

KMyacc is a tool similar to yacc and bison, designed for LALR(1) parsing. It supports generating parsers in various programming languages such as C, Java, JavaScript, and Perl.

This is a fork of https://github.com/Kray-G/kmyacc, which is a fork of the original KMyacc project by MORI Koichiro.

## Features

## Installation

To install KMyacc, follow these steps:

1. Download the source code from [kmyacc-4.1.4.tar.gz](kmyacc-4.1.4.tar.gz).
2. Extract the archive using the following command:
   ```bash
   gzip -d kmyacc-4.1.4.tar.gz | tar xvf -
   ```
3. Navigate to the extracted directory `kmyacc-4.1.4`.
4. Modify the `Makefile` to set the installation paths:
   ```makefile
   BIN = /usr/local/bin
   PARLIB = /usr/local/lib
   ```
5. Compile and install KMyacc:
   ```bash
   make
   make install
   ```

## Usage

KMyacc can be invoked with the following syntax:

```bash
kmyacc [ -dvltani ] [ -b <i>X</i> ] [ -p <i>XX</i> ] [ -m <i>MODEL</i> ] [ -L <i>LANG</i> ] <i>grammarfile</i>
```

### Options

- `-d`: Generate a header file `y.tab.h` with definitions for `YYSTYPE` and token values.
- `-v`: Generate a verbose output file `y.output` containing the LR(0) state transitions.
- `-l`: Do not include `#line` directives in the generated C code.
- `-t`: Enable debugging output. For C, you may also need to define `YYDEBUG`.
- `-a`: Enable additional error recovery functions.
- `-b <i>X</i>`: Use `<i>X</i>.tab.c` and `<i>X</i>.output` as the output filenames instead of `y.tab.c` and `y.output`.
- `-p <i>XX</i>`: Use `<i>XX</i>` as the prefix for generated symbols instead of `yy`.
- `-m <i>MODEL</i>`: Use a specific parser model located at `/usr/local/lib/kmyacc.<i>LANG</i>.parser`.
- `-L <i>LANG</i>`: Specify the target language (e.g., `c`, `java`, `javascript`, `perl`).
- `-n`: Do not generate semantic value variables in C.
- `-i`: Use symbolic names for semantic values (e.g., `$$`, `$1`, `$2`).

## Environment

| Name        | Meaning                                 |
| ----------- | --------------------------------------- |
| `KMYACCPAR` | Prototype file name. Same as -m option. |

## Differences between kmyacc and AT&T yacc

- Options `-b`, `-p`, `-a`, `-m`, `-L` added
- Bison's `%expect`, `%pure_parser` statement added
- Treat `//` as comment
- Following obsolete features deleted
  - literal tokens surrounded by `"`
  - `\left`, `\right` etc.
  - `%<`, `%>`, `%binary`, `%2`, `%0`, `%=`
- `YYBACKUP` macro not supported

## Grammar Syntax

KMyacc supports standard yacc grammar syntax with some extensions. Below is a comparison of KMyacc and yacc syntax:

| Directive          | Description                        | Differences in KMyacc |
| ------------------ | ---------------------------------- | --------------------- |
| `%token`           | Define a token                     | -                     |
| `%left`            | Define left-associative operators  | -                     |
| `%right`           | Define right-associative operators | -                     |
| `%nonassoc`        | Define non-associative operators   | -                     |
| `%{ ... %}`        | Include code                       | Java: `import`        |
| `%union`           | Define a union type                | C-specific            |
| `%type`            | Define types for non-terminals     | C: `%union`           |
| `%start`           | Define the start symbol            | -                     |
| `%expect <i>N</i>` | Expect `N` shift/reduce conflicts  | -                     |
| `%pure_parser`     | Generate a reentrant parser        | -                     |
| `$$, $1, $2...`    | Access semantic values             | Symbolic names        |

### Semantic Values

KMyacc allows accessing semantic values using symbolic names. For example:

```c
foo: bar '+' baz { foo = bar + baz; }
```

This is equivalent to:

```c
foo: bar '+' baz { $$ = $1 + $3; }
```

### Java Support

In Java, the parser is generated as a class. The class name is derived from the grammar file name. For example, `Foo.jy` will generate a class named `Foo`.

#### Example

```java
%type <Integer> expr

%%
expr : expr '+' expr  { $$ = new Integer($1.intValue() + $3.intValue()); }
```

### JavaScript Support

KMyacc can generate JavaScript parsers that can be embedded in HTML. The generated parser is a function `yyparse()`.

### Perl Support

KMyacc can generate Perl parsers. Semantic values are accessed using `$$`, `$1`, `$2`, etc.

## Custom Parser Templates

KMyacc allows customizing the parser template using the `-m` option. The template file should be located at `/usr/local/lib/kmyacc.<i>LANG</i>.parser`.

### Template Directives

- `$include`: Include external files.
- `$listvar`: List variables.
- `$TYPEOF`: Get the type of a variable.
- `$if`, `$ifnot`: Conditional inclusion.
- `$reduce`: Generate reduction code.
- `$meta`: Define meta-characters.
- `$semval`: Access semantic values.
- `$tailcode`: Include tail code.
- `$union`: Define a union type.
- `$tokenval`: Define token values.

### Example

```c
$semval($) yyval
$semval($,%t) yyval.%t
$semval(%n) YYASP(%n-%l)
$semval(%n,%t) YYASP(%n-%l).%t
```

## Conclusion

KMyacc is a powerful tool for generating parsers in multiple languages. It extends the functionality of traditional yacc and bison, providing additional features and flexibility.
