# AI use log

I used OpenAI Codex to inspect the Cabina Abierta specification and the Prompt Drive APIs, implement two feedback features, regenerate the feedback bundle, and draft the design notes, reflection, and video script. I checked the implementation against the spec and revised places where the rendered cue could misstate the vehicle state. These features display simulator state; I did not use Colombian Spanish datasets or train a model for this separate Cabina Abierta task.

## Prompts that helped

1. “Read the repository instructions and the full Cabina Abierta specification. Check the actual APIs before implementing.” This led me to verify the VehicleState projector, PromptDrive weather events, and autodrive observable.
2. “Implement a top-down opening diagram that shows position and risk without changing vehicle state.” This produced cabin_openings, including the right-side-driver mirror, bounded percentages, reduced-motion support, and read-only climate/weather cues.
3. “Add an autonomy handover cue that waits for the engine handle and never writes the autonomy state.” This produced autonomy_handover, which attaches to the observable and polls only when listener methods are unavailable.

## A concrete mistake I caught

My first implementation plan treated the 150 ms batching window as enough to make the shade and roof sequence in x01 appear in order. The guide can separate their state updates by about 500 ms, while the shade animation may last several seconds. A simple batch would therefore start the roof too early. I changed the animation to wait while the shade is actively retracting, while still drawing a roof that the state reports as open if its shade is closed or partial. The animation is only a visual representation; it does not delay or modify simulator state.

## Review and limits

I use the repository build scripts and do not edit generated JavaScript by hand. During local validation I completed the full demo. I briefly muted browser speech to speed up playback, then restored Paulina (es-MX). I observed the window, roof, and autonomy sequences; I also confirmed that I could steer with the keyboard after stopping autonomy. After the final active-on-load change, a focused behavior check verified that an initially active car shows only the subdued border, while a new activation retains its three-second label. I have not visually checked a browser reload with autonomy already active, and the final console review remains outstanding. The scripted t11 phrase mentions rain but does not change scene weather, so I do not claim the full playback tested the rain alert. The task uses scripted dialogue and optional audio output; it does not require microphone input or speech recognition. No participant study was conducted. This log and REFLEXION.md belong at the root of my fork, outside the feature pull request. The Drive recording is ready to link in the PR description.
