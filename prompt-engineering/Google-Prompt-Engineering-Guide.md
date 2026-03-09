# This is a note from [Google Prompt Engineering Whitepaper](https://www.kaggle.com/whitepaper-prompt-engineering)

## LLM output optimal configuration
- Output length: set the number of tokens to generate in a response. Generating more tokens requires more computation from the LLM, leading to higher energy consumption and potentilly slower response times, which leas to higher costs.
- Sampleing controls: LLMs do not formally predict a single token. Rather, LLMs predict probabilities for what the next token could be, with each token in the LLM's vocabulary getting a probability. Those token probabilities are then sampled to determine what the next produced token will be. Temperature, top-K and top_p are the most common configuration settings that determine how predicted token probabilities are processed to choose a single output token.
  1. Temperature: controls the degree of randomness in token selection. 
    - Lower temps are good for prompts that expect a more deterministic response. A temp of 0(greedy decoding) is deterministic: the highest probability token is always selected)
    - Higher temps can lead to more diverse or unexpected results. Temps close to the max tend to create more random output. As temp gets high and higher, all tokens become equally likely to be the next predicted token.
  2. Top-K and Top-P(a.k.a nucleus sampling): used in LLMs to restrict the predicted next token to come from tokens with the top predicted probabilities.
    - Top-K: selects the top K most likely tokens from the model's predicted distribution.
    - Top-P: selects the top tokens whose cumulative probability does not exceed a certain value(P). Values for P range from 0(greedy decoding) to 1 (all tokens in the vocab)
    - The best way to choose between top-K and top-P is to experiment with both methods(or both together)
    - Note from me
      - The power of '0': For tasks where the format is critical, such as data extraction or JSON formatting, just set Temp=0. It makes debugging significantly eaiser.
      - Handling repetition loops: If it happens during production, consider `presence_penalty` and/or `frequency_penalty` rather than blindly increasing the temp

## Prompting tchniques
The clearer your prompt text, the better it is for the LLM to predict the next likely text. Additionally, specific techniques that take advantage of how LLMs are trained and how LLMs work will help you get the relevant results from LLMs.
1. General prompting / Zero shot
A zero-shot prompt is the simplest type of prompt. It only provides a description of a task and some text for the LLM to get started with. The name zero-shot stands for `no examples`. 

--- 
## Idioms & Misc
- Greedy decoding: At each step, the model identifies the single token with the highest probability and selects it as the next output
- What is 'K' in 'Top-K'?: In Top-K sampling, the "K" represents a fixed integer that defines the size of the "shortlist" of candidate tokens.

