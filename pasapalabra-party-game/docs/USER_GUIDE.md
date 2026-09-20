# User Guide

## 1. Overview

Pasapalabra Party Game is a host-operated alphabet quiz. The public file includes one generic Spanish clue for each of 27 letters: A-Z plus Ñ. The host selects a letter, reads or plays its clue, and marks the answer as correct, passed, or incorrect.

Everything is stored in `index.html`. You do not need to install software, run a server, or build the project.

## 2. Make a private event copy

Do not place personal stories, names, or family information in the public `index.html`.

1. Copy `index.html`.
2. Rename the copy to `game.personal.html`.
3. Edit only that private copy for the event.
4. Open `game.personal.html` in the browser when you play.

`game.personal.html` is ignored by Git. Keep it outside the repository too if several people can access your computer or repository folder.

Before a public push, run:

```bash
git status
git diff --staged
```

Check that no personal file is staged. If a private file was previously committed, adding it to `.gitignore` is not enough. Remove it from Git history before publishing.

## 3. Edit the questions

Open `game.personal.html` in a text editor and find:

```js
const PREGUNTAS = [
```

Every entry must use this exact format:

```js
{ letra: "A", definicion: "Empieza por la A: ...", respuesta: "..." },
```

The fields are:

- `letra`: the letter shown in the ring
- `definicion`: the clue displayed and spoken by the browser
- `respuesta`: the answer displayed for the host

Keep all 27 entries and their order:

```text
A B C D E F G H I J K L M N Ñ O P Q R S T U V W X Y Z
```

Safe editing rules:

- Change only the quoted value after `definicion:` and `respuesta:`.
- Keep every opening and closing brace.
- Keep the comma after each object.
- Keep straight quotation marks (`"`), not typographic quotation marks.
- Keep the Ñ entry between N and O.
- If a clue or answer contains a double quote, either replace it with single quotes or escape it as `\"`.
- Save the file as UTF-8 so accents and Ñ remain correct.

Example:

```js
{ letra: "A", definicion: "Empieza por la A: Capital de Grecia.", respuesta: "Atenas" },
```

After saving, refresh the browser. The voice announcer always reads the current `definicion` text, so no audio recording needs to be updated.

## 4. Set the timer

Find:

```js
const SEGUNDOS_TEMPORIZADOR = 300;
```

The value is in seconds:

- `300` = 5 minutes
- `180` = 3 minutes
- `60` = 1 minute
- `0` = disabled

On the game screen:

- Click `▶` or press `T` to start or pause.
- Click `⟲` beside the timer to reset it.
- Click `⏱` to show or hide it.

The timer does not start automatically. This lets the host prepare the screen before beginning the round.

## 5. Change the scrolling banner

Find:

```js
const TEXTO_BOTE = "Prize challenge: complete all 27 letters";
```

Replace only the text inside the quotation marks. This banner is used while more than five questions remain. At five remaining questions, the game automatically changes to a countdown message until the final question.

## 6. Voice announcer

When a letter is opened, the browser reads its `definicion` aloud in Spanish (`es-ES`). If another letter is selected, the current speech is cancelled and the new clue begins.

- Click `🔊` or press `V` to mute or restore the voice.
- The game still works if speech is unavailable.
- A Spanish system voice gives the best result.
- Chrome and Edge on Windows usually provide the most predictable behaviour.
- Voice quality, availability, and offline behaviour depend on the browser and operating system.

Test the voice on the event laptop in advance. If no Spanish voice is available, install one through the operating system or keep the announcer muted and let the host read the clues.

## 7. Play a round

1. Open the HTML file.
2. Enter fullscreen mode if needed.
3. Start the timer.
4. Select a letter to show and speak its clue.
5. Mark the result:
   - **OK**: marks the letter green.
   - **PASS**: leaves it pending and advances.
   - **NOK**: marks the letter red.
6. Continue until no pending letters remain.

The counters update after every marked answer. A completed game shows confetti. A perfect 27/27 round also shows fireworks and the jackpot message.

## 8. Keyboard controls

| Key | Action |
| --- | --- |
| `←` / `→` | Select previous or next pending letter |
| `Space` / `Enter` | Open the selected clue |
| `1` or `O` | Correct / OK |
| `2` or `P` | Pass |
| `3` or `N` | Incorrect / NOK |
| `Esc` | Close the clue panel |
| `T` | Start or pause the timer |
| `F` | Toggle browser fullscreen |
| `V` | Mute or restore the voice |
| `R` | Restart the game |

Restarting clears all answers and resets the timer.

## 9. Projector and party checklist

### Before the event

- Use the same laptop, browser, speakers, cable, adapter, projector, or TV planned for the event.
- Open the private HTML file once with the internet disconnected.
- Test the Spanish voice and speaker volume.
- Check every question and answer for spelling.
- Confirm the timer duration and banner text.
- Keep a backup copy on a USB drive.
- Disable sleep mode, notifications, and automatic restarts.
- Connect power and close unrelated applications.

### Before the round

- Set display scaling so the full ring and question panel fit.
- Use the in-game fullscreen button or `F`. Browser `F11` is a useful fallback.
- Place the host where they can see the answer without blocking the screen.
- Decide whether the audience should see the host answer. This version shows the answer in the same panel as the clue.
- Keep a mouse available even if you plan to use the keyboard.

### If something goes wrong

- No voice: reload once, click a letter, check system volume, then use the mute button and read manually.
- Text does not update: save the file and refresh the browser.
- Layout does not fit: leave fullscreen, adjust browser zoom, then re-enter fullscreen.
- Timer needs a clean start: use the reset button before pressing play.
- Accidental restart: the current round state is not saved, so begin again.

## 10. Publishing checklist

- `index.html` contains only generic example questions.
- `game.personal.html` is not staged.
- No screenshots show private names or clues.
- README links work.
- The game opens by double-clicking `index.html`.
- The Spanish voice requirement is documented.
- The repository is licensed under MIT.
