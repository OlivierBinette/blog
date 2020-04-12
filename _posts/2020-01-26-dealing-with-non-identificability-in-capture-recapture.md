---
layout: post
title: Dealing with non-identifiable population size in overparameterized capture-recapture models.
categories: [Capture-Recapture, Multiple Systems Estimation, Bayesian Statistics]
---

Multiple systems estimation (or the capture-recapture census) refers to a set of methods used to estimate the size of a given population when exhaustive enumeration is infeasible. The methods rely on multiple relatively small samples or on multiple sources of incomplete information in order to estimate the population size through various deductions.

One of the first recorded use of multiple systems estimation, here taking its form as a simple ratio estimator, dates back to the 17th century. John Graunt (1620-1674), a well-aquainted London citizen and later member of the newly established Royal Society, estimated London's population size in 1661 to be at 384,000. This number was derived as follows in his "Observations Made Upon the Bills of Mortality", a successful book published in five editions at the time and which is now considered an early landmark of population statistics. Estimating the yearly death rate to be at "3 [persons] out of 11 families per annum" using information from some parishes, and comparing this to the figure of about 13,000 burials per year, he obtains 48,000 families in London. Following a rough argument for an average of 8 persons per family, he concludes the population size is at $8\cdot 48\,000 = 384\,000$. This number is corroborated by Graunt in two ways: by considering the christening rates instead of the death rates, and by estimating the number of houses within the walls of London. Later in 1665, Graunt also corrected a 1631 census of the central part of London by a vague area argument, arriving at a population size of $403\,000$. Even though some elements of the analyses amount to cherry-picked guesses, Graunt's work can be commended for its transparency, its critical assessment of the reliability of the data, his analysis of the stability of statistical ratios over time, and for the multiple arguments through which he derives and validates estimates. [Hald, 1990]

Another notable application of this idea is from Laplace in 1802 (Hald, 1990; Cochran, 1978 Stigler's The History of Statistics p. 166; Laplace, 1886 p.399), who estimated France's population at the time to be around 28 millions. This was done by combining together two sources of information. First, censuses from a number of municipalities were used to estimate the population birth rate to be about $3.53\%$. Second, assuming a million birth in France in a year (which according to Laplace is "not far from the truth" (Laplace, 1886)), this gave the total population size estimated at 
$$
\frac{1 \text{ million}}{3.53\%}\approx 28\text{ million}. \tag{1}
$$

This kind of computation was not new at the time (see e.g. Moheau, 1778); Laplace's main contribution, was in bounding the error of his estimate. Using an asymptotic approximation, he calculated the posterior probability that his estimate was off by more than half a million to be less than $1/1000$ [(Cochran, 1978)].





> I know only of Laplace's method through the explanation which M. Quetelet has been kind enough to give me. [...]
>
> If it were easy to divide any arbitrary country according to the differences among these laws, the procedure as described would lead without doubt to the proposed end. But is is here that difficulties appear which, it seems to me, are nearly impossible to overcome.
>
> The law regulating mortality is composed of a large number of elements: it is different for towns and for the flatlands, for large opulent cities and for smaller and less rich villages, and depending on wether the locality is dense or sparsely populated. [...]
>
> It is nearly the same as regards the laws which regulate births.
>
> [...] If such a division of the kingdom could be accomplished on an approximately exact basis, it is likely that it would consist of such a large number of parts that there would be little advantage in terms of work saved.
>
> In my opinion there is only one way of attaining exact knowledge of the population and the elements of which it is composed, and that is an actual and complete census, the formation of a register of the names of all inhabitants, together with their ages and professions. (Keverberg, 1827, as cited by Stigler's The History of Statistics p.165).

> [Quetelet] was acutely aware of the infinite number of factors that could affect the quantities he wished to measure, and he lacked the information that could tell him which were indeed important. He, like the generation of social scientists to follow, was reluctant to group together as homogeneous, data that he had reason to believe was not.

> After Quetelet had learned for himself (in a way Laplace never did) the extent to which brith and death rates could vary, he could not bring himself to treat large regions as homogeneous, he coult not think of a single rate as applying to a large area, and a fortiori he could not conceive of measuring the uncertainty of an estimate where the very thing being estimated was uncertain and ill-defined.

> Quatelet's first instinct had been to group observations crudely and treat ratios as constant in large, superficially similar districts. But Keverberg's comments and his own empirical evidence had robbed him of his boldness. Astronomers had overcome a similar case of intellectual cold feet in the previous century by comparing observation with fact, by comparing prediction with realization. Success had bolstered confidence in the combination of observations. Social scientists were to require massive empirical data gathered under a wide variety of circumstances before they gained the astronomer's confidence that the quantities they measured were of sufficient stability that the uncertainty of the estimates was itself susceptible to measurement.

(Quotes above from Stigler's The History of Statistics)



**References:**

- Moheau, M. (1778) Recherches et considérations sur la population de France. Moutard, Paris. https://gallica.bnf.fr/ark:/12148/bpt6k1055816q
- Laplace (1886) Oeuvres complètes VII.
- Laplace (1886) Oeuvres complètes XI.
- Lincoln, F. C. (193) Calculating Waterfowl Abundance on the Basis of Banding Returns

