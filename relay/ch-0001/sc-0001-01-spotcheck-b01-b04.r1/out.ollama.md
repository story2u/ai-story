Thinking...
Thinking Process:

1.  **Analyze the Request:**
    *   **Role:** Editor-in-Chief (总编).
    *   **Task:** Perform a spot check (L0) on beats 1-4 of scene `sc-0001-[9D[K
`sc-0001-01〈清册点名〉`.
    *   **Constraint:** Output *only* one line in a strict format: `SPOT_CH[8D[K
`SPOT_CHECK(beat 1-4): pass | flag(beat k: 理由+证据)`.
    *   **Context:** The user provided the role definition and the specific[8D[K
specific task payload (showrunner scheduling, stand-in, embedded materials)[10D[K
materials).
    *   **Goal:** Check for OOC, logic breaks, power system/violation, info[4D[K
information leakage (Shen Yan shouldn't know Ke Jiu's identity/old seal tru[3D[K
truth/show supernatural, Ke Jiu shouldn't expose spy status/cultivation/sei[22D[K
status/cultivation/seize seal, town constables as pressure props only, char[4D[K
characters shouldn't act on others' INNER).
    *   **Input Data:** Beat 1 (Shen Yan) and Beat 2 (World/Constable NPC).[5D[K
NPC). The prompt mentions beats 1-4, but the input only shows Beat 1 and Be[2D[K
Beat 2 text. However, the instruction says "Check beat 1-4". I need to eval[4D[K
evaluate based on the provided text which covers Beats 1-2. The instruction[11D[K
instruction says "Only output one line".
    *   **Current Status:** I am the Editor-in-Chief. I need to evaluate th[2D[K
the provided snippets against the rules.
    *   **Key Rules:**
        *   Shen Yan must not know Ke Jiu's identity/old seal truth/show su[2D[K
supernatural. (Not mentioned in beats 1-2 yet, but Shen Yan's inner thought[7D[K
thought says "They want to make me low first").
        *   Constables are pressure props. (Beat 2 shows them struggling wi[2D[K
with rules, pressing with "Kaifeng is a big matter").
        *   Character actions based on others' INNER: Shen Yan's INNER says[4D[K
says "They want me to be low...". This is his interpretation of their inten[5D[K
intent, which is standard POV.
        *   Information Isolation: Does Shen Yan know too much? He knows ab[2D[K
about the register and the old seal being his.
        *   Logic: Constables can't cite specific rules immediately.
    *   **Wait, I need to check the constraints:**
        *   "Only output one line, strict format".
        *   "Input contains all your context; do not read files, do not exe[3D[K
execute commands, do not write files."
        *   "The task payload is embedded in this message."
        *   The user wants me to act as the Editor-in-Chief and output the [K
specific line.
        *   **Crucial:** I need to look closely at the provided Beats 1 and[3D[K
and 2 for violations.
        *   Beat 1: Shen Yan speaks. Inner thought: "Again 'lowly' (zhi jia[3D[K
jian). They want me to be low... Can't be impatient...". This is internal m[1D[K
monologue, not leaking secret info to the world.
        *   Beat 2: Constable NPC props. They can't cite rules.
        *   Are there violations?
            *   Shen Yan doesn't know Ke Jiu (Ke Jiu isn't in this beat yet[3D[K
yet, presumably).
            *   Constables aren't showing supernatural.
            *   Logic seems okay so far.
        *   However, the prompt says "Check beat 1-4". Only Beats 1 and 2 a[1D[K
are provided in the text block. I must evaluate what is there. If it's pass[4D[K
pass, output pass. If flag, output flag.
        *   Wait, looking at Beat 1 `STATE_DELTA`: "Emotion shifts from cal[3D[K
calm to suppressed alert". This is fine.
        *   Looking at `INNER(private)`: It's his own thoughts. No leakage.[8D[K
leakage.
        *   Looking at `KNOWLEDGE_GAINED`: "Register review is targ[4D[K
targeting me... they want to
