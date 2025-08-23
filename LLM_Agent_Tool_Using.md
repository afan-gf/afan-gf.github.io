# LLM Agent Tools Using, From Prompt and SFT to Agentic RL

Tool using is a crucial capability for LLM Agents, enabling them to truly interact with the environment and expand the boundaries of agent capabilities. How to enable LLM Agents to better use tools has always been a popular and valuable research direction. This post discuss the current LLM Agent tools using from a survey perspective.

## 1. How LLM Agent Uses Tools and Key Challenges

The basic pattern of LLM Agent using tools can be summarized as follows:

1) Inform the LLM about the problem/task to solve and the available tool set information (tool name, using description, parameter introduction, etc.) through prompts.

2) The LLM reasons and outputs solution steps. If a tool is needed, it outputs the tool name and parameters.

3) The Agent executes the corresponding tool in the tool space, generates results, and if needed, feeds the results back to the next round of prompts.

<img width="604" height="209" alt="Foed back" src="https://github.com/user-attachments/assets/685859f6-282e-4369-b47e-efe372cd3efd" />

The LLM is the most critical element in the tool using process, determining the upper limit of the Agent's tool using capabilities. The LLM needs to:

1) Decide which tool to use for planning

2) Determine when to use it

3) Know how to use it - provide function call parameters and tool using context

4) Dynamically adjust based on tool execution feedback to handle open scenarios

5) Find optimal tool using solutions for multi-step complex tasks

These challenges can be summarized as: how to improve LLM's tool using capabilities?

## 2. Methods to Improve LLM Tool Using Capabilities Over Time

Three phases of methods can be identified chronologically:
- Early approaches used Prompt engineering
- Later, data-centric approaches used SFT or DPO methods
- Since DeepSeek-R1's work is released, RL (Reinforcement Learning) has become a hot research direction

### Method 1: Prompt
Using in-context learning to provide prompt examples of tool using, or carefully designing specific reasoning and tool using prompt schemes. Representative work: ReAct.

### Method 2: SFT
Based on data-centric ideas, adding tool using training data to LLM's training dataset and improving tool using capabilities through SFT. Representative works: ToRA, Toolace.

### Method 3: RL
Since DeepSeek-R1's work, test-time compute scaling has become a hot research direction. Many works reference DeepSeek-R1's approach, using similar rule-based RL methods for specific tool using capabilities or general open environment tool using, achieving good results.

The Prompt method attempts to unlock the LLM's tool using capabilities through structured prompts, but is limited by the model's inherent capabilities and static parameters. Essentially, it does not improve the model's tool using capabilities and instead sacrifices some generality due to the introduction of structured prompts.

The SFT method relies on the quantity and quality of training data. Tool using data is inherently sparse compared to other training data, making it difficult to substantially improve the model's tool using capabilities at the core level.

In contrast, the RL method guides the model through **tool using reasoning**, then uses tools to interact with the environment to instruct the model in learning tool using capabilities. This method has been verified to simply and effectively greatly enhance the model's ability to handle complex tool using and open-ended tasks.

## 3. Comparison of Three Methods

| Method | Advantages | Limitations | Representative Works |
|--------|------------|-------------|---------------------|
| Prompt | 1) In-context learning provides tool using examples<br>2) Carefully designed reasoning and tool using prompt schemes | Simple and generic implementation without changing LLM parameters | ReAct, Ecoact |
| SFT | Data-centric approach, improves tool using through training data | Depends on data quantity and quality, tool using data is sparse | ToRA, Toolace, xlam |
| RL | Rule-based RL methods guide LLM to autonomously improve tool using capabilities through training | Makes complex task and open environment tool using possible, but training efficiency is a bottleneck | ARTIST, ToRL, OTC, ZeroTIR, Kimi-Researcher, Nemotron-Tool-N1 |

## Agentic RL Training for Tool Using

The RL approach can be simply summarized as shown in the diagram.
<img width="689" height="219" alt="Reward" src="https://github.com/user-attachments/assets/30e0f445-c8c3-40d1-8119-cfa478f1b151" />


### Representative Work: ARTIST
Microsoft's recent work: ARTIST: Agentic Reasoning and Tool Integration for LLMs via Reinforcement Learning, 2025
<img width="892" height="346" alt="Figure 2 Overview of the ARTIST methodolory  Thie fmumework illusinites how reamningrollouts" src="https://github.com/user-attachments/assets/b5750df9-538e-4458-8154-49faa54dcdcf" />

Based on rule-based RL using GRPO algorithm. Compared to SFT which requires training a reward model, this approach doesn't need that. Reward design doesn't focus on reasoning output details, but includes:
1) Problem solving results (Answer Reward)
2) LLM output format correctness (Format Reward)
3) Tool execution situation (Tool Execution Reward)
<img width="903" height="537" alt="Algorithm 1 Trlinine ARTIST with Group Relative Policy Optimization (GRFO)" src="https://github.com/user-attachments/assets/ae2f210f-597b-4499-a1d2-191cf03908e5" />

Performance shows significant improvement.
<img width="878" height="358" alt="Owen2 5 7B-ingruct" src="https://github.com/user-attachments/assets/07ef0d02-069f-4d28-9cfc-91bbf86b0d6f" />

## Open Questions

1) How to let LLM Agent evolve from using tools to creating tools.

2) How to train more effective and general tool-using LLMs while pushing LLM's vertical domain tool using capabilities to the limit.

3) Evaluation systems and methods aligned with real-world application scenarios.

## References

[1] React: Synergizing reasoning and acting in language models, 2023  
[2] ToRA: A Tool-Integrated Reasoning Agent for Mathematical Problem Solving, 2023  
[3] ReTool: Reinforcement Learning for Strategic Tool Use in LLMs, 2025  
[4] Agentic Reasoning and Tool Integration for LLMs via Reinforcement Learning, 2025  
[5] Agent RL Scaling Law: Spontaneous Code Execution for Mathematical Problem Solving, 2025  
[6] AReaL: A Large-Scale Asynchronous Reinforcement Learning System for Language Reasoning, 2025  
[7] Nemotron-Research-Tool-N1: Exploring Tool-Using Language Models with Reinforced Reasoning, NVIDIA, 2025  
[8] OTC: Optimal Tool Calls via Reinforcement Learning, 2025  
[9] ToRL: Scaling Tool-Integrated RL, 2025  
[10] Kimi-Researcher End-to-End RL Training for Emerging Agentic Capabilities, 2025
