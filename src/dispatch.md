---
title: Динамическая диспетчеризация
subtitle: Объектно-Ориентированное Программирование
author: Иван Трепаков
institute: NSU
---

# Полиморфизм

> *Полиморфизм* --- возможность функции с одним именем
> обрабатывать данные разных типов

# Полиморфизм {.fragile .t}

## \centering Ad hoc полиморфизм

\vspace{0.5em}
> Ad hoc (букв. «к этому») --- латинская фраза,
> означающая «для данного случая», «специально для этого».
> `\hfill`{=latex} [Wikipedia](https://ru.wikipedia.org/wiki/Ad_hoc)

. . .

::: columns
:::: {.column width=50%}

- Выбор реализации делается в зависимости от количества и типов
  формальных параметров функции
  - Перегрузка функций в Java
  - Перегрузка операторов в C++
  - Type classes в Haskell

. . .

::::
:::: {.column width=47%}

```{=latex}
\lstset{
  style=default,
  language=java,
  morekeywords={var},
  basicstyle={\small\ttfamily},
  columns=fixed,
}
```

\vspace{-1em}

```{=latex}
\begin{onlyenv}<+>
```
```
var x = ...;
var y = ...;
var z = x + y; // ???
```
```{=latex}
\end{onlyenv}
\begin{onlyenv}<+>
```
```
var x = 1;     // int
var y = ...;
var z = x + y; // ???
```
```{=latex}
\end{onlyenv}
\begin{onlyenv}<+>
```
```
var x = 1;     // int
var y = 2;     // int
var z = x + y; // ???
```
```{=latex}
\end{onlyenv}
\begin{onlyenv}<+>
```
```
var x = 1;     // int
var y = 2;     // int
var z = x + y; // 3 (int)
```
```{=latex}
\end{onlyenv}
\begin{onlyenv}<+>
```
```
var x = 1;     // int
var y = 2.0;   // double
var z = x + y; // ???
```
```{=latex}
\end{onlyenv}
\begin{onlyenv}<+>
```
```
var x = 1;     // int
var y = 2.0;   // double
var z = x + y; // 3.0 (double)
```
```{=latex}
\end{onlyenv}
```

. . .

```{=latex}
\begin{onlyenv}<.->
```
```
String add(int x, int y) {
  return "ints: " + (x + y);
}
String add(String x, int y) {
  return "mixed: " + (x + y);
}
String add(String x, String y) {
  return "strings: " + (x + y);
}
$\pause$add(1, 2) $\pause$// ints: 3
$\pause$add("1", 2) $\pause$// mixed: 12
$\pause$add("1", "2") $\pause$// strings: 12
```
```{=latex}
\end{onlyenv}
```

::::
:::

# Полиморфизм {.fragile .t}

## \centering Параметрический полиморфизм

. . .

::: columns
:::: {.column width=47%}

- Реализация функции использует *обобщенный* параметр
  - Generics в Java
  - Templates в C++
- Можно задавать дополнительные ограничения на обобщенный тип
- `\textcolor{CtpLavender}{`{=latex} *Подробнее на следующей лекции* `}`{=latex}

. . .

::::
:::: {.column width=53%}

```{=latex}
\lstset{style=default,basicstyle={\small\ttfamily}}
\setbeamercovered{transparent=40}
```

\vspace{-1em}

```java
static <T, S> T foo(T x, S y) {
  return x;
}

static <T extends I> boolean bar(I x, I y) {
  return x.test(y);
}
```

```{=latex}
\begin{uncoverenv}<0>
```
```java
interface I {
  boolean test(I x);
}
```
```{=latex}
\end{uncoverenv}
```

::::
:::

# Полиморфизм {.fragile .t}

## \centering Полиморфизм подтипов

::: columns
:::: {.column width=50%}

- Отношение *подтипа* `S <: T`

  \vspace{0.2em}
  > \footnotesize Любое значение типа `S` является значением типа `T`

. . .

- В объектно-ориентированных языках отношение подтипа обычно совпадает
  с отношением наследования

. . .

- Выбор реализации делается
  в зависимости от реального типа объекта
  *receiver* в момент исполнения вызова
  - *Виртуальные* методы
  - *Переопределение* методов

::::
:::: {.column width=47%}

. . .

```{=latex}
\lstset{
  style=default,
  language=java,
  morekeywords={var},
  basicstyle={\small\ttfamily},
  columns=fixed,
}
```

```
class A {
  void foo() { println("A.foo"); }
}
class B extends A {
  void foo() { println("B.foo"); }
}
class C extends A { }
```

. . .

```{=latex}
\begin{onlyenv}<+>
```
```
A x = ...;
x.foo();   // ???
```
```{=latex}
\end{onlyenv}
\begin{onlyenv}<+>
```
```
A x = ...; // new A()
x.foo();   // ???
```
```{=latex}
\end{onlyenv}
\begin{onlyenv}<+>
```
```
A x = ...; // new A()
x.foo();   // A.foo
```
```{=latex}
\end{onlyenv}
\begin{onlyenv}<+>
```
```
A x = ...; // new B()
x.foo();   // ???
```
```{=latex}
\end{onlyenv}
\begin{onlyenv}<+>
```
```
A x = ...; // new B()
x.foo();   // B.foo
```
```{=latex}
\end{onlyenv}
\begin{onlyenv}<+>
```
```
A x = ...; // new C()
x.foo();   // ???
```
```{=latex}
\end{onlyenv}
\begin{onlyenv}<+>
```
```
A x = ...; // new C()
x.foo();   // A.foo
```
```{=latex}
\end{onlyenv}
```

::::
:::

# Полиморфизм

> *Полиморфизм* --- возможность функции с одним именем
> обрабатывать данные разных типов

\vspace{1.5em}

. . .

> *Диспетчеризация* --- процесс выбора реализации полиморфной функции


# Диспетчеризация {.fragile}

::: columns
:::: {.column width=50%}
```{=latex}
\begin{uncoverenv}<2->
```
::::: block

## \centering Статическая диспетчеризация

- Реализация известна до исполнения
  - Прямой вызов (например статический)
  - Перегрузка
  - *Девиртуализация* в компиляторе
- Эффективно без поддержки среды исполнения

:::::

```{=latex}
\end{uncoverenv}
```
::::
:::: {.column width=50%}
```{=latex}
\begin{uncoverenv}<4->
```
::::: block

## \centering Динамическая диспетчеризация

- Реализация известна только во время исполнения конкретного вызова
  - Виртуальный вызов
  - Интерфейсный вызов
- Требует поддержки среды исполнения

:::::

```{=latex}
\end{uncoverenv}
```
::::
:::

\vspace{1em}
\hrule
\vspace{1em}

::: columns
:::: {.column width=50%}
```{=latex}
\begin{uncoverenv}<3->
\begin{minipage}[c][.1\textheight][t]{\linewidth}
\centering
\begin{tikzpicture}
  \node [anchor=east] at (-1,0) {
\begin{BVerbatim}
C.foo()
\end{BVerbatim}
  };
  \node [anchor=west] at (1,0) {
\begin{BVerbatim}
call &C::foo()
\end{BVerbatim}
  };
  \draw [->] (-0.5,0) -- (0.5,0);
\end{tikzpicture}
\end{minipage}
\end{uncoverenv}
```
::::
:::: {.column width=50%}
```{=latex}
\begin{uncoverenv}<5->
\begin{minipage}[c][.1\textheight][t]{\linewidth}
\centering
\begin{tikzpicture}
  \node [anchor=east] at (-1,0) {
\begin{BVerbatim}
x.foo()
\end{BVerbatim}
  };
  \node [anchor=west] at (1,0) {
\begin{BVerbatim}
???
\end{BVerbatim}
  };
  \draw [->] (-0.5,0) -- (0.5,0);
\end{tikzpicture}
\end{minipage}
\end{uncoverenv}
```
::::
:::

# Наследование

::: columns
:::: {.column width=33%}
## \centering Одиночное
\vspace{0.5em}
\centering
\begin{tikzpicture}

    \matrix [row sep=1.0em, column sep=1.0em,ampersand replacement=\&] {
    \& \node [class] (A) {A}; \& \\
    \& \node [class] (B) {B}; \& \\
    \node [class] (C) {C}; \& \& \node [class] (D) {D}; \\
    };
    \graph [use existing nodes] {
        {C, D} -> B -> A
    };

\end{tikzpicture}
\vspace{0.5em}
::::
\vrule
:::: {.column width=33%}
## \centering Интерфейсное
\vspace{0.5em}
\centering
\begin{tikzpicture}

    \matrix [row sep=1.0em, column sep=1.0em,ampersand replacement=\&] {
    \node [class] (A) {A}; \& \node [interface] (I) {I}; \& \\
    \node [class] (B) {B}; \& \node [interface] (J) {J}; \& \node [interface] (K) {K};\\
    \node [class] (C) {C}; \& \node [interface] (L) {L}; \& \\
    };
    \graph [use existing nodes] {
        C -> {B -> {A, I, J}, L -> {J, K}}
    };

\end{tikzpicture}
\vspace{0.5em}
::::
\vrule
:::: {.column width=33%}
## \centering Множественное
\vspace{0.5em}
\centering
\begin{tikzpicture}

    \matrix [row sep=1.0em, column sep=1.0em,ampersand replacement=\&] {
    \& \node [class] (A) {A}; \& \\
    \node [class] (B) {B}; \& \& \node [class] (C) {C}; \\
    \& \node [class] (D) {D}; \& \\
    };
    \graph [use existing nodes] {
        D -> {B, C} -> A
    };

\end{tikzpicture}
\vspace{0.5em}
::::
:::
\hrule
::: columns
:::: {.column width=33%}
:::::: block
##
\vspace{0.5em}
\begin{minipage}[t]{.35\columnwidth}
\centering
\includegraphics[height=2em]{images/dispatch/Simula.pdf}
\end{minipage}
\hfill
\begin{minipage}[t]{.35\columnwidth}
\centering
\colorbox{maininverted}{\includegraphics[height=2em]{images/dispatch/Oberon.pdf}}
\end{minipage}
\hfill
\begin{minipage}[t]{.23\columnwidth}
\centering
\includegraphics[height=2em]{images/dispatch/Modula-3.pdf}
\end{minipage}
::::::
::::
\vrule
:::: {.column width=33%}
:::::: block
##
\vspace{0.5em}
\begin{minipage}[t]{\columnwidth}
    \begin{minipage}[t]{.23\columnwidth}
    \centering
    \includegraphics[height=2em]{images/dispatch/Csharp.pdf}
    \end{minipage}
    \hfill
    \begin{minipage}[t]{.23\columnwidth}
    \centering
    \includegraphics[height=2em]{images/dispatch/Java.pdf}
    \end{minipage}
    \hfill
    \begin{minipage}[t]{.23\columnwidth}
    \centering
    \includegraphics[height=2em]{images/dispatch/Scala.png}
    \end{minipage}
    \hfill
    \begin{minipage}[t]{.23\columnwidth}
    \centering
    \includegraphics[height=2em]{images/dispatch/Kotlin.pdf}
    \end{minipage}
\end{minipage}
\begin{minipage}[t]{\columnwidth}
\vspace*{-1em}
    \begin{minipage}[t]{.23\columnwidth}
    \centering
    \includegraphics[height=2em]{images/dispatch/Clojure.pdf}
    \end{minipage}
    \hfill
    \begin{minipage}[t]{.23\columnwidth}
    \centering
    \includegraphics[height=2em]{images/dispatch/Ruby.pdf}
    \end{minipage}
    \hfill
    \begin{minipage}[t]{.23\columnwidth}
    \centering
    \includegraphics[height=2em]{images/dispatch/Delphi.pdf}
    \end{minipage}
    \hfill
    \begin{minipage}[t]{.23\columnwidth}
    \centering
    \includegraphics[height=2em]{images/dispatch/Swift.pdf}
    \end{minipage}
\end{minipage}
::::::
::::
\vrule
:::: {.column width=33%}
:::::: block
##
\vspace{0.5em}
\begin{minipage}[t]{.31\columnwidth}
\centering
\includegraphics[height=2em]{images/dispatch/C++.pdf}
\end{minipage}
\hfill
\begin{minipage}[t]{.31\columnwidth}
\centering
\includegraphics[height=2em]{images/dispatch/Python.pdf}
\end{minipage}
\hfill
\begin{minipage}[t]{.31\columnwidth}
\centering
\includegraphics[height=2em]{images/dispatch/OCaml.pdf}
\end{minipage}
\begin{minipage}[t]{\columnwidth}
\vspace*{-1em}
\centering
\colorbox{maininverted}{\includegraphics[height=2em]{images/dispatch/Eiffel.pdf}}
\end{minipage}
::::::
::::
:::

# Диспетчеризация виртуальных методов {.fragile}

. . .

::: columns
:::: {.column width=52%}
::::: {.block}
## \centering Таблица виртуальных методов
> \centering \footnotesize Virtual Method Table, VMT, vtable

- `\uncover<3->{`{=latex} Массив с адресами реализаций виртуальных методов класса `}`{=latex}
- `\uncover<4->{`{=latex} Таблицы наследников расширяют таблицу суперкласса `}`{=latex}
- `\uncover<5->{`{=latex} Таблица доступна напрямую из каждого объекта класса `}`{=latex}
- `\uncover<6->{`{=latex} Для каждого виртуального метода можно определить *виртуальный номер* `}`{=latex}
:::::
```{=latex}
\begin{uncoverenv}<7->
```
::::: {.block}
## \centering Виртуальный вызов `x.b()`
\vspace{-0.5em}
```{=latex}
\begin{uncoverenv}<8->
```
```
invokevirtual #1 // Method B.b:()V
```
```{=latex}
\begin{uncoverenv}<9->
```
```c
call x.vmt[vnum$\textsubscript{B,b}$]
```
```{=latex}
\end{uncoverenv}
```
```{=latex}
\end{uncoverenv}
```
:::::
```{=latex}
\end{uncoverenv}
```
::::
\vrule
\hspace{0.2em}
:::: {.column width=48%}
::::: {.block}
##
```{=latex}
\centering
\begin{tikzpicture}

    \uncover<5->{
    \begin{struct}{object}
        \header             {object header} {Object}
        \field [dotted]  {} {object vmt}    {\&VMT\textsubscript{C}}
        \field           {} {object rest}   {...}
    \end{struct}
    }

    \uncover<3->{
    \begin{struct}[right={1.6*\structnodewidth} of object]{vmt C}
        \header                {vmt C header} {VMT\textsubscript{C}}
        \field [dotted]  {\only<6->{[0]}} {vmt C 0}      {\&B::a()}
        \field [dashed]  {\only<6->{[1]}} {vmt C 1}      {\&C::b()}
        \field           {\only<6->{[2]}} {vmt C 2}      {\&K::c()}
    \end{struct}
    }

    \uncover<5->{
    \connect[0.25]{object vmt.east}{vmt C header.west}{}
    }

    \uncover<4->{
    {\setbeamercovered{transparent=40} \uncover<0-3>{

    \begin{struct}[right={1.6*\structnodewidth} of vmt C]{vmt B}
        \header                {vmt B header} {VMT\textsubscript{B}}
        \field [dotted]  {\only<6->{[0]}} {vmt B 0}      {\&B::a()}
        \field           {\only<6->{[1]}} {vmt B 1}      {\&I::b()}
    \end{struct}

    }}
    }

    \uncover<9->{
        \node [draw,color=CtpRed,fit=(vmt C 1 @extra) (vmt B 1)] {};
    }

    %% To prevent jumping
    \uncover<0>{
    \begin{struct}[below=\structnodeheight of object rest]{imts}
        \header              {imts header} {IMTs}
        \field [dotted]  {I} {imts I}      {\&IMT\textsubscript{C,I}}
        \field [dotted]  {J} {imts J}      {\&IMT\textsubscript{C,J}}
        \field           {K} {imts K}      {\&IMT\textsubscript{C,K}}
    \end{struct}
    }

    \begin{scope}[on background layer]
        \uncover<4->{
        {\setbeamercovered{transparent=40} \uncover<0-3>{
        \draw [dashed] (vmt C 0.north east) -- (vmt B 0.north west);
        \draw [dashed] (vmt C 1.south east) -- (vmt B 1.south west);
        }}
        }
    \end{scope}

\end{tikzpicture}
\begin{tikzpicture}[remember picture, overlay]
    \node [shift={(-4em,3em)}]  at (current page.south east)
        {%
        \begin{tikzpicture}[remember picture,overlay,scale=0.6, every node/.style={scale=0.6}]

            \matrix [row sep=0.5em, column sep=0.5em,ampersand replacement=\&] {
            \node [class] (B) {B}; \& \node [interface] (I) {I}; \& \node [interface] (J) {J};\\
            \node [class] (C) {C}; \& \node [interface] (K) {K}; \& \\
            };
            \graph [use existing nodes] {
                C -> {B -> I, K -> {I, J}}
            };

        \end{tikzpicture}
        };
\end{tikzpicture}
```
:::::
::::
:::

# Диспетчеризация интерфейсных методов

::: columns
:::: {.column width=52%}
::::: {.block}
## \centering Таблица интерфейсных методов
> \centering \footnotesize Interface Method Table, IMT, itable

- `\uncover<2->{`{=latex} Массив с адресами реализаций методов `}`{=latex}
- `\uncover<3->{`{=latex} Раскладка фиксирована во всех реализующих классах `}`{=latex}
- `\uncover<4->{`{=latex} Таблицы доступны из каждого объекта `}`{=latex}
- `\uncover<5->{`{=latex} Необходим поиск нужной таблицы `}`{=latex}
- `\uncover<6->{`{=latex} Для каждого интерфейсного метода можно определить *виртуальный номер* `}`{=latex}
:::::
```{=latex}
\begin{uncoverenv}<7->
```
::::: {.block}
## \centering Интерфейсный вызов `x.b()`
\vspace{-0.5em}
```{=latex}
\begin{uncoverenv}<8->
```
```
invokeinterface #1, 1 // Method I.b:()V
```
```{=latex}
\begin{uncoverenv}<9->
```
```c
imt$\textsubscript{C,I}$ = lookupIMT(x, &I)
call imt$\textsubscript{C,I}$[vnum$\textsubscript{I,b}$]
```
```{=latex}
\end{uncoverenv}
```
```{=latex}
\end{uncoverenv}
```
:::::
```{=latex}
\end{uncoverenv}
```
::::
\vrule
\hspace{0.2em}
:::: {.column width=48%}
::::: {.block}
##
```{=latex}
\centering
\begin{tikzpicture}

    \only<1-3>{
    \begin{struct}{object}
        \header             {object header} {Object}
        \field [dotted]  {} {object vmt}    {\&VMT\textsubscript{C}}
        \field           {} {object rest}   {...}
    \end{struct}
    }

    \only<4->{
    \begin{struct}{object}
        \header             {object header} {Object}
        \field [dotted]  {} {object vmt}    {\&VMT\textsubscript{C}}
        \field [dotted]  {} {object imts}   {\&IMTs}
        \field           {} {object rest}   {...}
    \end{struct}
    }

    \begin{struct}[right={1.6*\structnodewidth} of object]{vmt C}
        \header                {vmt C header} {VMT\textsubscript{C}}
        \field [dotted]  {[0]} {vmt C 0}      {\&B::a()}
        \field [dashed]  {[1]} {vmt C 1}      {\&C::b()}
        \field           {[2]} {vmt C 2}      {\&K::c()}
    \end{struct}

    \connect[0.25]{object vmt.east}{vmt C header.west}{}

    \uncover<4->{
    \begin{struct}[below=\structnodeheight of object rest]{imts}
        \header              {imts header} {IMTs}
        \field [dotted]  {I} {imts I}      {\&IMT\textsubscript{C,I}}
        \field [dotted]  {J} {imts J}      {\&IMT\textsubscript{C,J}}
        \field           {K} {imts K}      {\&IMT\textsubscript{C,K}}
    \end{struct}
    }

    \only<4->{
    \draw [->] (object imts.west) 
            -| ($ (imts header.west) - (0.2,0) $)
            -- (imts header.west);
    }

    \uncover<2->{
    \begin{struct}[below=\structnodeheight of vmt C 2]{imt C}
        \field [draw]    {\only<6->{[0]}} {imt C I 0}    {\&C::b()}
        \field [draw]    {\only<6->{[0]}} {imt C J 0}    {\&K::c()}
        \field [dotted]  {\only<6->{[0]}} {imt C K 0}    {\&C::b()}
        \field           {\only<6->{[1]}} {imt C K 1}    {\&K::c()}
    \end{struct}

    \imtR{imt C I 0}{imt C I 0}{\tiny IMT\textsubscript{C,I}}
    \imtR{imt C J 0}{imt C J 0}{\tiny IMT\textsubscript{C,J}}
    \imtR{imt C K 0}{imt C K 1}{\tiny IMT\textsubscript{C,K}}
    }

    \begin{scope}[on background layer]
        \uncover<4->{
        \connect[0.10]{imts I.east}{imt C I 0.west}{}
        \connect[0.20]{imts J.east}{imt C J 0.west}{}
        \connect[0.30]{imts K.east}{imt C K 0.west}{}
        }
    \end{scope}

    \uncover<3->{
    {\setbeamercovered{transparent=40} \uncover<0>{
    \begin{struct}[right={1.6*\structnodewidth} of imt C I 0.north]{imt B}
        \field           {} {imt B I 0}    {\&I::b()}
    \end{struct}
    }}
    }

    \uncover<9->{
        \node [draw,color=CtpRed,fit=(imt C I 0 @extra) (imt B I 0)] {};
    }

    {\setbeamercovered{transparent=40} \uncover<0>{

    \begin{struct}[right={1.6*\structnodewidth} of vmt C]{vmt B}
        \header                {vmt B header} {VMT\textsubscript{B}}
        \field [dotted]  {[0]} {vmt B 0}      {\&B::a()}
        \field           {[1]} {vmt B 1}      {\&I::b()}
    \end{struct}

    }}

    \begin{scope}[on background layer]
        {\setbeamercovered{transparent=40} \uncover<0>{
        \draw [dashed] (vmt C 0.north east) -- (vmt B 0.north west);
        \draw [dashed] (vmt C 1.south east) -- (vmt B 1.south west);
        }}
        \uncover<3->{
        {\setbeamercovered{transparent=40} \uncover<0-2>{
        \draw [dashed] (imt C I 0.north east) -- (imt B I 0.north west);
        \draw [dashed] (imt C I 0.south east) -- (imt B I 0.south west);
        }}
        }
    \end{scope}

\end{tikzpicture}
\begin{tikzpicture}[remember picture, overlay]
    \node [shift={(-4em,3em)}]  at (current page.south east)
        {%
        \begin{tikzpicture}[remember picture,overlay,scale=0.6, every node/.style={scale=0.6}]

            \matrix [row sep=0.5em, column sep=0.5em,ampersand replacement=\&] {
            \node [class] (B) {B}; \& \node [interface] (I) {I}; \& \node [interface] (J) {J};\\
            \node [class] (C) {C}; \& \node [interface] (K) {K}; \& \\
            };
            \graph [use existing nodes] {
                C -> {B -> I, K -> {I, J}}
            };

        \end{tikzpicture}
        };
\end{tikzpicture}
```
:::::
::::
:::

# Заключение

::: columns
:::: {.column width=50%}

## Что узнали?

- Виды полиморфизма
  - `\textcolor{CtpPeach}{`{=latex} Ad hoc полиморфизм `}`{=latex}
  - `\textcolor{CtpOverlay1}{`{=latex} Параметрический полиморфизм `}`{=latex}
  - `\textcolor{CtpPeach}{`{=latex} Полиморфизм подтипов `}`{=latex}
- Виды диспетчеризации
  - `\textcolor{CtpPeach}{`{=latex} Статическая `}`{=latex}
  - `\textcolor{CtpPeach}{`{=latex} Динамическая `}`{=latex}
- Реализация динамической диспетчеризации
  - `\textcolor{CtpPeach}{`{=latex} Tаблица виртуальных методов`}`{=latex}
    для одиночного наследования
  - `\textcolor{CtpPeach}{`{=latex} Tаблица интерфейсных методов`}`{=latex}
    для интерфейсного наследования

. . .

::::
:::: {.column width=50%}

## Что осталось за кадром?

- `\textcolor{CtpLavender}{`{=latex} Параметрический полиморфизм`}`{=latex} на следующей лекции
- Диспетчеризации в полноценном множественном наследовании (например, в C++)
- Оптимизации компилятора
  - Открытая подстановка
  - Девиртуализация
  - Условная девиртуализация
  - Profile-guided optimization (PGO)
- Оптимизации времени исполнения
  - Polymorphic inline cache (PIC)
  - Профилировка
  - Деоптимизация

::::
:::

# {.plain}

\centering
```{=latex}
{\fontsize{48pt}{7.2}\selectfont Q\&A }
```

