---
title: HCI - Klausurfragensammlung
aliases:
tags:
description:
draft: false
---
## Perception & Cognition

> [!question]- What is Affordance?
> Affordances are properties or features of an artefact which indicate a certain type of usage, often grounded in our physiology/body/nature.
> 
> If the affordances are good, no labels are needed for easy/trivial functions.
> 
> - Door with knob implies turning is needed
> - Door with handle implies pulling is needed

> [!question]- Give an example of a False Affordance.
> A False Affordance suggests a possible action that doesn't actually exist or doesn't work - e.g. a door handle that invites pulling even though the door must be pushed (a "Norman Door"), or underlined, colored text that looks like a link but isn't.

> [!question]- What are Constraints? How do they relate to Affordances?
> Restricting the possible actions that can be performed - "inverse" of affordances, possibly augmenting them.
> 
> - **Goals**: avoid usage errors, minimize the information to be remembered
> - **Types**: physical, semantic, logical, cultural
>
> **Physical** - cable can only plug in one way
> **Logical** - use logical conclusions to exclude certain solutions (e.g. Only valid days can be selected on a calendar)
> **Semantic** - use common knowledge about the world and the meaning of the situation (e.g. a driver figurine in a model plane kit must face forward); powerful but only valid if the rule holds across the whole user population
> **Cultural** - rely on generally accepted cultural conventions (e.g. red = stop/attention); only applies within a specific cultural group - hand gestures and writing direction differ
>
> Relationship to affordances: constraints are the **inverse** of affordances - while affordances suggest what *can* be done, constraints restrict what *cannot* be done, together narrowing the perceived possibility space down to the intended actions.

> [!question]- What are Analogies/Mappings?
> Connect functionality to (UI) elements/to the real world.
> 
> - **Spatial Analogy** - arrange controls the same way as their real-world counterparts (room lamps, driving wheel, car stereo audio fader)
> - **Physical Analogy** - mapping follows physical real-world behavior (e.g. rising level = more, falling level = less); natural for additive dimensions like amount, heat, volume, thickness, brightness, weight
> - **Cultural Analogy** - mapping follows cultural conventions (e.g. Western left-to-right writing conveys linear ordering)
> - **Perceptual Analogy** - the input/output device looks like the actual thing it controls or monitors (e.g. Mercedes car seat controls)

> [!question]- What are Metaphors? Name all types.
> The interface (or part of it) is designed to be similar to a physical entity. Example: desktop metaphor - monitor treated as a desktop, objects placed/moved/opened into windows, moved to recycle bin, printer, etc.
>
> **Advantages**: helps users understand the underlying conceptual model, makes learning new systems easier
> **Disadvantages**: forces users to understand the system only in terms of the metaphor, designers can transfer bad parts of an existing design, metaphors can be understood differently by each user (ambiguity)
>
> **Types**:
> - **Verb-based** - established/new activities share conceptual similarities (cut and paste, drag and drop)
> - **Noun-based** - conceptual similarity between known and new objects (folders have creation dates and owners, an inbox contains new/unread info, warning signs)
> - **Noun+verb-based** - transfer activities performable on a known object to a new one (folder can be deleted (land in trashbin), folder can be recovered (be picked out of trashbin))

> [!question]- What are the 7 stages of actions?
> Perception → Interpretation → Comparison → Goal → Intention → Action Sequence → Execution

> [!question]- What is the Gulf of Execution and of Evaluation? Relate the gulfs to the 7 stages.
> **Gulf of Execution** - does the system provide actions that correspond to the intentions of the user? Opens up through differences between:
> - the user's goals and the available/visible possibilities to reach them
> - actions the user intends and actions the system offers
> - actions the system affords and actions that are actually possible
>
> Ideally the system lets users execute intended actions directly, without extra effort.
>
> **Gulf of Evaluation** - does the system provide visible feedback that is directly interpretable in terms of the user's intentions and expectations? Opens up through:
> - actual lack of feedback
> - non-interpretable feedback
> - feedback that doesn't match the intention/goal, so the user can't assess whether the goal was reached
>
> **Relation to the 7 stages**: the Gulf of Execution spans the "downhill" half of the cycle (Goal → Intention → Action Sequence → Execution) - the gap between forming a goal and actually performing the action. The Gulf of Evaluation spans the "uphill" half (Perception → Interpretation → Comparison) - the gap between perceiving the resulting system state and evaluating whether it matches the goal.

> [!question]- What is the Conceptual Model?
>???

> [!question]- What is distributed Cognition? Name examples.
> Forms of reducing internal memory/computation load by using the external world:
> - **External memory** - navigating with a map or writing down notes.
> - **External Process** -  speed display in your car or calculator

> [!question]- What is the extended mind theory?
> - technology (e.g. smartphones) are replacing parts of your mind/memory
> - instead of remembering numbers and paths we use functionalities of the phone
> - putting the emphasizes even more onto good interfaces with the technology

> [!question]- How many chunks fit into working memory?
> Classically, per Miller: **7 ± 2 chunks**

> [!question]- What isn't contained in the Human Information Processing?
> - social, emotional, and motivational factors of the user

> [!question]- Explain the 2 directions of perception (Bottom-Up and Top-Down).
> - **Bottom-Up (data-driven)**: perception is built directly from sensory input - starting from simple features (edges, colors, contrasts) up to more complex structures, without prior knowledge.
> - **Top-Down (knowledge-driven)**: prior knowledge, expectations, and context shape how sensory data is interpreted - incomplete or ambiguous stimuli are filled in/interpreted using experience.
> - Example application: hard-to-read handwriting or noisy images are recognized through both bottom-up feature extraction (stroke shapes) AND top-down contextual knowledge (expected word/object).

> [!question]- What does Helmholtz's theory of unconscious inference state? Sketch an example.
> Perception is the result of unconscious, automatic inferences that the brain draws from ambiguous sensory data based on prior experience, arriving at the most likely interpretation of the world. 
> 
> [Example](https://upload.wikimedia.org/wikipedia/commons/0/02/Ponzo_illusion.gif)

> [!question]- What are Gestalt Laws? Name all types.
> Gestalt Principles are principles/laws of human perception that describe how humans group similar elements, recognize patterns and simplify complex images when we perceive objects.
> - Closure: The principle of closure states that when we look at a complex arrangement of visual elements, we tend to look for a single, recognizable pattern.
> - figure-ground: The figure-ground principle states that people instinctively perceive objects as either being in the foreground or the background. As a human, you can focus on either the foreground or the background
> - Common Fate: The law of common fate suggests that when multiple visual elements move in the same direction or at the same speed, we tend to perceive them as a cohesive unit or a single entity rather than individual components.
> - proximity: The principle of proximity states that things that are close together appear to be more related than things that are spaced farther apart.
> - similarity: The principle of similarity states that when things appear to be similar to each other, we group them together and we also tend to think they have the same function.
> - common-region: The principle of the common region is highly related to proximity. It states that when objects are located within the same closed region, we perceive them as being grouped together
> - continuity: The principle of continuity states that elements that are arranged on a line or curve are perceived to be more related than elements not on the line or curve.

## Dark Patterns

> [!question]- Name all Dark Patterns and explain.
> Nagging · Obstruction · Sneaking · Interface Interference · Forced Action
> - **Nagging** - redirection of expected functionality that persists across interactions (e.g. repeated pop-ups asking to enable notifications after being dismissed)
> - **Obstruction** - making a process more difficult than necessary to dissuade an action (e.g. burying "cancel subscription" behind multiple confirmation screens)
> - Sneaking - Attempting to hide, disguise, or delay the divulging of information that is relevant to the user (hide ads in reviews)
> - Interface Interference - Manipulation of the user interface that privileges certain actions over others (highlight buttons etc)
> - Forced Action - ?