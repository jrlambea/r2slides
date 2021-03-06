@title[Introduction]

Reversing para newbies
<br>
![](src/logo.png)
<br>
con Radare2

---

@title[whoami]

### <span class="gold">$ whoami</span>

1. Curioso del reversing desde los 15 años.
2. Miembro de kUT hasta su fin (2003-04).
3. Sysadmin.
4. Dejo cosas a medias en inceptor.me y tengo un doppelgänger en Twitter @jr_lambea.
5. Eterno aprendiz.

---

@title[resume]

### <span class="gold">TL;DR</span>

* Reverse engineering (RE), wtf?!
* Procesadores y arquitecturas.
* ASM y opcodes.
* Estructura básica de ejecutables

---

@title[what's reverse engineering]

### <span class="gold">L33t me in motherf*cker!</span>

La RE se basa en el aprendizaje de funcionamiento de un mecanismo sin información previa. Luego puede ser usado para alterar ese funcionamiento o reproducirlo en otro sitio. Durante la historia el concepto de RE ha ido mutando según el uso que se le daba.

---

@title[what's reverse engineering]

* En los 80 los poke asaltaban las revistas de videojuegos.
* En los 90 nació el concepto de cracking, loaders, trainers, keygens, parches, unpackers... era y es un arte (scene). A finales de los 90 aparece el exploiting de corrupción de memoria.
* En los 2000 muerte de la scene, el concepto de Teams y la forma de compartir cambia, el conocimiento se diversifica, se centra el reversing para el exploiting.
* Actualmente exploiting y malware analysis.

---

@title[CPU]

### <span class="gold">Central processing unit</span>

El procesador se encarga de procesar los datos residentes en los diferentes tipos de soportes de memoria.

![](src/cpu.gif)

Pero cómo?

---

@title[processor parts]

### <span class="gold">Procesador</span>

* Unidad de control: Ejecuta el flujo del código.
* Unidad aritmetico-lógica: Realiza operaciones matemáticas (sumas, restas, xor...), cada procesador puede tener diferentes implementaciones para estas funciones.
* Registros: Elementos de almacenamiento. A la capacidad máxima de estos se les llama `word` definen los bits del procesador (8, 16, 32, 64), consecuentemente también el límite de direccionamiento.

---

@title[processor example]

### <span class="gold">Ejemplo sencillo</span>

Imaginemos un programa que pasándole un valor te devuelve el resultado de la suma con 16.

![CPU](src/CPU.flv)

---

@title[Registers]

|Intel16|Intelx32|Intelx64|Descripción|
|---|---|---|---|
|AX|EAX|RAX|Propósito general|
|BX|EBX|RBX|Propósito general|
|CX|ECX|RCX|Propósito general|
|DX|EDX|RDX|Propósito general|
|SP|ESP|RSP|Stack Pointer|
|BP|EBP|RBP|Base Pointer
|IP|EIP|RIP|Instruction Pointer|


---

@title[Registers Example]

### Registros
Ejemplo de nomenclaturas y relación con longitud.

```
0x1122334455667788
  ================ rax (64bits)
          ======== eax (32bits)
              ==== ax  (16bits)
              ==   ah  (8bits)
                == al  (8bits)
```

---

@title[ASM]

### Assembler
ASM (o ensamblador) es el lenguaje para humanos de más bajo nivel que pude ser usado en una computadora moderna.

En él se describen las instrucciones tal cual las ejecuta secuencialmente el CU.

```x86asm
mov eax, 0x0f
mov ebx, 0x10
add eax, ebx
push eax
```

---

@title[OPCodes]

### Operational Code

Cada instrucción en ASM se traduce a un valor en el lenguaje de la CU, cada valor es un código operacional. Por ejemplo:
* 0xeb == JMP
* 0x0f84 == JE
* ...

![](src/instructionset.png)

---

@title[Binarios ejecutables]

### Binarios ejecutables

Existen diferentes tipos de compilados, generalmente ELF (Linux) y PE (Windows).

Ambos tienen al menos los siguientes bloques:
* `.data`: Datos que utiliza el ejecutable, strings, arrays, etc.
* `.text`: Código ejecutable (opcodes).

Cuando se ejecutan, se copian en memoria y empiezan en la primera instrucción del bloque `.text` (entry point).

---

@title[Herramientas]

### Herramientas
En los 90/2k surgieron cientos de herramientas para facilitar el trabajo de RE.

Una lista podría ser: SoftIce, w32dasm, file insPEctor, SmartCheck, Pecode, WKTVBDE, Ida, DeDe, OllyDbg, ProcDump, VeoVeo, etc...

---

@title[r2intro]

![](src/r2pirate.png)