
---
Created : 2026-09-23
---

Throughout my project, a habit that experience has frequently demonstrated the value of is keeping very detailed notes while researching and implementing features. During my project I have recorded a vast majority of any results, research, issues, and ideas relating to the project in dated weekly development logs, the current list of which can be seen in *Artefact: ```weekly_log_ls_output.txt```*. Examples of my weekly logs can be seen in *Artefact: ```Weekly-Log-2026-05-05.md```*, where I record notes from discussions with my supervisors about developing a particular algorithm, and *Artefact: ```Weekly-Log-2026-07-20.md```*, where I investigate the source of an error related to face orientation encoding. Being able to refer back to these notes on nearly any topic or issue I have encountered has improved my work efficiency as I would not need to go and effectively re-research a topic which I have already recorded, which would typically break my mental flow.

I record my notes in Markdown (```.md```) documents, which, as can be seen by the format of my reflections (also Markdown), has grown on me. Markdown is very simple and efficient to write, not requiring the use of graphical user interfaces (GUIs) to format, and allows the user to frictionlessly write syntax-highlighted code blocks, and LaTeX-style mathematical typesetting (see the appendix for examples of both). Markdown, as I have discovered from observing my supervisors writing, is also commonly used in high-performance computing and mathematics. Markdown has made recording notes on a variety of topics significantly easier than the previous formats I have used, being far simpler and more efficient for recording mathematics and code compared to Microsoft Word or LibreOffice Writer, and requiring less syntactic caution and abstraction (e.g. handling source documents and PDFs) than pure LaTeX.

Refining my methodology of managing digital information was a skill of mine that I highlighted as needing improvement in my Independent Study Contract (ISC) under *Use of Tools and Technology 3*, specifically in developing a methodology for collaborative and technical environments. Keeping thorough records and notes of all aspects of my project and the aforementioned benefits, alongside a talk by Dr. Jacob Martin regarding the value of lab books in professional physics laboratories, has driven home how important and valuable *almost* excessive pedanticism can be in high-performance computing (HPC) and mathematical research. Consistently recording my notes in Markdown over the year has made both my use of Markdown and my tendency to record an idea or issue almost second-nature.

The aforementioned improvement to my work efficiency has obvious benefits to my future career in high-performance computing and mathematics. Additionally, being very comfortable and fluent with synthesising my thoughts in Markdown has helped me better retain what I have learnt and take notes quicker, both of which have similarly clear benefits to a career in HPC and mathematics, as well as careers in general.

# Appendix

## Syntax-Highlighted Code Block Example

Below is an example of a C++ program that prints "Hello World":

```cpp
#include <iostream>

int main( int argc, char** argv ) {
  std::cout << "Hello World" << std::endl;

  return 0;
}
```

## LaTeX-Style Mathematical Typesetting Example

This is the general solution for an inhomogeneous first-order linear difference equation (note that some Markdown viewers don't render LaTeX):

$$
x_n = x_0 \prod_{i = 1}^{n} a \left( i \right)  + \sum_{k = 2}^{n} \left( b \prod_{l = k}^{n} a \left( l \right) \right) + b
$$

