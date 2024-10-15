---
title: Динамическая диспетчеризация
subtitle: Объектно-Ориентированное Программирование
author: Иван Трепаков
institute: NSU
---

# Полиморфизм

## Ad-hoc полиморфизм

## Полиморфизм подтипов

## Параметрический полиморфизм

# Диспетчеризация

## Статическая

## Динамическая

## Одиночная

## Множественная

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

# Таблица виртуальных методов

::: columns
:::: {.column width=60%}
##
\centering
\begin{tikzpicture}

    \only<1>{
    \begin{struct}{object}
        \header             {object header} {Object}
        \field [dotted]  {} {object vmt}    {\&VMT\textsubscript{C}}
        \field           {} {object rest}   {...}
    \end{struct}
    }

    \visible<2>{
    \begin{struct}{object}
        \header             {object header} {Object}
        \field [dotted]  {} {object vmt}    {\&VMT\textsubscript{C}}
        \field [dotted]  {} {object imts}   {\&IMTs}
        \field           {} {object rest}   {...}
    \end{struct}
    }


    \begin{struct}[right={2*\structnodewidth} of object]{vmt C}
        \header                {vmt C header} {VMT\textsubscript{C}}
        \field [dotted]  {[0]} {vmt C 0}      {\&B::a()}
        \field [dashed]  {[1]} {vmt C 1}      {\&C::b()}
        \field           {[2]} {vmt C 2}      {\&K::c()}
    \end{struct}

    {\setbeamercovered{transparent=40} \uncover<1-2>{
    \connect{object vmt}{vmt C header}{}
    }}


    \begin{visibleenv}<2>
    {\setbeamercovered{transparent=40} \uncover<2>{
    \begin{struct}[below=\structnodeheight of object rest]{imts}
        \header              {imts header} {IMTs}
        \field [dotted]  {I} {imts I}      {\&IMT\textsubscript{C,I}}
        \field [dotted]  {J} {imts J}      {\&IMT\textsubscript{C,J}}
        \field           {K} {imts K}      {\&IMT\textsubscript{C,K}}
    \end{struct}

    \draw [->] (object imts.west) 
            -| ($ (imts header.west) - (0.5,0) $)
            -- (imts header.west);
    }}



    \begin{struct}[below=\structnodeheight of vmt C 2]{imt C}
        \field [draw]    {[0]} {imt C I 0}    {\&C::b()}
        \field [draw]    {[0]} {imt C J 0}    {\&K::c()}
        \field [dotted]  {[0]} {imt C K 0}    {\&C::b()}
        \field           {[1]} {imt C K 1}    {\&K::c()}
    \end{struct}

    \imtR{imt C I 0}{imt C I 0}{IMT\textsubscript{C,I}}
    \imtR{imt C J 0}{imt C J 0}{IMT\textsubscript{C,J}}
    \imtR{imt C K 0}{imt C K 1}{IMT\textsubscript{C,K}}
    \end{visibleenv}

    \begin{scope}[on background layer]
        \begin{visibleenv}<2>
        {\setbeamercovered{transparent=40} \uncover<2>{
        \connect[0.20]{imts I.east}{imt C I 0.west}{}
        \connect[0.35]{imts J.east}{imt C J 0.west}{}
        \connect[0.50]{imts K.east}{imt C K 0.west}{}
        }}
        \end{visibleenv}
    \end{scope}


    {\setbeamercovered{transparent=40} \uncover<0>{

    \begin{struct}[right={2*\structnodewidth} of vmt C]{vmt B}
        \header                {vmt B header} {VMT\textsubscript{B}}
        \field [dotted]  {[0]} {vmt B 0}      {\&B::a()}
        \field           {[1]} {vmt B 1}      {\&I::b()}
    \end{struct}


    \begin{visibleenv}<2>
    \begin{struct}[right={2*\structnodewidth} of imt C I 0.north]{imt B}
        \field           {} {imt B I 0}    {\&I::b()}
    \end{struct}

    \imtR{imt B I 0}{imt B I 0}{IMT\textsubscript{B,I}}
    \end{visibleenv}

    \begin{scope}[on background layer]
        \uncover<0>{
        \draw [dashed] (vmt C 0.north east) -- (vmt B 0.north west);
        \draw [dashed] (vmt C 1.south east) -- (vmt B 1.south west);
        \begin{visibleenv}<2>
        \uncover<2>{
        \draw [dashed] (imt C I 0.north east) -- (imt B I 0.north west);
        \draw [dashed] (imt C I 0.south east) -- (imt B I 0.south west);
        }
        \end{visibleenv}
        }
    \end{scope}

    }}

\end{tikzpicture}
::::
\vrule
\hspace{0.5em}
:::: {.column width=40%}
##
\centering
\begin{tikzpicture}

    \matrix [row sep=1em, column sep=1em,ampersand replacement=\&] {
    \node [class] (B) {B}; \& \node [interface] (I) {I}; \& \node [interface] (J) {J};\\
    \node [class] (C) {C}; \& \node [interface] (K) {K}; \& \\
    };
    \graph [use existing nodes] {
        C -> {B -> I, K -> {I, J}}
    };

\end{tikzpicture}
\vspace{1em}
\hrule
::::: {.block}
## \centering Виртуальный вызов `x.b()`
```
// Формальный тип x: C
call x.vmt[vnum$\textsubscript{C,b}$]
```
:::::
`\begin{visibleenv}<2>`{=latex}
\hrule
::::: {.block}
## \centering Интерфейсный вызов `x.b()`
```
// Формальный тип x: I
imt$\textsubscript{C,I}$ := x.imts.find(&I)
call imt$\textsubscript{C,I}$[vnum$\textsubscript{I,b}$] 
```
:::::
\End{visibleenv}
::::
:::

# Таблица интерфейсных методов

# Полиморфный инлайн кэш

# Заключение

# {.plain}

\centering
```{=latex}
{\fontsize{48pt}{7.2}\selectfont Q\&A }
```

