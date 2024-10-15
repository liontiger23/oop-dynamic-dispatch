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

# Таблица интерфейсных методов

# Полиморфный инлайн кэш

# Заключение

# {.plain}

\centering
```{=latex}
{\fontsize{48pt}{7.2}\selectfont Q\&A }
```

