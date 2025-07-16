<!---
@darkceius, Axype
-->

# Paste Script Documentation

> Paste source & scripts ran under NS() will always have this environment

# Globals

### `owner` [Player?](https://create.roblox.com/docs/reference/engine/classes/Player)

**type**: `userdata | nil`

**description**: represents the user that ran the paste in-game, can be nil. internally, axype uses the second argument passed to the loader function to determine the owner (said argument can be a **case-insensitive username**, **userid**, **userdata** that returns a valid result when indexed with `Name`, or **Player** instance)

---

### `NewLocalScript` [LocalScript](https://create.roblox.com/docs/reference/engine/classes/LocalScript)

**type**: `function (data: string, parent: Instance?, ...: any)`

**description**: creates a LocalScript in `parent`. it also passes the varargs to the client for easy one-time replication (don't pass functions or other non-replicateable types & classes due to security reasons). has no timeout.

**aliases**: `newLocalScript`, `NewLocalScript`, `nLS`, `NLS`

**quirks**: `data: string` arg can be one of the following:

- `bytecode`: **Lua 5.1** or **LuaU**
- `lua 5.1 code`: syntactically correct **Lua 5.1** source code
- `luau code`: disabled by default, enable via `axypeFlags` global

**example snippet**:

```lua
NewLocalScript([==[
    print("Hello from LocalScript!")
    print("Arguments passed", ...) --> Arguments passed pizza water
]==], owner.Character, "pizza", "water")
```

check out the client environment [here](./client.md)

---

### `NewPeristentLocalScript` [nil](https://create.roblox.com/docs/luau/nil)

**type**: `function (data: string, parent: Instance?, ...: any)`

**description**: identical to `NewLocalScript`, but the interpreter is fully client-sided and nilled, therefore indestructible.

**aliases**: `newPersistentLocalScript`, `NewPersistentLocalScript`, `nPLS`, `NPLS`

**quirks**: refer to `NewLocalScript`

---

### `NewScript` [Script](https://create.roblox.com/docs/reference/engine/classes/Script)

**type**: `function (data: string, parent: Instance?, ...: any)`

**description**: identical to `NewLocalScript`, but server-based and accepts any kind of varargs.

**aliases**: `newScript`, `NewScript` `nS`, `NS`

**quirks**: refer to `NewLocalScript`

---

### `notify` [boolean](https://create.roblox.com/docs/luau/booleans)

**type**: `function (text: string, duration: number?, target: Player?)`

**description**: creates a roblox core ui notification

---

### `xshared`

**type**: `table { [any]: any }`

**description**: identical to `shared` but only accessible by Axype pastes

---

### `isolatedStorage`

**type**: `table { [any]: any }`

**description**: isolated `shared`-like global, unique for every script with a different id. `paste1` does not have `paste2`'s isolatedStorage. scripts of the same kind ran multiple times will share the same isolatedStorage.

---

### `storage`

**type**: `table`

**description**: contains multiple functions that helps you interact with other Axype scripts. it's similar to \_G and shared but only available to Axype pastes, with some restrictions. you can't modify a key set by another script.

**methods**:<br>
`.get(key: any): any`<br>
`.exists(key: any): boolean`<br>
`.list(byYou: boolean?): {string}`<br>
`.getOwner(key: any): string?`<br>
`.set(key: any, value: any): nil`<br>
`.remove(key: any): nil`<br>

**example snippet**:

```lua
storage.set("axyreLoaded", true)

print(storage.get("axyreLoaded")) --> true
```

---

### `axypeFlags`

**type**: `userdata`

**description**: allows you to change the behaviour of the running paste by giving you access to flags. newindex metamethod only supports `string` as key and `boolean` as value.

**aliases**: `AxypeFlags`

**flags**:

- `persistentLocalDestroyUponPing` - It will destroy the script made by `NewPeristentLocalScript` right after the client pings the server.

- `isDebuggerEnabled` - Enables the debugger that pops up when the paste errors

- `BETA_useLuauSupport` - enables experimental luau support for ns & nls

**example snippet**:

```lua
axypeFlags.persistentLocalDestroyUponPing = true
--^^ you should put this at the top of your script
```

---

### `compile`

**type**: `function`

**description**: will use `compileLua`, and if luau support is enabled, `compileLuau`

---

### `compileLua` [string](https://create.roblox.com/docs/luau/strings)

**type**: `function (code: string, processName: string?)`

**description**: compiles lua 5.1 code, via yueliang.

---

### `compileLuaU` [string](https://create.roblox.com/docs/luau/strings)

**type**: `function (code: string, processName: string?, optimizationLevel: number?, debugLevel: number?, coverageLevel: number?)`

**description**: compiles luau code, via [LuauCeption](https://github.com/RadiatedExodus/LuauCeption).

---

### `require`

**type**: `function`

**description**: `require` but with output flood to make logging "more" difficult

---

### `LoadAssets`

**type**: `function`

**description**: mirror of altered `require` global, added to make Lua Sandbox scripts compatible with Axype

---

### `printf`

**type**: `function`

**description**: mirror of `print`, added to make Lua Sandbox scripts compatible with Axype

---

### `warnf`

**type**: `function`

**description**: mirror of `warn`, added to make Lua Sandbox scripts compatible with Axype

---

### `rawrequire`

**type**: `function`

**description**: mirror of the real `require` global provided by the rbx env.

---

### `getrenv`

**type**: `function`

**description**: mirror of the real `getfenv` global provided by the rbx env.

<!---

---

### `NAME_HERE` [Instance](EXAMPLE_URL_HERE)

**type**: `TYPE_HERE`

**description**: DESCRIPTION_HERE

**aliases**: N/A

-->
