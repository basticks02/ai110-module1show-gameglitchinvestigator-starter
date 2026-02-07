# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?
  > first things first, and seems like the secret number didn't actually have commitment issues! I seemed to alread be wrapped in `session_state` !

- What did the game look like the first time you ran it?
  > The game looked overall quite ok. I knew there were issues, but it took some time to identify what exactly they were
- List at least two concrete bugs you noticed at the start  
  (for example: "the secret number kept changing" or "the hints were backwards").
  > I wrote these out as bullets in my notes app. I have attached them verbatim:
    > [x] scoring is incorrect - should either increase or decrease (increments of 5) and be update accordingly. Also, should not go below 0
    > [x] after submission, attempt, score & history is not appended to until you clear what you have and click out of the box - history should be appended immediately 
    > [x] when you start a new game, it says ‘You have already won. Start a new game to play again’ 
    > [x] history should be cleared when you start a new game
    > [x] attempts start with 1 (when page is first loaded)
    > [x] hints are wrong - telling me to go lower when I need to go higher & vice versa

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
> I made use of Codespace's Copiolt 
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
> This is a quick interaction that Copilot and I had where their suggestions we correct:
  > Me: nice. is there a way to keep the debug window open/where it was on the UI before without encountering this issue? or must it be below
  > Copilot: Good question! Yes, you can keep it at the top by using a container placeholder pattern. Create the container at the top, but fill it with content after all the handlers execute: 
  ```python
    # At the TOP of the page (after st.info)
    debug_container = st.container()

    # ... rest of your code: text_input, buttons, handlers ...

    # Then at the BOTTOM, fill the debug container
    with debug_container:
        with st.expander("Developer Debug Info"):
            st.write("Secret:", st.session_state.secret)
            st.write("Attempts:", st.session_state.attempts)
            st.write("Score:", st.session_state.score)
            st.write("Difficulty:", difficulty)
            st.write("History:", st.session_state.history) 
  ```
- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).
>When I first brought up the issue: after submission, attempt and history is not appended to until you clear what you have and click out of the box - history and attept should be appended immediately, Copilot responded: Fixed! I added st.session_state[f"guess_input_{difficulty}"] = "" at the end of the submission block. This clears the input field immediately after processing the guess, so attempt and history update properly without requiring the user to manually clear the input box.
>This was incorrect.

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
  > I would: 1. reload and test the local instance of the app. 2. Run the unit test created for the feature
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
  > I tested all features I updated manually. I updated the 1 pytest for the Hints: High vs Low and ran it. this was the outcome:
  ```
  @basticks02 ➜ /workspaces/ai110-module1show-gameglitchinvestigator-starter (main) $  python -m pytest -q tests/test_game_logic.py ...  [100%]                                                                            
  3 passed in 0.01s
  ```

- Did AI help you design or understand any tests? How?
  > Yes, I used AI to update the tests within the `test_game_logic.py` file to accomodate the changes made in the `logic_utils.py`


---

## 4. What did you learn about Streamlit and state?

- In your own words, explain why the secret number kept changing in the original app.
  > This was not a bug I identified
- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
  > Streamlit reruns the entire script top-to-bottom whenever a user interacts with a widget. Regular variables disappear on each rerun, so `st.session_state` stores persistent data (like game state) across reruns. You initialize it once with `if key not in st.session_state`, then update it during user interactions to keep values stable between reruns.
- What change did you make that finally gave the game a stable secret number?
  > This was not a bug I identified.

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
    > The ability to understand and write unit tests! I am glad that I was able to actually understand waht the tests do, modify them with AI and run them accordingly
- What is one thing you would do differently next time you work with AI on a coding task?
  > Seeking understanding before implementation
- In one or two sentences, describe how this project changed the way you think about AI generated code.
  > AI it's always print making mistakes, and that makes testing very important and if possible test should not be completely written by AI.
