# Ffxi-addons-KupoKit
Inventory and job change manager addon

KupoKit - Simple Instructions
=====================================

WHAT IT DOES
KupoKit keeps your bags clean. It learns which gear each of
your jobs uses, then - standing at a Porter Moogle - it parks
every other job's armor on storage slips and pulls out only
the gear for the job you are playing. Switch jobs, and it
swaps the whole wardrobe for you.

Your storage slips live in your Mog Case: a run pulls
them all into your Inventory at the start and stores
them all back into the Case at the end.

Commands start with //kk (or //kupokit). Type //kk help in
game for the full list.


WHAT YOU NEED
- Windower 4, with GearSwap.
- One GearSwap .lua file per job you play.
- Storage slips. Buy them from the Porter Moogle by hand,
  1,000 gil each. (//kk active tells you if any are missing.)
- Nothing else. The job changing is built into KupoKit
  itself - no extra addon needed.


!!! THE ONE RULE THAT MATTERS !!!
YOUR JOB .LUA FILES MUST BE ACCURATE.

KupoKit does not guess what a job uses - it READS your
GearSwap files and builds each job's gear list from the
sets written in them. The lists are only as good as the
files. If your luas are out of date, your results WILL
be skewed:

- Gear in your lua that you no longer use? KupoKit will
  keep protecting it and pulling it out anyway.
- Gear you really wear that is NOT in your lua (a set you
  never wrote, a new piece you never added to the file)?
  KupoKit does not know it belongs to that job - and it
  can be parked on a slip when you change jobs.

So before you approve anything: clean up your job files
first. Every set in the file should be gear you actually
own and use on that job, spelled exactly as the game
spells it. Then check the lists with //kk review (below)
before approving - what you see there is exactly what
KupoKit believes.

One exception to know about: if a job file pulls in
other files with include(), KupoKit reads those too -
EXCEPT files whose names say they are shared across
jobs or list your whole inventory (names containing
'shared' or 'inventory', plus ZBrain files). Those are
never read: a file that serves every job cannot say
what one job wears. Keep each job's own sets in the job
file itself or in includes named for that job.


FIRST-TIME SETUP
1. Put the KupoKit folder in your Windower\addons folder
   and load it:  //lua l kupokit
2. Buy your storage slips from the Porter Moogle.
3. Look at what it learned, one job at a time:
      //kk review WAR
   Read the list. It should match the gear that job
   really uses - no more, no less.
4. Happy with a list? Approve it:
      //kk approve WAR        (or //kk approve all)
   Nothing moves before you approve. Until then, //kk
   active only prints a report and touches nothing.
5. A piece missing from a list? Best fix: correct the
   job's .lua file, then //kk refresh WAR and review
   again. Quick fix: //kk add WAR <item name>.
   A piece that must NEVER be parked, whatever any file
   says: //kk never <item name>.
6. Changed a job file later? Run //kk refresh <JOB>,
   review, and approve again. (KupoKit also warns you on
   its own when a file change would drop a piece's
   protection.)


THE ON-SCREEN PICKER
Type //kk panel to open a grid of all 22 jobs.
Each job is its own picture now, drawn in its own gear.

1. Click a job - it lights up GOLD. That is your MAIN job.
2. Click another job - it lights up BLUE. That is your SUB.
3. Click CHANGE at the bottom. KupoKit changes your jobs
   and sorts your gear, same as typing the command.

The GEAR button sorts gear for the job you are already on,
without changing jobs. Under them sits a second row:
CHECK dry-runs the MAIN job you picked (or the job you are
on) without moving anything, MAKESPACE tidies consumables
out of your Inventory, and the number beside it is a
pulldown - click it and pick how much room makespace
should aim for: 10, 20, 30, 40 or 50 free slots. Scroll the mouse wheel over the
panel to make it bigger or smaller. The STOP button halts a run in
progress. Drag the top strip to move the panel, and click
the X to close it. Jobs you have not unlocked yet show dim
and cannot be clicked.

Not sure what a run would do? Type //kk check WAR (any job)
first: it prints what would be parked and what would be
pulled, and which storage slips you are missing - without
moving a single thing.

Want to know what is actually ON your slips? Stand at the
Porter Moogle and type //kk slipdump. It reads every slip
you carry - taking nothing off them - and saves the full
list to a file named after your character in the KupoKit
data folder.

Missing some storage slips? Stand at the Porter Moogle
and type //kk buy: KupoKit buys every slip you are missing
for you, 1,000 gil each, one at a time. (//kk buy 21 buys
just Slip 21.)

If a run warns you about Inventory space, type
//kk makespace: it moves your food, medicines, tools and
other consumables into your Sack and Satchel until there
is room. It never touches gear, slips or ammo. If it
says there is nothing to move, //kk itemtypes shows what
it sees in your Inventory, item by item.

To clear out everything movable at once, type
//kk makespace any: every consumable that can move goes
- Sack first, then Satchel, then your Mog Case - until
nothing movable is left in Inventory. The panel's space
pulldown (the number next to MAKESPACE) has an ANY pick
that does the same thing.

Trusted friends can also ask by tell: "Kupo check WAR"
runs a check on your machine and tells them the summary,
and "Kupo makespace" runs makespace for them. The job
change tell ("Kupo BRD/NIN") works the same way, and it
tells them again when the run settles: done, or the snag
that stopped it. Turn all
of it off with //kk remote off.


EVERYDAY USE
Stand next to a Porter Moogle (the Pilgrim Moogle in
Sheol Gaol works too), then:

   //kk WAR/SAM
      Change to WAR/SAM AND swap the gear in one go:
      it changes your jobs, waits until the change has
      really landed, then parks the old job's gear and
      pulls WAR's gear off the slips.

   //kk active WAR
      Already on WAR? This just does the gear swap:
      park everything else, pull WAR's gear out.

   //kk active none
      Park everything, pull nothing out.

   //kk stop
      Stop a run that is in progress.


GOOD TO KNOW
- A few pieces cannot be stored on slips at all (pieces
  on a trial, some augmented pieces). KupoKit leaves
  those in your bags, remembers them, and skips them on
  later runs. Fixed the piece and want it tried again?
  //kk clearskips
- Gear sitting in Mog House Storage is never touched -
  the Porter Moogle cannot see it, and neither can
  KupoKit.
- Approvals are saved per character, so each character
  approves their own lists once.
- If a job change does not land within 12 seconds,
  KupoKit stops and moves NO gear - it never gears up
  the wrong job.
- REMOTE TRIGGER (new in 1.8.0): a player on your trust
  list can /tell your character "Kupo BRD/NIN" and KupoKit
  runs the job change + gear chain, exactly like the panel.
  It only works by tell, only from trusted names, never
  mid-fight, and it always tells the sender what happened.
  //kk trust           shows the list (it starts with the
                       MLParty names)
  //kk trust <name>    adds a player
  //kk untrust <name>  removes a player
  //kk remote off      turns the trigger off entirely