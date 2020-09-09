---
title: thought vectors
date: "2019-05-08"
description: natural language processing and its implications
---

>*Just trying to deal with the unanalyzed chaotic data is unlikely to get you anywhere.*
>
>***Noam Chomsky (2012)***

![](https://cdn.substack.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fbucketeer-e05bbc84-baa3-437e-9518-adb32be77984.s3.amazonaws.com%2Fpublic%2Fimages%2F52a4abd1-4693-4d7c-90f4-bdc4bc9ac26b_661x504.png)

# Computers, Language, and Thought

Four years before his tragic death and six years before the official creation of the field called artificial intelligence, Alan Turing [proposed a linguistic game](http://cogprints.org/499/1/turing.html) to consider the question of whether or not a machine can think. He suggested using a digital computer as the machine and teaching it how to learn English by providing training data instead of explicitly programming it.

>*We may hope that machines will eventually compete with men in all purely intellectual fields. But which are the best ones to start with? Even this is a difficult decision. Many people think that a very abstract activity, like the playing of chess, would be best. It can also be maintained that it is best to provide the machine with the best sense organs that money can buy, and then teach it to understand and speak English. This process could follow the normal teaching of a child. Things would be pointed out and named, etc. Again I do not know what the right answer is, but I think both approaches should be tried.*
>
>***Alan Turing***  
>***Computing Machinery and Intelligence, 1950***

# Machine Translation

One year earlier Warren Weaver [published a memorandum](http://www.mt-archive.info/Weaver-1949.pdf) urging further research into the use of digital computers to automatically translate between languages.

>*The attached memorandum on translation from one language to another, and on the possibility of contributing to this process by the use of modern computing devices of very high speed, capacity, and logical flexibility, has been written with one hope only - that it might possibly serve in some small way as a stimulus to someone else, who would have the techniques, the knowledge, and the imagination to do something about it.*
>
>***Warren Weaver***  
>***Translation, 1949***

As a basis for Weaver’s belief that a computer could perform translations he referenced Warren McCulloch and Walter Pitts. They stated that regenerative loops of a certain formal character (neural networks) are capable of deducing any legitimate conclusion from a finite set of premises.

>*The role of brains in determining the epistemic relations of our theories to our observations and of these to the facts is all too clear, for it is apparent that every idea and every sensation is realized by activity within that net.*
>
>***Warren McCulloch, Walter Pitts***  
>***A Logical Calculus of the Ideas Immanent in Nervous Activity, 1943***

# Question Answering

Mass production of computers in the 50s and 60s enabled more individuals to experiment. Daniel Bobrow wrote a [computer program in Lisp](https://dspace.mit.edu/bitstream/handle/1721.1/5922/AIM-066.pdf) that could answer questions about algebraic story problems posed in plain English.

>*I shall not bore the reader at this point with a diatribe on why one would want to communicate to the Computer in English. Man's ability to use symbols and language is a prime factor in his intelligence, and when we learn how to make a computer understand any natural language, we will have taken a large step toward creating an "artificially intelligent" machine.*
>
>***Daniel Bobrow***  
>***Natural Language Input for a Computer Problem Solving System, 1964***

# Conversational Agents

Around the same time Joseph Weizenbaum created a program that could [simulate a conversation](https://web.stanford.edu/class/linguist238/p36-weizenabaum.pdf) with the user. It used simple pattern matching rules to reply to the user’s input.

>*ELIZA is a program which makes natural language conversation with a computer possible. Its name was chosen to emphasize that it may be incrementally improved by its users, since its language abilities may be continually improved by a "teacher". Like the Eliza of Pygmalion fame, it can be made to appear even more civilized, the relation of appearance to reality, however, remaining in the domain of the playwright.*
>
>***Joseph Weizenbaum***  
>***ELIZA: A Computer Program for the Study of Natural Language Communication Between Man and Machine, 1966***

# Natural Language Understanding

Increasingly sophisticated programming languages were designed for a variety of tasks as computer processing power increased. Carl Hewitt designed [Planner](https://dspace.mit.edu/bitstream/handle/1721.1/6171/AIM-168.pdf) for proving theorems. A subset of the language, Micro-Planner, was used in Winograd's natural-language understanding program [SHRDLU (1971)](https://apps.dtic.mil/dtic/tr/fulltext/u2/721399.pdf), Eugene Charniak's [story comprehension work (1972)](https://dspace.mit.edu/handle/1721.1/13796), and Thorne McCarty's [work on legal reasoning (1977)](https://www.researchgate.net/profile/L_Thorne_Mccarty2/publication/259872868_Reflections_on_TAXMAN_An_Experiment_in_Artificial_Intelligence_and_Legal_Reasoning/links/00b4952e55de995ab3000000.pdf).

>*A foundation for problem solving must specify a goal-oriented formalism in which problems can be stated. Furthermore there must be a formalism for specifying the allowable methods of solution of problems. As part of the definition of the formalisms the following elements must be defined: the data structure, the control structure, and the primitive procedures.*
>
>***Carl Hewitt***  
>***PLANNER: A Language for Manipulating Models and Proving Theorems in a Robot, 1969***

# Winter

Some researchers’ excitement for these pioneering techniques lead to overconfident predictions. The government funding agencies were disappointed by the relatively modest success of these approaches. [The ALPAC Report (1966)](http://www.mt-archive.info/ALPAC-1966.pdf) and the [Lighthill Report (1972)](http://www.chilton-computing.org.uk/inf/literature/reports/lighthill_report/p001.htm) cast significant doubt on the entire field. Finally, the [Mansfield Amendment (1973)](https://www.bibliotecapleyades.net/sociopolitica/sociopol_DARPA01.htm) limited ARPA appropriations to only projects with direct military application.

# Rebirth

The first generation of language researchers tasked with teaching computers to read, write, listen, and speak were humbled by the seer immensity of their problem space. They collided head first into the oldest and most fundamental philosophical questions of meaning, knowledge, and reason. Linguistics fractured into fractal subfields of Cognitive Linguistics, Neurolinguistics, Psycholinguistics, Sociolinguistics, and many more.

Progress continued in the field of Computational Linguistics. [Statistical language models](https://www.aclweb.org/anthology/J92-4003) started to surpass old methods in [translation](https://www.aclweb.org/anthology/J90-2002), [topic modeling](http://www.psychology.uwo.ca/faculty/harshman/latentsa.pdf), and [sentiment analysis](http://www.cs.cornell.edu/home/llee/papers/sentiment.pdf). [Distributional semantics](https://www.tandfonline.com/doi/pdf/10.1080/00437956.1954.11659520) and [neural networks](http://www.jmlr.org/papers/volume3/bengio03a/bengio03a.pdf) were rediscovered and reconfigured to capitalize on the exponentially increasing web data and processing power five [orders-of-magnitude](https://en.wikipedia.org/wiki/Computer_performance_by_orders_of_magnitude) higher than 70 years ago.

Neural languages models currently dominate both large scale production systems ([Google](https://arxiv.org/pdf/1609.08144.pdf%20(7.pdf), [Baidu](https://www.aclweb.org/anthology/P15-1166), [Amazon](https://twimlai.com/twiml-talk-030-natural-language-understanding-amazon-alexa-zornitsa-kozareva/)) and state of the art research ([Microsoft](https://arxiv.org/pdf/1901.11504.pdf), [Facebook](https://arxiv.org/pdf/1605.07683.pdf), [Apple](https://machinelearning.apple.com/2018/09/27/can-global-semantic-context-improve-neural-language-models.html)). The creators of the [GPT-2 model](https://openai.com/blog/better-language-models/) at OpenAI believe their model may be powerful enough to pose a danger to society.

>*Pride even in numbers; wit's a kind pretence*  
>*To something foreign still, but ne'er to sense;*
>
>*A constant waste of words, the world produces,*  
>*That's foreign still unknown to the soul*
>
>***GPT-2***  
>***Neural Network Poetry, 2019***

# Characteristica universalis

Marin Mersenne asked René Descartes to [evaluate a project](http://www.autodidactproject.org/other/descartes-lg1.html) in 1629 concerning a new universal language. The symbols would serve as an interlingua with a universal grammar. This idea would go on to captivate many philosophers including John Wilkins, Francis Lodwick, George Dalgarno, and most famously Gottfried Leibniz.

Below is a section of Descartes’ reply to Mersenne. I entered the original French text into Google Translate. Here is the unedited English output:

>*And if anyone had clearly explained what are the simple ideas that are in the imagination of men, of which everything is composed, and that it was received by everyone, I would then dare to hope for a universal language, very easy to learn, pronounce and write. But do not expect to see it ever in use; that presupposes great changes in the order of things, and the whole world should be but an earthly paradise, which is only good to propose in the country of novels.*