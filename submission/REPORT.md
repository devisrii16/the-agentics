# CrewAI Build Report

**Name:** Devi Sri Sagurupilli  
**Topic I used:** How AI can help university students explore career options

## 1. What I changed

I modified the Technical Writer agent in `crewai-kit/main.py` to explain the topic to a 10-year-old instead of a smart reader outside the field. I changed the Writer’s `goal` and `backstory` to request short sentences, familiar words, explanations of unfamiliar terms, and everyday examples from school, hobbies, and games.

I chose this modification because career guidance often contains technical language that beginners may find difficult to understand. The topic also connects to my interest in using AI for career exploration. Changing the intended audience provided a practical way to observe how agent instructions influence generated content.

I kept the Research Analyst, Editor, task definitions, model settings, and sequential process unchanged. I used the same topic for both runs. The modification visibly changed the Writer’s intermediate draft, but the Editor did not preserve the simpler style in the final output. Therefore, the result demonstrated partial success and revealed a limitation in how audience instructions were carried through the workflow.

## 2. How CrewAI works

CrewAI organizes a workflow using agents, tasks, and a crew. Each agent has a role, goal, and backstory that guide how the language model approaches its work. This starter kit contains three agents: a Research Analyst, a Technical Writer, and an Editor.

Each task describes the work assigned to an agent and the expected result. The research task requests five facts and two open questions. The writing task requests a 250-word explanation based on the research brief. The editing task asks for a tighter explanation with unsupported claims marked.

The crew brings these agents and tasks together. It uses `Process.sequential`, which runs the tasks in order and provides earlier results as context for later tasks. The agents share the same configured language model, but their different instructions give them separate responsibilities.

My modification influenced the Writer because its goal and backstory explicitly requested language suitable for children. However, the Editor had its own instructions, which did not require preserving that audience. The final response returned to formal language. This showed me that an instruction given to one agent does not automatically become a requirement for every later agent. To preserve the audience consistently, I would also need to include that requirement in the editing stage.

## 3. Evidence

The original final explanation is saved in `explainer_run1.md`, and its terminal record is saved in `run1_original.txt`. It used formal language, named commercial platforms, and included numerical claims about career matching and advising.

The modified execution is recorded in `run2_changed.txt`, and its final explanation is saved in `explainer_run2.md`. The Writer’s intermediate draft began with “Imagine you have a smart helper.” It also used examples involving clubs, games, and school. These changes showed that the revised audience instructions affected the Writer.

The surprising result was that the Editor replaced the simpler wording with formal expressions such as “occupational clusters” and “labor-market demand.” The final explanation therefore did not retain the intended child-friendly style. I preserved this result as evidence and identified the missing audience requirement in the editing stage as a possible improvement.

The second run also reported an empty LLM response during the Writer task. Execution continued, and the task subsequently completed without a manual restart.

Although both runs used the same topic, their research briefs differed. Therefore, I cannot attribute every content difference to the Writer modification.

## 4. Choosing a framework

I would choose CrewAI for a project that can be divided into clear responsibilities. For a career exploration project, one agent could summarize occupation information, another could explain possible career paths, and another could review the explanation for clarity and unsupported claims. CrewAI makes these responsibilities easy to express through roles, goals, and tasks.

The terminal output was useful because it displayed each agent’s response separately. This allowed me to identify where the audience change appeared and where it was lost. However, the experiment also showed that having several agents does not automatically guarantee consistent instructions or accurate information.

Based on the class guide, LangGraph would provide more explicit control through state, nodes, and edges. It could be useful if a career guidance system needed a review checkpoint or a loop that returned unsuitable recommendations for revision.

LangGraph would require me to define those transitions and conditions explicitly. CrewAI was a convenient choice for this small sequential writing workflow. For a larger application requiring controlled review and revision, I would consider LangGraph. Neither framework would automatically verify factual claims; that would require appropriate sources, tools, and checks.

## 5. Verification and AI use

I checked that the setup test displayed `CrewAI kit OK` and that both runs completed. I compared the original and modified outputs, including the intermediate responses in the terminal logs. The modified Writer used simpler language and familiar examples, but the Editor returned to a formal style. This showed that my change affected the Writer without fully achieving the intended final result.

I also noticed that the outputs included statistics and references to university studies. Because the kit has no web access, I treated these claims as unverified. The Editor did not consistently mark them with `[source needed]`, so its review was not sufficient to establish factual accuracy.

I used ChatGPT for setup guidance, troubleshooting, modifying the Writer’s instructions, comparing the results, and drafting this report. I ran the code myself in VS Code and checked the suggested change against the actual execution output.