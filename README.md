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

## Observed quirks and issues

1. **Genre and favorite genre override energy in classification** — A song can be forced into Hype by any one of three independent conditions: its energy meets the threshold, its genre contains a hype keyword ("rock", "punk", "party"), or its genre matches the profile's `favorite_genre`. Because these are joined with `or`, a low-energy song is still classified as Hype if its genre matches — energy is never considered. This behavior is not documented anywhere.

2. **Hype and chill sliders only register every other interaction** — The sliders update on alternating moves: the first move registers, the second does nothing, the third registers, the fourth does nothing, and so on indefinitely. Every other adjustment is silently ignored.

3. **Search only matches exact values** — Typing a partial name into the search box returns no results unless the query exactly matches the entire field value. For example, searching "Eagles" does not surface songs by "The Eagles".

4. **Search returns no results when searching by song attributes** — The search function produces no results regardless of what is typed, even when the query exactly matches a song's artist, title, genre, or other attribute.

5. **Average energy stat is calculated incorrectly** — The average energy displayed in the stats section is only summed from songs in the Hype playlist, then divided by the total number of songs across all playlists. It should use energy values from all songs, not just Hype.

6. **Hype ratio uses the wrong denominator** — The hype ratio is calculated by dividing the number of Hype songs by the length of the Hype playlist itself, always producing 1.0. It should be divided by the total number of songs across all playlists.

7. **"Feeling Lucky" ignores Mixed songs** — The lucky pick feature only draws from the Hype and Chill playlists. Songs classified as Mixed are never considered, regardless of which mode is selected.

8. **Duplicate songs are allowed despite normalization** — Songs are normalized before being added, but there is no deduplication check. Adding the same song multiple times results in duplicates appearing in the playlist.

9. **Merge playlist is a no-op** — `merge_playlists` is always called with an empty dict `{}` as the second argument in `app.py`, so no actual merging ever occurs. The function exists but its purpose is never fulfilled.

---

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
