---
type: game-research
game: Police Quest I - In Pursuit of the Death Angel
edition: original AGI command-parser release
status: extracted-route-awaiting-runtime-validation
---

# Police Quest I AGI: Command Route

## Evidence Boundary

The guide was generated from a locally owned original AGI build and cross-checked against independent public route and point references. The local build identifies itself as AGI `2.915`; its parser vocabulary includes the command families below and its extracted logic contains score gates. This is the 1987 command-parser game, not the later SCI remake. No game resources or extracted scripts are published here.

The route is arranged as parser commands plus required physical positioning. `[]` means move Sonny to the indicated object or room with the keyboard before entering the command. Save before each traffic stop, arrest, poker sequence, and final operation.

This is a high-score route draft. A published point checklist totals `242/245` for this AGI release, so do **not** claim a verified 245/245 finish until a runner records the final score from this specific archive.

## Parser Conventions

- Use all-caps commands below exactly first; the local vocabulary also accepts many synonyms.
- `RADIO DISPATCH` is the safe generic form when a scene requires a report; follow the prompted question if one appears.
- Code keys: `F8` is Code 2, `F10` is the nightstick action, and Code 3 is used for active pursuit where the game offers it.
- Treat every arrest as a procedure: secure weapon as needed, control suspect, cuff, search, read rights, transport, book, uncuff, cell.

## Travel and Interface Context

- The police station begins as a practical hub: locker room is through the lower-right doorway; briefing is upper-right; the key rack and radio extender are in the main hall; the patrol car is outside at lower left.
- Use the in-game city map for destination navigation. During driving, remain on the road grid and save before any pursuit; traffic mistakes can terminate the run.
- `F4` handles entering/exiting or driving/parking the vehicle. `F5` saves and `F7` restores. `F8` is the fast/code-two control; `F10` is the siren or nightstick action depending on context.
- “Wait” steps are real state changes. Do not leave a scene until the named NPC arrives, the call is received, or the game explicitly advances the sequence.
- Hotel Delphoria’s critical geography: lobby -> bar -> elevator -> room 204 -> bar/back room -> final upper-floor room. Save before both poker sequences.

## 1. First Shift: Station and Patrol Car

At the locker:

```text
OPEN LOCKER
GET GUN
GET AMMO
GET BRIEFCASE
OPEN BRIEFCASE
GET NOTEBOOK
GET PEN
GET TICKET BOOK
CLOSE BRIEFCASE
CLOSE LOCKER
```

In the briefing room: `READ NEWSPAPER`, advance pages, then stop reading. Stand in the designated briefing position and wait. Afterwards inspect the pigeonhole: `LOOK IN PIGEONHOLE` and take the note.

Before leaving, collect the patrol keys and radio extender. At the car perform the inspection:

```text
WALK AROUND CAR
EXAMINE DOOR
OPEN DOOR
GET IN CAR
LOOK IN CAR
GET NIGHTSTICK
CLOSE DOOR
DRIVE
```

## 2. Patrol Calls

### Crash

At the crash: `LOOK AT DRIVER`, `HELP DRIVER`, then `RADIO DISPATCH`. Question the witness about the plate, report again, and wait for Dooley before returning to patrol.

### Carol's Phone Call

At Carol's: `SIT DOWN`, `TALK TO STEVE`, wait for the phone, then `ANSWER PHONE`. Return to Steve, finish the conversation, and leave.

### Red-Light Stop

Use Code 2, follow the red car, then after it stops:

```text
LOOK AT LICENSE
RADIO DISPATCH
LOOK AT GIRL
SAY HELLO
TELL GIRL SHE RAN RED LIGHT
NO
WRITE TICKET
GIVE LICENSE TO GIRL
ASK GIRL TO SIGN TICKET
GIVE TICKET TO GIRL
```

### Wino Willy's

At Carol's, ask about the complaint. At Willy's tell the man in black to move the motorcycles. When attacked, press `F10`. Then `ASK GIRL ABOUT DRUGS`; return to Carol and report that the complaint is resolved.

### Drunk Driver

Use Code 3, then:

```text
LOOK AT LICENSE PLATE
RADIO DISPATCH
TALK TO DRIVER
LOOK AT DRIVER
ASK DRIVER FOR LICENSE
TELL DRIVER TO GET OUT
ADMINISTER FIELD SOBRIETY TEST
ARREST DRIVER
HANDCUFF DRIVER
OPEN BACK DOOR
CLOSE BACK DOOR
RADIO FOR TOW TRUCK
```

At jail: secure the gun, `BOOK DRIVER FOR DRUNK DRIVING`, `REMOVE HANDCUFFS`, and lead the prisoner to the cell. Recover the gun before leaving.

## 3. Off Duty, Stolen Car, and Transfer

At the station: return the nightstick, `WRITE MEMO`, `PUT MEMO IN BASKET`, inspect Dooley's office, then change into civilian clothes twice as the scene requires. Collect Corvette keys and wallet, attend the Blue Room sequence, then return for the next briefing and repeat the full patrol-car inspection.

For the stolen car, wait for backup before leaving the vehicle:

```text
RADIO FOR BACKUP
OPEN DOOR
GET OUT
LOAD GUN
DRAW GUN
TELL SUSPECT TO GET OUT
TELL SUSPECT TO RAISE HANDS
TELL SUSPECT TO LIE DOWN
PUT GUN AWAY
HANDCUFF SUSPECT
SEARCH SUSPECT
READ RIGHTS
```

Then inspect Jack's weapon and the stolen car: `LOOK AT GUN`, `READ SERIAL NUMBER`, `LOOK AT DOOR JAMB`, `OPEN GLOVE BOX`, `READ BOOK`, `READ LICENSES`, `OPEN TRUNK`, `LOOK AT DOPE`. Transport and book the prisoner using the same safe jail procedure.

## 4. Narcotics and No-Bail Warrant

Read Dooley's memo, change back to uniform, collect gun/ammo, meet Morgan and Laura. In the records area:

```text
GET CLIPBOARD
READ CLIPBOARD
GET POSTER
OPEN FILE CABINET
READ HOFFMAN FILE
GET HOFFMAN FILE
```

At the courthouse, say you need the judge, request a no-bail warrant, state it is an emergency, then identify the subject as Marvin Hoffman. When prompted, provide the Hoffman file, then the poster/list, then mention the tattoo. Give the warrant to the jailer.

## 5. Park Stakeout and Office Work

At the park: hide, `DRAW GUN`, `LOAD GUN`, report being in position, wait for the fight, report again, then type `HALT POLICE`. Once the remaining suspect is controlled:

```text
PUT GUN AWAY
HANDCUFF SUSPECT
READ RIGHTS
SEARCH SUSPECT
LOOK AT ID CARD
LOOK AT DOPE
QUESTION SIMMS
QUESTION SIMMS
QUESTION COLBY
QUESTION COLBY
```

Transport and book both suspects. Complete the Blue Room conversation sequence.

For office work:

```text
ASK FOR BLACK BOOK
READ BLACK BOOK
RETURN BLACK BOOK
ASK TO SEE WEAPON
READ TAG
RETURN WEAPON
TURN ON COMPUTER
SW9764912
EXIT
```

At the phone dial `1-312-555-3382` and ask about Taselli. Later, use information to contact Cobb and Williams; identify as Sonny Bonds and answer `HOFFMAN` when prompted.

## 6. Cotton Cove and Undercover Preparation

At jail, leave the gun outside and ask Marie to help. At Cotton Cove:

```text
REMOVE BLANKET
REMOVE SHIRT
COVER BODY
RADIO DISPATCH
```

After Morgan provides the disguise items: leave the radio extender at the station, change clothes, turn on the right shower, use bleach, `WET HAIR`, `RINSE HAIR`, turn off the shower, change again, then inspect Morgan's phone before leaving for the hotel.

## 7. Hotel Delphoria Finale

At check-in: ring bell, rent room, pay. At the bar, order a beer, pay for information, then later give the bartender money. Unlock room 204.

In the room, agree to Marie's prompts, then phone:

```text
555-6674
WHITEY
411
CAB
555-9222
HOTEL DELPHORIA
```

Back at the bar: pay the entry money, allow the frisk, win the first poker sequence, then obtain the transmitter. For the final game, tell the bartender Frank sent you, win the required hands, agree to both prompts, follow Frank, use the pen before entering the final room.

## Runtime Validation Checklist

- Record score after every named sequence.
- Capture the exact parser phrase if a listed command is rejected; keep the accepted synonym beside it.
- Record every score delta and save identifier in an append-only run log.
- Compare the final score with the local score-variable trace before declaring the route complete.
