---
title: oracles
date: "2019-05-30"
description: Question answering and answering questions
---

Sophocles is wise, Euripides is wiser, but of all men Socrates is wisest.
-Pythia (440 BCE)


During WWII, Vannevar Bush was the director of the Office of Scientific Research and Development (OSRD). The OSRD received funding from Congress and had the authority to develop weapons and technologies with or without the military. The organization grew to 850 full-time employees, produced over 30,000 reports, and signed 2,500 contracts worth $536 million. Toward the end of the war he published As We May Think, a hypothetical blueprint for an information retrieval system of the future called the Memex.

Much needs to occur between the collection of data and observations, the extraction of parallel material from the existing record, and the final insertion of new material into the general body of the common record. For mature thought there is no mechanical substitute. But creative thought and essentially repetitive thought are very different things. For the latter there are, and may be, powerful mechanical aids.

Machines have been made which will read typed figures by photocells and then depress the corresponding keys; these are combinations of photocells for scanning the type, electric circuits for sorting the consequent variations, and relay circuits for interpreting the result into the action of solenoids to pull the keys down.

The advanced arithmetical machines of the future will be electrical in nature, and they will perform at 100 times present speeds, or more. Moreover, they will be far more versatile than present commercial machines, so that they may readily be adapted for a wide variety of operations. They will be controlled by a control card or film, they will select their own data and manipulate it in accordance with the instructions thus inserted, they will perform complex arithmetical computations at exceedingly high speeds, and they will record results in such form as to be readily available for distribution or for later further manipulation. Such machines will have enormous appetites.

-Vannevar Bush (As We May Think, 1945)

Open and Closed Domains
Baseball was the first computer program built to answer questions phrased in natural language. An example question is, "Where did each team play on July 7?" It was written in IPL-V, a language that inspired LISP by using list structures to represent information. The program performed a series of operations on a given piece of text:

Read question from punched card.

Look up words and idioms in a dictionary.

Determine the phrase structure and syntactic facts.

List attribute-value pairs to specify information given and information requested.

Extract requested information from the data matching the specifications.

Process extracted information and print

Since the program is designed for the specific use case of Baseball it is considered a closed-domain QA system. The authors speculate about the possibilities of improving the system to answer a broader range of questions, a direction that will eventually become known as open-domain question answering.

Considerable pains were taken to keep the program general. Most of the program will remain unchanged and intact in a new context, such as voting records. The processing program will handle data in any sort of hierarchical form, and is indifferent to the attributes used. The syntax program is based entirely on parts of speech, which can easily be assigned to a new set of words for a new context.

On the other hand, some of the subroutines contained in the dictionary meanings are certainly specific to baseball; probably each new context would require certain subroutines specific to it. Also, each context might introduce a number of modifiers and derived attributes that would have to be defined in terms of special subroutines for the processor. Hopefully, all such occasions for change have been isolated in a small area of special subroutines, so that the main routines can be unaltered. However, until we have actually switched contexts, we cannot say definitively that we have been successful in producing a general question-answering program.

-Bert Green et al. (Baseball: An Automatic Question-Answerer, 1961)

First-Order Logic
A larger variety of question answering systems started to appear in the mid-60s as higher level programming languages and time sharing grew. Early programs include Bertram Raphael's SIR (1964) and James Slagle's DEDUCOM (1965). Researchers were exploring different methods for loading and analyzing large collections of information.

Claude Green and Bertram Raphael described two versions of a QA system in 1967 and define a question answering system as having the following abilities:

Accepts statements of facts and store them in memory.

Searches stored information and recognizes items relevant to the question.

Recognizes if the relevant knowledge to answer to question is not explicitly available.

Previous work in question answering has pointed up two key problems that must be solved before practical question-answering systems can be developed: the problem of identifying relevant facts and the problem of deducing answers that are not explicit in the data.

-Green, Raphael (The Use of Theorem-Proving Techniques in Question-Answering Systems, 1968)

QA1 uses a list-structured memory for relational information. It consists of facts about relations and specific facts about objects. QA2 uses predicate calculus to employ theorem-proving techniques. This enables more sophisticated logical reasoning with a simpler memory structure. They considered theorem-proving promising for several reasons:

The language is well defined, unambiguous, and general.

The proof procedure allows all possible interaction among the axioms and is logically complete. If a theorem is a logical consequence of the axioms, then this procedure will find a proof, given enough time and space.

The theorem-prover is subject-independent. Describing a new subject or modifying a previous description only requires changing the axioms and not the program.

These formal techniques may be generally valuable to the field of artificial intelligence.

Efficiency of theorem-provers is increasing.