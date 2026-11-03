[**WEEK SIX SLIDES**](https://shawngraham.github.io/hist3000-f26/slides/wk6.html#/0/1) 

- three-sentence reading memos
    1. name, date, thesis (what)
    2. how 
    3. why
       
[Electric Archaeology](https://electricarchaeology.ca/)
  
[Herculaneum Archaeological Park](https://ercolano.cultura.gov.it/the-theater/?lang=en)
    - origins of American political obsession with classical architecture

- three vague eras of archaeology
    1. culture history: distinguishing and signalling the presence and belonging of X group to Y place through history. diffusionism 
    2. processual: 1960s. Lewis Binford (jerk) laws of culture and human behaviour which can be identified by hypothesizing and gathering as much data as possible (emergence of peer review as a scholarly method; until this point work was published based on relationships.) interest in processes: computational archaeology, formulas, pragmatism, empirical data collection
    3. post-processual: 1980s. Michael Shanks, Chris Tilley, Ian Hodder. Recognition that scientific objectivity doesn't exist. we are all biased. archaeology exists beyond white men.
    4. post-post-processual: today. countless intellectual frameworks for interpreting and understanding
       
Doing Stuff!!!!!!!

- seriation: battleship curves --> diagonal correspondence indicates change over time
- stratigraphy: comes from geology. superposition (chronology). sedimentology: things at the top are newer/younger than things at the bottom. context: single events/actions leave traces (cuts, fills, structures, surfaces) --> reveals intention and changing values
      - becomes massively important and relevant in post-war Europe (war destruction and postwar infrastructure development; superhighways, reconstructing cities, etc.)
      - [harris matrices](https://harrismatrix.com/about-the-matrix/) become a signifier of archaeological professionalism in the era of commercially driven work in the 20th century
  

R: statistics.... not like Python

[Chi-square association test (Pearson, 1950s):](https://statisticsfundamentals.com/hypothesis-testing/chi-square-test-examples/) 

1. what kind of data are you dealing with?
2. contingency table

wtf is a cramer's v OH its just statistical significance. its just a (p) value. ok

point pattern analysis--> yay environmental science!!!!!!!!!!
    - intersite comparisons to visualize a broader network of relations 

-----

R Archaeostats Activity

- data doesnt tell a story but it is something from which a story can be told; the distinction is small but immensely significant


View(DartPoints) notice that View starts with a capital V. Lower-case 'view' will give you an error. case matters for command function!!

`mean(DartPoints$Length) 
summary(DartPoints$Length)`

options(digits=3)
`numSummary(DartPoints[, 5:11])`

'column 1-4' where 1=5; 4=8
  options(digits=3)
`numSummary(DartPoints[, 5:8])`

remember to add View() command to actually see the data

`data(EngrBone)
View(EngrBone)`

for this activity everything is inside (archdata) so i don't have to use the data(name) command every time?

'(MESO_Type <- table(Axes$Microliths)) 
barplot(MESO_Type, main="mesolithic", xlab="microliths", ylab="axes")'

> Error: object 'Axes' not found
Traceback:
.handleSimpleError(function (cnd) 
 . {
 .     watcher$capture_plot_and_output()
 .     cnd <- sanitize_call(cnd)
 .     watcher$push(cnd)
 .     switch(on_error, continue = invokeRestart("eval_continue"), 
 .         stop = invokeRestart("eval_stop"), error = NULL)
 . }, "object 'Axes' not found", base::quote(eval(expr, envir)))

https://colab.research.google.com/github/shawngraham/digiarch-labbench/blob/main/week-05/archaeo-stats-in-R.ipynb#scrollTo=ad0026df-a3f8-42da-adc0-f26e568e73e3&line=2&uniqifier=1 


couldn't find PKM in command palette to id my cell so here is a screenshot instead. 
<img width="549" height="637" alt="Screenshot 2026-11-03 at 1 24 23 PM" src="https://github.com/user-attachments/assets/24d7455a-8fda-4fca-8774-586fbc0f3472" />

i used a different dataset and it worked better:
`data(EWBurials)
(EWBurials.tbl <- xtabs(~Sex+Age, EWBurials))
barplot(EWBurials.tbl, ylab="age", main="EWB")`

<img width="579" height="480" alt="Screenshot 2026-11-03 at 1 49 30 PM" src="https://github.com/user-attachments/assets/343c5a21-da7c-4174-b8c5-939daf58b727" />

`chisq.test`

`chisq.test(Mesolithic$Axes, Mesolithic$Saws, correct=FALSE`

`correct=FALSE` -> no Yates correction
`correct=TRUE` -> Yates correction 

the reason my tables were looking so weird was bc i was using datasets with different kinds of variables. i needed one with factors to get a nice table 

`data(PitHouses)` -> factors

`data(Mesolithic)` -> no factors

`data(RBPottery)` -> Kiln & Region factors!

`data(RBPottery)
(table(RBPottery$Kiln, RBPottery$Region))`

  this is a good example bc the kiln style is very clearly associated with region so if i get a small p-value i'm on the right track. unless everything is wonky because of the zero values 

  `chisq.test(RBPottery$Kiln, RBPottery$Region, correct=FALSE)`

   Warning message in chisq.test(RBPottery$Kiln, RBPottery$Region, correct = FALSE):
“Chi-squared approximation may be incorrect”

Pearson's Chi-squared test

data:  RBPottery$Kiln and RBPottery$Region
X-squared = 96, df = 8, p-value <2e-16

ok


BACups: is there a relationship between cup height and chronological phase?

`data(BACups)
chisq.test(BACups$H, BACups$Phase, correct=FALSE)`

data:  BACups$H and BACups$Phase
X-squared = 38, df = 35, p-value = 0.4

