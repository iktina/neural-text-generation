# Neural Text Generation
## Welcome
The service receives a textual seed and uses it as input to the pre-trained generative model.
## What’s the point?
The service outputs generated text that is a continuation of a given seed.
## Model details:
The service receives a textual seed in English and uses it as input to the neural GPT-2 model trained to solve diverse text generation task using large-scale Reddit-dump based dataset and outputs the generated text for a given seed. The model runs on a P100 GPU. The basic commonsense model generates diverse text adapting to the style and content of the given text seed. The number of models will be expanded to allow the generation of texts related to specific subject areas and simulate the discourse of public persons. 

The following models are currently available:
"Phil Plait", "Barack Obama", "Bethany Brookshire", "Bernie Sanders", "Bill Gates", "Chris Hadfield", "Conan O'Brien", "Deborah Blum", "Deepak Chopra", "wint", "Elon Musk", "Eric Weinstein", "Hillary Clinton", "jimmyfallon", "Joe Biden", "Joe Rogan", "Dr Jordan B Peterson", "Justin Bieber", "Katy Perry", "Kevin Hart", "Kim Kardashian West", "Lady Gaga", "Brian Switek", "Neil deGrasse Tyson", "NietzscheQuotes", "John McAfee", "Donald J. Trump", "Rebecca Skloot", "Richard Dawkins", "Ricky Gervais", "Sam Harris", "Terence McKenna", "Ellen DeGeneres", "Dwayne Johnson", "God", "TicBot", "Very Short Story", "Virginia Hughes".
## How does it work?
The user must provide the following inputs in order to start the service and get a response:
Inputs:
 -   `org_id`: snet
 -   `service_id`: text-generation
 -   `group_name`: gefault_group
 -   `method`: gen_gpt_2
 -   `input_path`: Path to '\*.txt' file containing JSON representation of input arguments `start_text`, `temperature` (optional) and `top_k` (optional), and their respective values.
Input arguments:
 -   `start_text`: leave this field empty or insert the beginning of the text to generate a continuation.
 -   `run_name`: The name of the model to use for text generation. Should be selected as a key from [persons.txt](https://github.com/iktina/neural-text-generation/blob/master/persons.txt).
 -   `temperature`: prediction variability; May take values in the interval `(0.1, 1.2)`; `1.0` by default.
 -   `top_k`: limit on the number of tokens to take/on output; May take integer values in the interval `(0, 100)`; `0` by default.
 -   `length`: length of generated sequence. May take integer values in the interval `(0,1024)`; `256` by default.
 
Example of input file content:
```
{"start_text": "Before boarding your rocket to Mars, remember to pack these items", "run_name":"trump", "temperature": 1.2, "top_k": 20, "length":512}
```
You can call the service from SingularityNET CLI (`snet`).
Assuming that you have an open channel (`id: 0`) to this service:
```
$ snet client call snet text-generation default_group gen_gpt_2 samples/sample.txt
Read call params from the file: samples/sample.txt
"Before boarding your rocket to Mars, remember to pack these items : A small camera and the ability to take pictures. 
And if you can do it alone, bring the best outfit for the job: black leather boots, heavy gloves, a helmet, an oxygen pack, water bottle… 
If you're worried about getting your boots and gloves wet or if there will be any dust in them, pack enough sunscreen for a couple hours and leave that on, too. 
Make sure, though, that it's your only outfit on the Martian. No need to pack sunglasses with you. 
If you have a helmet, don't forget: wear it if you're in the shade. If the wind blows it up into your eyes then get a helmet from a friend who is going to wear them anyway and then use them for the journey as much as possible in the shade."
```
## What to expect from this service?
Input data:
Start text:  `Before boarding your rocket to Mars, remember to pack these items`
Response:
```
"Before boarding your rocket to Mars, remember to pack these items : A small camera and the ability to take pictures. 
And if you can do it alone, bring the best outfit for the job: black leather boots, heavy gloves, a helmet, an oxygen pack, water bottle… 
If you're worried about getting your boots and gloves wet or if there will be any dust in them, pack enough sunscreen for a couple hours and leave that on, too. 
Make sure, though, that it's your only outfit on the Martian. No need to pack sunglasses with you. 
If you have a helmet, don't forget: wear it if you're in the shade. If the wind blows it up into your eyes then get a helmet from a friend who is going to wear them anyway and then use them for the journey as much as possible in the shade."
```
Input data:
Start text:  *(empty)*
Response:
```
"The Browns have announced the release of running back Kyler Fackrell, leaving a vacancy on the roster after losing multiple receiving targets and finding itself on the hot seat heading into the season.
The Browns announced the decision in announcing that Fackrell had been released. A fourth-round pick by the Browns in 2011, Fackrell had rushed for 1,134 yards and 10 touchdowns while averaging 4.8 yards per carry in six season. He rushed for 12 touchdowns in 2007, before when he went down with a broken kneecap and subsequent shoulder injury.
This news comes a day after the team announced running back Ray Rice allegedly assaulted an unconscious woman. That was after reporters called out what they described as widespread allegations of knee-on-knee abuse, including a coordinated assault, against some of the team's other players. It wasn't clear exactly how serious those allegations were."
Former Browns quarterback Quizz Rodgers said Monday on ESPN 105.7 FM's Saturday Sports Show that there was "balance" between the allegations and a sordid history between the team and some of its players.
"I'm convinced that if you launch a lie against somebody, then you're going to fire the person responsible, and the fireman will only define his line every time," Rodgers said. "That was the intricate folded way it was real, one for a woman in the stands and then in the hotel elevator of his hotel room, all its own deep fabric, and that was telling, and that shows a failure of control that can never be fixed."
