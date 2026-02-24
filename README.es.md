# Pipex

Proyecto de la escuela 42 que replica el comportamiento del operador de tubería
(`|`) del shell. Toma dos comandos, los conecta mediante una tubería, lee desde
un fichero de entrada y escribe el resultado final en un fichero de salida.
Equivale a ejecutar:

```
< infile cmd1 | cmd2 > outfile
```

## Autor

ruortiz-

## Lo que aprenderás / Habilidades adquiridas

- Gestión de procesos en Unix: `fork`, `execve`, `waitpid`
- Comunicación entre procesos (IPC) mediante tuberías
- Manipulación de descriptores de fichero con `dup2`, `open` y `close`
- Resolución del PATH para localizar ejecutables en tiempo de ejecución
- Gestión de memoria en C (reserva, liberación y prevención de fugas)
- Automatización de compilación con Makefiles

## Compilación y ejecución

**Compilar:**

```bash
make
```

**Eliminar ficheros objeto:**

```bash
make clean
```

**Limpieza completa (objetos + binario):**

```bash
make fclean
```

**Recompilar desde cero:**

```bash
make re
```

## Uso

```
./pipex infile cmd1 cmd2 outfile
```

| Argumento | Descripción                                    |
|-----------|------------------------------------------------|
| `infile`  | Ruta al fichero de entrada                     |
| `cmd1`    | Primer comando (lee desde `infile`)            |
| `cmd2`    | Segundo comando (lee la salida de `cmd1`)      |
| `outfile` | Ruta al fichero de salida                      |

**Ejemplo** — contar líneas en `input.txt` que contengan "hello":

```bash
./pipex input.txt "grep hello" "wc -l" output.txt
```

Equivale a:

```bash
< input.txt grep hello | wc -l > output.txt
```

## Estructura del proyecto

| Fichero         | Descripción                                                   |
|-----------------|---------------------------------------------------------------|
| `pipex.c`       | Punto de entrada: validación de argumentos, tuberías y forks  |
| `child.c`       | Lógica del primer y segundo proceso hijo                      |
| `utils.c`       | Ejecución de comandos, resolución del PATH, utilidades        |
| `check_error.c` | Inspección del estado de salida tras la ejecución del hijo    |
| `pipex.h`       | Cabecera: includes, macros y prototipos de funciones          |
| `libft/`        | Biblioteca C propia utilizada en todo el proyecto             |
| `Makefile`      | Reglas de compilación (`all`, `clean`, `fclean`, `re`)        |
