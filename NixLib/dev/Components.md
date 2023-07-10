Component available in NixLib:

# `NixLib_partialDirectionalSpriteChange`
An entity with this component will use different sprites when facing in some directions, while other directions will be treated as "use last selected sprite" (unlike the vanilla `directionalSpriteChange` component where every direction picks a sprite offset, with all unspecified directions defaulting to ±0).

This component contains the following fields:

* `frameX`, constant table, default `{}`. This is a key-value table where keys are [`Action.Direction`](https://vortexbuffer.com/synchrony/docs/modules/necro.game.system.Action/#enum-Direction) constants and the value corresponding to that constant is the frame-x-offset on the spritesheet to use. When the entity is facing a specified direction, the specified offset is used.
* `ignored`, constant table, default `{}`. This is a key-value table where keys are `Action.Direction` (see above link) constants and values are `true`. When the entity is facing a specified direction, the offset of the most recently faced direction specified in `frameX` continues to be used.
* `lastFacing`, field `Action.Direction` (see above link), default `RIGHT`. This is the last non-ignored direction the entity was facing. It should be given a default that matches a direction specified in `frameX` and then not externally changed during gameplay.

This component is available for mods to used but is not used by NixLib itself.