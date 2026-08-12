# AppADay 097: Field Marks

**Photograph what you found and get the field marks that name it.**

Live: https://augustineiacopelli.github.io/appaday-097-field-marks/

Part of [AppADay](https://augustineiacopelli.github.io/appaday/), one complete web app shipped every day.

## What it does

Point your camera at a bird, mammal, insect, reptile, plant, or fungus. Field Marks sends the photograph to Claude and returns a structured identification record: the common and scientific name, the taxonomic rank ladder from kingdom down to species, and above all the specific visible features that drove the identification rather than a generic species description. It lists the species most often confused with it and the single most reliable way to separate them, along with habitat, range, and the timing that matters, whether that is bloom, migration, activity period, or fruiting.

Every identification is filed in a local field journal grouped by kind, so a season of birds stays together and can be read back later.

## Safety

This app makes assumptions that lean toward caution, deliberately and by design.

Hazards are ranked by the worst plausible candidate, not the most likely one. If the photograph could reasonably show either a harmless snake or a venomous one, the record describes the venomous one and says plainly that it has not been ruled out.

Hedging is enforced in code, not left to the model. When confidence comes back low or uncertain and the subject belongs to a group that can hurt you, the hazard floor is raised and the record prints an explicit paragraph explaining that the warning is higher than the identification alone would justify. An existing high hazard is never lowered. A missing or malformed hazard level defaults to caution rather than none. This normalization runs again every time a record is drawn from the journal, so a record saved by an earlier version still warns correctly.

Harmful and dangerous readings are placed above the specimen name, before you see what it is, and carry the United States Poison Control number.

**The app never assesses edibility and never will.** Plants and fungi always carry a fixed refusal that no model output can suppress. Mushrooms carry stronger wording, because spore print, gill attachment, smell, and substrate are precisely what a photograph cannot capture, and deadly species have harmless twins.

Nothing here replaces a regional field guide, a county extension office, or a person who knows the ground.

## Beyond identification

Species flagged as invasive or introduced come with a removal plan: ordered practical steps, the best window in the year to act, and the legal, ecological, and safety cautions that apply. Every plan defers explicitly to your county extension office, since some species are protected, some are regulated, and herbicide rules vary by state and by proximity to water.

Plants showing visible stress get a separate assessment: what the damage looks like, the likely causes ranked with the evidence for each, a care plan ordered cheapest and least invasive first, and an honest read on when to stop guessing and call an arborist.

Both are offered for your review and judgment, not as instructions to follow blindly.

## The field journal

Records are grouped the same way the intake dropdown is: Birds, Mammals, Insects, Herps, Aquatic life, Plants, Fungi, Tracks and sign, and Other. Filter chips appear only for groups that hold records and carry their counts.

The tally under the chips separates sightings from species, which is the distinction a life list exists to make. Three photographs of the same cardinal read as three records and one species named.

Up to 120 records are kept in browser storage with small thumbnails. The oldest drops off when it fills. Clearing is scoped to whatever group you are viewing, and individual records can be removed from their own sheet. Your chosen group persists between visits, and each new identification opens the log to that specimen's group.

## Setup

Open the gear icon and paste an Anthropic API key from console.anthropic.com. The key is stored in your browser's local storage, is sent only to Anthropic, and is never committed anywhere. You can also set a session name, which is printed on each specimen tag so a day of walking stays together.

Usage is billed to your own Anthropic account.

## Photographs

Capture uses a plain file input, so phones offer both the camera and the photo library. EXIF orientation is honored, so sideways iPhone photos are corrected rather than sent rotated. Every image is re-encoded to JPEG at a 1400 pixel long edge before it is sent, which handles oversized phone photos and keeps requests small. If a HEIC file cannot be decoded, the app says so and tells you to export it as a JPEG.

Photographs are never uploaded anywhere except to the Anthropic API for the identification itself. Only a small thumbnail is retained, in your own browser.

## Built with

A single self-contained file of vanilla HTML, CSS, and JavaScript. No frameworks, no build step, no dependencies beyond Google Fonts. Newsreader carries the binomials in true italic, Karla handles the interface, IBM Plex Mono handles the taxonomy and the specimen tags. The result is laid out as a herbarium mounting sheet: warm bone paper on wet slate green, the photograph mounted with an accession stamp, the ranks set as a ruled ladder, and a specimen tag along the bottom carrying accession number, session, locality, and date.

Model: `claude-sonnet-5`, called directly from the browser.

## Disclaimer

Field Marks is a study aid, not an authority. Every identification is a best reading of one photograph. Confirm anything that matters against a regional guide, a local extension office, or a naturalist before acting on it. Do not use it to decide what is safe to eat, touch, or approach.
