---
title: HCI - Klausurfragensammlung
aliases:
tags:
description:
draft: false
---
## Perception & Cognition

> [!question]- What is Affordance?
> Affordances are the actions that the design of an object suggests to the user. Affordance can be substituted with "is for". Examples: knobs are for ("afford") turning, slots are for inserting, chairs are for sitting.
> - **Real affordances** - physical objects, affording e.g. grasping; perceptually obvious
> - **Perceived affordances** - screen-based interfaces, "learned conventions"
>
> See [[Affordances]].

> [!question]- Give an example of a False Affordance.
> A False Affordance suggests a possible action that doesn't actually exist or doesn't work - e.g. a door handle that invites pulling even though the door must be pushed (a "Norman Door"), or underlined, colored text that looks like a link but isn't.

> [!question]- What are Constraints? How do they relate to Affordances?
> Restricting the possible actions that can be performed - "inverse" of affordances, possibly augmenting them.
> - **Goals**: avoid usage errors, minimize the information to be remembered
> - **Types**: physical, semantic, logical, cultural
>
> **Physical** - e.g. where do you plug in the mouse and the keyboard, does the coloring help?
> **Logical** - use logical conclusions to exclude certain solutions (e.g. all parts of a jigsaw puzzle are to be used); natural mappings often use logical constraints
> **Semantic** - use common knowledge about the world and the meaning of the situation (e.g. a driver figurine in a model plane kit must face forward); powerful but only valid if the rule holds across the whole user population
> **Cultural** - rely on generally accepted cultural conventions (e.g. red = stop/attention); only applies within a specific cultural group - hand gestures and writing direction differ
>
> Relationship to affordances: constraints are the **inverse** of affordances - while affordances suggest what *can* be done, constraints restrict what *cannot* be done, together narrowing the perceived possibility space down to the intended actions. See [[Constraints in HCI]].

> [!question]- What are Analogies/Mappings?
> - **Spatial Analogy** - arrange controls the same way as their real-world counterparts (room lamps, driving wheel, car stereo audio fader)
> - **Physical Analogy** - mapping follows physical real-world behavior (e.g. rising level = more, falling level = less); natural for additive dimensions like amount, heat, volume, thickness, brightness, weight
> - **Cultural Analogy** - mapping follows cultural conventions (e.g. Western left-to-right writing conveys linear ordering)
> - **Perceptual Analogy** - the input/output device looks like the actual thing it controls or monitors (e.g. Mercedes car seat controls)
>
> See [[Mapping and Analogy in HCI]].

> [!question]- What are Metaphors? Name all types.
> The interface (or part of it) is designed to be similar to a physical entity. Example: desktop metaphor - monitor treated as a desktop, objects placed/moved/opened into windows, moved to recycle bin, printer, etc.
>
> **Advantages**: helps users understand the underlying conceptual model, makes learning new systems easier
> **Disadvantages**: forces users to understand the system only in terms of the metaphor, designers can transfer bad parts of an existing design, metaphors can be understood differently by each user (ambiguity)
>
> **Types**:
> - **Verb-based** - established/new activities share conceptual similarities (cut and paste, drag and drop)
> - **Noun-based** - conceptual similarity between known and new objects (folders have creation dates and owners, an inbox contains new/unread info, warning signs)
> - **Noun+verb-based** - transfer activities performable on a known object to a new one (wastebasket, buttons, checkboxes)
>
> See [[Metaphors in HCI]].

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
> **Relation to the 7 stages**: the Gulf of Execution spans the "downhill" half of the cycle (Goal → Intention → Action Sequence → Execution) - the gap between forming a goal and actually performing the action. The Gulf of Evaluation spans the "uphill" half (Perception → Interpretation → Comparison) - the gap between perceiving the resulting system state and evaluating whether it matches the goal. See [[Gulf of Execution and Evaluation]].

> [!question]- What is the Conceptual Model?
> A conceptual model is a high-level description of a product - a mental model that allows users to predict the effects of their actions, cope with problems, and is formed through experience, practice, and instruction. A good conceptual model presents operations and results consistently, giving the user a coherent image of the system.

> [!question]- What is external Cognition? Name examples.
> Forms of reducing internal memory/computation load by using the external world:
> - **Externalizing to reduce memory load** - transform knowledge into external representations to reduce memory load, e.g. birthdays/appointments → calendar, phone numbers → address book, things to do → post-it notes/to-do lists. Location can matter.
> - **Computational offloading** - reduce cognitive effort by using an external representation, e.g. using pen and paper to solve a math problem (multiplying 234 × 456 in your head vs. with pen and paper - you offload partial results by writing them down). The representation itself matters too - Arabic numerals make this much easier than Roman numerals, even though the problem is mathematically equivalent.
> - **Annotating and cognitive tracing** - e.g. marking/checking an entry in a to-do list once it's finished.

> [!question]- What is the extended mind theory?
> *(Draft, possibly not covered in the slides)* Clark & Chalmers (1998): cognitive processes can extend beyond the head into external tools and the environment, if those tools are functionally integrated into the thinking process in the same way as internal memory/processing ("active externalism"). Classic example: a notebook that performs the same function as biological memory for someone with a memory impairment then counts as part of the cognitive system. Closely related to [[Situated Action]] and External Cognition above - please cross-check whether/how this term was covered in the slides.

> [!question]- How many chunks fit into working memory?
> Classically, per Miller: **7 ± 2 chunks** (also used this way in the [[Model Human Processor]]). More recent estimates (Cowan) suggest closer to **~4 ± 1 chunks**, see [[Human Memory Systems]]. The exam likely wanted the 7±2 figure from the lecture - please double-check which number was used in the slides.

> [!question]- What isn't contained in the Human Information Processing?
> *(Draft)* The [[Model Human Processor]] (perceptual/cognitive/motor processors + memories) does **not** model:
> - social, emotional, and motivational factors of the user
> - situated, improvised action that doesn't follow from pre-formed internal plans (see [[Situated Action]] as a competing view)
> - collaboration between multiple users
> - learning and change processes over time (long-term learning curves)
> - external contextual factors that situationally influence behavior

> [!question]- Explain the 2 directions of perception (Bottom-Up and Top-Down). Explain them in detail using the example of the image [shown in the lecture].
> *(Draft)*
> - **Bottom-Up (data-driven)**: perception is built directly from sensory input - starting from simple features (edges, colors, contrasts) up to more complex structures, without prior knowledge.
> - **Top-Down (knowledge-driven)**: prior knowledge, expectations, and context shape how sensory data is interpreted - incomplete or ambiguous stimuli are filled in/interpreted using experience.
> - Example application: hard-to-read handwriting or noisy images are recognized through both bottom-up feature extraction (stroke shapes) AND top-down contextual knowledge (expected word/object) - compare with [[Gestalt Principles]] (Closure) and Helmholtz's unconscious inference (next question).

> [!question]- What does Helmholtz's theory of unconscious inference state? Sketch an example.
> *(Draft)* Perception is the result of unconscious, automatic inferences that the brain draws from ambiguous sensory data based on prior experience, arriving at the most likely interpretation of the world. Classic example: the Necker cube or the hollow-face illusion, where the same sensory data leads to different perceptions depending on the unconscious interpretation.

> [!question]- What are Gestalt Laws? Name all types.
> Good Shape · Proximity · Closure · Similarity · Continuity · Experience · Common Fate · Symmetry · Law of Common Region
>
> See [[Gestalt Principles]] for the commonly-used modern subset (Proximity, Similarity, Continuity, Closure, Common Region, Figure-Ground, Connectedness, Common Fate) with UI examples.

> [!question]- Name 4 Gestalt Laws. Explain two and show example applications in design.
> Four examples: Proximity, Similarity, Closure, Common Region.
> - **Proximity**: elements placed close together are perceived as belonging together - e.g. grouping of form fields.
> - **Common Region**: elements within the same bounded area are perceived as a group - e.g. cards/panels with a visible border.
>
> See [[Gestalt Principles]].

> [!question]- Which 2 Gestalt Laws does this image violate? ["Keep Red Off Line" from the lecture]
> *(Cannot be answered without the image from the lecture - please check the slides.)*

## Errors & Dark Patterns

> [!question]- Name 3 Dark Patterns and explain 2.
> Nagging · Obstruction · Sneaking · Interface Interference · Forced Action
> - **Nagging** - redirection of expected functionality that persists across interactions (e.g. repeated pop-ups asking to enable notifications after being dismissed)
> - **Obstruction** - making a process more difficult than necessary to dissuade an action (e.g. burying "cancel subscription" behind multiple confirmation screens)
>
> See [[Dark Patterns]].

> [!question]- Name a Dark Pattern used in each of the following images. [Once the "Nagging" example and the "Obstruction" example from the lecture]
> Image 1: **Nagging**. Image 2: **Obstruction**. See [[Dark Patterns]].

## Design

> [!question]- What 2 types of errors are there, and what distinguishes them?
> **Slips** (execution errors) - the intention is correct, but the action goes wrong (occurs during automatic, skilled behavior).
> **Mistakes** (planning errors) - the plan itself is wrong, the intention doesn't match the goal (stems from incorrect [[Mental Models]] or incomplete knowledge).
>
> See [[Human Error in HCI]].

> [!question]- What is Transparency?
> *(Draft)* Transparency refers to how well the current system state and its way of functioning are visible and understandable to the user - the more transparent a system, the easier it is for the user to interpret feedback across the [[Gulf of Execution and Evaluation|Gulf of Evaluation]] and keep their [[Mental Models|mental model]] of the system accurate.

> [!question]- What are the 4 components of User Centered Design? Name the goal of each. Name and explain a practical method for each component.
> The four stages of the iterative cycle (ISO 9241-210):
> 1. **Specify context of use** - Goal: understand who the users are, what tasks they perform, and in what environment. Method: [[Ethnography in HCI|Ethnography]] - observing users in their natural environment.
> 2. **Specify user requirements** - Goal: translate context understanding into explicit, testable requirements. Method: [[Interview Techniques in HCI|Interviews]] - targeted questioning about needs and goals.
> 3. **Produce design solutions** - Goal: create prototypes ranging from low- to high-fidelity. Method: [[Prototyping in HCI|Prototyping]] (e.g. paper prototyping).
> 4. **Evaluate** against the requirements - Goal: test the design with real users; if requirements are unmet, go back to step 1. Method: controlled experiment / usability test.
>
> See [[Human-Centered Design Process]].

> [!question]- What are Horizontal and Vertical Prototypes?
> **Horizontal Prototype** - implements many features at a shallow, non-functional level (e.g. a full click-through UI with no working logic).
> **Vertical Prototype** - implements a narrow slice of the product in full depth and functionality (e.g. one complete user flow that fully works end-to-end).
>
> See [[Prototyping in HCI]].

> [!question]- Explain the difference between "Getting the design right" and "Getting the right design".
> *(Draft)* **Getting the design right** - iteratively improving the execution quality of a given design (usability, details, ergonomics). **Getting the right design** - making sure the correct product/problem is being tackled in the first place, before refining it (validity of the requirements). Doing the former without the latter results in a well-executed product that misses the actual need.

> [!question]- What is high and low fidelity Prototyping?
> **Low Fidelity** - uses a medium unlike the final one (paper, cardboard); quick, cheap, easily changed; maximizes design iterations before coding. Examples: paper prototypes, post-it notes, [[Wizard of Oz Prototyping|Wizard of Oz]].
> **High Fidelity** - looks more like the final system; more detail, precise, interactive; mock-up of some (not all) aspects of the final UI - only create after initial low-fidelity prototypes; UI (not functionality) is key. Example: Flash animation, series of screenshots.
>
> **Pros of high fidelity**: more engaging, user can interact without designer present.
> **Cons**: users may think it's a full system, focus on details over larger problems, be afraid to criticize a "nice" UI, or management may think it's almost done.
>
> See [[Prototyping in HCI]].

> [!question]- What is the Design-Implement-Analyze Model?
> *(Not answered - please check the slides; the original protocol had no notes on this.)*

> [!question]- What are the Golden Rules?
> "10 Golden Rules" (Shneiderman).
>
> **What they can achieve**:
> - They give the designer confidence that all essential points have been considered.
> - They provide orientation even for less experienced designers.
> - You can tell early on what makes a good design and what doesn't.
> - They save costs, since problems are caught early and no extensive evaluation is needed.
> - They can be used in heuristic evaluation.
>
> **What they cannot achieve**:
> - They provide no detailed knowledge of what users actually do with an interface.
> - They don't help with understanding how the interface is used in a concrete application domain.
> - They assume an average user, i.e. they offer no help in understanding specific user groups.
> - They can only uncover a small fraction of all possible design problems.
> - They cannot support real innovation.
> - They give no insight into concrete errors.
> - A narrow focus on just these aspects leads to an interface that avoids the most severe problems - but not to a very good interface, since the Golden Rules alone are not sufficient for that.

> [!question]- Criticism of Norman's Human Centered Design. Give an example of a well-suited and a less well-suited application.
> *(Draft)* Criticism: HCD assumes users know and can articulate their needs, and therefore tends to optimize existing product categories incrementally rather than enabling radical innovation - users find it hard to imagine needs for technologies that don't exist yet ("If I had asked people what they wanted, they would have said faster horses").
> - **Well suited**: improving a known, established product like a kettle or an office chair, where user feedback on concrete problems can be directly implemented.
> - **Less well suited**: entirely new technologies without a reference frame (e.g. the first touchscreen smartphones or AI-based interfaces), where users can't yet imagine the possibilities, and HCD tends to produce incremental rather than disruptive solutions.

## Evaluation

> [!question]- What is a controlled experiment?
> Quantitative, empirical method that tests hypotheses to discover new knowledge by investigating the relationship between two or more variables, usually in a controlled environment (laboratory).
>
> **Types of variables**: independent (varied under your control, e.g. number of menu entries), dependent (measured, e.g. execution time, error rates, subjective preference), confounding (uncontrolled factors influencing (in)dependent variables, e.g. motivation).
>
> **Hypothesis**: a claim predicting the outcome of an experiment (e.g. reading uppercase text takes longer than sentence case). Goal: confirm the hypothesis by rejecting the null hypothesis (the inverse claim of "no influence" - samples drawn from the same distribution).
>
> **Steps**: 1. Formulate hypothesis 2. Design experiment, pick variables and fixed parameters 3. Choose subjects 4. Run pilot experiment 5. Improve experiment design 6. Run experiment 7. Interpret results to accept or reject hypothesis.
>
> **Advantages**: high reliability, examines one precise aspect in a very controlled setting. **Problem**: hard to generalize results (answers only one very specific question).

> [!question]- The results show that the different levels of the independent variable have no notable effect on finger discomfort. Can the opposite be concluded from this? Justify your answer.
> *(Draft)* No. Failing to reject the null hypothesis ("no significant effect found") is **not proof** that no effect actually exists ("absence of evidence is not evidence of absence"). Possible reasons for a non-significant result despite a real underlying effect: insufficient statistical power/sample size, too much variance/confounding factors, or an effect that is genuinely too small to detect with the chosen design (risk of a Type II error).

> [!question]- Explain Within-Subject and Between-Subject design. Name one disadvantage of each.
> **Within-Subject** - all participants go through all conditions. Disadvantage: learning/order/carryover effects (experience from one condition influences the next).
> **Between-Subject** - different groups of participants per condition. Disadvantage: individual differences between the groups act as a confounding factor, and it requires more participants to achieve the same statistical power.

> [!question]- Explain the difference between a lab study and a field study.
> **Lab study** - controlled environment, high internal validity (confounding factors excluded), but lower ecological validity (results transfer less well to real-world use).
> **Field study** - conducted in the real usage environment, high ecological validity, but less control over confounding factors and thus lower internal validity.

> [!question]- Is data collected via a Likert scale quantitative or qualitative? Justify your answer.
> *(Draft)* Strictly speaking, it is **ordinal** data (an intermediate form) - the categories are ordered, but the distances between levels are not guaranteed to be equal, which is why they shouldn't formally be treated like interval-scaled, true quantitative data. In practice, however, Likert data is often numerically coded and analyzed like quantitative data (means, significance tests). See [[Qualitative vs Quantitative Research Methods]].

> [!question]- A new keyboard layout was developed that places the most frequently typed keys next to each other. The development team claims this allows for faster typing and less finger fatigue. This is now to be tested.
> *(Draft)*
> - **Independent variable**: keyboard layout. Possible values: standard QWERTY/QWERTZ layout, new layout, a third comparison layout (e.g. Dvorak).
> - **Measuring the dependent variables**: typing speed (words/characters per minute), error rate, subjectively perceived finger fatigue (e.g. via questionnaire/Likert scale after the task).
> - **Task in the experiment**: transcribing a standardized text of fixed length on each layout, measuring time and errors.
> - **Hypotheses**: (1) The new layout leads to higher typing speed than the standard layout. (2) The new layout leads to lower subjective finger fatigue than the standard layout.
> - **Control variable**: e.g. the text to be typed (identical across all conditions). **Random variable**: the order in which the layouts are tested (randomly assigned). **Confounding variable**: the participant's typing experience/prior familiarity with one of the layouts.
> - **Within- or Between-Subject?**: Within-Subject would be the natural choice to control for individual differences in typing speed - though with a learning-effect risk, since practice with one layout could influence performance on the next (countermeasure: counterbalancing the order).

## Fitts's Law

> [!question]- How should a frequently clicked UI element in a PC application be placed according to Fitts's Law? Justify your answer.
> As **large** and as **close** to the expected cursor position as possible, ideally at the **screen edge or in a corner**, since the cursor can't overshoot there (effectively infinite width $W$) - this reduces the Index of Difficulty $ID = \log_2(D/W + 1)$ and thus the movement time. See [[Fitts's Law]].

> [!question]- Does this change with touch input instead of mouse input? Justify your answer.
> *(Draft)* Yes. With touch input there is no cursor that gets stopped at the screen edge - the "infinite width" advantage of edge/corner positions therefore disappears. In addition, the effective target size is larger and less precise due to the "fat finger effect" than with a mouse pointer, which is why touch targets generally need to be dimensioned larger than comparable mouse targets to achieve the same hit rate.
