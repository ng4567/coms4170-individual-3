GitHub repo: https://github.com/ng4567/coms4170-individual-3

# Part 8 screenshot

<img src="images/Part-8-My-Events.png" alt="My Events showing one Going event, two Invited events, and an empty Declined group" width="640">

MyEvents.jsx open beside My Events. Recreated after Part 12 from the course's Part 8 finished code (the Part 9 folder), since dragging in Part 9 replaced my own Part 8 code before I took an editor screenshot.

<img src="images/Part-8-MyEvents-code-and-preview.png" alt="MyEvents.jsx source on the left; My Events page on the right with Going, Invited, and an empty Declined group" width="640">


## Part 9:

I submitted "someone@columbia.edu". The fields greyed out and the button was "Sending..." and later "You are going." `setFormState("submitting")` makes `isSubmitting=true` for `disabled={isSubmitting}`, and after `await sendRsvp(rsvp)` resolved, `setFormState("confirmed")` and `onSubmit(rsvp)` marka it event `Going`. 

<img src="images/Part-9-submitting.png" alt="RSVP form in the submitting state: fields greyed out, button reads Sending…, State: submitting" width="640">
<img src="images/Part-9-confirmed.png" alt="Event page after the send resolved, showing You are going. See you there." width="640">

## Part 10:
 
I submitted x@fail.test and the focus landed on the red failure message. Messages only exist once `formState` is `failed`, so `useEffect` watching `formState` calls `summaryRef.current?.focus()` after it's drawn.


<img src="images/Part-10-failed-focus.png" alt="RSVP form in the failed state with the focus outline on the failure message and the button reading Try again" width="640">


## Part 11: 

 I set `SIMULATE_FAILURE` equal to true and saw the error box display Try again. After pressing again, it showed "Loading events..." and then the same error. In `App.jsx`, `useEffect` with `[]` called `load()` once on start (the empty `[]` means run only after the first render), `load()` calls `loadEvents()`, which rejects and hits the catch statement which sets "error". Try again is `onRetry={load}`, so it calls `loadEvents()` again. 

<img src="images/Part-11-error.png" alt="Events page showing the error box and Try again button with SIMULATE_FAILURE set to true" width="640">
<img src="images/Part-11-loading-after-retry.png" alt="Events page showing Loading events… right after pressing Try again" width="640">

## Part 12:

**12a. Going count.** Before 12a (Part 11 code): start +42, one click (Going, still +42), two clicks (Invited, still +42).

<img src="images/Part-12-count-before-1-start.png" alt="Before 12a (Part 11 code): fresh load, first card reads +42" width="640">
<img src="images/Part-12-count-before-2-one-click.png" alt="Before 12a: after one click the pill reads Going but the count is still +42" width="640">
<img src="images/Part-12-count-before-3-two-clicks.png" alt="Before 12a: after a second click the pill reads Invited and the count is still +42" width="640">

After 12a: start +42, one click (Going, +43), two clicks (Invited, +42).

<img src="images/Part-12-count-after-1-start.png" alt="After 12a: fresh load, first card reads +42" width="640">
<img src="images/Part-12-count-after-2-one-click.png" alt="After 12a: after one click the pill reads Going and the count is +43" width="640">
<img src="images/Part-12-count-after-3-two-clicks.png" alt="After 12a: after a second click the pill reads Invited and the count is back to +42" width="640">

Forum Going → Invited (+318 → +317); Friday declined on its page (still +88); Friday's Declined pill clicked (Going, +89).

<img src="images/Part-12-test-forum-invited-317.png" alt="Campus Creative AI Forum after clicking its Going pill: Invited, +317" width="640">
<img src="images/Part-12-test-friday-declined-88.png" alt="Friday Night Social after pressing Decline on its page: Declined, still +88" width="640">
<img src="images/Part-12-test-friday-going-89.png" alt="Friday Night Social after clicking its Declined pill: Going, +89" width="640">

**12b. Search.** "friday", "FRIDAY", "f" (two cards), and Past with "mixer" (one card).

<img src="images/Part-12-search-lowercase.png" alt="Events page searched for &quot;friday&quot; in lowercase: one card, Friday Night Social" width="640">
<img src="images/Part-12-search-uppercase.png" alt="Events page searched for &quot;FRIDAY&quot; in capitals: the same one card, Friday Night Social" width="640">
<img src="images/Part-12-test-search-f.png" alt="Events page searched for f: two cards, Campus Creative AI Forum and Friday Night Social" width="640">
<img src="images/Part-12-test-past-mixer.png" alt="Past view searched for mixer: one card, Orientation Mixer" width="640">

**12c. Empty state.** "zzz" shows the message.

<img src="images/Part-12-test-search-zzz.png" alt="Events page searched for zzz: No upcoming events match “zzz”. Try fewer letters." width="640">

**12d. Note**

What I tried: I was looking at the going count on the details page after accepting.

What I saw: The details page never displayed `goingCount`; after accepting, the count only updates on the Events page (+42 to +43). Getting back to Events with a refresh or typing the URL restarted the app and displayed the old count, since events reloads from data/events.js.

One thing I fixed: I modified `handleStatusChange()` to also update `goingCount`, not just status, so accepting changes the count on the Events page.

# AI Process Note

I used Claude Code to help me debug code errors in a few parts and to help me take screenshots when testing during the testing part. I would tell Claude exactly what to enter into the fields or where to click to test and then it would take screenshots. I checked each fix and screenshot manually myself before keeping it.