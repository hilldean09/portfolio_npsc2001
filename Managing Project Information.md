
---
Created : 2026-09-23
---

Throughout my project, a habit that experience has frequently demonstrated the value of is keeping very detailed notes while researching and implementing features. During my project I have recorded a vast majority of any results, research, issues, and ideas relating to the project in dated weekly development logs, the current list of which can be seen in *Artefact: ```weekly_log_ls_output.txt```*. Examples of my weekly logs can be seen in *Artefact: ```Weekly-Log-2026-05-05.md```*, where I record notes from discussions with my supervisors about developing a particular algorithm, and *Artefact: ```Weekly-Log-2026-07-20.md```*, where I investigate the source of an error related to face orientation encoding.

I record my notes in Markdown (```.md```) documents, which, as can be seen by the format of my reflections (also Markdown), has grown on me. Markdown is very simple and efficient to write, not requiring the use of graphical user interfaces (GUIs) to format, and allows the user to frictionlessly write syntax highlighted code blocks, and LaTeX style mathematical typesetting (see the appendix for examples of both).



# Appendix

## Syntax Highlighted Code Block Example

Below is an example of a C++ program that prints "Hello World":

```cpp
#include <stdio>

int main( int argc, char** argv ) {
  std::cout << "Hello World" << std::endl;

  return 0;
}
```

## LaTeX Style Mathematical Typesetting Example

This is general solution for a inhomogeneous first-order linear difference equation (note that some Markdown viewers don't render LaTeX):

$$
x_n = x_0 \prod_{i = 1}^{n} a \left( i \right)  + \sum_{k = 2}^{n} \left( b \prod_{l = k}^{n} a \left( l \right) \right) + b
$$

