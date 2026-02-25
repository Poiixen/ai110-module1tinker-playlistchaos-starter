# Summary

This assignment reinforces a key principle: AI is a tool and its impact depends entirely on how you use it. Here, AI served as a resource to help identify bugs and suggest fixes in the "Playlist Chaos" codebase, while students were first encouraged to analyze the code documentation on their own.

Students may struggle most with two things: over-reliance on AI, and reading in-code documentation. While AI use is encouraged in this course, leaning on it too early can crowd out independent thinking. The UPI pathway is a good guardrail against that. For beginners feeling overwhelmed by unfamiliar code, AI can be valuable for breaking down documentation in digestible ways.

AI proved useful for testing features, classifying behavior, and suggesting fixes. That said, it can develop tunnel vision. This is a good reminder that AI focuses on the immediate task, so it is on the user to read broadly and provide context as you work alongside it.

AI also works well as a nudge, reinforcing the objective, prompting students to test the software, and guiding them toward finding bugs rather than just handing over answers. It has limits, and filling those gaps is the student's job.

## What I fixed:

**Fix 1 — Wrong `total` in `compute_playlist_stats` (`playlist_logic.py:119`)**
Source: `total` was set to `len(hype)` instead of `len(all_songs)`, so `hype_ratio` was always 1.0 (or 0.0 when empty) regardless of how many songs existed across all playlists. Changed `total` to `len(all_songs)`.

**Fix 2 — `avg_energy` summed only hype songs (`playlist_logic.py:124`)**
Source: `total_energy` iterated over `hype` while dividing by `len(all_songs)`, producing a misleadingly low (and wrong) average. Changed the generator to iterate over `all_songs` so the average reflects every song.

**Fix 3 — Inverted substring check in `search_songs` (`playlist_logic.py:171`)**
Source: The condition `value in q` checked whether the full artist string was a substring of the short search query, which almost never matches. It should be `q in value` (does the query appear inside the artist name). Search now returns results correctly.

**Fix 4 — `random_choice_or_none` crashes on empty playlist (`playlist_logic.py:196`)**
Source: `random.choice([])` raises an `IndexError`. The function name promises `None` for empty input, and `lucky_pick` relies on that contract. Added a guard: `return random.choice(songs) if songs else None`.

**Fix 5 — `is_chill_keyword` checked `title` instead of `genre` (`playlist_logic.py:74`)**
Source: The chill-keyword test compared keywords like "lofi" and "ambient" against the song's `title`, while the equivalent hype-keyword test correctly checks `genre`. A song titled "Lo-fi Rain" was classified differently depending on its title, not its genre. Changed to check `genre` for consistency.



# Weekly task:
The most important thing for students to understand with this tinker is that they should approach this unfamiliar code using AI as a support tool and not like a replacement for thinking. Many students will probably struggle with setting up their environment and running Streamlit for the first time. AI tools like Copilot were helpful for explaining what certain functions were doing and pointing out possible logic issues, such as why the search feature behaved unexpectedly. But AI can miss deeper problems if you don’t question its explanations or test its suggestions. I would guide a student without giving the answer is by encouraging them to focus on one function at a time and ask the AI to explain what each line is doing. I would also suggest that they test small changes and compare expected versus actual behavior so they can gradually build their understanding.


# Playlist Chaos

Your AI assistant tried to build a smart playlist generator. The app runs, but some of the behavior is unpredictable. Your task is to explore the app, investigate the code, and use an AI assistant to debug and improve it.

This activity is your first chance to practice AI-assisted debugging on a codebase that is slightly messy, slightly mysterious, and intentionally imperfect.

You do not need to understand everything at once. Approach the app as a curious investigator, work with an AI assistant to explain what you find, and make targeted improvements.

---

## How the code is organized

### `app.py`  

The Streamlit user interface. It handles things like:

- Showing and updating the mood profile  
- Adding songs  
- Displaying playlists  
- Lucky pick  
- Stats and history

### `playlist_logic.py`  

The logic behind the app, including:

- Normalizing and classifying songs  
- Building playlists  
- Merging playlist data  
- Searching  
- Computing statistics  
- Lucky pick mechanics

You will need to look at both files to understand how the app behaves.

---

## What you will do

### 1. Explore the app  

Run the app and try things out:

- Add several songs with different titles, artists, genres, and energy levels  
- Change the mood profile  
- Use the search box  
- Try the lucky pick  
- Inspect the playlist tabs and stats  
- Look at the history  

As you explore, write down at least five things that feel confusing, inconsistent, or strange. These might be bugs, quirks, or unexpected design decisions.

### 2. Ask AI for help understanding the code  

Pick one issue from your list. Use an AI coding assistant to:

- Explain the relevant code sections  
- Walk through what the code is supposed to do  
- Suggest reasons the behavior might not match expectations  

For example:

> "Here is the function that classifies songs. The app is mislabeling some songs. Help me understand what the function is doing and where the logic might need adjustment."

Before making changes, summarize in your own words what you think is happening.

### 3. Fix at least four issues  

Make improvements based on your investigation.

For each fix:

- Identify the source of the issue  
- Decide whether to accept or adjust the AI assistant's suggestions  
- Update the code  
- Add a short comment describing the fix  

Your fixes may involve logic, calculations, search behavior, playlist grouping, lucky pick behavior, or anything else you discover.

### 4. Test your changes  

After each fix, try interacting with the app again:

- Add new songs  
- Change the profile  
- Try search and stats  
- Check whether playlists behave more consistently  

Confirm that the behavior matches your expectations.

### 5. Optional stretch goals  

If you finish early or want an extra challenge, try one of these:

- Improve search behavior  
- Add a "Recently added" view  
- Add sorting controls  
- Improve how Mixed songs are handled  
- Add new features to the history view  
- Introduce better error handling for empty playlists  
- Add a new playlist category of your own design  

---

## Tips for success

- You do not need to solve everything. Focus on exploring and learning.  
- When confused, ask an AI assistant to explain the code or summarize behavior.  
- Test the app often. Small experiments reveal useful clues.  
- Treat surprising behavior as something worth investigating.  
- Stay curious. The unpredictability is intentional and part of the experience.

When you finish, Playlist Chaos will feel more predictable, and you will have taken your first steps into AI-assisted debugging.
