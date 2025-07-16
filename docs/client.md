<!---
@darkceius, Axype
-->

# Client Script Documentation

> Scripts ran by NLS() will always have this environment

# Globals

### `owner` [Player](https://create.roblox.com/docs/reference/engine/classes/Player)

**type**: `userdata`

**description**: the **LocalPlayer**

---

### `runnerId`

**type**: `number?`

**description**: equivalent to the server's `owner.UserId`

---

### `runner`

**type**: `Player?`

**description**: equivalent to the server's `owner`

---

### `getrenv`

**type**: `function`

**description**: mirror of the real `getfenv` global provided by the rbx env.
