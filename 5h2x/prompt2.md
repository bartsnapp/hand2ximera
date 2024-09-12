# Handwriting to Ximera LaTeX Source

You will find a PNG that contains handwritten notes representing a Ximera document. **Use handwriting recognition** to interpret this PNG and convert it to LaTeX source written in the Ximera documentclass.

## In the Input PNG
- In the PNG and this document, capital words such "ANS" and "THE TITLE IF GIVEN" are words that you are supposed to replace with the correct words from the PNG.
- In the PNG, the title will be double underlined if there is a title; if nothing at the top of the page has a double underline, then omit the title. 
- In the PNG, the abstract (if it exists) will be in parentheses directly below the title.  At the end of these parenthesis, the document begins. 
- If the author identifies themselves, put their name in as `\author{THEIR NAME}` in the preamble of the document.
- If a license is given (e.g. CC BY-NC-SA 4.0), state it as `\license{THEIR LICENSE}. 
- Basically, if there is a title and abstract and/or author and license in the PNG, it should be returned as something like (follow the suggestions of the comments!)
  ```latex
  \documentclass{ximera}
  \title{THE TITLE IF GIVEN}         %% Only if there is a title, omit this line otherwise
  \author{THE AUTHOR IF GIVEN}       %% Only if there is a author, omit this line otherwise
  \license{THE LICENSE IF GIVEN}     %% Only if there is a license, omit this line otherwise
  \begin{document}   
  \begin{abstract}                   %% Only if there is an abstract, omit this line otherwise
    WORDS THAT WERE IN PARENTHESIS   %% Express in LaTeX WITHOUT parenthesis
  \end{abstract}                     %% Only if there is a abstract, omit this line otherwise
  \maketitle                         %% Only if there is a title, omit this line otherwise
  ```
- If there is no double-underlined title at the top of the page, then there is no title, and none of `\author`, `\title`, `abstract`, nor `\maketitle`, should be used.
- In the PNG, if objects (like numbers, mathematical expressions) are written within a rectangle, that means you should replace the OBJECT in the rectangle with `\answer{OBJECT}`. There may be several such answer box in a string of equations.
- If parenthesis are surrounding a drawn rectangle, use `\left(` and `\right)`  
- Carefully verify each transformation and ensure any boxed expressions during intermediate steps are accurately transcribed as `\answer` in the LaTeX output
- In the PNG, if a box is drawn around "ANS" then, please write the correct answer inside `\answers{CORRECT ANS}`. 
- In the PNG, if equations are stacked you should use `align*`. As an abstract example, if you think of each EXPRESSION as being what is in the PNG, it must be formatted like this:
  ```latex
  \begin{align*}
  EXPRESSION &= EXPRESSION \\
             &= EXPRESSION \\
             &= EXPRESSION %% no \\ here
\end{align*}
  ```
- Carefully verify that all vertical series of equations a correct implementation of `align*` in the LaTeX output.
- In the PNG, we denote Ximera environments multipleChoice and selectAll with these words and each choice with an open circle. If the open circle is checked, this means `\choice[correct]{SOME CHOICE}`.
- In the PNG, we denote wordChoice with a box drawn around WC, connected to another box containing the choices. The correct choices have a checkmark in front of them.
- In the PNG, we denote the scope of an environment by drawing a rectangle around the environment. Nested rectangles mean nested environments.

## The Ximera LaTeX Output

- In the LaTeX output, all math needs to be in math-mode. All numbers and variables are math.
- In the LaTeX output `\answer` always needs to be in math-mode. As an example: 
  ```latex
  $2+2 = \answer{4}$  %% this is correct
  \[
    2+2 = \answer{4}  %% is also correct
  \]
  ```
- All theorem-like environments will have a single underline. Here is a list of Ximera environments: theorem, algorithm, axiom, claim, conclusion, condition, conjecture, corollary, criterion, definition, example, explanation, fact, feedback, formula, hint, idea, lemma, model, notation, observation, paradox, procedure, proposition, remark, summary, template, warning.
- Replace all instances of ANS within `\answer` with the correct answer, formatted in LaTeX.
- Carefully verify that all instances of "ANS" have been replaced by a correct answer in the LaTeX output.
- In the LaTeX output `\wordChoice` needs to be in text-mode. For example, something like this:
  ```latex
  This is an example of \wordChoice{\choice{multiple choice} \choice{select all} \choice[correct]{word choice}}.
  ```
- In the LaTeX output, all answerables, (answer, multipleChoice, selectAll, wordChoice) must be enclosed in some theorem-like environment. Print a warning if you find an answerable that is only bounded by `\begin{document}` and `\end{document}`.
  ```latex
  \begin{exercise}  %% the bounding environment is exercise
  Compute
  \[
    \frac{d}{dx} x^2 = \answer{2x} %% the \answer is in math mode, and is bounded by an environment
  \]
  \end{exercise}
  ```
- Theorem-like environments that are "logically connected" (e.g., theorem/proof, example/explanation, problem/solution, and so on) should be nested.
  For example:
  ```latex
  \begin{theorem}
  SOME THEOREM
    \begin{proof}
    SOME PROOF
    \end{proof}
  \end{theorem}
  ```
  If you nest exercise/problem/question/exploration you get follow-up questions, assuming each has an answerable. For example:
  ```latex
  \begin{problem}
  First add one to two
  \[
  1+2 = \answer{3}
  \]
    \begin{problem} %% this unfolds when the \answer above is completed
    Now add two to your previous answer
    \[
      3+2 = \answer{5}
    \]
    \end{problem}
  \end{problem}
  ```
- As a rule of thumb, TikZ images should be "inside of" the center environment
  ```latex
  \begin{center}
  SOME TIKZ PICTURE
  \end{center}
  ```
- Attempt to render all images in TikZ. This means you will provide TikZ code that you think is correct.
- The syntax for multipleChoice is
  ```latex
  \begin{multipleChoice}
  \choice{SOME INCORRECT CHOICE}
  \choice{SOME INCORRECT CHOICE}
  \choice[correct]{A CORRECT CHOICE}
  \choice{SOME INCORRECT CHOICE}
  \end{multipleChoice}
  ```
- The syntax for selectAll is
  ```latex
  \begin{selectAll}
  \choice{SOME INCORRECT CHOICE}
  \choice[correct]{A CORRECT CHOICE}
  \choice[correct]{A CORRECT CHOICE}
  \choice{SOME INCORRECT CHOICE}
  \end{selectAll}
- Follow the Ximera documentclass guidelines for formatting answers, choices, and other elements.
- Use display math `\[` `\]` to center and highlight math and answers 
Finally, check your output against these directions once complete
- All theorem-like environments (such as theorem, proof, definition, etc.) must be correctly nested. Specifically:
  - If a proof is associated with a theorem (or similar environment), the `proof` environment must be nested within the `theorem` (or similar) environment.
  - If a solution/explanation/freeResponse/etc is associated with a example/problem/etc (or similar environment), the `solution/explanation/freeResponse/etc` environment must be nested within the `example/problem/etc` (or similar) environment.
  - This nesting ensures the logical connection between the outside environment and its inside environment is maintained.

- **Example of Correct Nesting**:
  ```latex
  \begin{theorem}
  SOME THEOREM STATEMENT
    \begin{proof}
    SOME PROOF CONTENT
    \end{proof}
  \end{theorem}
## An ABSTRACT Example

```latex
\documentclass{ximera}
\title{TITLE IF GIVEN}         %% Only if there is a title, omit this line otherwise
\author{AUTHOR IF GIVEN}       %% Only if there is an author, omit this line otherwise
\license{LICENSE IF GIVEN}     %% Only if there is a license, omit this line otherwise
\begin{document}   
\begin{abstract}               %% Only if there is an abstract, omit this line otherwise
  Abstract content             %% Express in LaTeX WITHOUT parenthesis
\end{abstract}                 %% Only if there is an abstract, omit this line otherwise
\maketitle                     %% Only if there is a title, omit this line otherwise

\begin{example}
Example content...
\begin{align*}
EXPRESSION &= EXPRESSION \\
           &= EXPRESSION
\end{align*}
\begin{solution}
Solution content...
\begin{align*}
EXPRESSION &= EXPRESSION \\
           &= EXPRESSION WITH \answer{SOME OTHER EXPRESSION}
           &= EXPRESSION WITH \answer{SOME OTHER EXPRESSION}
           &= \answer{CORRECT ANSWER}
\end{align*}
\end{solution}
\end{example}

\begin{example}
Example content...
\begin{center}
TIKZ PICTURE
\end{center}
\begin{align*}
EXPRESSION &= EXPRESSION WITH \answer{SOME OTHER EXPRESSION}
           &= EXPRESSION WITH \answer{SOME OTHER EXPRESSION}
           &= EXPRESSION
\end{align*}
\begin{solution}
Solution content...
\begin{align*}
EXPRESSION &= EXPRESSION \\
           &= \answer{CORRECT ANSWER}
\end{align*}
\end{solution}
\end{example}
```
\end{document}


Here is another example of a Ximera document:

```latex
\documentclass{ximera}


\outcome{Calculate limits using the limit laws.}

\input{../preamble.tex}
\title[Dig-In:]{The limit laws}
\begin{document}
\begin{abstract}
We give basic laws for working with limits. 
\end{abstract}
\maketitle
In the previous section were able to compute the limits

\[
\lim_{x\to \pi} x^3=\pi^3,\quad\lim_{x\to \pi} \sqrt{2}=\sqrt{2},\quad\lim_{x\to \pi} \cos{x}= -1,
\]

using continuity of the functions $x^3$, $\sqrt{2}$, and $\cos{x}$, at
$x=\pi$.  Does this imply that we can compute the limits
\begin{align*}
  &\lim_{x\to \pi} (x^3-\cos{x}),\\
  &\lim_{x\to \pi} \frac{\sqrt{2}}{\cos{x}},\\
  &\lim_{x\to \pi} (\sqrt{2}\cdot x^3\cdot\cos{x}), \text{ or}\\
  &\lim_{x\to \pi} \cos({x^3})?
\end{align*}

Well, we cannot use continuity here, because we don't know if the
functions $x^3-\cos{x}$, $\frac{\sqrt{2}}{\cos{x}}$, $\sqrt{2}\cdot
x^3\cdot\cos{x}$, and $\cos({x^3})$ are continuous at $x=\pi$, and

 we have no other tools available, since the graphs and tables are not reliable. Obviously, we need more tools to help us with computation of limits.

 

In this section, we present a handful of rules, called the \textit{Limit Laws},
that allow us to find limits of various combinations of functions.

\begin{theorem}[Limit Laws]\index{limit laws}\label{theorem:limit-laws}
Suppose that $\lim_{x\to a}f(x)=L$, $\lim_{x\to a}g(x)=M$.
\begin{description}
%\item[\textbf{Constant Multiple Law}] $\lim_{x\to a} kf(x) = k\lim_{x\to a}f(x)=kL$.
\item[Sum/Difference Law] $\lim_{x\to a} (f(x) \pm g(x)) =
  \lim_{x\to a}f(x) \pm \lim_{x\to a}g(x)=L \pm M$.
\item[Product Law]  $\lim_{x\to a} (f(x)g(x)) = \lim_{x\to
  a}f(x)\cdot\lim_{x\to a}g(x)=LM$.
\item[Quotient Law]  $\lim_{x\to a} \frac{f(x)}{g(x)} =
  \frac{\lim_{x\to a}f(x)}{\lim_{x\to a}g(x)}=\frac{L}{M}$, if
  $M\ne0$.
\end{description}
\label{thm:limit laws}
\end{theorem}

In plain language, ``limit of a sum equals the sum of the limits,'' ``limit of a product equals the product of the limits,'' etc.

Let's examine how the Limit Laws can be used in computation of limits.
%begin{question}
  %True or false: If $f$ and $g$ are continuous functions on an
  %interval $I$, then $f\pm g$ is continuous on $I$.
  %\begin{multipleChoice}
   % \choice[correct]{True}
  %  \choice{False}
 % \end{multipleChoice}
 % \begin{feedback}
    %This follows from the Sum/Difference Law.
 % \end{feedback}
%\end{question}

%\begin{question}
 % True or false: If $f$ and $g$ are continuous functions on an
 % interval $I$, then $f/g$ is continuous on $I$.
 % \begin{multipleChoice}
    %\choice{True}
   % \choice[correct]{False}
 % \end{multipleChoice}
 % \begin{feedback}
   % In this case, $f/g$ will not be continuous for $x$ where $g(x) =
    %0$.
 % \end{feedback}
%\end{question}


\begin{example}
  Compute the following limits using Limit Laws:
  \begin{enumerate}
  \item\label{lle1a} $\lim_{x\to \pi} (x^3-\cos{x})$
  \item\label{lle1b} $\lim_{x\to \pi} \frac{\sqrt{2}}{\cos{x}}$
  \item\label{lle1c} $\lim_{x\to \pi} (\sqrt{2}\cdot x^3\cdot\cos{x})$
  \item\label{lle1d} $\lim_{x\to \pi} \cos({x^3})$
  \end{enumerate}
  \begin{explanation}
    For $\lim_{x\to \pi} (x^3-\cos{x})$, write:
    \begin{align*}
      \lim_{x\to \pi} (x^3-\cos{x})&=\lim_{x\to \pi} x^3-\lim_{x\to \pi}\cos{x} && \text{by Difference Law}\\
      &=\pi^3-(-1)\\
      &=\pi^3+1
    \end{align*}
    For $\lim_{x\to \pi} \frac{\sqrt{2}}{\cos{x}}$, write:
    \begin{align*}
      \lim_{x\to \pi} \frac{\sqrt{2}}{\cos{x}}&=\frac{\lim_{x\to \pi}\sqrt{2}}{\lim_{x\to \pi}\cos{x}} && \text{by Quotient Law}\\
      &=\frac{\sqrt{2}}{-1}\\
      &=-\sqrt{2}
    \end{align*}
    For $\lim_{x\to \pi} (\sqrt{2}\cdot x^3\cdot\cos{x})$, using the Product Law, we can write:
    \[
    \lim_{x\to \pi} (\sqrt{2}\cdot x^3\cdot\cos{x})=\lim_{x\to \pi} \sqrt{2}\cdot \lim_{x\to \pi}x^3\cdot \lim_{x\to \pi}\cos{x}
    \]
    \begin{align*}
      &=\sqrt{2}\cdot \pi^3\cdot(-1)\\
      &=-\sqrt{2}\pi^3
    \end{align*}
    For $\lim_{x\to \pi} \cos({x^3})$, write:
    \[
    \lim_{x\to \pi} \cos({x^3})= \cdots 
    \]
    The function $\cos({x^3})$ is a combination of the functions
    $\cos({x})$ and $x^3$, but it is neither a sum/difference, nor a
    product, nor a quotient of these two functions, so we cannot apply
    any of the Limit Laws. This function is a composition of the two
    functions, $\cos({x})$ and $x^3$.
  \end{explanation}
\end{example}
\begin{example}
\begin{enumerate}
\item  Compute the following limit using limit laws:
\[
  \lim_{x\to 1}(5x^2+3x-2)
\]
\begin{explanation}
  Well, get out your pencil and write with me:
  \[
  \lim_{x\to 1} (5x^2+3x-2) = \lim_{x\to 1} 5x^2 + \lim_{x\to 1} \answer[given]{3x} - \lim_{x\to 1}2
  \]
  by the Sum/Difference Law. So now
  \[
  = 5\lim_{x\to 1} x^2 + 3\lim_{x\to 1} x - \lim_{x\to 1}\answer[given]{2}
  \]
  by the Product Law. Finally by continuity of $x^b$ and $k$,
  \[
  = 5(1)^2 + 3(1) - 2 =\answer[given]{6}.
  \]
  \begin{onlineOnly}
    We can check our answer by looking at the graph of $y=f(x)$:
    \[
    \graph{5x^2+3x-2}
    \]
  \end{onlineOnly}
\end{explanation}  
\item Is the polynomial function  $f(x)=5x^2+3x-2$ continuous at $x=1$?
\begin{explanation}
We have to check whether
\[
 \lim_{x\to 1} f(x)=f(1). 
\]
Since we already know that $ \lim_{x\to 1} (5x^2+3x-2)=6$,  we only have  to compute $f(1)$.
\begin{align*}
f(1)&=5(1)^2 + 3(1) - 2\\
&=6
\end{align*}
Therefore, the polynomial function $f$ is continuous at $x=1$.

But what about continuity at any other value $x$? Is the function $f$ continuous on its entire domain?

And what about any other polynomial function?

Are polynomials continuous on their domains?
\end{explanation}
\end{enumerate}
\end{example}

We can generalize the example above to get the following theorems.

\begin{theorem}[Continuity of Polynomial Functions]\index{continuity of polynomial functions}
 \textbf{All polynomial functions}, meaning functions of the form
  \[
  f(x) = a_nx^n + a_{n-1}x^{n-1} + \dots + a_1 x + a_0
  \]
  where $n$ is a positive integer  and each coefficient $a_i$, $i=0, 1,...,n$, is a real number, are
  \textbf{continuous for all real numbers}.
  \begin{explanation}
  In order to show that any polynomial, $f$, is continuous at any real number, $a$, we have to show that
  \[
  \lim_{x\to a} f(x)=f(a).
  \]
  Write with me:
  \[
  \lim_{x\to a} f(x) = \lim_{x\to a} (a_nx^n + a_{n-1}x^{n-1} + \dots + a_1 x + a_0 )
  \]
  Now by the Sum Law,
  \[
  = \lim_{x\to a} a_nx^n + \lim_{x\to a} a_{n-1}x^{n-1} + \dots +  \lim_{x\to a}a_1 x + \lim_{x\to a} a_0
  \]
  and by the Product Law,
  \begin{align*}
    = \lim_{x\to a} a_n\cdot \lim_{x\to a}x^n + \lim_{x\to a} a_{n-1}\cdot \lim_{x\to a}x^{n-1} &+ \dots\\
    &+  \lim_{x\to a}a_1 \cdot \lim_{x\to a}x + \lim_{x\to a} a_0
  \end{align*}
  and by Continuity
  \[
  = a_n\cdot a^n +  a_{n-1}\cdot a^{n-1} + \dots + a_1 \cdot a + a_0
  \]
  And this equals\dots
  \[
  =f(a)
  \]
  Since we have shown that $\lim_{x\to a} f(x) = f(a)$, we have
  shown that $f$ is continuous at $x=a$.
\end{explanation}
\end{theorem}

\begin{theorem}[Continuity of Rational Functions]\index{continuity of rational functions}
   A \textbf{rational function} h, meaning a function of the form 
  \[
  h(x)=\frac{f(x)}{g(x)}
  \]
  where $f $and $g$ are polynomials, is \textbf{continuous} for all real numbers except where $g(x)=0$.  That is,
  rational functions are continuous wherever they are defined.
\begin{explanation}
      Let $a$ be a real number such that $g(a)\neq 0$.  Then, since
      $g(x)$ is continuous at $a$, $\lim_{x\to a} g(x) \neq 0$.
      Therefore, write with me, 
      \[
      \lim_{x \to a} h(x) = \lim_{x\to a} \frac{f(x)}{g(x)}
      \]
      and now by the Quotient Law, 
      \[
      \frac{\lim_{x\to a} f(x)}{ \lim_{x\to a} g(x)}
      \]
      and by the continuity of polynomials we may now set $x=a$
      \[
      \frac{f(a)}{g(a)}=h(a).
      \]
      Since we have shown that $\lim_{x\to a} h(x) = h(a)$, we have
      shown that $h$ is continuous at $x=a$.
\end{explanation}
\end{theorem}

\begin{question}
  Where is $f(x) = \frac{x^2-3x+2}{x-2}$ continuous?
  \begin{prompt}
  \begin{multipleChoice}
    \choice{for all real numbers}
    \choice{at $x=2$}
    \choice[correct]{for all real numbers, except $x=2$}
    \choice{impossible to say}
  \end{multipleChoice}
  \end{prompt}
\end{question}
\begin{question}
  True or false: If $f$ and $g$ are continuous functions on an
  interval $I$, then $f\pm g$ is continuous on $I$.
  \begin{prompt}
  \begin{multipleChoice}
    \choice[correct]{True}
    \choice{False}
  \end{multipleChoice}
  \begin{feedback}
     Let's assume that $I$ is an open interval and $a$ is a number in $I$. Remember, since $f$ and $g$ are both continuous on $I$, they are both continuous at $a$. 
     
     This means that $ \lim_{x\to a}f(x)=f(a)$ and $ \lim_{x\to a}g(x)=g(a)$.
     
      Now, define a new function, $h$, where $h(x)= f(x)+g(x)$, for all $x$ in $I$. We have to show that $h$ is continuous at $a$, or that
    
    \[
    \lim_{x\to a} h(x) = h(a).
    \]
    Lat's start with
     
    \[
    \lim_{x\to a} h(x) =  \lim_{x\to a} (f(x)+g(x)) = \lim_{x\to a} f(x)+\lim_{x\to a}g(x)\hspace{0.04in}by \hspace{0.04in}Sum\hspace{0.04in} Law,
    \]
    and, therefore,
    
     \[
    \lim_{x\to a} h(x) =  f(a)+g(a)=h(a) \checkmark
    \]
We have proved that $h$ is continuous at  any number $a$ in $I$. Therefore, $h$ is continuous on $I$.
Similarly, we can prove that $f+g$ is continuous on any interval $I$, by showing it is left-or right-continuous at the endpoints.
We can adjust the proof for the function $f-g$.
  \end{feedback}
  \end{prompt}
\end{question}

\begin{question}
  True or false: If $f$ and $g$ are continuous functions on an
  interval $I$, then $f/g$ is continuous on $I$.
  \begin{prompt}
  \begin{multipleChoice}
    \choice{True}
    \choice[correct]{False}
  \end{multipleChoice}
  \begin{feedback}
    In this case, $f/g$ will not be continuous for $x$ where $g(x) =
    0$.
  \end{feedback}
  \end{prompt}
\end{question}


We still don't know how to compute  a limit of a composition of two functions.
Our next theorem provides basic rules for how limits interact with composition
of functions.

\begin{theorem}[Composition Limit Law]\index{composition limit law}
  If $f(x)$ is continuous at $b = \lim_{x\to a} g(x)$, then
  \[
  \lim_{x\to a} f(g(x)) = f(\lim_{x\to a} g(x)).
  \]
\end{theorem}

Because the limit of a continuous function is the same as the function
value, we can now pass limits inside continuous functions.

\begin{corollary}[Continuity of Composite Functions]

If $g$ is continuous at $x=a$, and if $f $ is continuous at $g(a)$,  then $f(g(x))$ is continuous at $x=a$.



\end{corollary}
Using the Composition Limit Law, we can compute the last example from the beginning of this section.
\begin{example}
  Compute the following limit using limit laws:
  \[
  \lim_{x \to \pi}\cos({x^3})
  \]
  \begin{explanation}
  We will use the Composition Limit Law. 
Let
 \[ 
 f(g(x))=\cos({x^3}),
 \]
 where $f(x)=\cos{x}$, and $g(x)=x^3$.
  Now, continuity of $x^3$ implies that $\lim_{x \to \pi}g(x)=\pi^3$.
    Continuity of $\cos{x}$ implies that $f$ is continuous at $\pi^3=\lim_{x \to \pi}g(x)$.
     Now, the Composition Limit Law implies that
    \[
    \lim_{x \to \pi}\cos({x^3})= \cos\Bigl({\lim_{x \to \pi} x^3}\Bigr)=\cos({\pi^3})\approx 0.91726.
    \]
   
  \begin{onlineOnly}
    We can confirm our results by checking out the graph of $y=f(g(x))$:
    \[
    \graph{\cos({x^3})}
    \]
  \end{onlineOnly}
  \end{explanation}
\end{example}

Many of the Limit Laws and theorems about continuity in this section
might seem like they should be obvious.  You may be wondering why we
spent an entire section on these theorems.  The answer is that these
theorems will tell you exactly when it is easy to find the value of a
limit, and exactly what to do in those cases.

The most important thing to learn from this section is whether the
limit laws can be applied for a certain problem, and when we need to
do something more interesting.  We will begin discussing those more
interesting cases in the next section.  
\section{A list of questions}

Let's try this out.

\begin{question}
  Can this limit be directly computed by limit laws?
  \[
  \lim_{x\to 2}\frac{x^2+3x+2}{x+2} 
  \]
  \begin{prompt}
  \begin{multipleChoice}
    \choice[correct]{yes}
    \choice{no}
  \end{multipleChoice}
  \begin{question}
    Compute:
    \[
    \lim_{x\to 2}\frac{x^2+3x+2}{x+2}\begin{prompt} =\answer{3}\end{prompt}
    \]
    \begin{feedback}
      Since $f(x)=\frac{x^2+3x+2}{x+2}$ is a rational function, and
      the denominator does not equal $0$, we see that $f(x)$ is
      continuous at $x=2$.  Thus, to find this limit, it suffices to
      plug $2$ into $f(x)$.
    \end{feedback}
  \end{question}
  \end{prompt}
\end{question}


\begin{question}
  Can this limit be directly computed by limit laws?
  \[
  \lim_{x\to 2}\frac{x^2-3x+2}{x-2}
  \]
  \begin{prompt}
  \begin{multipleChoice}
    \choice{yes}
    \choice[correct]{no}
  \end{multipleChoice}
  \begin{feedback}
    $f(x) = \frac{x^2-3x+2}{x-2}$ is a rational function, but the
    denominator $x-2$ equals $0$ when $x=2$. None of our current
    theorems address the situation when the denominator of a fraction
    approaches $0$.
  \end{feedback}
  \end{prompt}
\end{question}


\begin{question}
  Can this limit be directly computed by limit laws?
  \[
  \lim_{x\to 0} x\sin(1/x)
  \]
  \begin{prompt}
  \begin{multipleChoice}
    \choice{yes}
    \choice[correct]{no}
  \end{multipleChoice}
  \begin{feedback}
    If we are trying to use limit laws to compute this limit, we would
    first have to use the Product Law to say that
    \[
    \lim_{x\to 0}x\sin(1/x)= \lim_{x\to 0} x \cdot \lim_{x\to 0} \sin(1/x).
    \]
    We are only allowed to use this law if both limits exist, so we
    must check this first.  We know from continuity that
    \[
    \lim_{x\to  0}x=0.
    \]
    However, we also know that $\sin(1/x)$ oscillates ``wildly'' as
    $x$ approaches $0$, and so the limit
    \[
    \lim_{x\to 0} \sin(1/x)
    \]does not exist.  Therefore, we cannot use the
    Product Law.
  \end{feedback}
  \end{prompt}
\end{question}


\begin{question}
  Can this limit be directly computed by limit laws?
  \[
  \lim_{x\to 0} \cot(x^3)
  \]
  \begin{prompt}
  \begin{multipleChoice}
    \choice{yes}
    \choice[correct]{no}
  \end{multipleChoice}
  \begin{feedback}
    Notice that
    \[
    \cot(x^3) = \frac{\cos(x^3)}{\sin(x^3)}.
    \]
    If we are trying to use limit laws to compute this limit, we would
    like to use the Quotient Law to say that
    \[
    \lim_{x\to 0} \frac{\cos(x^3)}{\sin(x^3)} = \frac{\lim_{x\to 0}
      \cos(x^3)}{\lim_{x\to 0} \sin(x^3)}.
    \]
    We are only allowed to use this law if both limits exist and the
    denominator is not $0$. We suspect that the limit in the
    denominator might equal $0$, so we check this limit.
    \begin{align*}
      \lim_{x\to 0} \sin(x^3) &= \sin(\lim_{x\to 0}x^3)\\
      &=\sin(0) \\
      &=0.
  \end{align*}
  This means that the denominator is zero and hence we cannot use the
  Quotient Law.
  \end{feedback}
  \end{prompt}
\end{question}


\begin{question}
  Can this limit be directly computed by limit laws?
  \[
  \lim_{x\to 0}\sec^2(e^x-1)
  \]
  \begin{prompt}
  \begin{multipleChoice}
    \choice[correct]{yes}
    \choice{no}
  \end{multipleChoice}
  \begin{question}
    Compute:
    \[
    \lim_{x\to 0}\sec^2(e^x-1)\begin{prompt} =\answer{1}\end{prompt}
    \]
    \begin{feedback}
      Notice that
      \[
      \lim_{x\to 0} \sec^2(e^x-1) = \lim_{x\to 0} \frac{1}{\cos^2(e^x-1)}.
      \]
      If we are trying to use Limit Laws to compute this limit, we
      would now have to use the Quotient Law to say that
      \[
      \lim_{x\to 0} \frac{1}{\cos^2(e^x-1)} = \frac{ \lim_{x\to 0}1}{
        \lim_{x\to 0}\cos^2(e^x-1)}.
      \]
      We are only allowed to use this law if both limits exist and the
      denominator is not $0$.  Let's check the denominator and numerator
      separately. First we'll compute the limit of the denominator:
      \begin{align*}
        \lim_{x\to 0}\cos^2(e^x-1) &= (\lim_{x\to 0}\cos{(e^x-1)})^{2}\\
        &= \Bigl(\cos{\Big(\lim_{x\to 0}(e^x-1)\Bigr)}\Bigr)^{2}\\
        & =\cos^2\Bigl(\lim_{x\to 0}(e^x-1)\Bigr)\\
        &=\cos^2\Bigl(\lim_{x\to 0}(e^x)-\lim_{x\to 0}(1)\Bigr)\\
        &=\cos^2(1-1)\\
        &= \cos^2(0)\\
        &=1
      \end{align*}
      Therefore, the limit in the denominator exists and does not
      equal $0$. We can use the Quotient Law, so we will compute the limit of the numerator:
      \[
      \lim_{x\to 0}1=1
      \]
      Hence
      \[
      \frac{ \lim_{x\to 0}1}{ \lim_{x\to 0}\cos^2(e^x-1)} =
      \frac{1}{1}=1
      \]
    \end{feedback}
  \end{question}
  \end{prompt}
\end{question}


\begin{question}
  Can this limit be directly computed by limit laws?
  \[
  \lim_{x\to 1}{(x-1)\cdot \csc(\ln(x))}
  \]
  \begin{prompt}
  \begin{multipleChoice}
    \choice{yes}
    \choice[correct]{no}
  \end{multipleChoice}
  \begin{feedback}
    If we are trying to use limit laws to compute this limit, we would have to use the Product Law to say that
    \[
    \lim_{x\to 1}{(x-1)\cdot \csc(\ln(x))}= \lim_{x\to 1}{(x-1)\cdot \lim_{x\to 1}\csc(\ln(x))}.
    \]
    We are only allowed to use this law if both limits exist.  Let's
    check each limit separately.
    \begin{align*}
      \lim_{x\to 1} (x-1) &= \lim_{x\to 1} (x)-\lim_{x\to 1}(1)\\
      &=1-1\\
      &=0.
    \end{align*}
   So this limit exists. Now we check the other factor.
   Notice that
   \[
   \lim_{x\to 1}\csc(\ln(x)) = \frac{1}{\sin(\ln(x))}.
   \]
   If we are trying to use limit laws to compute this limit, we would now have to use the Quotient Law to say that
   \[
   \frac{1}{\sin(\ln(x))} = \frac{\lim_{x\to 1}1}{\lim_{x\to
       1}\sin(\ln(x))}.
   \]
   We are only allowed to use this law if both limits exist and the
   denominator does not equal $0$.  The limit in the numerator definitely
   exists, so let's check the limit in the denominator.
   \begin{align*}
   \lim_{x\to 1}\sin(\ln(x)) &= \sin(\lim_{x\to 1}\ln(x))\\
   &=\sin(\ln(1))\\
   &= \sin(0)\\
   &= 0
  \end{align*}
  Since the denominator is $0$, we cannot apply the Quotient Law.
  \end{feedback}
  \end{prompt}
\end{question}

\begin{question}
  Can this limit be directly computed by limit laws?
  \[
  \lim_{x\to 0} x\ln x
  \]
  \begin{prompt}
  \begin{multipleChoice}
    \choice{yes}
    \choice[correct]{no}
  \end{multipleChoice}
  \begin{feedback}
  If we are trying to use limit laws to compute this limit, we would
  have to use the Product Law to say that
  \[
  \lim_{x\to 0} x\ln x =\lim_{x\to 0} x \cdot \lim_{x\to 0}\ln x.
  \]
  We are only allowed to use this law if both limits exist.  We know
  $\lim_{x\to 0} x = 0$, but what about $\lim_{x\to 0}\ln x$?  We do
  not know how to find $\lim_{x\to 0}\ln x$ using limit laws because $0$
  is not in the domain of $\ln x$.
  \end{feedback}
  \end{prompt}
\end{question}


\begin{question}
  Can this limit be directly computed by limit laws?
  \[
  \lim_{x\to0}\frac{2^x-1}{3^{x-1}}
  \]
  \begin{prompt}
  \begin{multipleChoice}
    \choice[correct]{yes}
    \choice{no}
  \end{multipleChoice}
  \begin{question}
    Compute:
    \[
    \lim_{x\to0}\frac{2^x-1}{3^{x-1}}\begin{prompt} =\answer{0}\end{prompt}
    \]
    \begin{feedback}
      If we are trying to use limit laws to compute this limit, we
      would have to use the Quotient Law to say that
      \[
      \lim_{x\to 0}\frac{2^x-1}{3^{x-1}} = \frac{\lim_{x\to
          0}(2^x-1)}{\lim_{x\to 0}(3^{x-1})}.
      \]
      We are only allowed to use this law if both limits exist and the
      denominator does not equal $0$.  Let's check each limit
      separately, starting with the denominator
      \begin{align*}
        \lim_{x\to 0}(3^{x-1}) &=3^{\lim_{x\to0}(x-1)}\\
        &=3^{-1}\\
        &=\frac{1}{3}
      \end{align*}

      On the other hand the limit in the numerator is
      \begin{align*}
        \lim_{x\to 0}(2^x-1) &=\lim_{x\to0}(2^x)-\lim_{x\to0}(1)\\
        &=1-1\\
        &=0
      \end{align*}
      The limits in both the numerator and denominator exist and the
      limit in the denominator does not equal $0$, so we can use the
      Quotient Law.  We find:
      \[
        \frac{\lim_{x\to 0}(2^x-1)}{\lim_{x\to 0}(3^{x-1})}
        =\frac{0}{\frac{1}{3}}=0.
        \]
    \end{feedback}
  \end{question}
  \end{prompt}
\end{question}


\begin{question}
  Can this limit be directly computed by limit laws?
  \[
  \lim_{x\to 0}(1+x)^{1/x}
  \]
  \begin{prompt}
  \begin{multipleChoice}
    \choice{yes}
    \choice[correct]{no}
  \end{multipleChoice}
  \begin{feedback}
  We do not have any limit laws for functions of the form $f(x)^{g(x)}$, so we cannot compute this limit.
  \end{feedback}
  \end{prompt}
\end{question}

\end{document}
```


Here are examples of Ximera Exercises

\documentclass{ximera}

\author{Parisa Fatheddin \and Bart Snapp}

\begin{document}
  \begin{exercise}
    Which of the following quantites are vectors?
    \begin{selectAll}
      \pdfOnly{\begin{multicols}{2}}
      \choice{Zip codes.}
      \choice{Social security numbers.}
      \choice[correct]{Financial transactions.}
      \choice{Credit card numbers.}
      \choice[correct]{Consumer Data.}
      \choice{Phone numbers.}
      \choice[correct]{Earnings.}
      \choice[correct]{Distances.}
      \choice[correct]{Inventory counts.}
      \choice{License plate numbers.}
      \pdfOnly{\end{multicols}}
    \end{selectAll}
  \end{exercise}


\begin{exercise}
If a cruise ship starts at $(0,0)$ at 7:00am and travels with the
true bearing $53^\circ$ at $20$ knots until 5:00pm, when it reaches
its destination, then what are its coordinates at the end of the trip?
Round your answers to two decimal places.
\begin{prompt}
  We start by converting the bearing and speed into cartesian
  coordinates. Since we want to round our final answers to two decimal
  places, we will round this intermediate results to three decimal
  places.  Write with me:
  \begin{align*}
    \vec{c} &=
    \begin{pmatrix}
      \left(\answer{20}\right)\cdot\sin\left(\answer{53}^\circ\right)\\
      \left(\answer{20}\right)\cdot\cos\left(\answer{53}^\circ\right)
    \end{pmatrix}\\
    &=\begin{pmatrix}
      \answer{15.973} \\
    \answer{12.036}
  \end{pmatrix}
  \end{align*}
  The number of hours between 7:00am and 5:00pm is $\answer{10}$ hours.
  Hence we are at the coordiantes (in nautical miles):
  \[
10 \cdot \vec{c} = \begin{pmatrix}
      \answer{159.73} \\
    \answer{120.36}
  \end{pmatrix}
  \]
\end{prompt}
\end{exercise}


\begin{exercise}
  Suppose an airplane is scheduled to fly from Columbus to Cincinnati, a
  flight that takes $40$ minutes.  If the initial bearing of the plane
  is $235^{\circ}$ at $435$ knots, what are its coordinates when it
  reaches Cincinnati? Round your answers to two decimal places.
  \begin{prompt}
    We start by converting the bearing and speed into cartesian
    coordinates. Write with me:
    \begin{align*}
      \vec{p} &=
                \begin{pmatrix}
                  \left(\answer{435}\right)\cdot\sin\left(\answer{235}^\circ\right)\\
                  \left(\answer{435}\right)\cdot\cos\left(\answer{235}^\circ\right)
                \end{pmatrix}\\
              &=\begin{pmatrix}
                % \answer{-192.5} \\
                % \answer{-134.79}
                \answer{-356.33} \\
                \answer{-249.51}
              \end{pmatrix}
    \end{align*}
    Since the flight takes $\answer{40}$ minutes,
    which equals $\answer{2/3}$ hours,
    % and $\answer{40}$ minutes is $\answer{2/3}$ hours,
    the coordinates at the end of the
    flight are:
    \[
      \answer{2/3} \cdot \vec{p} = \begin{pmatrix}
        % \answer{-128.33} \\
        % \answer{-89.86}
        \answer{-237.55} \\
        \answer{-166.34}
      \end{pmatrix}
    \]
  \end{prompt}
\end{exercise}

\begin{exercise}
  Let $\vec{u},\vec{v},\vec{w}$ be nonzero column vectors with the same
  number of entries. Which of the following expressions make sense?
  \begin{selectAll}
    \pdfOnly{\begin{multicols}{2}}
    \choice[correct]{$(\vec{w} \dotp \vec{u} ) \vec{u}$}
    \choice[correct]{$5(\vec{u} +\vec{w}) \dotp {\vec{u}}$}
    \choice{$\vec{w} / \vec{u}$}
    \choice{$\vec{v}\vec{w}$}
    \choice[correct]{$\vec{w} / ( \vec{u} \dotp \vec{u})$}
    \choice{$\vec{u}\dotp \vec{v}+\vec{w}$}
    \pdfOnly{\end{multicols}}
  \end{selectAll}
  \begin{hint}
    Think about which terms/factors are vectors and which
    terms/factors are scalars.
  \end{hint}
\end{exercise}



\begin{exercise}
  The following column $3$-vector $\vec{g}$ represents the
  \link[official gray color]{https://bux.osu.edu/color/primary-colors}
  of the Ohio State University, in RGB:
  \[
    \vec{g} = \begin{pmatrix}
      167\\ 177\\ 183
    \end{pmatrix}
    \qquad
    \begin{array}{l}
      \text{Red}\\
      \text{Green}\\
      \text{Blue}
    \end{array}
    \]
    Create two shades of gray, one that is $50\%$ lighter than
    $\vec{g}$ and one that is $75\%$ lighter than $\vec{g}$.
    \begin{prompt}
      Recall that white is represented by
      \[
      \vec{w} = \begin{pmatrix}
        255\\ 255\\ 255
      \end{pmatrix}
      \qquad
      \begin{array}{l}
        \text{Red}\\
        \text{Green}\\
        \text{Blue}
      \end{array}
      \]
      To find a color $n\%$ lighter than $\vec{g}$, we will first find
      the difference between white and our color, and add various
      fractions of this difference to $\vec{g}$.

      First, compute the differences of RGB intensities between white
      and the OSU gray.
      \[
      \vec{d} = \vec{w} - \vec{g} =
      \begin{pmatrix}
        \answer{88}\\
        \answer{78}\\
        \answer{72}
      \end{pmatrix}
      \]
      Generate a lighter gray by adding $50\%$ of $\vec{d}$ to
      $\vec{g}$.
      \[
      \vec{g}_1 = \vec{g} + \left(\answer{0.5}\right)\vec{d} =
      \begin{pmatrix}
        \answer{211}\\
        \answer{216}\\
        \answer{219}
      \end{pmatrix}
      \]
      Generate an even lighter gray by adding $75\%$ of $\vec{d}$
      onto $\vec{g}$.
      \[
        \vec{g}_2 = \vec{g} + \left(\answer{0.75}\right)\vec{d} =
        \begin{pmatrix}
          \answer{233}\\
          \answer{235.5}\\
          \answer{237}
        \end{pmatrix}
      \]

      \begin{feedback}[correct]
        Use an online RGB color picker such as
        \link[this]{https://rgbcolorpicker.com} for visual confirmation of
        your work!
      \end{feedback}
    \end{prompt}
\end{exercise}


\begin{exercise}
  Which of the following vectors is/are orthogonal to $ \vec{v} = \begin{pmatrix} 1 & 5 & -2 & 0 \end{pmatrix}$.
  \begin{selectAll}
    \pdfOnly{\begin{multicols}{2}}
      \choice[correct]{$\vec{u} = \begin{pmatrix} 0 & 2 & 5 & 3 \end{pmatrix}$}
      \choice{$\vec{u} = \begin{pmatrix} 1 & 5 & -2 & 0 \end{pmatrix}$}
      % Zero vector is orthogonal to any vector.
      \choice[correct]{$\vec{u} = \begin{pmatrix} 0 & 0 & 0 & 0 \end{pmatrix}$}
      \choice[correct]{$\vec{u} = \begin{pmatrix} 4 & 1 & 9/2 & 10 \end{pmatrix}$}
      \choice{$\vec{u} = \begin{pmatrix} 1 & 0 & 0 & 0 \end{pmatrix}$}
      \choice[correct]{$\vec{u} = \begin{pmatrix} 1/3 & 3/5 & 5/3 & 2/3 \end{pmatrix}$}
      \choice{$\vec{u} = \begin{pmatrix} 2 & -2/5 & 1 & 0 \end{pmatrix}$}
      \pdfOnly{\end{multicols}}
  \end{selectAll}
\end{exercise}

\begin{exercise}
  For the vectors
  \[
    \vec{u} = \begin{pmatrix} 2\\ -3\\ -4 \end{pmatrix}, \quad
    \vec{v} = \begin{pmatrix} -5\\ 0\\ 1 \end{pmatrix}, \quad
    \vec{w} = \begin{pmatrix} 3 \\ 1 \\ -4 \end{pmatrix},
  \]
  find the following. Round answers to two decimal places, writing
  ``NA'' if it is not possible.
  \begin{enumerate}
    \pdfOnly{\begin{multicols}{3}}
    \item $\|\vec{u}\| + \|\vec{u}\|_{1} + \|\vec{u}\|_{\infty}$
      \begin{prompt}
        $=\answer{18.39}$
      \end{prompt}
    \item $2 \|\vec{v}\|_{\infty} \|\vec{w}\|_{\infty}$
      \begin{prompt}
        $=\answer{40}$
      \end{prompt}
    \item $\frac{\vec{u}}{\|\vec{v}\|_{1} \|\vec{w}\|_{1}}$
      \begin{prompt}
        $=\begin{pmatrix}
          \answer{.04} \\
          \answer{-.06} \\
          \answer{-.08}
        \end{pmatrix}$
      \end{prompt}
    \item $\|\vec{u}\| \dotp \|\vec{w}\|$ % dot product of two scalars = product of the scalars
      \begin{prompt}
        $=\answer{27.46}$
      \end{prompt}
    \item $\|\vec{v}\| \dotp \vec{v}$
      \begin{prompt}
        $=\answer[format=string]{NA}$
      \end{prompt}
    \item $\|\vec{w}\|_{1} \|\vec{v}\|_{\infty}$
      \begin{prompt}
        $=\answer{40}$
      \end{prompt}
    \item $\vec{u} \dotp \vec{v} + \|\vec{w}\|$
      \begin{prompt}
        $=\answer{-8.9}$
      \end{prompt}
    \item $\|\vec{v}\|_{1} \|\vec{w}\|_{\infty} \dotp \vec{u}$
      \begin{prompt}
        $=\answer[format=string]{NA}$
      \end{prompt}
    \item $\|\vec{v}\|_{\infty} \dotp \|\vec{u}\|_{\infty}$
      \begin{prompt}
        $=\answer{20}$
      \end{prompt}
      \pdfOnly{\end{multicols}}
  \end{enumerate}
\end{exercise}

\begin{exercise}
  Let
  \[
    \vec{u} = \begin{pmatrix} 0 & -2& -3 \end{pmatrix}, \quad
    \vec{v} = \begin{pmatrix} -1 & 0 & 4 \end{pmatrix}, \quad
    \vec{w} = \begin{pmatrix} 2 & 1 & -1 \end{pmatrix}, \quad
    \vec{h} = \begin{pmatrix} -3\\ 7\\ 0 \end{pmatrix}.
  \]
  Compute the following. If any of them is not possible, write ``NA''.
  \begin{enumerate}
    \pdfOnly{\begin{multicols}{4}}
    \item $\vec{u}\dotp \vec{v}$ \begin{prompt}$= \answer{-12}$\end{prompt}
    \item $\vec{v}\dotp \vec{u}$ \begin{prompt}$= \answer{-12}$\end{prompt}
    \item $\vec{u}\dotp \vec{v} \dotp\vec{w} $\begin{prompt} $= \answer[format=string]{NA}$\end{prompt}
    \item $\vec{w}\dotp \vec{v} $\begin{prompt} $=\answer{-6}$\end{prompt}
    \item $\vec{v}\vec{w}$ \begin{prompt} $= \answer[format=string]{NA}$\end{prompt}
    \item $\vec{v} \dotp \vec{h}$ \begin{prompt}$= \answer[format=string]{NA}$\end{prompt}
    \item $5 \vec{v} + 2\left(\vec{w}-\vec{u}\right)$ \begin{prompt} $= \begin{pmatrix} \answer{-1} & \answer{6} & \answer{24}\end{pmatrix}$ \end{prompt}
    \item $2 \vec{w}^\transpose - 3\left(\vec{u}^\transpose + \vec{h}\right)$\begin{prompt}$= \begin{pmatrix} \answer{13} \\
      \answer{-13}\\
      \answer{7}
    \end{pmatrix}$\end{prompt}
  \pdfOnly{\end{multicols}}
\end{enumerate}
\end{exercise}


\begin{exercise}

  Normalize the following vector using Euclidean norm, 1-norm and infinity norm. Round your answers to two decimal places.
  \[
    \vec{u} = \begin{pmatrix} 2 & -3& 4 & -8 & 0\end{pmatrix}
  \]

  \begin{prompt}
    Normalizing by Euclidean norm:
    \[
      \begin{pmatrix}
        \answer{.21} & \answer{-.31} & \answer{.41} & \answer{-.83} & \answer{0}
      \end{pmatrix}
    \]

    Normalizing by 1-norm:
    \[
      \begin{pmatrix}
        \answer{.12} & \answer{-.18} & \answer{.24} & \answer{-.47} & \answer{0}
      \end{pmatrix}
    \]

    Normalizing by $\infty$-norm:
    \[
      \begin{pmatrix}
        \answer{.25} & \answer{-.38} & \answer{.5} & \answer{-1} & \answer{0}
      \end{pmatrix}
    \]
  \end{prompt}
\end{exercise}


\end{document}

