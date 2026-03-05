# Brother's Modding Library

This mod contains various parts and features used most notably in the Faction Expansion mods. The mods it's used in are specified for each part so you can refer back to them if you have any doubt about usage.

---

# Documentation

## New Conversation Parts

The mod contains several new parts that can be called in any `.xml` conversation. You will find in the mod's files a sample conversation containing various examples of how said parts can be used, but here is a quick rundown.

---

### `Brothers_RequirePart`

Although the game already has the `IfHavePart` predicate that only displays a dialogue option if you have the relevant part (be it mutation or skill), the `Brothers_RequirePart` conversation part will actually display the dialogue option greyed out if you lack the relevant part, as well as the needed part in brackets.

```xml
<part Name="Brothers_RequirePart" Part="Carapace" Render="Mutation: Carapace" />
```

*Notably used in:*
[Walking Dune conversation](https://github.com/Patatifique/QUD-Faction-Expansion-Tortoises/blob/main/MiscBlueprints/Conversations.xml)

---

### `Brothers_RequireStat`

Similarly to the game's `RequireReputation` or this mod's `Brothers_RequirePart`, `Brothers_RequireStat` lets you display dialogue options that require a minimum attribute to select. If that minimum is not met, the option will be greyed out.

```xml
<part Name="Brothers_RequireStat" Stat="Ego" Value="20" />
```

*Notably used in:*
[Poacher conversation](https://github.com/Patatifique/QUD-Faction-Expansion-Tortoises/blob/main/MiscBlueprints/Conversations.xml)

---

### `Brothers_ModifyReputation`

This part allows for manipulation of reputations through dialogue options. Up to two separate reputations can be either increased or decreased with a single dialogue option.

```xml
<part Name="Brothers_ModifyReputation" Faction="Cats" Value="100" Faction2="Dogs" Value2="-100" Shown="True" />
```

*Notably used in:*
[Warden conversation](https://github.com/Patatifique/QUD-Faction-Expansion-CatsAndDogs/blob/main/MiscBlueprints/Conversations.xml)

---

### `IfEvolutiveTileMoreOrEqual`

This conversation delegate allows you to check the evolutive stage of an object that has `Brothers_EvolutiveTile`.

It returns true if the object's stage is **greater than or equal** to the provided value.

Can be used as:
- `IfEvolutiveTileMoreOrEqual`
- `IfNotEvolutiveTileMoreOrEqual`
- `IfSpeakerEvolutiveTileMoreOrEqual`
- `IfSpeakerNotEvolutiveTileMoreOrEqual`

```xml
<choice IfSpeakerEvolutiveTileMoreOrEqual="2">
    You are very evolved.
</choice>
```

In this example, the option will only appear if the speaker’s evolutive stage is 2 or higher.

*Notably used in:*
[Dog Chef conversation](https://github.com/Patatifique/QUD-Faction-Expansion-CatsAndDogs/blob/main/MiscBlueprints/Conversations.xml)

---

### `Brothers_GiveRecipe`

This conversation delegate allows an NPC to teach the player a cooking recipe.

The value must match the **class name** of a recipe in `XRL.World.Skills.Cooking`.

If the player does not already know the recipe, it will:
- Show a popup message
- Add the recipe to the journal

```xml
<choice Target="End" Brothers_GiveRecipe="SpicedAppleJam">
    Teach me this recipe.
</choice>
```

*Notably used in:*
[Dog Chef conversation](https://github.com/Patatifique/QUD-Faction-Expansion-CatsAndDogs/blob/main/MiscBlueprints/Conversations.xml)

---

## Misc Parts

These parts are not conversation-related and can be attached directly to game objects.

---

### `Brothers_EvolutiveTile`

This is a reusable part that allows an object to have a tile that changes based on its **evolutive stage**.

The object defaults at `Stage = 0`, but this can be changed in xml. Each time the event `"Brothers_ChangeEvolutiveState"` is fired on it, the stage increases by 1 and the tile updates automatically.

You define all stage tiles in a comma-separated list.

```xml
<part Name="Brothers_EvolutiveTile" StageTiles="Creatures/egg.png, Creatures/egg_cracked.png, Creatures/creature.png" />
```

In this example:
- Stage 0 → `egg.png`
- Stage 1 → `egg_cracked.png`
- Stage 2 → `creature.png`

If the stage exceeds the number of tiles, it will clamp to the last available tile.

To advance the stage in code:

```csharp
gameObject.FireEvent(Event.New("Brothers_ChangeEvolutiveState"));
```

*Notably used in:*
[Hydric Hound blueprint sets up the tiles](https://github.com/Patatifique/QUD-Faction-Expansion-CatsAndDogs/blob/main/ObjectBlueprints/Creatures.xml)
[HydraDog part fires evolve tile event](https://github.com/Patatifique/QUD-Faction-Expansion-CatsAndDogs/blob/main/Parts/Brothers_HydraDog.cs)

---

### `Brothers_ElementalDamageOnHit`

This part applies elemental damage on hit.

It can be configured to work on the wielder's hits or the weapon's hits, as opposed to the regular `ElementalDamage` part.

It was made mainly for unarmed attacks, but can be used for any weapon type by adjusting the `RequireDamageAttribute` field.

`AttackMessage` can also be customized :>

```xml
<part Name="Brothers_ElementalDamageOnHit" WorksOnEquipper="true" Type="Cold" RequireDamageAttribute="Unarmed" Amount="3d2" />
```

*Notably used in:*
[Hyrk Cestus blueprint](https://github.com/Patatifique/QUD-Faction-Expansion-CatsAndDogs/blob/main/ObjectBlueprints/Items.xml)